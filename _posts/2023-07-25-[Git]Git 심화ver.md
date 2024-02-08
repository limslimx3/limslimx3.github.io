---
title: "[Git]Git 심화ver"

toc: true
toc_sticky: true

categories:
  - Git
tags:
  - Git
  - GitHub

last_modified_at: 2023-07-25T22:00:00

---

# Git 심화개념 다루기

> Git을 좀 더 깊게 다루기 위해 심화개념에 대해 알아보자

<br/>

## 1. Git의 3가지 공간

### Working directory & Staging area & Repository

---

1. Working directory
   - Untracked와 Tracked 2개로 나눠짐
     - Untracked는 기존에 add된적 없는 파일 또는 .gitignore에 명시된 파일
     - Tracked는 기존에 add된적 있지만 현재 변경내역이 존재하는 파일
   - `git add`명령어를 통해 Staging area로 이동시킴
2. Staging area
   - `git add`와 `git commit`작업 사이에 존재
   - `git commit`명령어를 통해 Repository로 이동시킴
3. Repository
   - `git commit`이후의 상태로 github의 repository와 유사한 개념



### git rm & git mv

---

- `git rm`은 파일을 지우고 `git mv`는 파일명을 변경하는 명령어이다
- 다만, 직접 파일을 지우고 삭제하는 것과는 차이점이 존재한다
  - `git rm`은 파일을 지운 상태가 `git add`까지 되어있는 상태이고, `git mv`는 파일명을 수정한 상태가 `git add`까지 되어있는 상태이다



### git restore

---

- `git add`명령어를 통해 Staging area로 이동한 파일들을 `git restore --staged`명령어를 통해 `git add`하기 전인 Working directory로 다시 옮길 수 있다
- 이후 `git restore`명령어를 통해 Working directory에서도 제거해버릴 수 있다



### git reset

---

- `--hard` 버전은 해당 커밋내역 시점으로 돌아감
- `--mixed` 버전은 hard버전에서 직후 커밋내역을 add하기 전인 Working directory로 보냄
- `--soft` 버전은 hard버전에서 직후 커밋내역을 commit하기 전인 Staging area로 보냄

<br/>

<br/>



## 2. HEAD

- 현재 위치한 브랜치의 가장 최신 커밋
- 각 브랜치마다 HEAD의 위치는 다를 수 있음



### git checkout

---

- `reset`, `revert` 명령어와 달리`git checkout '커밋해시값'`명령어를 통해 커밋내역삭제 없이 해당시점으로 돌아가기만 할 수도 있다
  - 이는 브랜치를 새로 만들어 해당 시점으로 돌아가는 것이라고 생각하면 된다
  - 즉, `git switch`명령어를 통해 다시 다른 시점으로 돌아갈 수 있다
  - `git checkout HEAD^`를 이용하여 '^' 개수만큼 과거의 커밋내역으로 돌아갈 수도 있다
- `git checkout`을 통해 과거의 시점으로 돌아간후 새로운 브랜치를 분기하는 식으로 사용할 수도 있다
- `git checkout origin/main`를 통해 `git switch`로는 불가능한 원격 브랜치로의 전환이 가능하다



### fetch vs. pull

---

- `fetch`는 원격의 최신 커밋을 로컬로 가져와 최신화하고, `pull`은 원격의 최신 커밋을 로컬로 가져와 `merge` 혹은 `rebase`하는 과정이다
  - 사실상 `pull`은 `fetch`과정을 포함하고 있다고 보면 된다
- pull 하기 전에 fetch를 통해 원격에서 어떻게 수정되었는지 확인하는 것이 가능하다
  - `git fetch`명령어를 통해 원격의 변경사항을 local에 최신화한 후에 `git checkout origin/main`명령어로 원격의 main브랜치로 이동하여 원격의 변경사항을 확인할 수 있다

