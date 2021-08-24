---
layout: default
comments : true
---

PTP 프로토콜과 xtime 을 소개하는 게시물입니다.<br>

<ul>

목차<br>
1) PTP 프로토콜 예시<br>
2) array_index_mask_nospec 에서 ~ 의 의미<br>
3) timekeeper xtime<br>
4) (next) shadow timekeeping<br><br><br>

1) PTP 프로토콜 예시<br>
https://endruntechnologies.com/pdf/PTP-1588.pdf<br>

프로토콜 동작의 포인트는 SLAVE CLOCK 을 MASTER CLOCK 에게 맞추는 것입니다.<br> 
{% drawio path="images/PTP_example.drawio" page_number=0 height=500 %}<br><br>

2) array_index_mask_nospec 에서 ~ 의 의미<br>
https://dojang.io/mod/page/view.php?id=183<br><br>

정상범위일땐 음수비트를 산술시프트하여 0xffffffff 마스크를<br>
비정상범위일땐 양수비트를 산술시프트하여 0x0 마스크를 획득합니다.<br><br>

{% gist feather973/c08f665d38593f30ae5fa7ccd87fd717 %}<br><br>

3) timekeeper xtime<br>
http://jake.dothome.co.kr/timekeeping<br><br>

54Mhz 시스템에서 1사이클에 소요되는 시간은 아래식으로 계산됩니다.<br>
1사이클 / 54,000,000Hz = 18.518518518ns 소요<br><br>

n사이클에 소요되는 시간을 계산하려면<br>
18.518518518(실수) x n(정수) 이므로, 소수점 이하 정확도가 떨어지게 됩니다.<br><br>

18.518518518 x 2^10 = 18962 처럼 정수화 시켜서 사용하게 되는데,<br>
이때 18962 는 mult 입니다. ( n사이클에 곱하는 수 )<br>
ex) xtime = 10사이클 * mult<br>
          = 10 * 18962 = 189620<br><br>

반대로 xtime 을 소요시간으로 되돌리고 싶을땐 >> 10 하게 되는데,<br>
이때 10 는 shift 입니다. ( xtime 을 shift 하는 수 )<br>
ex) xtime >> shift = 189620 >> 10<br>
                   = 185ns<br><br>

shift 가 클수록, mult 값은 2의 승으로 커지고, xtime 이 갖는 자릿수 정확도는 상수증가 합니다.<br><br>

4) shadow timekeeping<br><br>
</ul>

{% if page.comments %}
<div id="post-disqus" class="container">
{% include disqus.html %}
</div>
{% endif %}
