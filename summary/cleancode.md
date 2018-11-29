---
description: 'https://kwosu87.gitbooks.io/clean-code/content 의 내용의 요약'
---

# \[요약\] 클린코드

## 1. 의미 있는 이름

<table>
  <thead>
    <tr>
      <th style="text-align:left">구분</th>
      <th style="text-align:left">BAD</th>
      <th style="text-align:left">GOOD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">분명한 의도</td>
      <td style="text-align:left">
        <p>public List getThem() {</p>
        <p>List list1 = new ArrayList();</p>
        <p>for (int[] x : theList) {</p>
        <p>if (x[0] == 4) {</p>
        <p>list1.add(x);</p>
        <p>}</p>
        <p>}</p>
        <p>return list1;</p>
        <p>}</p>
      </td>
      <td style="text-align:left">
        <p>public List getFlaggedCells() {</p>
        <p>List flaggedCells = new ArrayList();</p>
        <p>for (int[] cell : gameBoard) {</p>
        <p>if (cell[STATUS_VALUE] == FLAGGED){</p>
        <p>flaggedCells.add(cell);</p>
        <p>}</p>
        <p>}</p>
        <p>return flaggedCells;</p>
        <p>}</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">올바른 정보</td>
      <td style="text-align:left">accountList</td>
      <td style="text-align:left">accountGroup, bunchOfAccounts, accounts</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>의미 있는 구분</p>
        <p>(noise word 금지)</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">발음하기 쉬운 이름</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">검색하기 쉬운 이름</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>인코딩 피하기</p>
        <p>헝가리안 표기법</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>인코딩 피하기</p>
        <p>멤버 변수 접두어</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>인코딩 피하기</p>
        <p>인터페이스와 구현</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">기억력 과신 금물</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">클래스 이름</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">메서드 이름</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">개념 : 단어 = 1 : 1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">해법 영역 용어</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">문제 영역 용어</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">의미 있는 맥락</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">불필요한 맥락</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## 2. 함수

## 3. 주석

## 4. 형식 맞추기

## 5. 객체와 자료구조

## 6. 에러 핸들링

## 7. 경계 

## 8. 단위 테스트

## 9. 클래스

## 10. 시스템

## 11. 창발성

## 12. 동시성

## 13Chapter 14 - 점진적인 개선

