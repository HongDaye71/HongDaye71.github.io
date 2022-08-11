---
layout: post
title:  Programmers/Python3/신고결과받기
date:   2022-08-11 12:38:35 +0300
image:  '/images/Programmers.jpg'
tags:   [Programmers]
---
<br/>


### Programmers Level01 신고결과받기 [Python Algorithm] <br/>

**문제풀이**

```python
def solution(id_list, report, k):
    answer = []
    a = list(set(report)) 
    #report복사
    
    dictionary = {name : [] for name in id_list} 
    dictionary2 = {name : 0 for name in id_list} 
    #name : [] 형태의 index를 가진 dictionary 생성
    #name = id_list index
    
    for i in a :
        dictionary[i.split()[1]].append(i.split()[0])
        #print(i) = report개별 index출력
        #print(i.split()) = report개별 index를 split하여 출력
        #print(i.split()[1]) = report개별 index를 split한것 중 1번째 값 출력
        # print(dictionary[i.split()[1]]) = dictionary의 1번째 값 출력([])
        #dictionary[i.split()[1]].append(i.split()[0]) = []에 name을 신고한 유저정보 추가
        #i = name역할 / name의 index를 가져와 0번 값(name을 신고한 사람)을 name의 배열에 추가
    
    
    for i in dictionary :
        if len(dictionary[i]) >= k : 
            #name을 신고한 유저가 두 명 이상이라면
            for j in dictionary[i] : 
                #name을 신고한 유저만큼을 돌면서
                dictionary2[j] += 1 
                #name을 신고한 유저의 배열에 += (본인이 신고한 사람 중 정지된 사람의 수 += 1)

    for i in dictionary2:
        answer.append(dictionary2[i])
        print(dictionary2[i])
    return answer
```












