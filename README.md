# woowahan-tech-camp-pro-branching
우아한테크캠프Pro 4기 과정을 진행하면서 개인 GitHub도 같이 관리하기 위한 브랜칭 전략.

## Issue
fork한 repository에서 GitHub username으로 branch를 생성하다보니, 기본 branch가 아니라서 바로 작업내용을 확인하기 어렵고, contribution 기록에 용이하지 않음.

## Solution
`*-personal` repository 생성 후 fork한 repository의 `stevejkang` branch를 `*-personal` repository의 `main` branch를 바라보도록 push한다.

## Full-Cycle
> 직접 사용하고자 하는 경우 `stevejkang` 필드를 본인에게 맞춰 변경하여 사용할 것.

### Repository Setup
```bash
# Fork repository
git clone -b stevejkang --single-branch https://github.com/stevejkang/java-lotto-pro.git
cd java-lotto-pro
git remote add upstream https://github.com/next-step/java-lotto-pro.git # 최초 1회만
# Create *-personal repository
git remote add personal https://github.com/stevejkang/java-lotto-pro-personal.git # 최초 1회만
```

### Step 시작 ~ PR
```bash
git checkout -b step1
# Commit something
git push origin step1
# Make PR
# Base: stevejkang/java-lotto-pro:step1
# Destination: next-step/java-lotto-pro:stevejkang
```

### PR 머지 후 새로운 Step 시작
```bash
git checkout stevejkang
git branch -D step1 # do not delete branch from remote repository
git fetch upstream stevejkang
git rebase upstream/stevejkang
git push origin stevejkang
git push personal stevejkang:main
git checkout -b step2
```

> `git remote -v` 의 결과는 아래와 같다.
```
origin	https://github.com/stevejkang/java-lotto-pro.git (fetch)
origin	https://github.com/stevejkang/java-lotto-pro.git (push)
personal	https://github.com/stevejkang/java-lotto-pro-personal.git (fetch)
personal	https://github.com/stevejkang/java-lotto-pro-personal.git (push)
upstream	https://github.com/next-step/java-lotto-pro.git (fetch)
upstream	https://github.com/next-step/java-lotto-pro.git (push)
```

### Reference
- [NEXTSTEP 코드리뷰 사이클](https://github.com/next-step/nextstep-docs/tree/master/codereview)
