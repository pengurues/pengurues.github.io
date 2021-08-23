---
layout: default
comments : true
---

# Timekeeper-1

<ul>

목차<br>
1) PTP 프로토콜 예시<br>
2) array_index_mask_nospec 에서 ~ 쓰는 이유<br>
3) timekeeper xtime<br>
4) shadow timekeeping<br><br>

1) PTP 프로토콜 예시<br>
https://endruntechnologies.com/pdf/PTP-1588.pdf<br>

포인트는 SLAVE CLOCK 을 MASTER CLOCK 에게 맞추는 것입니다.<br> 
{% drawio path="images/PTP_example.drawio" page_number=0 height=500 %}<br><br>

2) array_index_mask_nospec 에서 ~ 쓰는 이유<br>
https://dojang.io/mod/page/view.php?id=183<br><br>

포인트는 정상범위일땐 음수비트를 '산술시프트'하여 0xffffffff 마스크를<br>
비정상범위일땐 양수비트를 산술시프트하여 0x0 마스크를 획득합니다.<br><br>

{% gist feather973/c08f665d38593f30ae5fa7ccd87fd717 %}<br><br>

3) timekeeper xtime<br>
http://jake.dothome.co.kr/timekeeping<br><br>

1사이클 / 54,000,000Hz = 18.518518518ns 소요<br><br>

소요시간의 정확도를 높이기 위해 xtime 개념등장<br>
xtime += 소요된 사이클 x mult<br><br>

mult 를 구하는 방법은?<br><br>

18.518518518 x 2^10 의 정수부 18962 : mult<br>
  - 10자리 정확도의 '이진화 정수'<br>
  - mult 는 1사이클 당 소요시간을 '이진화' 시킨 값<br>
  - 그럼 mult 이진화된 내용을 다시 원복시키려면?<br><br>

mult 에서 소요시간을 구하는 방법<br><br>

18962 >> 10 = 18962 / 1024 = 18.51757813ns : shift<br><br>


4) shadow timekeeping<br><br>
</ul>

{% if page.comments %}
<div id="post-disqus" class="container">
{% include disqus.html %}
</div>
{% endif %}
