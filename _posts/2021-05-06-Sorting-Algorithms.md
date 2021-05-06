# 정렬 알고리즘

------



## 1. 버블 정렬(Bubble Sort)

 버블 정렬 알고리즘이란 이웃하는 숫자를 비교하여 작은 수를 앞쪽으로 이동시키는 과정을 반복하여 정렬하는 알고리즘이다. 오름차순으로 정렬하면 작은 수는 배열의 앞부분으로 이동하게 되는데, 이를 좌우가 아닌 상하로 그린 배열로 생각하여 보면 작은 수가 마치 '거품'처럼 위로 올라가는 것을 연상하게 한다.

```java
public static int[] BubbleSort(int[] A) {
    for (int pass = 1; pass <= A.length - 1; pass++) {
        for (int i = 1; i <= A.length - pass; i++) {
            if (A[i - 1] > A[i]) { //이웃하는 숫자를 비교
                int temp = A[i - 1];
                A[i - 1] = A[i];
                A[i] = temp;
            }
        }
    }
    return A;
}
```

- 버블 정렬 알고리즘은 이중 for문으로 구성되어 있는데, pass가 1에서 n-1로 증가함에 따라 비교 횟수가 n-1에서 1로 감소하므로 총 비교 횟수는 (n-1)+(n-2)+(n-3)+...+1=n(n-1)/2 이다. if 조건이 참일때 실행되는 자리 바꿈은 O(1) 시간이 소요되므로 버블 정렬 알고리즘의 시간 복잡도는 O(n^2)*O(1)=**O(n^2)**이다.



## 2. 선택 정렬(Selection Sort)

 선택 정렬 알고리즘이란 입력 배열 전체에서 최소값을 '선택'하여 배열의 0번 원소와 자리를 바꾸고, 다음엔 0번 원소를 제외한 나머지 원소에서 최솟값을 '선택'하여 배열의 1번 원소와 자리를 바꾸는 알고리즘이다. 즉, 원소 중 최솟값을 '선택'하는 과정을 통해 오름차순 정렬된 배열을 얻을 수 있다.

```java
public static int[] SelectionSort(int[] A) {
    for (int i = 0; i <= A.length - 2; i++) {
        int min = i;
        for (int j = i + 1; j <= A.length - 1; j++) {
            if (A[j] < A[min]) {
                min = j;
            }
        } //원소 중 최솟값을 '선택'하는 과정
        int temp = A[i];
        A[i] = A[min];
        A[min] = temp;
    }
    return A;
}
```

- 선택 정렬 알고리즘도 이중 for문으로 구성되어 있는데 버블 정렬과 마찬가지로 i가 증가함에 따라 안의 for문 즉, 비교가 n-1, n-2, ..., 1번 수행되어 총 비교 횟수는 (n-1)+(n-2)+(n-3)+...+1=n(n-1)/2 이다. for문 안의 자리 바꿈은 O(1) 시간이 소요되므로 선택 정렬 알고리즘의 시간 복잡도는 **O(n^2)**이다.



## 3. 삽입 정렬(Insertion Sort)

 삽입 정렬 알고리즘이란 배열을 정렬된 부분(앞부분)과 정렬 안 된 부분(뒷부분)으로 나누고, 정렬 안된 부분의 가장 왼쪽 원소를 정렬된 부분의 적절한 위치에 삽입하여 정렬되도록 하는 과정을 반복하는 알고리즘이다. 이렇게 정렬 안 된 부분의 원소 하나가 정렬된 부분에 삽입됨으로써 정렬된 부분의 원소의 수는 줄어들고 정렬이 안 된 부분의 원소 수는 줄어들게 된다. 이를 반복하여 수행하면 정렬이 안 된 부분엔 아무 원소도 남지 않고 정렬된 부분에 모든 원소가 있게 된다.

*이때, 정렬은 배열의 첫 번째 원소만이 정렬된 부분에 있는 상태에서 정렬을 시작한다.*

