# Level 6 -> 7

## 목표
서버 어딘가에 있는 다음 조건을 만족하는 파일을 찾아서 읽기

* `owned by user bandit7` : 소유자가 `bandit7`
* `owned by group bandit6` : 그룹이 `bandit6`
* `33 bytes in size` : 사이즈가 `33bytes`

## 사용한 명령어 및 문법
```bash
ssh
ls -a
find /
2>/dev/null
cat
```

### 실행 과정
ssh로 bandit 서버에 원격 연결 후에 (비밀번호 입력) 디렉토리 내에 어떤 파일이 있는지를 확인
```bash
ls
```

아무것도 출력이 되지 않음
```bash
ls -a
```
`.  ..  .bash_logout  .bashrc  .profile` 출력됨

조건에 만족하는 파일을 탐색
```bash
find -user bandit7 -group bandit6 -size 33c
```
현재 디렉토리 내에는 조건에 맞는 파일이 없음. 

범위를 루트 디렉토리로 다시 탐색
```bash
find / -user bandit7 -group bandit6 -size 33c
```

`Permission denied`메세지는 숨기도록 다시 시도
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

`/var/lib/dpkg/info/bandit7.password` 출력됨
```bash
cat /var/lib/dpkg/info/bandit7.password
```
비밀번호 출력됨

### 정리
기존 `find`로는 현재 디렉토리 내에서만 탐색이 가능하다.

`find . -user bandit7 -group bandit6 -size 33c`와 같은 의미임

이번 레벨의 목표에서도 서버 어딘가에 있는 파일을 찾으라고 했기에 `.` 대신 `/`를 넣어주어 범위를 최상위 디렉토리로 확장할 수 있다.

실제로 실행시켜보면 권한이 없는 디렉토리들 때문에 수많은 줄이 `Permission denied`와 함께 출력된다. 

이러한 메세지를 가리기 위해 `2>/dev/null`를 붙인다. (에러메세지를 모두 숨기는 기능) 

###### `find`와 `cat`을 한번에 실행하는 방법
저번 레벨 마크다운에도 작성한 것과 마찬가지로 `-exec`를 쓰면 된다.
```bash
find -user bandit7 -group bandit6 size 33c -exec cat {} \; 2>/dev/null
```
`2>/dev/null`가 find 바로 뒤에 들어가도 잘 작동하긴 하지만 관습적으로 맨 뒤에 작성한다고 한다.

##### `2>/dev/null`의 의미
* 리눅스에는 프로그램이 입출력할 때 번호를 쓴다.
  * 0: 표준 입력 (stdin)
  * 1: 표준 출력 (stdout)
  * 2: 에러 출력 (stderr)
 
* `>`는 출력을 다른 곳으로 보내는 기호다. 에러 출력을 `/dev/null`로 보낸다는 뜻
* `/dev/null`은 쉽게 말해 리눅스의 쓰레기통이다. 저장되지 않고 버려진다.
