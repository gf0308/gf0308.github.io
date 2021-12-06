# git bash

git 커맨드창(CLI) 환경인 git bash 에서 사용하는 명령어

---

# 로컬에서 기본적인 작업과 커밋 작업

## 간단히 파일 만들고 저장하기

: echo 작성하는내용 >> 내용을 _담아_저장할_파일명

```bash
echo "my first commit test" >> README.md
```

## 로컬의 한 장소에 깃 로컬 저장소 정의하기

: git init

```bash
git init
```

## 로컬에 있는 파일을 commit 항목으로 추가하기(staged 시키기)

: git add {커밋대상으로_추가할_파일명}

```bash
// 1개 추가
git add {추가할_파일명}

		or

// 여러개 추가
git add {추가할_파일명} {추가할_파일명} {추가할_파일명} {추가할_파일명} ....

		or

// 현 경로 내용 전부 추가
git add *
```

## 로컬 commit 대기열에 올려놨던(staged) 것들을 커밋하기

: git commit -m "커밋_메시지"

```bash
git commit -m "커밋 메시지"
```

---

# 리모트 저장소

## 리모트 저장소 등록(추가)

: git remote add {저장소닉네임} {저장소git주소}

```bash
git remote add SpringBootStudyRepo https://github.com/gf0308/SpringBoot_Learning.git
```

## 리모트 저장소 삭제하기

: git remote rm {리모트저장소}

```bash
git remote rm main2
		or
git remote remove main2
```

## 리모트 저장소명 변경

: git remote rename {기존저장소명} {new저장소명}

```bash
git remote rename main master // main -> master 로 원격저장소명 변경
```

---

# 브랜치

## 브랜치 목록(branches)

- **로컬의 브랜치들 목록**
    
    : git branch (or git branch -l)
    
    ```bash
    git branch 
    		or
    git branch -l
    ```
    
- **리모트의 브랜치들 목록**
    
    : git branch -r
    
    ```bash
    git branch -r
    ```
    
- **로컬/리모트 전 브랜치들 목록**
    
    : git branch -a
    
    ```bash
    git branch -a
    ```
    

## 브랜치 생성하기

- **로컬 브랜치**
    - 기 존재하는 브랜치의 분기가 아닌, 완전 새로 파는 신생 브랜치
        
        : git branch {새 브랜치 명}
        
        ```bash
        git branch submaster2
        ```
        
    - 기 존재하던 한 브랜치로부터 분기해서 나오는 브랜치 생성
        
        : git branch {새로만들브랜치} {분기점으로삼는브랜치}
        
        ```bash
        git branch submaster3 submaster
        
        //이미 존재하고 있는 branch 한테는 **"git branch {브랜치명} {분기해나올원천브랜치}"** 적용불가
        ```
        
    - 리모트 브랜치를 따와서 로컬 브랜치를 생성 (리모트 브랜치를 로컬로 가져오기)
        
        : git checkout --track {리모트브랜치/브랜치명} 
        
        ```bash
        git checkout --track origin/submaster
        ```
        

- **리모트 브랜치**
    - 신규 리모트 브랜치 만들기
        
        : git push {원격저장소명} {**브랜치명**}
        
                          ㄴ 기존에 없던 브랜치면 '새로 만들면서' push / 있던거면 해당 branch에 push
        
        ```bash
        // submaster5라는 새로운 브랜치를 만들면서 푸쉬
        git push origin submaster5
        
        // 기존에 있던 master 브랜치에 푸쉬
        git push origin master
        ```
        

## 브랜치명 변경하기

- **로컬 브랜치명 변경**
    
    : git branch -M (or -m) {새로바꿀 브랜치명}
    
    ```bash
    git branch -M new_branch_name   // 이러면 현재 checkout 상태의 브랜치(현재활성 브랜치) 의 브랜치명이 변경
    		or
    git branch -M old_branch_name new_branch_name // 이러면 기존의어떠한 브랜치명 -> 새브랜치명 으로 바꿔줌
    ```
    
    - git branch -M 명령에 대한 설명
    
    : ([https://git-scm.com/docs/git-branch](https://git-scm.com/docs/git-branch))
    
    ```bash
    (With a m or M option, <oldbranch> will be renamed to <newbranch>.
    If <oldbranch> had a corresponding reflog, it is renamed to match <newbranch>, 
    and a reflog entry is created to remember the branch renaming. 
    If <newbranch> exists, -M must be used to force the rename to happen.)
    ```
    

- **리모트 브랜치명 변경**
    
    : **리모트 브랜치명 변경하기는 없다.**
    
    다른 리모트 브랜치명을 이용하고 싶다면
    
    **기존 old브랜치를 삭제**하고 ($ git push {리모트명} : {old_branch_name} )
    
    **new 원격브랜치를 새로 생성**해서 거기에 push 하는 식으로 한다
    
    ($ git push {리모트명} {new_branch_name} )
    

## 브랜치 전환하기

: git checkout {브랜치명}

```bash
git checkout submaster
```

## 새 브랜치를 만들면서 거기로 체크아웃하기

: git checkout -b {new 브랜치명}

```bash
git checkout -b new_branch
```

## 브랜치 삭제하기

- **로컬 브랜치의 경우**
    
    : git branch -d {로컬브랜치명}
    
    ```bash
    git branch -d submaster2
    ```
    
- **리모트 브랜치의 경우**
    
    : git push {리모트저장소명} : {브랜치명}
    
    ```bash
    git push origin : submaster3
    
    		or
    
    git push origin --delete submaster3
    ```
    

([https://www.nobledesktop.com/learn/git/git-branches](https://www.nobledesktop.com/learn/git/git-branches))