```java
public static int[] InsertionSort(int[] A) {
    for (int i = 1; i <= A.length - 1; i++) { //첫번째 원소만이 정렬된 부분에 있는 사애에서 정렬을 시작하므로 i=1부터 시작한다.
        int c = A[i]; //정렬 안 된 부분의 가장 왼쪽 원소
        int j = i - 1; //정렬된 부분에 c를 삽입할 위치를 고르는 j
        while (j >= 0 && A[j] > c) {
            int temp = A[j + 1];
            A[j + 1] = A[j];
            A[j] = temp;
            j--;
        }
        A[j + 1] = c;
    }
    return A;
}
```

- 삽입 정렬 알고리즘은 i가 증가함에 따라 정렬된 부분의 원소가 증가해 c를 삽입할 위치를 고르기 위해 시행되는 비교 횟수도 1, 2, ...., n-1로 증가하므로 총 비교 횟수는 1+2+...+(n-1)=n(n-1)/2이다. while 루프 안의 코드의 수행시간은 O(1) 이므로 삽입 정렬 알고리즘의 시간 복잡도는 O(n^2)*O(1)=**O(n^2)**이다.

  

## 4. 쉘 정렬(Shell Sort)

 버블 정렬이나 삽입 정렬의 경우 오름차순 정렬을 가정했을 때 가장 작은 숫자가 배열의 마지막에 있다면 이 원소가 배열의 끝에서 끝으로 이동하는 과정에서 많은 비교를 하며 느리게 이동하게 된다. 쉘 정렬은 이러한 단점을 보완하기 위해서 삽입 정렬을 이용하여 배열 뒷부분의 작은 숫자를 앞부분으로 빠르게 이동시키는 동시에 앞부분의 큰 숫자는 뒷부분으로 이동시킨 다음 마지막으로 삽입 정렬을 수행하는 알고리즘이다.

 간격을 이용하여 간격별로 그룹을 만들어서 그룹별로 정렬을 하는 과정을 반복한 후 마지막엔 간격을 1로 놓고 수행함으로써 삽입 정렬 그 자체를 수행하여 준다.

```java
public static int[] ShellSort(int[] A) {
    int[] gap = {1750, 701, 301, 132, 57, 23, 10, 4, 1}; //Marcin Ciura의 간격
    int k;
    for (k = 0; k < gap.length; k++) {
        if (A.length > gap[k]) {
            break;
        }
    } //간격을 정해주기 위함
    for (int h = k; h < gap.length; h++) {
        int g = gap[h];
        for (int i = g; i < A.length; i++) {
            int c = A[i];
            int j = i;
            while (j >= g && A[j - g] > c) {
                int temp = A[j];
                A[j] = A[j - g];
                A[j - g] = temp;
                j -= g;
            }
            A[j] = c;
        }
    }
    return A;
}
```

- 쉘 정렬은 간격 선정에 따라 수행 속도가 좌우된다. 최악의 경우 시간복잡도는 O(n^2)이고, 히바드의 간격 2k-1(2k-1, ..., 7, 5, 3, 1)을 사용하면 O(n^1.5)이다. 많은 실험을 통한 쉘 정렬의 시간복잡도는 **O(n^1.25)**로 알려지고 있다. 지금까지 알려진 가장 좋은 성능을 보인 간격은 Marcin Ciura의 간격 1, 4, 10, 23, 57, 132, 301, 701, 1750 이다. 이러한 쉘 정렬은 입력 크기가 매우 크지 않은 경우에서 매우 좋은 성능을 보여준다. 



## 5. 성능 평가

 성능 평가는 각 알고리즘을 세 개의 다른 입력을 넣어주어 비교해 주었다.

1. 랜덤으로 배치되어 있는 입력
2. 어느정도 정렬되어 있는 입력 (여기선 정렬 후 10% 정도 swap 해주었다.)
3. 내림차순으로 정렬되어 있는 입력 (우리는 오름차순 배열을 원한다고 가정)

