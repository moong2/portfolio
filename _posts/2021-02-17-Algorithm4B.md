---
layout: post
title: "알고리즘 문제해결기법 입문 문제4B"
date: 2021-02-17
excerpt: "Python 알고리즘 문제해결기법 입문 문제4B"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.4]
comments: true
---
# 4B

### 문제
행사 기획자인 수정이는 이 번에 자신이 담당하게 된 행사에서 행운권 추첨을 기획하고 있다. 이번 행사에서는 최대 수천명 정도의 사람이 방문할 수 있기 때문에 어떻게 하면 공평하고 불규칙적으로 행운권 번호를 배정할 수 있을지가 큰 관건이었다. 하지만 똑똑한 수정이는 아래와 같은 아이디어를 냈다.

- 모든 행운권 번호는 0~(N-1)의 정수로 총 N개이다.
- 모든 고객은 회원번호를 가지고 있으며 회원 번호는 자연수이다.
- 입장한 고객은 자신의 회원 번호를 N으로 나눈 나머지를 계산해 그 번호와 같은 행운권을 지급받는다.
	- 해당 행운권이 다른 사람에게 지급된 상황이라면 그것보다 +1한 번호를 지급받는다.
	- 아직 아무에게도 지급되지 않은 번호를 찾을 때 까지 행운권 번호를 +1씩 증가시켜가며 찾는다.
	- 만약 (N-1)번 행운권도 이미 지급된 상태라면 0번 행운권부터 다시 조회한다.
	- 이렇게 순서대로 조회하다가 가장 먼저 발견된 아직 지급되지 않은 행운권을 지급받는다.
- 고객들은 순서대로 한 명씩 입장하며 한번 지급된 행운권 번호는 교환할 수 없다.

수정이는 행사 중간에도 바쁠 예정이기에 당신에게 이를 자동화할 수 있는 프로그램을 작성해달라고 요청했다. 수정이를 도와주자. 

### 입력 형식
첫 줄에는 준비한 행운권의 수 N과 입장 할 회원의 수 M이 공백으로 구분되어 주어진다. N은 1이상 5,000이하의 자연수이며 M은 1이상 1,000이하의 자연수이다. 또한, M은 항상 N이하의 값을 가진다.

이후 총 M줄에 걸쳐서 입장 한 회원들의 회원번호가 순서대로 주어진다. 각 회원번호는 1이상 1억 이하의 자연수이다.

### 출력 형식
입장한 회원들의 순서대로 해당 회원이 지급받게 될 행운권 번호를 한 줄에 하나 씩 정수 형태로 출력한다.

### 예시 1
#### 입력
{% highlight css %}
5000 5
2878
15092880
1
18762879
77787879
{% endhighlight %}
#### 출력
{% highlight css %}
2878
2880
1
2879
2881
{% endhighlight %}

# 풀이

### 설명
원형배열을 이용하듯이 풀면 되는 문제입니다. 먼저 티켓은 N개만큼 배부되므로 크기가 N인 배열을 선언합니다. 멤버십 번호는 N으로 해싱되므로 해당 멤버십 번호를 가진 사람이 받을 행운권 번호는 멤버십 번호 % N임을 알 수 있습니다. 하지만 이미 해당 행운권 번호가 다른 사람에게 돌아갔을 경우, 재해싱 되어야합니다. 해당 문제에서 재해싱은 +1을 하며 이루어집니다. 이 과정은 행운권 번호 배열의 value가 0이 될 경우에 멈춥니다. 

### 코드
{% highlight css %}
import sys

n, m = map(int, sys.stdin.readline().split())
ticket = [0] * n

for _ in range(m) :
	membership_num = int(sys.stdin.readline())
	index = membership_num % n
	while(ticket[index] == 1) :
		index = (index + 1) % n
	ticket[index] = 1
	print(index)
{% endhighlight %}

### 기타
- `Memory` : 9428
- `Time` : 0.032