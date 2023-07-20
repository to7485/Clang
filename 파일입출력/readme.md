# 파일 입출력

## 파일(file)이란?
- 파일(file)이란 의미 있는 정보를 담고 있으며, 이름을 가지고 있는 저장 장치상의 논리적인 단위를 의미합니다.
- C언어에서는 이러한 파일을 바이트별로 따로 읽을 수 있는 연속적인 바이트의 집합으로 취급합니다.

## 파일의 종류
- 컴퓨터는 파일을 다음과 같이 두 가지 종류로 나누어서 다룹니다.

1. 바이너리 파일(binary file)
  - 바이너리 파일은 데이터의 저장과 처리를 목적으로 0과 1의 이진 형식으로 인코딩된 파일을 가리킵니다.
  - 프로그램이 이 파일의 데이터를 읽거나 쓸 때는 데이터의 어떠한 변환도 일어나지 않습니다.
2. 텍스트 파일(text file)
  - 텍스트 파일은 사람이 알아볼 수 있는 문자열로 이루어진 파일을 가리킵니다.
  - 프로그램이 이 파일의 데이터를 읽거나 쓸 때는 포맷 형식에 따라 데이터의 변환이 일어납니다.

## 파일의 입출력
- C언어에서 파일에 대한 입출력 동작은 다음과 같은 순서에 따라 진행됩니다.

1. 파일과의 스트림 생성
2. FILE 구조체 변수의 포인터를 이용한 작업 진행
3. 파일과의 스트림 종결

※ 스트림 : 스트림은 운영체제에 의해 생성되는 가상의 연결 고리를 의미합니다.

![image](https://github.com/to7485/Clang/assets/54658614/3b7d10c1-0dee-4959-ad20-91fed0ebda88)

## 파일열기작업
- FILE형 포인터 변수 생성
- FILE 포인터를 사용해 파일 스트림 생성

※FILE 포인터 :FILE의 주소를 저장하는 공간

## fopen()함수
- fopen() 함수는 파일을 열어주는 함수입니다.
- 파일을 연다는 것은 파일과의 입출력을 위한 스트림을 생성한다는 의미입니다.

### fopen()함수의 원형
```c
#include <stdio.h>

FILE *fopen(const char * restrict filename, const char * restrict mode);
```
- 함수의 첫 번째 인수는 열고자 하는 파일의 이름과 그 경로를 가지고 있는 문자열입니다.
- 두 번째 인수는 파일을 여는 데 사용할 모드를 지정하는 문자열입니다.

## 모드 문자열
- fopen() 함수는 파일을 여는 데 사용할 모드 문자열을 두 번째 인수로 전달받습니다.
- 이 모드 문자열은 파일의 사용 용도를 결정하고, 파일의 데이터를 어떤 방식으로 입출력할지를 결정합니다.

### 파일의 사용 용도를 결정하는데 사용할 수 있는 모드 문자열
1. r (read mode) : 읽기 전용 모드
  	- 파일 없으면 NULL값 반환
2. w (write mode) : 쓰기 전용 모드
  	- 파일 없으면 새로 생성
  	- 파일 있으면 내용 다 지우고 새로 만듦
  	- 여는 순간 파일 내용 다 날아감
3. a (append mode) : 추가 모드
  	- 파일 없으면 새로 생성
  	- 파일 있으면 내용 그대로 두고 뒤에 추가로 쓰게 됨

### 파일의 데이터를 어떤 방식으로 입출력할지를 결정하는 사용할 수 있는 모드 문자열
1. t (text mode) : 해당 파일의 데이터를 텍스트 파일로 인식하고 입출력함.
2. b (binary mode) : 해당 파일의 데이터를 바이너리 파일로 인식하고 입출력함.

### 추가적인 모드문자열
1. x (exclusive mode) : 열고자 하는 파일이 이미 존재하면 파일 개방에 실패함.
2. + (update mode) : 파일을 읽을 수도 있고 쓸 수도 있는 모드
  

# 쓰기작업
## 문자단위 쓰기작업
- 정수형으로 입력받아, 해당 값의 아스키코드문자로 파일에 쓰기
```c
//fputc('문자',포인터명)
int fput(int c,FILE *fp);
```

## 문자열단위 쓰기작업
```c
//fputs("문자열",파일포인터)
fputs(const char *buf,FILE *fp);
```

  
## fclose()함수
- fclose() 함수는 파일을 닫아주는 함수입니다.
- 파일을 닫는다는 것은 파일과의 입출력을 위해 생성한 스트림을 소멸시키는 것을 의미합니다.
- C언어에서 다 사용한 파일은 반드시 fclose() 함수를 사용하여 닫아줘야 합니다.

```c
#include <stdio.h>
int fclose(FILE *stream);  
```

## 파일열고 작성하기

```c
#include <stdio.h>
#include <stdlib.h>

void main() {

	FILE *fp1 = NULL;

	//1. 파일열기
	fp1 = fopen("file1.txt", "w");

	//2. 파일작업
	if (fp1 == NULL) {
		printf("파일열기 실패\n");
	}
	else {
		printf("파일열기 성공\n");
		fputs("hello", fp1);
	}

	//3. 파일닫기
	fclose(fp1);
}
```

## 회원가입.c
- 원하는 타입으로 파일에 적고싶을때
- fprintf(파일포인터, "형식지정자", 변수or값);
```c
#include <stdio.h>

int main() {
	char id[20];
	char pw[20];
	char name[20];
	int age;

	printf("id를 입력하세요:");
	scanf("%s", id);
	printf("pw를 입력하세요:");
	scanf("%s", pw);
	printf("Name을 입력하세요:");
	scanf("%s", name);
	printf("Age를 입력하세요:");
	scanf("%d", &age);

	FILE *fp1 = NULL;
	fp1 = fopen("회원가입.txt", "w");
	//	2. 파일작업
	if (fp1 == NULL) {
		printf("파일열기 실패\n");
	}
	else {
		printf("파일열기 성공\n");
		/*	fputs(id, fp1);
			fputs(pw, fp1);*/
		fprintf(fp1, "id:%s\npw:%s\n", id, pw);
		fprintf(fp1, "name:%s\nage:%d\n", name, age);
	}
	fclose(fp1);

	return 0;
}
```

# 읽기작업
## 문자 단위 읽기
- 지정된 스트림으로부터 하나의 문자를 읽어 들이는 함수
```c
int fgetc(FILE *stream);  
```

## 문자열 단위 읽기
- 첫 번째 매개변수(str)에는 파일에서 읽은 문자열을 저장할 메모리의 주소를 넘겨주면 된다.
- 두 번째 매개변수(numChars)에는 저장할 문자의 최대 개수를 지정한다.
- 세 번째 매개변수(stream)은 파일포인터를 넣어준다.
```c
char* fgets(char* str, int numChars, FILE* stream);
```



## 파일 읽어오기
```c
#include <stdio.h>

int main(){
	// 회원가입.txt 를 읽기 전용(r)으로 text 모드(t)로 열기
	FILE* pFile = NULL;
	fopen_s(&pFile, "회원가입.txt", "rt");

	if (pFile != NULL){
		char str[128];
		if (fgets(str, 128, pFile) != NULL){
			// 읽어온 문자열을 화면에 출력한다.
			printf("%s", str);
		} else {
		    printf("파일에서 문자열을 읽지 못하였습니다.");
		}
		// 파일을 다 사용했으니, 파일을 닫는다.
		fclose(pFile);
	}

	return 0;
}
```
