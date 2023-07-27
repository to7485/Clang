# 스택
- Stack은 건초나 짚더미처럼 뭔가를 쌓아올린 더미를 뜻합니다.
- Stack ADT도 데이터를 바닥부터 쌓아올리는 구조로 되어있다.
- 스택에서는 <b>가장 마지막에 들어간 데이터가 제일 먼저 나오고(Last In First Out), 가장 먼저 들어간 데이터는 가장 나중에 나온다(First In Last Out)</b>
- C언어의 Stack 메모리 영역도 자료구조 Stack으로 구현이 되어 있습니다. 그래서 지역변수는 스택에 할당된다 라고 표현합니다.
- 스택은 소프트웨어 분야에서 매우 중요한 역할을 맡고 있다.
- 자동 메모리가 스택을 기반으로 동작하고 거의 대부분의 네트워크 프로토콜도 스택을 기반으로 구성되어 있습니다.
- 뿐만 아니라 컴파일러의 구문 분석기, 이미지 편집 프로그램의 되돌리기(Undo)기능도 스택을 이용하고 있다.

## 스택의 핵심기능 : 삽입과 제거 연산
- 스택 ADT의 주요 기능은 삽입(Push)과 제거(Pop)연산 이다.
- 그 외의 기능들은 두 연산을 위한 보조 연산에 지나지 않는다.

- 삽입 연산은 스택 위에 새로운 노드(요소)를 '쌓는'일을 합니다.

