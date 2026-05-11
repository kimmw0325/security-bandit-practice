# Level 4 -> 5

## 목표
inhere 디렉토리 내에 있는 인간만이 읽을 수 있는 파일을 읽기

## 사용한 명령어
```bash
ssh
cd 
cat
file
```

### 실행 과정
ssh로 bandit 서버에 원격 연결 후에 (비밀번호 입력) 디렉토리 내에 어떤 파일이 있는지를 확인
```bash
ls
```

inhere 디렉토리가 있는 것을 확인. inhere 디렉토리로 이동
```bash
cd inhere/
```

inhere 디렉토리 내에 어떤 파일이 있는지를 확인
```bash
ls
```

`-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09` 출력됨.

`-file00`부터 `-file09`까지 하나씩 파일 읽어본 결과, `-file07`에서 비밀번호가 출력됨


읽을 수 있는 텍스트가 들어있는 파일을 찾는 방법
```bash
file ./*
```
디렉토리 내의 모든 파일의 타입을 알려줌.

출력 결과
```bash
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
`-file07`이 ASCII text이므로 바로 접근하면 된다.


### 정리
* `file *`을 하게 되면 디렉토리 내의 모든 파일들의 타입을 알려준다.
  * 해당 문제에서 `file ./*`을 하는 이유는 파일명들이 `-`로 시작하기 때문에, `./`를 붙이지 않게 되면 옵션으로 해석할 여지가 있기 때문이다.
  * 안전하게 처리하기 위해 `./`를 붙이는걸 습관 들이자.

* `reset`을 실행하게 되면 터미널 화면이 정리된다. 
  * 실제로 이 문제에서 `cat`으로 파일내용들을 출력하게 되면 터미널 형식이 깨지는데, reset 커맨드를 실행하면 터미널이 초기화 된다.
