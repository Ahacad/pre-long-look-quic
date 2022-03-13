---
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
title:
---

# Take a Long Look at QUIC

An Approach for Rigorous Evaluation of Rapidly Evolving Transport Protocols

IMC 17'

<a href="https://ahacad.github.io/LSM-pre" target="_blank" alt="GitHub"
  class="abs-br m-6 text-xl icon-btn opacity-50 !border-none !hover:text-white">
  <carbon-logo-github />
</a>

--- 

# Take a long look ahead

<div class="mt-26" />


- many results relating to QUIC, at the time of 2017
- the *approach* used: for a rapidly evolving protocol (QUIC)

<style>
li {
    font-size: 34px;
}
</style>

---


# Roadmap

<div>
<ul>
<li class="text-black">Backgrounds
    <ul>
        <li>Features of QUIC</li>
        <li>Real-world problems</li>
    </ul>
</li>
<li class="text-gray-400">Experiment setups</li>
<li class="text-gray-400">2 problems of the experiment</li>
<li class="text-gray-400">Results and analyses</li>
<li class="text-gray-400">Conclusions</li>
<li class="text-gray-400">Extension: about Alan Mislove</li>
</ul>
</div>

<style>
ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>

---

<div class="mt-5"/>


<img class="m-auto" src="/pics/unix-everyday.png" alt="unix everywhere" width="700"/>

<div class="text-4xl text-black flex justify-center w-full"> it's too difficult to update everyone's machine!</div>


---

<div class="mt-5"/>


<img class="m-auto" src="/pics/httpquic.png" alt="httpquic" width="700"/>


---

## Features of QUIC <sup>[4] [5]</sup>
<div class="grid grid-cols-2">

<div>
<div class="mt-10"/>

<img class="m-auto" src="/pics/rtts.png" alt="unix everywhere" width="500"/>
</div>

<div class="pl-6">
<div class="mt-15"/>
<ul class="list-none">
<li> "0-rtt": previously visited websites don't need the handshakes </li>
<li> reduced head-of-line blocking (HOL) </li>
<li> improved congestion control </li>
</ul>

</div>

</div>

<style>
ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>

---

<img class="m-auto" src="/pics/quicblog.png" alt="quicblog" width="700"/> 



---

## The reality we are in

<div class="mt-16" />

Back to 2017:
- QUIC still under heavy development, codes change everyday (so analyses may become obsolete quickly)
- codes published, but detailed settings were not (so need gray-box testing)
- a protocol in reality will face many many situations (so need comprehensive setups)


<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>
---

# Roadmap

<div class="mt-10"/>
 
<div>
<ul>
<li class="text-gray-400">Backgrounds
</li>
<li class="text-black">Experiment setups</li>
<li class="text-gray-400">2 problems of the experiment</li>
<li class="text-gray-400">Results and analyses</li>
<li class="text-gray-400">Conclusions</li>
<li class="text-gray-400">Extension: about Alan Mislove</li>
</ul>
</div>

<style>
ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>
--- 

## Experiment setups

<div class="mt-10"/>

<div class="grid grid-cols-2">

<div>
<div class="mt-10"/>
<img class="m-auto" src="/pics/parameters.png" alt="state machine" width="500"/>
</div>

<div>

<ul>
<li> 

