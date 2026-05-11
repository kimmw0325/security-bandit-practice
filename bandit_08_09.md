# Level 8 -> 9

## 목표
비밀번호는 `data.txt`파일 내에 있고 단 한번만 나온 줄이 비밀번호다.

## 사용한 명령어 및 문법
```bash
ssh
ls
sort
|
uniq
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
아래와 같이 출력된다.
```bash
McfCopsVMkSjH0RczhUpMNz3wj8lByZU
0YJPG1dC42w6W80WLWO5FuRPKIlHuKQ3
uoe0s8oZ9OAwOGB3AnlQHuTSUUueK5XZ
wpslsPAsYxj6MzzHL3EsTAdzhudfmvpE
rNOYB72WEMqUoieQw6sUbTWXdOFrlep8
HnIPzmFPIFXjWRRazZDboFLa5Ce4bIkK
7kMTZ5nS9WB0e4knWljlseFynU6jssga
...
```
이와 같이 문자열이 여러 줄 출력된다.

이 문자열들 중 단 한 번만 등장하는 줄을 찾아야 한다.
```bash
sort data.txt | uniq -u
```
비밀번호가 출력됨.

### 정리
* `sort (파일명)` : 파일의 줄들을 알파벳 순으로 정렬한다.
* `|` : 파이프라고 부른다. 왼쪽의 실행 결과를 오른쪽에 넘겨준다.
* uniq : 중복을 비교한다.
  * 단 **인접한 줄끼리만 비교**를 하기에, 중복을 처리하려면 sort가 선행되어야 한다.
  * 파이프를 쓰지 않으면 `uniq -u data.txt`로도 입력 가능하다.(그러나 정렬된 결과를 넘겨야 정상적인 처리가 가능하므로 파이프 사용)

###### uniq의 여러 가지 옵션
* `-u` : 중복되지 않은 줄을 출력
* `-d` : 중복된 줄을 출력
* `-c` : 각 줄이 몇 번 나왔는지를 출력
* `-i` : 대소문자 차이를 무시하고 비교(다른 옵션과 같이 사용 권장)

위 옵션들은 함께 사용이 가능하다.

ex) `-cd` or `-dc` : 중복된 줄을 출력하는데, 각 줄이 몇번 나왔는지도 함께 출력 (작성 순서는 상관X)
