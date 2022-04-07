# 3장. 주소와 포인터

<aside>
💡 *(에스테리스크) : 선언할 때 변수가 포인터라는 것을 나타내는 연산자.
💡 &(앰퍼샌드) : 주소연산자. 변수의 주소를 나타낸다.

</aside>

1. 포인터
    - 정의: 포인터(포인터 변수)란 다른 변수의 주소를 저장하는 변수이다.
    - 선언 및 초기화: (자료형) *(포인터 변수이름) = &(대상변수);
        
        단 대상변수와 포인터변수의 자료형은 동일해야 한다.
        
        ```cpp
        int i, j;
        int *ptr; //ptr은 포인터 변수(선언)
        
        ptr = &i //ptr은 i의 주소를 가리키는 포인터(초기화)
        *ptr = 10; //ptr이 가리키는(i) 변수값에 10을 저장
        j = *ptr; //j에 ptr이 가리키는(i) 변수값을 저장
        ```
        
    - 주의점: 초기화가 안된 상태에서 사용하지 않는다 - 가리키지 않을 때는 NULL로 초기화
    - 필요성 - swap함수
        
        ```cpp
        swap(int x, int y){
        int temp;
        temp = x;
        x = y;
        y = temp;
        }
        
        main () {
        	int i = 10;
        	int j = 20;
        	
        	cout << 'i =' << i << endl;
        	cout << 'j =' << j << endl;
        	
        	swap(i, j); //변수의 값을 바꾸는 함수
        	
        	cout << 'i =' << i << endl;
        	cout << 'j =' << j << endl;
        }
        ```
        
        ```cpp
        swap(int *x, int *y){
        int temp;
        temp = *x;
        *x = *y;
        *y = temp;
        }
        
        main () {
        	int i = 10;
        	int j = 20;
        	
        	cout << 'i =' << i << endl;
        	cout << 'j =' << j << endl;
        	
        	swap(&i, &j); //변수대신 주소값을 넘긴다
        	
        	cout << 'i =' << i << endl;
        	cout << 'j =' << j << endl;
        }
        ```
        
    
2. 배열과 포인터
    - 배열명
        - 배열은 그 자체로 주소(위치)를 나타낸다. 그 배열의 시작 주소를 의미한다.
        - 즉 배열명은 포인터 변수와 유사하다. 단, 포인터 변수와 달리 배열명의 값(주소)는 임의로 변경할 수 없다. like ’상수 포인터’
            
            ```cpp
            double scores[10] = { 10, 20, 30 };
            double *ptr;
            
            ptr = scores;
            
            cout << ptr++ << endl;//가능
            cout << scores++ << endl;//불가능-배열명의 값을 변경할 수 없다.
            ```
            
    - 증감 연산: 포인터 변수가 배열명을 가리킬 때 그 변수의(혹은 그 변수명의) 연산(증가/감소)은 다음/이전 원소를 가리키는 것이다. 왜냐면 배열은 연속된 기억장소를 차지하므로.
        
        ```cpp
        double scores[10] = {10, 20, 30};
        double *ptr;
        
        ptr = &scores;
        
        cout << scores << endl;
        cout << &scores << endl;
        cout << &scores[0] << endl;
        //위 세 줄은 scores 배열의 첫번째 원소(배열의 시작점) 주소를 출력한다. 
        
        for(int i =0, i < 10, i++){ 
        	cout << *(scores) + i << endl; //
        	cout << *(scores + i) << endl; // 컴퓨터가 사용하는 방식. scores[i] 가리킴
        	cout << scores[i] << prt[i] << *(ptr + i) 
        	//전부 scores 베열의 i번째 원소를 출력한다.
        }
        
        //*(scores) === *scores === *(scores + 0) === scores[0]
        ```
        
    
    <aside>
    💡 배열명을 이용한 포인터를 어떻게 표기하든 컴퓨터는 *(score + i)의 형태로 받아들인다.
    
    </aside>
    

1. 2차원 배열과 포인터
    - 2차원 배열의 배열명은 이중 포인터의 성격을 가진다. →포인터가 가리키는 곳에 가면 또 포인터(배열명)가 있는 것!! ‘원소가 배열인 배열’이라고 생각하면 더 쉽다.
    
    ```cpp
    int scores [3][4];
    
    cout << &score << score << &score[0] << score[0] << endl; 
    // 전부 같은 값 - 이 배열의 시작 주소
    
    cout << *score << *(score+1) << *(score+2) << endl;
    // score[0][0], score[1][0], score[2][0]의 주소 가리킴
    ```
    
    - 이중 포인터: 2차원 배열의 원소를 가리키고 싶을 땐 * 연산이나 []기호를 2개 붙여야 원소를 의미한다
        
        ex) *score[1], score[1][2], **score
        

1. 문자열
    - 정의: 배열의 특성을 사진, 여러 개의 문자로 구성된 하나의 자료. 배열의 특성을 그대로 가진다.
    - 선언 및 초기화: char 배열명[] = “문자열의 내용”
    - 원칙
        - 문자열의 배열명을 출력하면 문자 전체를 출력한다. (즉 배열명이 주소를 나타내긴 하지만 출력하면 ‘그 주소에서 null까지 출력’하는 동작을 수행하는 것)
        - 문자열의 끝을 지정해주기 위해서는 null을 표시해주어야 한다. 때문의 문자열의 길이를 딱 문자 길이만큼만 하면 안됨
    
    ```cpp
    char *ptr, string[] = "This is my world";
    ptr = string;
    
    cout << string << " : " << strlen(string) << endl; //문자열 길이 출력
    cout << string + 5 << " : " << ptr + 8 << endl; // 문자열 + 상수 값 출력
    
    *(ptr + 12) = NULL;
     // *(ptr+16) = NULL; or *(ptr+18)=NULL // *(ptr+16) = ‘A’; NULL을 지우면???
    
    cout << string << " : " << ptr << endl;
    ptr ++;
    cout << string << " : " << ptr << endl;
    ```
    
    - 출력값
        
        **This is my world : 16 //문자열의 길이에서 null은 포함되지 않는다.**
        
        **is my world:my world // 문자열 + n 출력 시 n번째 문자부터 null까지 출력한다.**
        
        **This is my w : This is my w //**
        
        **This is my w : his is my w**
        

1. 동적 메모리 할당
    - 동적 메모리: 메모리를 실행할 때 그 크기가 결정되는 것(↔정적메모리: 컴파일 시 결정)
    - 원소의 개수를 미리 파악하지 못하는 경우 동적 메모리 할당을 활용해야 한다.
    
    ```cpp
    double ave, sum = 0;
    int num;
    int *ptr;
    //아직 개수를 모르기 때문에 배열이 아니라 포인터를 선언한다.
        
    cout << "학생 수는? ";
    cin >> num;
    ptr = new int[num]; 
    //입력받은 학생수만큼 ptr주소에 메모리를 확보한다. 포인터가 가리키는 곳에 추가적인 메모리를 할당하는 방식.
    //int ptr[num]과 같은 효과(배열선언시 변수를 사용할 수는 없음)
        
    for (int i = 0; i < num; i++)
        {cout << "학생 " << i+1 << "의 점수는? ";
         cin >> score[i]; //*(score+i)도 가능
         sum += score[i];
        }
        
    ave = sum / num;
    cout << "average: "<< ave << endl;
    ```
