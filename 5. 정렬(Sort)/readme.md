# 정렬
- 정렬이란 정해진 기준에 따라 데이터를 순서대로, 그리고 체계적으로 정리하는 일고리즘이다.
- 가격 비교 사이트는 가격, 평점, 출시일 등을 기준으로 상품을 오름차순/내림차순으로 정렬하여 고객의 선택을 돕는다.
- 대학은 학생의 입시 성적을 정렬하여 합격 여부를 가려낸다.

## 정렬을 사용하는 이유
- 정렬의 목적은 <b>탐색</b>에 있다.
- 데이터를 가지런히 나열하는 것 자체가 목적이 아니라 데이터를 빠르고 쉽게 찾을 수 있도록 하는것이 목적이다.

## 버블정렬
- 자료구조를 순회하면서 이웃한 요소들끼리 데이터를 교환하며 정렬을 수행한다.

![image](https://github.com/to7485/Clang/assets/54658614/ef745733-98ff-48bf-896c-86739b397fd1)

- 오름차순으로 정렬을 할 것이기 때문에 왼쪽에 있는 요소가 오른쪽에 있는 요소보다 작아야 한다.

![image](https://github.com/to7485/Clang/assets/54658614/12a3c37d-ef8f-4731-8f37-e42df8949a7d)

- 왼쪽이 5, 오른쪽이 1 이므로 왼쪽 데이터가 큽니다. 두 이웃 요소간 데이터를 교환해야 한다.

![image](https://github.com/to7485/Clang/assets/54658614/0adfa8e5-9be6-4a5c-b055-891b7460b185)

![image](https://github.com/to7485/Clang/assets/54658614/9b9ec087-eea6-42de-9208-9bf72b702191)

![image](https://github.com/to7485/Clang/assets/54658614/3319d073-79ea-4c0b-bfb5-0bde92172bc5)

![image](https://github.com/to7485/Clang/assets/54658614/1a9da664-7722-4c01-bd1d-40dfb06c4330)

- 1차 버블 정렬을 마쳤을 때 제일 큰 수인 6이 정렬이 된 모습을 볼 수 있다.
- 마지막 요소를 제외한 나머지 요소에 대해 처음부터 다시 버블정렬을 수행해야 한다.

![image](https://github.com/to7485/Clang/assets/54658614/2eb557e7-1ecc-4010-bd5e-191e0d7f05fa)

## 버블정렬의 성능 측정
- 버블정렬은 자료구조를 한 번 순회할 때 마다 정렬해야 하는 자료구조의 범위가 하나씩 줄어든다.
- 자료구조의 범위가 N이라면 N-1만큼 순회를 반복해야 정렬이 마무리 된다.

![image](https://github.com/to7485/Clang/assets/54658614/7c4c5b3c-d8e8-463d-98f5-79f63c9ac419)

- 정렬 대상 범위가 5개일때는 네 번, 4개일때는 세 번, 남은 요소가 2개일 때는 한 번만 비교를 수행한다.
- 위의 예제에서 총 비교 횟수는 모두 15회(5+4+3+2+1)가 된다.

![image](https://github.com/to7485/Clang/assets/54658614/286641c8-d35d-4db7-9587-6fc1ca3c3972)

## 버블정렬 예제 프로그램
```c
#include <stdio.h> 
 
void BubbleSort(int DataSet[], int Length) 
{ 
    int i = 0; 
    int j = 0; 
    int temp = 0; 
 
    for ( i=0; i<Length-1; i++ ) //자료구조의 크기만큼 반복 실행
    { 
        for ( j=0; j<Length-(i+1); j++ )
//외부가 한번 실행될 때마다 내부 for문의 반복 횟수는 줄어든다.
//이는 외부 for문을 실행할때마다 정렬 대상이 줄어들기 때문이다.
        { 
            if ( DataSet[j] > DataSet[j+1] ) //이웃한 요소를 비교하여 교환한다.
            { 
                temp = DataSet[j+1]; 
                DataSet[j+1] = DataSet[j]; 
                DataSet[j] = temp; 
            } 
        } 
    } 
} 
 
int main( void ) 
{ 
    int DataSet[] = {6, 4, 2, 3, 1, 5}; 
    int Length = sizeof DataSet / sizeof DataSet[0];  //배열의 길이 구하기  
    int i = 0; 
 
    BubbleSort(DataSet, Length); 
 
    for ( i=0; i<Length; i++ ) 
    { 
        printf("%d ", DataSet[i]); 
    } 
 
    printf("\n"); 
 
    return 0; 
}
```








