# 자료구조

생성일: 2022년 3월 22일 오후 2:02

## week 3 포인터

 0. 자

<aside>
💡 * : 선언할 때 변수가 포인터라는 것을 나타내는 연산자.

*은 사용의 따라 다양한 의미를 나타낸다. → 곱하기, 포인터 변수 선언, 간접참조

& : 변수의 계산을 계산하는 연산자.

</aside>

1. 포인터
2. 배열과 포인터
- 배열은 그 자체로 주소(위치)를 나타낸다. 즉 포인터 변수와 유사하다. 단, 포인터 변수와 달리 배열명의 값(주소)는 임의로 변경할 수 없다. like ’상수 포인터’

```cpp
double scores[10] = { 10, 20, 30 };
double *ptr;

ptr = scores;

cout << ptr++ << endl;//가능
cout << scores++ << endl;//불가능-배열명의 값을 변경할 수 없다.
```

- 포인터 변수가 배열명을 가리킬 때 그 연산은 다음/이전 원소를 가리키는 것이다.

```cpp
double scores[10] = { 10, 20, 30};
double ptr;

ptr = scores;

cout << scores << endl;
cout << &scores << endl;
cout << &scores[0] << endl;

cout << *(scores) + i << endl; 
cout << *(scores + i) << endl; // 컴퓨터가 사용하는 방식
cout << scores[i] << prt[i] << *(ptr + i) //전부 scores 베열의 i번째 원소를 출력한다.

//*(scores) === *scores === *(scores + 0) === scores[0]

//위 세 줄은 scores 배열의 첫번째 원소(배열의 시작점) 주소를 출력한다. 
```