![image](https://github.com/to7485/Clang/assets/54658614/5bfd3cf0-46d3-4683-96ed-619ca3278e38)

- 반대로 제거 연산은 스택에서 최상위 노드를'걷어'낸다.

![image](https://github.com/to7485/Clang/assets/54658614/b3f51f54-9acb-4059-84b4-3a3f6099882f)

## 배열로 구현하는 스택
- 배열을 이용한 스택은 용량을 동적으로 변경하는 비용이 크다는 단점이 있지만 구현이 간단하다는 장점 있다.
- 배열 기반의 스택은 각 노드를 동적으로 생성하고 제거하는 대신, 스택 생성 초기에 사용자가 부여한 용량만큼 노드를 한꺼번에 생성한다.
- 최상위 노드의 위치를 나타내는 변수를 두고 삽입과 제거 연산을 수행한다.

## 노드의 표현
- 노드가 존재하는 위치는 배열의 인덱스로 알 수 있기 때문에 노드에 대한 포인터가 필요 없다.
```c
typedef int ElementType;

typedef struct tagNode{
ElementType Data;
} Node;
```

## 스택의 표현
- 배열 기반의 스택은 다음 세가지 필드를 갖고 있어야 한다.
  - 용량
  - 최상위 노드의 위치
  - 노드 배열
 
- 용량은 스택이 얼마만큼의 노드를 가질 수 있는지 알기 위해 사용된다.
- 최상위 노드의 위치는 삽입/제거 연산을 할 때 최상위 노드에 접근할 수 있게 도와준다.
- 노드 배열은 스택에 쌓이는 노드를 보관하는데 사용된다.

```c
typedef struct tagArrayStack{
  int Capacity; //노드의 개수
  int Top; //최상위 노드의 위치
  Node* Nodes; //노드 배열
} ArrayStack;
```

- 노드배열을 자유 저장소(Heap)에 할당하고 Node포인터는 자유 저장소(Heap)에 할당된 배열을 가리키는 용도로 사용할 것이다.

![image](https://github.com/to7485/Clang/assets/54658614/96cef174-d4ab-45d4-9a35-7bc2b77a9ef0)

## 스택 및 노드 생성/소멸

### 스택의 생성
- 첫번째 인자는 ArrayStack 구조체이고, 두번재는 스택의 용량을 나타내는 노드의 개수이다.
- 처음 호출된 malloc()은 ArrayStack을 자유저장소(Heap)에 쌓기 위해 사용됐고
- 두번재 호출된 malloc()은 매개변수로 입력된 개수만큼 노드를 미리 생성하는데 사용이 되었다.
- ArrayStack의 Capacity는 배열의 용량을 저장하고 최상위 노드의 위치를 가리키는 Top을 -1로 초기화 한다.
- Top을 0이 아닌 -1로 초기화를 하는 이유는 C언어에서 첫 번째 배열의 요소를 가리키는 첨자가 0이므로 비어있는 스택의 최상위 위치가 이보다 작아야 하기 때문이다.
- Top은 노드가 삽입될 때마다 1씩 증가하고 노드가 삭제될 때마다 1씩 감소합니다.
```c
void AS_CreateStack(ArrayStack** Stack, int Capacity) {
	//스택을 자유 저장소(Heap)에 생성
	(*Stack) = (ArrayStack*)malloc(sizeof(ArrayStack));

	//입력된 Capacity만큼의 노드를 자유 저장소(Heap)에 생성
	(*Stack)->Nodes = (Node*)malloc(sizeof(Node)*Capacity);

	//Capacity 및 Top의 초기화
	(*Stack)->Capacity = Capacity;
	(*Stack)->Top = -1;
}
```

### 스택의 삭제
```c
void AS_DestroyStack(ArrayStack* Stack) {
	//노드를 자유 저장소에서 해제
	free(Stack->Nodes);

	//스택을 자유 저장소에서 해제
	free(Stack);
}
```

## 노드 삽입 연산
- 삽입(Push)연산은 최상위 노드의 Index(Top)에서 1을 더한 곳에 새 노드를 입력하도록 구현한다.
```c
void AS_Push(ArrayStack* Stack, ElementType Data) {
	Stack->Top++;
	Stack->Nodes[Stack->Top].Data = Data;
}
```

## 노드 제거 연산
- 최상위 노드의 인덱스(Top)값을 1만큼 낮추도록 구현을 하면 된다.
- 주의해야 할 점은 제거 연산에서는 최상위 노드에 있던 데이터를 반환을 해야 한다.

```c
ElementType AS_Pop(ArrayStack* Stack) {
	int Position = Stack->Top--;
	return Stack->Nodes[Position].Data;
}
```

# 배열 기반 스택 예제 프로그램
```c
int AS_GetSize(ArrayStack* Stack) { //스택의 사이즈를 반환
	return Stack->Top + 1;
}

ElementType AS_Top(ArrayStack* Stack) { //최상위 노드의 데이터만 반환
	return Stack->Nodes[Stack->Top].Data;
}

int AS_IsEmpty(ArrayStack* Stack) { //스택이 비어있는지 검사하는 함수
	return(Stack->Top == -1);
}

void main() {
	ArrayStack* Stack = NULL;

	AS_CreateStack(&Stack, 10);

	AS_Push(Stack, 3);
	AS_Push(Stack, 37);
	AS_Push(Stack, 11);
	AS_Push(Stack, 12);

	printf("Capacity: %d, Size: %d, Top:%d\n\n", Stack->Capacity, AS_GetSize(Stack), AS_Top(Stack));

	for (int i = 0; i < 4; i++) {
		if (AS_IsEmpty(Stack)) {
			break;
		}
		printf("Popped: %d ", AS_Pop(Stack));
		if (!AS_IsEmpty(Stack)) {
			printf("Current Top: %d\n", AS_Top(Stack));
		}
		else {
			printf("Stack is Empty.\n");
		}
	}

	AS_DestroyStack(Stack);
}
```
# 링크드 리스트로 구현하는 스택
- 링크드 리스트가 배열보다 좋은점은 스택 용량에 제한을 두지 않아도 된다는점이다.

## 링크드 리스트 기반 스택과 스택의 노드 표현
- 링크드 리스트는 배열과 달리 인덱스를 활용하여 노드에 접근할 수 없다.
- 따라서 링크드 리스트로 스택을 구현하려면 노드는 자신의 위에 위치하는 노드에 대한 포인터를 갖고 있어야 한다.
```c
typedef struct tagNode{
	char* Data;
	struct tagNode* NextNode;
}Node;
```

<img width="400" alt="image" src="https://github.com/to7485/Clang/assets/54658614/0af4e55b-7ec5-4434-82ab-5dcd4ba83ddf">

- 링크드 리스트 스택은 배열 기반 스택과 달리 '스택의 용량'이나 '최상위 노드의 인덱스'가 없다.
- 대신 링크드 리스트(List포인터)의 헤드와 테일(Top 포인터)에 대한 포이터가 필요합니다.
```c
typedef struct tagLinkedListStack{
	Node* List; //데이터를 담는 링크드 리스트를 가리킨다.
	Node* Top; // 스택의 입출력이 이루어지는 최상위 노드에 대한 포인터
}LinkedListStack;
```
- Top포인터 없이도 List포인터를 사용해서 스택의 최상위 노드에 접근을 할 수 도 있다.
- 대신 순차탐색을 해야 하기 때문에 비효율적이다.
- Top포인터를 이용하면 8바이트를 소비하는 대신 최상위 노드를 찾는 시간을 아낄수 있다.

<img width="484" alt="image" src="https://github.com/to7485/Clang/assets/54658614/7dd7e975-3178-40f6-bfc2-d11c2bef5ea7">

## 링크드 리스트 기반 스택의 기본 연산
- Single Linked List로 스택을 구현해보자.

## 스택 생성/소멸 연산
- 스택의 생성
- LinkedListStack 구조체를 Heap영역에 할당하는것 뿐입니다.
```c
//스택의 생성
void LLS_CreateStack(LinkedListStack** Stack){
    //스택을 Heap영역에 생성
    (*Stack) = (LinkedListStack*)malloc(sizeof(LinkedListStack));
    (*Stack)->List = NULL;
    (*Stack)->Top = NULL;
};
```
- 스택의 소멸
- 먼저 각 노드를 제거하고 Heap영역에서 LinkedListStack의 구조체의 할당을 해제합니다.
```c
//스택의 소멸
void LLS_DestroyStack(LinkedListStack* Stack){
    while(!LLS_IsEmpty(Stack)){
        Node* Popped = LLS_Pop(Stack);
        LLS_DestroyStack(Popped);
    }

    //스택을 Heap영역에서 해제
    free(Stack);
};
```

## 노드의 생성/소멸
- 노드의 생성
	- Stack의 Node를 Heap에 생성할 때 문자열을 저장할 공간도 함께 생성해야 한다.
	- malloc()함수가 Node구조체를 할당하기 위해 한번, Node구조체의 Data필드를 할당하기 위해 한번 총 두번 호출된다는 사실을 알 수 있다.
```c
Node* LLS_CreateNode(char* NewData){
    Node* NewNode = (Node*)malloc(sizeof(Node));
    NewNode->Data = (char*)malloc(strlen(NewData)+1);

    strcpy(NewNode->Data, NewData); //데이터를 저장한다.

    NewNode->NextNode = NULL; //다음 노드에 대한 포인터는 NULL로 초기화한다.

    return NewNode; //노드의 주소를 반환한다.
};
```

- 노드의 소멸
	- Data필드를 할당 해제 하기 위해 한번
   	- 노드를 할당 해제 하기 위해 한번 free()함수는 총 두번 호출된다.
```c
void LLS_DestroyNode(Node* _Node){
    free(_Node->Data);
    free(_Node);
};
```

## 노드 삽입 연산
- 삽입 연산은 스택의 최상위 노드 Top에 새 노드를 얹도록 구현만 하면 된다.
- 그리고 최상위 노드의 주소를 LinkedListStack 구조체의 Top필드에 등록하면 된다.
```c
//노드의 삽입
void LLS_Push(LinkedListStack* Stack, Node* NewNode){
    if(Stack->List == NULL){
        Stack->List = NewNode;
    } else{
        //스택의 Top위에 새 노드를 얹는다.
        //Stack->Top : 맨위에 있는 노드
        Stack->Top->NextNode = NewNode;
    }

    //스택의 Top필드에 새 노드의 주소를 등록한다.
    Stack->Top = NewNode;
};
```

## 노드 삭제 연산
- Linked List Stack에서 제거 연산은 네 단계로 이루어진다.
	- 현재 최상위 노드(Top)의 주소를 다른 포인터에 복사한다.
 	- 새로운 최상위 노드(현재 최상위 노드)의 바로 아래(이전)노드를 찾는다.
  	- LnikedListStack 구조체의 Top 필드에 새로운 최상위 노드의 주소를 등록한다.
  	- 단계1에서 포인터에 저장했던 예전 최상위 노드의 주소를 반환한다.
```c
//노드의 삭제
Node* LLS_Pop(LinkedListStack* Stack){
    //LLS_Pop()함수가 반환할 최상위 노드 저장
    Node* TopNode = Stack->Top;

    if(Stack->List == Stack->Top){
        Stack->List = NULL;
        Stack->Top = NULL;
    } else{
        //Top아래에 있던 노드를 새로운 CurrentTop에 저장
        Node* CurrentTop = Stack->List;
        while(CurrentTop != NULL && CurrentTop->NextNode != Stack->Top){
            CurrentTop = CurrentTop->NextNode;
        }
        //CurrentTop을 Top에 저장
        Stack->Top = CurrentTop;
        Stack->Top->NextNode = NULL;
    }
    return TopNode;
};
```
## 그 외의 메서드
```c
//최상위 노드를 반환
Node* LLS_Top(LinkedListStack* Stack){
    return Stack->Top;
}

//스택의 개수 반환
int LLS_GetSize(LinkedListStack* Stack){
    int Count = 0;
    Node* Current = Stack->List;

    while(Current != NULL){
        Current = Current->NextNode;
        Count++;
    }
    return Count;
}

//스택이 비어있는지 검증하는 메서드
int LLS_IsEmpty(LinkedListStack* Stack){
    return (Stack->List == NULL);
}
```

## Linked List 기반 Stack 예제 프로그램
```c
int main(){
    int Count = 0;
    Node* Popped;

    LinkedListStack* Stack;

    LLS_CreateStack(&Stack);

    LLS_Push(Stack, LLS_CreateNode("abc"));
    LLS_Push(Stack, LLS_CreateNode("def"));
    LLS_Push(Stack, LLS_CreateNode("efg"));
    LLS_Push(Stack, LLS_CreateNode("hij"));

    Count = LLS_GetSize(Stack);
    printf("Size: %d, Top: %s\n",Count,LLS_Top(Stack)->Data);

    for(int i = 0; i< Count; i++){
        if(LLS_IsEmpty(Stack)){
            break;
        }
        Popped = LLS_Pop(Stack);

        printf("Popped: %s, ",Popped->Data);

        LLS_DestroyNode(Popped);

        if(!LLS_IsEmpty(Stack)){
            printf("Current Top: %s\n",LLS_Top(Stack)->Data);
        } else {
            printf("Stack Is Empty.\n");
        }
    }

    LLS_DestroyStack(Stack);



    return 0;
}
```

# 사칙연산 계산기
- 수식 분석기 기반의 사칙연산 계산기 만들기
- 계산기가 갖춰야 하는 기능은 단순하다.
- 사칙연산만으로 이루어진 식을 분석해서 풀 수 있으면 된다.
```
1+3.334/(4.28*(110-7729))
```
- 우리는 괄호부터 풀고 그 다음 곱셈과 나눗셈을 처리한다는 것을 알고 있다.
- 하지만 컴퓨터가 이 문제를 풀게 하려면 알고리즘을 제공해야 한다.
- 첫번째 단계는 원본 수식을 컴퓨터가 풀기 쉬운 형식으로 변환한다.
- 두번재 단계는 변환된 수식을 계산하도록 할것이다.

## 수식의 중위 표기법과 후위 표기법
- 후위 표기법은 <b>연산자가 피연산자 뒤에 위치한다는 규칙</b>을 갖는다.
- 우리가 평소에 사용하던 방법이 중위 표기법이다.

## 후위표기식을 계산하는 알고리즘
- 후위 표기식을 계산하는 알고리즘은 두 가지 규칙으로 이루어진다.

1. 식의 왼쪽부터 요소를 읽어내면서 
