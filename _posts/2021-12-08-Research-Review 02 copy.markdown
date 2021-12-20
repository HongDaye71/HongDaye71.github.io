---
layout: post
title:  Mental workload during n-back task—quantified in the prefrontal cortex using fNIRS
date:   2021-12-08 15:01:35 +0300
image:  '/images/fNIRS03.png'
tags:   [Researh review, fNIRS]
---
## Background Knowledge<br/>
* N-Back Task : Recall a sequence of items and determine whether the current item matches the item presented “n” positions prior <br/> [참고영상](https://www.youtube.com/watch?v=Ro5AI6nhzlQ&t=175s)

___

## Abstract<br/>
Human-machine interfaces (HCIs) are desirable which continuously monitor the users’ workload. and dynamically adapt the behavior of the interface to the measured workload. While memory tasks have been shown to elicit hemodynamic responses in the brain when averaging over multiple trials, a robust single trial classification is a crucial prerequisite for the purpose of dynamically adapting HCIs to the workload of its user. The prefrontal cortex (PFC) plays an important role in the processing of memory and the associated workload. 

In this study of 10 subjects, we used functional Near-Infrared Spectroscopy (fNIRS) The results show
up to 78% accuracy for single-trial discrimination of three levels of workload from each other. We use an n-back task (n ∈ {1, 2, 3}) to induce different levels of workload, Our experimental results show that measuring hemodynamic responses in the PFC with fNIRS, can be used to robustly quantify and classify mental workload. Single trial analysis is still a young field that suffers from a general lack of standards. To increase comparability of fNIRS methods and results, the data corpus for this study is made available online.<br/>

정리 : <br/>
1. HCI분야에서는 사용자의 인지부하를 지속적으로 모니터링하고 측정된 인지부하에 맞게 인터페이스를 조정하고자 하는 시도가 계속되고 있다.
2. Block Design을 통해 특정 조건에 대한 평균적인 인지부하를 측정하는 연구는 많이 진행되어 왔지만, 사용자의 인지부하에 맞추어 동적으로 인터페이스를 조정하기 위해선 단일 이벤트에 대한 정확한 분류가 필요하다. 
3. 본 실험은 10명의 피험자를 대상으로 3개 난이도의 N-Back Task를 진행했고, fNIRS장비를 사용하여 실시간으로 사용자의 Hemoglobin변화를 측정했다.
4. 그 결과 3개 난이도를 가진 N-Back Task에 대한 single-trial discrimination에서 78%의 정확도가 나타났고, 본 실험의 결과는 fNIRS가 사용자의 인지부하를 정확하고 정량적으로 분석해낼 수 있음을 증명한다.

___

## Experiment Design <br/>
<img src="/images/Posting/ResearchReview/fNIRS/12.png" alt="Project">

* Procedure : <br/>
In our experiment, we investigated 10 trials each of 1-,2-, and 3-back tasks. Each trial contained 3 ± 1 targets. The experiment was presented to the subjects on a screen.<br/>

A trial consisted of 5 s of instruction. informing the subject which task (1-,2- or 3-back) was about to start. The trial then presented a new letter every 2 s. Every letter was displayed for 500 ms. The screen was left blank for the remaining 1.5 s. A total of 22 letters was presented during every trial resulting in a trial length of 44 s. Subsequently, a cross was displayed for 15 s during which the subjects were asked to relax to ensure that hemoglobin levels returned to baseline<br/>

After half of the trials, an additional 10 s ofthe resting cross were displayed to have data periods with no activity to be used as RELAX trials. The order of the different n-back conditions was pseudo-randomized. A 150 s break during which the subjects could drink or chat was included after 15 trials. The entire experiment had a recording time of 37 min (30 trials of 64 s, 15 relax trials of 10 s and 150 s in the middle).<br/>

정리 : <br/>
1. 1-,2-,3-back tasks는 각각 10trial 씩 진행 (1trial동안 3 ± 1 번 task진행 / 22개 단어로 구성(1개 단어 당 2초))<br/>
2. 1trial : 1-,2-,3-back tasks 중 어떤 task가 시작될지 안내(5초) + 단어제공(0.5초) + Blank(1.5초) + Hemoglobin이 Baseline으로 돌아오기 위해 휴식(15초) + Hemoglobin Baseline측정(10초)<br/>
3. 1trial을 15번 반복한 후에는, 150초 간 휴식<br/>

* Participants : N = 10 (4 female, 6 male / 8 right-handed and 2 left-handed participants)<br/>
* Measure : 
___

## Signal Processing and Artifact Removal <br/>
To attenuate trends and Mayer Wave like effects, we used a moving average filter, which subtracted the mean of the 120 s before and after every sample from every HbO and HbR datapoint. 
___

## Feature Exraction and Selection <br/>

___

## Result <br/>
* User Performance and Subjective Rating : <br/>
* Hemodynamic Responses :<br/>

___

Herff, C., Heger, D., Fortmann, O., Hennrich, J., Putze, F., & Schultz, T. (2014). Mental workload during n-back task—quantified in the prefrontal cortex using fNIRS. Frontiers in human neuroscience, 7, 935.

