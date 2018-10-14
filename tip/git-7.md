---
description: '본문은 원문(https://meetup.toast.com/posts/106)의 내용 요약입니다.'
---

# \[요약\] 좋은 git 커밋 메시지를 작성하기 위한 7가지 약속

원문의 출처: Chris Beams의 [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)

### git 커밋 메시지를 잘 쓰려고 노력해야 하는 이유

* 커밋 로그 가독성
* 협업과 리뷰 프로세스
* 코드 유지보수

### 좋은 git 커밋 메시지를 작성하기 위한 7가지 약속

* 제목과 본문을 한 줄 띄워 분리하기
* 제목은 영문 기준 50자 이내로
* 제목 첫글자를 대문자로
* 제목 끝에 . 금지
* 제목은 명령조로
* 본문은 영문 기준 72자마다 줄 바꾸기
* 본문은 어떻게보다 무엇을, 왜에 맞춰 작성하기

### 좋은 사례

```text
commit eb0b56b19017ab5c16c745e6da39c53126924ed6
Author: Pieter Wuille <pieter.wuille@gmail.com>
Date:   Fri Aug 1 22:57:55 2014 +0200

   Simplify serialize.h's exception handling

   Remove the 'state' and 'exceptmask' from serialize.h's stream
   implementations, as well as related methods.

   As exceptmask always included 'failbit', and setstate was always
   called with bits = failbit, all it did was immediately raise an
   exception. Get rid of those variables, and replace the setstate
   with direct exception throwing (which also removes some dead
   code).

   As a result, good() is never reached after a failure (there are
   only 2 calls, one of which is in tests), and can just be replaced
   by !eof().

   fail(), clear(n) and exceptions() are just never called. Delete

```

### PLUS TIP! 커밋 메시지로 Github 이슈\(issue\)를 자동 종료시키기

* 커밋 메시지로 Github 이슈 닫기 가능

```text
키워드 #이슈번호
```

키워드: close, closes, closed, fix, fixes, fixed, resolve, resolves, resolved

* 사례

```text
# 제목에 이슈 한 개 닫기를 적용한 사례
Close #31 - refactoring wrap-up

* This is wrap-up of refactoring main code.
* main.c
  * removed old comments
  * fixed rest indentations
  * method extraction at line no. 35


# 본문에 이슈 여러 개 닫기를 적용한 사례
Update policy 16/04/02

* This closes #128 - cab policy, closes #129 - new hostname, and fixes #78 - bug on logging.
* cablist.txt: changed ACL due to policy update delivered via email on 16/04/02, @mr.parkyou
* hostname.properties: cab hostname is updated
* BeautifulDeveloper.java: logging problem on line no. 78 is fixed. The `if` statement is never happening. This deletes the `if` block.
```

`master` 브랜치가 아닌 브랜치에 푸시했다면, 이슈는 닫히지 않고 있다가 나중에 `Merge`가 되었을 때 알아서 닫힙니다.

### Reference

* [Chris Beams : How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
* [erlang/otp Wiki : Writing good commit messages](https://github.com/erlang/otp/wiki/Writing-good-commit-messages)
* [git.kernel.org : The core git plumbing](https://git.kernel.org/cgit/git/git.git/tree/Documentation/SubmittingPatches)
* [git-scm : Distributed Git - Contributing to a Project](https://git-scm.com/book/ch5-2.html)
* [git-scm : Pretty Formats](https://git-scm.com/docs/pretty-formats)
* [Github : Closing issues via commit messages](https://help.github.com/articles/closing-issues-via-commit-messages/)