a router running [tc](https://man7.org/linux/man-pages/man8/tc.8.html) and [netem](https://man7.org/linux/man-pages/man8/tc.8.html), networks under control
</li>
<li> clients: 1 Ubuntu desktop, 2 mobiles</li>
<li> servers: Amacon EC2</li>
<li> HTML only references images to avoid scripts execution</li>
<li> including websites and youtube video streaming</li>
</ul>

</div>
</div>


<style>
p, ul {
    list-style-type: disc;
    font-size: 20px;
}
</style>

---

# Roadmap

<div>
<ul>
<li class="text-gray-400">Backgrounds
</li>
<li class="text-gray-400">Experiment setups</li>
<li class="text-black">2 problems of the experiment
    <ul>
        <li>The problems and approaches</li>
        <li>Example state machine</li>
    </ul>
</li>
<li class="text-gray-400">Results and analyses</li>
<li class="text-gray-400">Conclusions</li>
<li class="text-gray-400">Extension: about Alan Mislove</li>
</ul>
</div>

<style>
ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>
---

## 2 problems (as mentioned)

<div class="mt-20" />

- published QUIC codes don't have settings really deployed on Google servers, but we need the right one to evaluate QUIC
- QUIC has much debug information, but there was no explanation of them

<style>
p,ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>
---

## Addressing the problems

<div class="mt-20"/>

- "reverse engineering": 
    - *exposed parameters* can be captured by communications between server and client (window size)
    - those *not exposed* can be gray-box tested to infer
- infer state machine from collected logs automatically by [synoptic](https://github.com/ModelInference/synoptic)

    <!--- for example, QUIC's performance suffers when packet re-ordering happens, because these packets cause QUIC to falsely report high numbers of losses -->

<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>
---

## Example state machine

<div class="mt-5" />

<img class="m-auto" src="/pics/states.png" alt="state machine" width="700"/>

<div class="mt-10"/>

---

# Roadmap
 
<div>
<ul>
<li class="text-gray-400">Backgrounds</li>
<li class="text-gray-400">Experiment setups</li>
<li class="text-gray-400">2 problems of the experiment</li>
<li class="text-black">Results and analyses
    <ul>
        <li>Fairness, PLT, video streaming, and more</li>
    </ul>
</li>
<li class="text-gray-400">Conclusions</li>
<li class="text-gray-400">Extension: about Alan Mislove</li>
</ul>
</div>

<style>
ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>

---

## Fairness

<img class="m-auto" src="/pics/window.png" alt="state machine" width="300"/>

- QUIC vs. TCP is expected to be fair <sup>[1]</sup>(both uses Cubic), but turn out that QUIC consumes much more bandwidth. Different buffer sizes and multiple TCP connection does not change this result.


<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>


---

## Page load time 1 (QUIC vs. TCP)

<div class="mt-10"/>

<img class="m-auto" src="/pics/quictcp1.png" alt="state machine" width="600"/>

- QUIC outperforms TCP most of the time, except when there are large number of objects
- this caused by early exit from Slow Start, and QUIC see this as path getting congested

<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>

---

## Page load time 2 (losses)

<div class="mt-10"/>

<img class="m-auto" src="/pics/quictcp2.png" alt="state machine" width="800"/>

- caused by packet reordering, and QUIC spends more time in recovery state

<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>

---

## Page load time 3 (Flutuating bandwidth)

<div class="mt-10"/>

<img class="m-auto" src="/pics/flutuateband.png" alt="state machine" width="500"/>

- QUIC more responsive to bandwidth changes and has higher average throughput

<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>
---

## Page load time 4 (Mobile)
<div class="mt-10"/>

<img class="m-auto" src="/pics/mobile.png" alt="state machine" width="800"/>

- not enough processing power on mobiles

<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>

---

## Page load time 5 (Mobile Explanation)
<div class="mt-15"/>

<img class="m-auto" src="/pics/mobileexplana.png" alt="state machine" width="700"/>


<style>
p,ul {
    list-style-type: disc;
    font-size: 26px;
}
</style>
---

## Page load time (Conclusion)

<div class="mt-15"/>

- QUIC behaves well most of the time, even under losses and flutuating bandwidth
- large number of objects and network jitters harm QUIC's performances
- processing power matters

<style>
p,ul {
    list-style-type: disc;
    font-size: 32px;
}
</style>

---

## Video streaming

<div class="mt-15"/>

<img class="m-auto" src="/pics/videos.png" alt="state machine" width="800"/>
<div class="mt-8"/>

- QUIC performs well in high resolution videos

<style>
p,ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>

---

## More results
<div class="mt-15"/>

- QUIC version from 25 to 34 performs largely the same
- TCP proxy helps to recover benefits of QUIC, especially in lossy scenarios

<style>
p,ul {
    list-style-type: disc;
    font-size: 32px;
}
</style>
---

# Roadmap

<div class="mt-10"/>

<div>
<ul>
<li class="text-gray-400">Backgrounds
</li>
<li class="text-gray-400">Experiment setups</li>
<li class="text-gray-400">2 problems of the experiment</li>
<li class="text-gray-400">Results and analyses</li>
<li class="text-black">Conclusions</li>
<li class="text-gray-400">Extension: about Alan Mislove</li>
</ul>
</div>

<style>
ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>

---

## Conclusions
<div class="mt-10"/>

- on desktops, QUIC outperforms TCP+HTTPS due to 0-rtt
- QUIC is sensitive ot out-of-order packets, where it performs badly
- processing power limits QUIC, so it may not do well no mobiles
- QUIC outperforms TCP under flutuating bandwidth
- QUIC is **unfair** to TCP, consuming more than twice its fair share
- QUIC gives better QoE for high-resolution video streaming
- TCP proxy helps to shrink the performance gaps
- QUIC performance improves since 2016 due to the change in congestion window size
- found a bug impacting QUIC server about Slow Start

<style>
p,ul {
    list-style-type: disc;
    font-size: 22px;
}
</style>
---

## What we learn
<div class="mt-15"/>

- QUIC is good and promising, but still has many problems (code bugs, fairness, CPU)
- used testbed to control experiment environments
- root cause analyses by automatically generated state machine

<style>
p,ul {
    list-style-type: disc;
    font-size: 32px;
}
</style>

---

# Roadmap

<div class="mt-10"/>

<div>
<ul>
<li class="text-gray-400">Backgrounds
</li>
<li class="text-gray-400">Experiment setups</li>
<li class="text-gray-400">2 problems of the experiment</li>
<li class="text-gray-400">Results and analyses</li>
<li class="text-gray-400">Conclusions</li>
<li class="text-black">Extension: about Alan Mislove</li>
</ul>
</div>

<style>
ul {
    list-style-type: disc;
    font-size: 30px;
}
</style>

---


<div class="mt-1" />

<div class="grid grid-cols-2" >

<img class="m-auto" src="/pics/alanmislove.jpg" alt="unix everywhere" width="300"/>

<div> 

- Networked Systems Research Group at [NEU](https://www.northeastern.edu/) (since 2009)
- BA, MS, and PhD from [Rice University](https://www.rice.edu/) respectively in 2002, 2005 and 2009.
- interests: working on social networks, systems, privacy, measurement, algorithmic auditing
- teaching: networks and distributed systems, computer systems, social computing, ...
- publications, services, honours, fundings, press coverages: too many to cover here, get the whole list on Mislove's website<sup>[8]</sup>

</div>

</div>

<style>
ul {
    list-style-type: disc;
    font-size: 20px;
}
</style>

---

- IMC'07 "Measurement and Analysis of Online Social Networks" (2007)
- PhD Thesis "Online Social Networks: Measurement, Analysis, and Applications to Distributed Information Systems" (2009) from Rice University: a 268-page long thesis
- IMC'14 "Measuring Price Discrimination and Steering on E-commerce Web Sites" (2014)
- IMC'15 "Peeking Beneath the Hood of Uber" (2015)
- "Using millions of emoji occurrences to learn any-domain representations for detecting sentiment, emotion and sarcasm" (2017), words into emojis: https://deepmoji.mit.edu/


<style>
ul {
    list-style-type: disc;
    font-size: 24px;
}
</style>

---

# References

- [1] Fairness measure: https://www.wikiwand.com/en/Fairness_measure
- [2] Orange Labs, France, R. Corbel, S. Tuffin, A. Gravey, X. Marjou, and A. Braud, “Assessing the Impact of QUIC on Network Fairness,” jcm, pp. 908–914, 2019, doi: 10.12720/jcm.14.10.908-914.
- [3] R. Corbel, S. Tuffin, A. Gravey, A. Braud, and X. Marjou, “Impact of QUIC on fairness in mobile networks,” in 2019 10th International Conference on Networks of the Future (NoF), 2019, pp. 82–89. doi: 10.1109/NoF47743.2019.9015005.
- [4] “天下武功，唯’QUICK’不破，揭秘QUIC的五大特性及外网表现 - 云+社区 - 腾讯云.” https://cloud.tencent.com/developer/article/1155289 (accessed Mar. 12, 2022).
- [5] “QUIC, a multiplexed transport over UDP.” https://www.chromium.org/quic/ (accessed Mar. 12, 2022).
- [6] A. Langley et al., “The QUIC Transport Protocol: Design and Internet-Scale Deployment,” in Proceedings of the Conference of the ACM Special Interest Group on Data Communication, Los Angeles CA USA, Aug. 2017, pp. 183–196. doi: 10.1145/3098822.3098842.

---

- [7] “本站开始支持 QUIC,” Halfrost’s Field | 冰霜之地, Jul. 22, 2018. https://halfrost.com/quic_start/ (accessed Mar. 12, 2022).
- [8] https://mislove.org/
- [9] Citizens and Technology Lab, Auditing Algorithms online: Christo Wilson at #CSMIT2018, (Jul. 09, 2018). Accessed: Mar. 13, 2022. [Online]. Available: https://www.youtube.com/watch?v=gxsKVDyX2ak





