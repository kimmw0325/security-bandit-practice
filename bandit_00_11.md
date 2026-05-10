# Level 0 -> 1

## 목표
readme 파일을 읽고, 비밀번호를 찾는 문제

## 사용한 명령어
```bash
ssh # 원격 서버에 접속하는 명령어
ls # 현재 디렉토리 내의 파일들을 출력
cat
```

### 실행 과정
ssh로 bandit 서버에 원격 연결

```bash
ls
```
현재 디렉토리에 어떤 파일이 있는지를 확인했습니다.

readme 파일이 있는 것을 확인

```bash
cat readme
```
cat 명령어로 파일 내용을 출력

비밀번호가 출력되었으므로 
```bash
exit
```
