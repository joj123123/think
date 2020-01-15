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
