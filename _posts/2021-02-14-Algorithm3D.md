---
layout: post
title: "알고리즘 문제해결기법 입문 문제3D"
date: 2021-02-14
excerpt: "Python 알고리즘 문제해결기법 입문 문제3D"
tags: [Python, 알고리즘 문제해결기법 입문, Chapter.3]
comments: true
---
# 3D

### 문제
피보나치 수열이란 0, 1부터 시작해서 이 전의 두 값을 더해 새로운 값을 만들어나가며 전개되는 수열이다. 

> 0, 1, 1, 2, 3, 5, 8, 13, 21, ...

피보나치 수열은 규칙이 간단하고 수학적으로 다양한 특징이 있기에 자주 사용되는 수열 중 하나이다. 하지만 수열이 진행될 수록 숫자가 급격히 커지기 때문에 손으로 계산하기에는 쉽지 않은 수열이다.

피보나치 수열과 8자리 전화번호의 관련성을 연구하고 있던 지애는 손으로 하던 계산을 프로그램으로 대체하기 위하여 당신에게 도움을 요청했다. 지애를 도와주기 위하여 어떤 수 N이 주어졌을 때, N번째 피보나치 수의 마지막 8자리 숫자를 정수형태로 출력하는 프로그램을 작성해주자.

예를 들어서 실제 수열의 값이 1,000,283,859이라면 283859만 출력하면 된다.

### 입력 형식
첫 줄에는 테스트케이스의 수 T가 1이상 10만 이하의 자연수로 주어진다.

각 테스트케이스의 입력은 한 줄로 구성되며, 1이상 100만 이하의 자연수 N이 공백없이 주어진다.

### 출력 형식
각 테스트케이스별로 한 줄에 정답을 출력한다. 피보나치 수열의 N번째 숫자를 공백없이 정수형태로 출력한다.  단, 숫자 가장 앞의 0들은 생략한다. 

단, 피보나치 수열의 1번째 숫자는 0이고 2번째 숫자는 1이다.

### 예시 1
#### 입력
{% highlight css %}
6
1
2
3
4
5
6
{% endhighlight %}
#### 출력
{% highlight css %}
0
1
1
2
3
5
{% endhighlight %}

### 예시 2
#### 입력
{% highlight css %}
5
999996
999997
999998
999999
1000000
{% endhighlight %}
#### 출력
{% highlight css %}
94312505
31921872
26234377
58156249
84390626
{% endhighlight %}

# 풀이

### 설명
시간 초과가 계속 나길래 문제 풀이 방법을 계속 바꿔주고 배열도 크기 2개만을 사용하는 방법으로 했었는데 시간 초과가 계속 발생했습니다. 문제를 계속 읽다가 미리 피보나치 수열을 구한 배열을 저장해 놓고 값을 바로바로 호출해주면 시간이 절약될 것으로 생각이 돼 fibo함수에서 100만 개 할당이 된 fibo_result함수에 수열을 미리 구했습니다. 다만 해당 방법은 너무 메모리 소모율이 크지만 문제에서 요구하는 시간제한을 맞추기 위해서는 이 방법을 썼어야 합니다.

### 코드
{% highlight css %}
def fibo() :
	fibo_result = [0] * (1000000+1)
	fibo_result[1] = 0
	fibo_result[2] = 1
	for i in range(3, 1000000+1) :
		fibo_result[i] = (fibo_result[i-2] + fibo_result[i-1]) % 100000000
	return fibo_result
	
t = int(input())
fibo_result = fibo()
for _ in range(t) :
	n = int(input())
	print(fibo_result[n])
{% endhighlight %}

### 기타
- `Memory` : 49028
- `Time` : 1.164