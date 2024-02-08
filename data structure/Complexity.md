
## 01. 시간 복잡도

프로그램이 실행되고, 완료되는데 걸리는 시간이다. 사용하는 데이터 n에 의해서 시간복잡도가 결정된다.

### 1. Big O
- 불필요한 정보를 제거하여 알고리즘 분석을 쉽게도와주는 표기법이다. 주로 Big O를 사용해서 시간복잡도를 표시한다. 
- 데이터나 사용자의 증가율에 따른 알고리즘의 성능을 예측하는 것이 목표이므로 상수와 같은 숫자들은 모두 1이 된다. 
- 정의 : 두개의 함수 f(n), g(n)이 주어졌을 때 모든 n>n0에 대하여 |f(n)|≤c|g(n)|을 만족하는 2개의 상수 c와 n0이 존재하면 f(n)=O(g(n))이다. ⇒ 즉 Big O는 함수의 상한값(worst case)을 나타내는 방법이다.
    
    |O(f(n))|||
    |---|---|---|
    |O(1)|데이터 양의 증가와 무관하게 실행 시간이 일정하다|Good|
    |O(log N)|데이터 양이 증가해도 처리 시간이 느리게 증가한다.||
    |O(N)|입력 데이터의 크기에 비례하여 처리 시간이 증가한다.||
    |O(N^2)|데이터 양이 증가함에 따라 처리 시간이 제곱 수준으로 증가한다.||
    |O(N^3)|데이터 양이 증가함에 따라 처리 시간이 세제곱 수준으로 증가한다.||
    |O(2^N)|데이터 양이 증가함에 따라 처리 시간이 기하급수적으로 증가한다.||
    |O(N!)|입력 크기 N의 팩토리얼에 비례하여 실행 시간이 증가한다. 대부분의 경우 실용적이지 않다|Bad|
    

### 2. **Big-Omega**
- 정의 : 두개의 함수 f(n), g(n)이 주어졌을 때 모든 n>n0에 대하여 |f(n)|≥c|g(n)|을 만족하는 2개의 상수 c와 n0이 존재하면 f(n)=Ω(g(n))이다. ⇒ Big-Omega는 함수의 하한(bestcase)을 나타낸다.

### 3. **Big-Theta**
- 정의 : 두개의 함수 f(n), g(n)이 주어졌을 때 모든 n>n0에 대하여 c1|g(n)|≤|f(n)|≤c2|g(n)|을 만족하는 3개의 상수 c1,c2와 n0이 존재하면 f(n)=θ(g(n))이다. ⇒ Big-Theta는 함수의 하한과 상한을 표시한다.

<br>

## 02. 공간 복잡도
프로그램이 실행되고, 완료되는데 필요한 자원공간의 양이다.

### 1. 고정 공간 요구량
- 자료구조가 사용하는 고정된 메모리 공간이다. 고정된 크기를 갖는 변수와 크기가 정해진 배열이 속한다.

### 2. 가변 공간 요구향
- 필요에 따라 동적으로 할당, 해제되는 메모리의 공간을 의미한다. instance에 따라서 사이즈가 달라지는 변수들이 속한다.