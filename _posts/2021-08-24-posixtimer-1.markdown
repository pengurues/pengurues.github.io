---
layout: default
comments : true
---

# Posixtimer-1

<ul>
참고링크 : https://man7.org/linux/man-pages/man2/timer_create.2.html<br><br>

do_sigaction<br>
int (*timer_create)(struct k_itimer *timer);<br>
k_itimer<br>
{% gist feather973/bedadb1288584a77e977207c5f60f258%}<br><br>

timer_queue_init
{% gist feather973/5b163f585e269a4a32faf6f4c566c7d9%}<br><br>

related structures
{% gist feather973/ffe28b076e95c2d11b740cd9ee414e53%}<br><br>

arm_timer 에 대해서<br><br>
feat. timerqueue_node / timerqueue_head

1. list<br>
-head : posix_cputimer_base.tqhead<br><br>

k_timer 에서 posix timer clock id 를 획득<br><br>

2. enqueue<br>
- cpu_timer.node 를 enqueue<br><br>

RLIMIT_RTTIME<br><br>

posix_cputimers_work<br><br>

handle_posix_cpu_timers<br><br>

task_tick_rt<br><br>

hard /soft ( SIGKILL / SIGXCPU )<br><br>

task_cputimers_expired<br><br>

posix_cputimers_init_work<br><br>

store_samples<br><br>

proc_sample_cputime_atomic<br><br>

utime / stime / rtime<br><br>

nice time?<br><br>

shallow idle state<br><br>


</ul>

{% if page.comments %}
<div id="post-disqus" class="container">
{% include disqus.html %}
</div>
{% endif %}
