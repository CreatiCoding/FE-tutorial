# Untitled



## 읽기 좋은 자바스크립트 코딩 기법

#### \[원제\] Maintainable JavaScript

### Part 1. 스타일 가이드라인

**Ch 1. 기본 포맷**

**1.1 들여쓰기**

**개요**

팀 구성원 모두가 들여쓰기를 정확하게 하는 것이 가장 첫 번째 단계입니다.

<p style=" border-color: #d32f2f; color: #d32f2f; border-top: 15px solid; font-weight: 500;"> Don't </p>

```text
  if (wl && wl.length) {
          for (i = 0, l = wl.length; i < l; ++i) {
      p = wl[i];
      type = Y.Lang.typr(r[p]);
      if (s.hasOwnProperty(p)) { if (merge && type == 'object') {
          Y.mix(r[p], s[p]);
      } else if (ov || !(p in r)){
                      r[p] = s[p];
                  }
              }
          }
      }
```

​

Do.​

```text
  if (wl && wl.length) {
      for (i = 0, l = wl.length; i < l; ++i) {
          p = wl[i];
          type = Y.Lang.typr(r[p]);
          if (s.hasOwnProperty(p)) {
              if (merge && type == 'object') {
                  Y.mix(r[p], s[p]);
              } else if (ov || !(p in r)){
                  r[p] = s[p];
              }
          }
      }
  }
```

