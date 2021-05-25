---
layout: post
current: post
cover:  assets/built/images/background-frontend.jpg
navigation: True
title: Algorithm Hash 개념정리
date: 2021-05-25
tags: [algorithm]
class: post-template
subclass: 'post tag-algorithm'
author: Ko
---

오늘은 Hash에 대하여 정리를 해보려고 한다.

주 언어가 Java이다보니 HashMap은 많이 써보았지만, 정확하게 정리를 해본적은 없는 듯하여 정리를 해보려한다.

내가 알고 있던 Hash에선 키와 값이 있으며, 키를 인덱스로 가지고 있기 때문에 시간복잡도가 O(1)이라는 것.


<h3>1 해시</h3>
- 해시는 임의의 크기를 가진 데이터를 고정된 데이터 크기로 변화시키는 것을 말하며,
- 해시함수를 사용하여 값을 계산하여 나온 고정된 길이의 값을 해시값이라고 부른다. 
- 여러 분야에 사용되며, 복잡하지 않은 알고리즘으로 이루어져 CPU,메모리 등 시스템 자원을 덜 소모한다고 한다.
- 여러분야 사용되고 여러가지(MDn, SHA-n 등) 해시 알고리즘이 있지만(자세하게 다룰일이 있으면 추가해야지)
  

![ex_screenshot](./assets/built/images/algorithm/hash/hash_hash.png)


<h3>2 해시 충돌</h3>
해시 충돌은 해시함수를 거친 키값이 같은 값들. 즉, 다른 데이터의 키 값(해시값)들이 동일할 경우 해시 충돌이 발생한다.
이 충돌은 해시 테이블의 성능을 떨어뜨린다. 
해시 충돌을 방지하려면 해시 함수를 잘 정의하면 된다. 하지만 해시함수의 입력값은 무한하지만, 
출력값의 가짓수는 유한(출력값, 즉 키가 유한하지 않다면 해시기법을 사용하는 의미가 없다.)하므로 
해시 충돌은 반드시 발생한다.(비둘기집 원리)

이러한 해시충돌을 방지할 방법은 크게 2가지가 있다.
<b>체이닝(Chaining)</b>
버킷내에 LinkedList를 할당하여, Bucket에 데이터를 저장하다가 해시 충돌이 발생하면 연결리스트로 데이터를 연결하는 방식이다.

<b>개방 주소법(Open Addressing)</b>
해시 충돌이 발생하면 다른 Bucket에 데이터를 삽입하는 방식이다.
체이닝은 주소값은 동일한 상태로 LinkedList를 이용하여 늘려가기 때문에, 주소값이 변경되지는 않는다는 부분과 차이가 있다.
![ex_screenshot](./assets/built/images/algorithm/hash/hash_chaining1.PNG)

<b>3가지 개방 주소법</b>
- <b>선형 탐색<Linear Probing>:</b> 해시 충돌 시 다음 버킷 혹은 몇개를 건너뛰어 데이터를 삽입
- <b>제곱 탐색<Quadratic Probing>:</b> 해시 충돌 시 제곱만큼 건너뛴 버켓에 데이터를 삽입
- <b>이중 해시<Double Hashing>:</b> 해시 충돌 시 다른 해시 함수를 한 번 더 적용한 결과를 이용
  
![ex_screenshot](./assets/built/images/algorithm/hash/hash_openaddressing.PNG)
  
<h3>해시를 이용한 자료구조</h3>
해시를 이용한 자료구조엔 <b>HashMap, HashTable</b>이 있다.
둘의 차이는 <b>동기화 지원</b>이 가능하냐 안하냐의 차이(synchronized)가 있다고 한다.


<h3>해시 자료구조의 시간 복잡도</h3>
해시함수로 만들어진 키값들은 고유한 인덱스를 가지게 되어 바로 접근할 수 있다.
그러므로 평균 O(1)의 시간복잡도를 가지고 있지만, 데이터 충돌이 발생할 경우 Chaining에 연결된 리스트들까지
검색해야 하므로 O(N)까지 시간복잡도가 증가할 수 있다.
충돌을 방지하는 방법들은 데이터의 규칙성(클러스터링)을 방지하기 위한 방식이지만 공간을 많이 사용한다는 치명적인 단점이 있다.
만약 테이블이 꽉 차있는 경우라면 테이블을 확장해주어야 하는데, 이는 매우 심각한 성능의 저하를 불러오기 때문에 가급적이면 확장을 하지 않도록 테이블을 설계해주어야 한다.
(통계적으로 해시 테이블의 공간 사용률이 70% ~ 80%정도가 되면 해시의 충돌이 빈번하게 발생하여 성능이 저하되기 시작한다고 한다.)
또한 해시 테이블에서 자주 사용하게 되는 데이터를 Cache에 적용하면 효율을 높일 수 있다. 자주 hit하게 되는 데이터를 캐시에서 바로 찾음으로써 해시 테이블의 성능을 향상시킬 수 있다

![ex_screenshot](./assets/built/images/algorithm/hash/hash_chaining_time.PNG)



출처 
https://mangkyu.tistory.com/102 [MangKyu's Diary]
https://preamtree.tistory.com/20 [Preamtree의 행복로그]

 