~~~cpp
#include <stdio.h>
#include <iostream>
#include <stack>
#include <string>
#include <sstream>
#include <cstdlib>
#include <queue>

using namespace std;

long long multiple(long long a, long long b, long long c) {
	if (b == 1) {
		return a % c;
	}

	if (b % 2 == 0) {
		return ((multiple(a, b / 2, c) % c) * (multiple(a, b / 2, c)%c)) % c;
	}
	else {
		return ((multiple(a, b / 2 + 1, c) % c) * (multiple(a, b / 2, c) % c)) % c;
	}
	}

int main(void) {
	cin.tie(NULL);
	ios_base::sync_with_stdio(false);

	long long a, b, c;
	cin >> a >> b >> c;
	cout << multiple(a, b, c);
}
~~~
# 1629.곱셈
위의 코드는 a^b를 a개로 분할해서 병합하기 떄문에 시간복잡도가 O(N) 임
그렇지만 a^b 를 구하는 과정은 N개로 분할하지 않아도 되기떄문에 O(log N) 으로 이루어 질 수 있었음.

~~~cpp
#include <stdio.h>
#include <iostream>
#include <stack>
#include <string>
#include <sstream>
#include <cstdlib>
#include <queue>
#include <algorithm>
#include <cmath>

using namespace std;

int c;

long long squared(long long n) {
	return n * n;
}

long long multiple(long long a, long long b) {
	if (b == 1) {
		return a % c;
	}
	if (b % 2 == 0) {
		return squared(multiple(a, b / 2) % c) % c;
	}
	else {
		b -= 1;
		return ((squared(multiple(a, b / 2) % c) % c) * (a % c)) % c ;
	}
}



int main() {
	cin.tie(NULL);
	ios_base::sync_with_stdio(false);
	long long A, B, C;
	cin >> A >> B >> C;
	c = C;
	cout << multiple(A,B);
}
~~~

위의 코드는 a^b 를 구할 때 두개의 함수를 재귀시키지 않기 떄문에 O(log N) 의 시간복잡도를 가지게 됨
분할정복을 사용할 떄 어떻게 divide 할까에 대해 고민해볼 것..


