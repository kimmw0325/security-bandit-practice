# Level 5 -> 6

## 목표
inhere 디렉토리 어딘가에 있는 다음과 같은 특징들을 가진 파일을 읽기
* human-readable (읽을 수 있고)
* 1033 bytes in size (크기가 1033byte)
* not executable (실행이 불가능)

## 사용한 명령어
```bash
ssh
cd 
find
file
cat
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

`maybehere00  maybehere04  maybehere08  maybehere12  maybehere16
maybehere01  maybehere05  maybehere09  maybehere13  maybehere17
maybehere02  maybehere06  maybehere10  maybehere14  maybehere18
maybehere03  maybehere07  maybehere11  maybehere15  maybehere19`

비슷한 이름을 가진 디렉토리 20개가 출력됨

* 우리가 찾아야 하는 것은 텍스트파일 & 1033byte & not executable
* 모든 디렉토리를 돌며 `file ./*`로 원하는 파일을 찾을 수는 없다.

```bash
find -type f -size 1033c ! -executable
```
`./maybehere07/.file2` 출력됨.

```bash
file ./maybehere07/.file2
```
타입이 ASCII text로 출력되니 human readable이다.

해당 파일 읽기
```bash
cat ./maybehere07/.file2
```
비밀번호 출력됨

### 정리
디렉토리가 너무 많아 일일히 들어가서 `file ./*`를 할 수 없는 상황이다.

`find` 커맨드를 사용하여 내가 원하는 범위에서 원하는 조건을 만족하는 파일을 찾을 수 있었다.

`find -type f -size 1033c ! -executable`
* `-type f` : 디렉토리가 아닌 일반 파일
* `-size 1033c` : 크기가 1033바이트인 파일
* `! -executable` : 실행이 불가능한 파일

실행과정에서는 찾은 파일이 human readable인지 확인하기 위해 `file` 커맨드를 추가로 사용해주었다.

###### `find`와 `file`을 한번에 실행하는 방법
```bash
find (조건) -exec (실행할커맨드) {} \;
```
조건에 맞는 파일을 발견하면 커맨드까지 바로 실행시켜주는 방법이다.

이번 레벨에 적용해보면 아래와 같이 작성할 수 있다.
```bash
find -type f -size 1033c ! -executable -exec file {} \;
```
* 세가지의 조건에 부합하는 파일을 탐색한다.
* 조건에 부합하는 파일을 찾으면 `file {}`을 실행하여 타입을 출력한다.