```java
public static int[] random(int n){
    Random r = new Random();
    int[] A = new int[n];
    for(int i=0; i<n; i++){
        A[i] = r.nextInt(100);
    }
    return A;
}

public static int[] somesort(int n){
    Random r = new Random();
    int[] A = new int[n];
    for(int i=0; i<n; i++){
        A[i] = r.nextInt(100);
    }
    A = BubbleSort(A);
    for(int i=0; i<(n*0.1); i++){
        int a = r.nextInt(A.length);
        int b = r.nextInt(A.length);
        int temp = A[a];
        A[a] = A[b];
        A[b] = temp;
    }
    return A;
}

public static int[] descending(int n){
    Random r = new Random();
    int[] A = new int[n];
    for(int i=0; i<n; i++){
        A[i] = r.nextInt(100);
    }
    for (int pass = 1; pass <= A.length - 1; pass++) {
        for (int i = 1; i <= A.length - pass; i++) {
            if (A[i - 1] < A[i]) {
                int temp = A[i - 1];
                A[i - 1] = A[i];
                A[i] = temp;
            }
        }
    }
    return A;
}
```
- 코드 실행 시간을 측정하기엔 어려움이 있어 알고리즘이 돌아가는 동안 배열의 원소 간에 비교 횟수를 세어 소요 시간을 비교하였다.

<img src="https://user-images.githubusercontent.com/80517298/117284525-e206db80-aea1-11eb-9ef9-2507d15a9d7d.jpg" alt="버블정렬 1" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284575-f0ed8e00-aea1-11eb-9b73-52a7e876071f.jpg" alt="버블정렬 2" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284608-fe0a7d00-aea1-11eb-9af2-60f4002f550e.jpg" alt="버블정렬 3" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284679-0e225c80-aea2-11eb-9d9c-05e32862e77b.jpg" alt="선택정렬 1" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284684-0fec2000-aea2-11eb-9d4e-52ddf4b313a5.jpg" alt="선택정렬 2" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284691-11b5e380-aea2-11eb-9ef4-f6c6971188f9.jpg" alt="선택정렬 3" width="300" height="150" />



<img src="https://user-images.githubusercontent.com/80517298/117287095-f00a2b80-aea4-11eb-86c9-2fabf5f15b8a.png" alt="버블정렬, 선택정렬" width="400" height="350" />

- 버블 정렬과 선택 정렬은 입력이 랜덤하거나 어느정도 정렬되어 있거나 역으로 정렬되어 있어도 이들을 구분하지 않고 항상 일정한 시간복잡도를 나타낸다. 즉, 입력에 민감하지 않은 (input insensitive) 알고리즘이다.

------

<img src="https://user-images.githubusercontent.com/80517298/117284779-2d20ee80-aea2-11eb-85fc-1db8032a3389.jpg" alt="삽입정렬 1" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284783-2eeab200-aea2-11eb-917c-c296f563253a.jpg" alt="삽입정렬 2" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284787-301bdf00-aea2-11eb-9bf7-16d680be074d.jpg" alt="삽입정렬 3" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117287101-f13b5880-aea4-11eb-972e-69725022028e.png" alt="삽입정렬" width="400" height="350" />

(랜덤한 배열 입력 : 파란색, 어느정도 정렬된 배열 입력 : 빨간색, 내림차순 정렬된 배열 입력 : 초록색)

- 삽입 정렬은 입력의 상태에 따라 수행시간이 달라지는데 이미 정렬되어 있으면 while 조건이 '거짓'이 되므로 원소의 이동이 없어 n-1만의 비교만 하면 정렬을 마치게 된다. 이에 의해 어느정도 정렬이 되어있는 입력에선 수행시간이 짧아지고 내림차순되어 있는 입력(역을 정렬되어 있는 입력)에서는 수행시간이 길어진다.

------

<img src="https://user-images.githubusercontent.com/80517298/117284819-3a3ddd80-aea2-11eb-9eee-4d65d68ab782.jpg" alt="쉘정렬 1" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284827-3b6f0a80-aea2-11eb-957e-3a6ad3258463.jpg" alt="쉘정렬 2" width="300" height="150" />

<img src="https://user-images.githubusercontent.com/80517298/117284834-3d38ce00-aea2-11eb-9cd6-b98c4a80c9d0.jpg" alt="쉘정렬 3" width="300" height="150" />



<img src="https://user-images.githubusercontent.com/80517298/117287105-f26c8580-aea4-11eb-87d1-ffc34961a35e.png" alt="쉘정렬" width="400" height="350" />

(랜덤한 배열 입력 : 파란색, 어느정도 정렬된 배열 입력 : 빨간색, 내림차순 정렬된 배열 입력 : 초록색)

- 쉘 정렬은 입력 크기가 매우 크지 않은 경우에서 매우 좋은 성능을 보여준다. 

------

