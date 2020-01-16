# 1. 스택 오버플로우
~~~cpp
#include <stdio.h>
#include <iostream>
#include <stack>
#include <string>
#include <sstream>
#include <cstdlib>
#include <queue>
#include <algorithm>
#include <list>
#include <cmath>

using namespace std;

int N, M;
vector<vector<int>> arr(50, vector<int>(50, 0));

int rect(int y, int x,int length) {
	if (length == 1) {
		return 0;
	}
	int distance = length - 1;
	if (arr[y][x] == arr[y][x + distance] && arr[y][x] == arr[y + distance][x] && arr[y][x] == arr[y + distance][x + distance]) {
		return length * length;
	}

	if (y + distance == N && x + distance == M) {
		rect(0, 0, length - 1);
	}
	else if (x + distance == M) {
		rect(y + 1, 0, length);
	}
	else {
		rect(0, x + 1, length);
	}
}

int main() {

	string str;
	cin >> N >> M;
	for (int i = 0; i < N; i++) {
		cin >> str;
		for (int k = 0; k < M; k++) {
			arr[i][k] = str[k]-'0';
		}
	}
	cout << rect(0, 0, min(N, M));
}
~~~

## 재귀함수 이용시 너무 많은 재귀가 일어나게 되면 재귀를 하기 위한 리소스와 각각의 함수에 대한 지역변수 때문에 스택오버플로우가 일어날 수 있었음
해결책은 다음과 같다.
### 1.1꼬리 재귀를 사용한다.
#### 꼬리재귀란 재귀함수를 호출할때 함수가 호출된 위치에 해당하는 스택을 없애는 방식의 재귀 호출방식이다. 그렇기 떄문에 호출된 함수의 위치를 기억해야 하는경우 부적절한 방식이라 할 수 있다
#### 또한 컴파일러에 따라서 스택을 없애줄 수 있고 없애주지 않을 수 있기 떄문에 컴파일 설정을 해놓아야 한다.
### 1.2.스택의 크기를 늘린다.
#### 스택의 크기를 늘리게 되면 자연스럽게 재귀함수를 호출할 수 있는 크기가 커질것임. 변수 하나짜리 재귀함수의 경우 1MB 당 4780번 정도의 연산이 가능한 것을 확인.
### 1.3.반복문으로 바꾼다.
#### 모든 재귀함수는 반복문으로 변환 가능하므로 반복문으로 변환해도 된다. 하지만 재귀함수를 반복문으로 바꿀경우 코드가 상당히 복잡해질 수 있기 때문에 각각 상황에 맞는 방법을 사용하는것이 중요하다.



# 2 재귀함수 파라미터 deep copy
#### 재귀함수를 사용할 떄 배열의 주소를 입력하게 되면 해당 배열을 사용하게 됨.
#### 하지만 벡터와 리스트 등 주소가 아닌 배열을 직접 넣게 되면 해당 배열을 deep copy 하게 됨.
#### 재귀함수의 파라미터로 배열을 쓸때에는 주의가 필요.
