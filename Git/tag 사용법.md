## Git tag 사용법

`git tag`는 Git에서 사용되는 명령어로, 특정 지점을 표시하기 위해 사용됩니다. 태그는 주로 프로젝트의 중요한 지점, 예를 들어 버전 릴리스를 표시하는 데 사용됩니다. 태그는 두 가지 유형이 있습니다: **경량 태그(lightweight)**와 **주석 태그(annotated)**입니다.

### 경량 태그 (Lightweight Tag)
경량 태그는 특정 커밋을 가리키는 포인터 같은 것으로, Metadata나 tag 정보를 저장하지 않습니다. 단지 커밋 ID에 대한 참조만을 포함합니다.

**생성:**

```bash
git tag <태그명>
```

### 주석 태그 (Annotated Tag)
주석 태그는 태그를 만든 사람의 이름, 이메일, 태그를 만든 날짜와 메시지를 포함하여 태그를 생성합니다. 이 정보는 Git 데이터베이스에 저장됩니다.

**생성:**
```bash
git tag -a <태그명> -m "메시지"
```
예를 들어, `v1.0`이라는 태그를 현재 커밋에 추가하고, 태그 메시지로 "버전 1.0 릴리스"를 사용하려면 다음과 같이 입력합니다:
```bash
git tag -a v1.0 -m "버전 1.0 릴리스"
```

### 태그 조회
생성된 모든 태그 목록을 보려면 다음 명령어를 사용합니다:
```bash
# Tag 전체 조회
git tag

# 특정 Tag 조회
git tag -l "<태그명>*"

# Tag 정보 조회
git show "<태그명>"
```

### 태그 공유
기본적으로 `git push` 명령은 태그를 원격 저장소에 전송하지 않습니다. 태그를 원격 저장소에 공유하려면 다음 명령어를 사용해야 합니다:

**특정 태그를 원격 저장소에 푸시:**
```bash
git push origin <태그명>
```

**모든 태그를 원격 저장소에 푸시:**
```bash
git push origin --tags
```

### 태그 삭제
로컬 저장소에서 태그를 삭제하려면 다음 명령어를 사용합니다:
```bash
git tag -d <태그명>
```

원격 저장소에서 태그를 삭제하려면:
```bash
git push --delete origin <태그명>
```

### 특정 태그에서 브랜치 생성
특정 태그에서 시작하는 새 브랜치를 만들고 싶다면 다음 명령어를 사용합니다:
```bash
git checkout -b <브랜치명> <태그명>
```

`git tag` 명령어는 프로젝트의 중요한 지점들을 효과적으로 관리할 수 있게 해주며, 버전 관리 전략의 일부로 널리 사용됩니다.

## 태그 일괄 삭제

CI(Continuous Integration:지속적 통합)를 관리하는중 누적된 Tag를 정리하고 관리하는데 사용.

#### Remote
```
$ git tag -l '<태그명>*' | xargs git push --delete origin
```
#### Local
```
$ git tag -l '<태그명>*' | xargs git tag -f 
```
#### Remote에서 태그 가져오는 방법
```
$ git fetch --tags
```

#### Remote 에 tag가 없으면 local tag 삭제
```
git tag -l | xargs git tag -d && git fetch -t
```