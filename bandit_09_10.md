# Level 9 -> 10

## 목표
비밀번호는 `data.txt`파일 내에 있다. 파일의 대부분은 사람이 못 읽지만 그 중 일부는 읽을 수 있다. 

비밀번호는 several `=` characters 뒤에 있다.

## 사용한 명령어
```bash
ssh
ls
cat
strings
grep
```

### 실행 과정
ssh로 bandit 서버에 원격 연결 후에 (비밀번호 입력) 디렉토리 내에 어떤 파일이 있는지를 확인
```bash
ls
```
`data.txt`가 있음

```bash
cat data.txt
```
알 수 없는 데이터들이 지저분하게 아주 많이 출력됨

`=` 여러 개가 있는 줄을 출력해야 하기 때문에
```bash
grep '=' data.txt
```
출력: `grep: data.txt: binary file matches`

```bash
strings data.txt | grep "="
```
비밀번호로 예상되는 문자열이 포함되어서 출력됨

### 정리
`grep`을 쓸 수 없는 이유: 해당 파일에는 바이너리 데이터가 다수 포함되어 있어서 `binary file matches`라고 매칭 결과만 출력한다.

`strings (파일명)` : 파일 내에서 `human-readable`한 데이터만 뽑아준다.

`|`로 추출한 데이터를 `grep`로 넘겨준다.

`human-readable`한 데이터만 넘겨받은 `grep`는 원하는 패턴을 가진 줄을 출력한다.
