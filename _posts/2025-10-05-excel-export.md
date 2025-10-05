---
layout: single
title:  "아웃시스템즈 엑셀 다운로드시 앞에 작은따옴표(’) 붙는 문제."
categories: outsystems
tags: [outsystems, excelExport]
toc: true
---

![image.png](/image.png)

- 참고 링크
    - https://www.outsystems.com/forums/discussion/104171/recordlisttoexcel-adds-hidden-apostrophe-when-exporting-values-to-excel/
    - https://www.outsystems.com/forums/Search.aspx?page=1&q=Apostrophe+Excel&scat=forums

# 0. 상황

엑셀 다운로드 시 특정 기호로 시작하는 셀은 앞에 자동적으로 작은따옴표(’) 가 붙음

![image.png](%EC%97%91%EC%85%80%20%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%EC%8B%9C%20%EC%95%9E%EC%97%90%20%EC%9E%91%EC%9D%80%EB%94%B0%EC%98%B4%ED%91%9C(%E2%80%99)%20%EB%B6%99%EB%8A%94%20%EB%AC%B8%EC%A0%9C%2027a7a2d7045680e9b9f0d2fb423cb2e8/image%201.png)

이런식으로 붙음

# 1. 이유(추정)

기본 리스트를 엑셀로 변환할때 다음과 같이 됨,

리스트를 → 엑셀 변환시, 맨 처음이 -면 이게 뒤에 값이 숫자인지 아닌지 아웃시스템즈에는 몰라서 자동으로 ‘를 붙이는 듯(실제 엑셀에서 010을 입력하면 10으로만 입력 및 표시되는데, 이때 앞에 ‘를 붙여 ‘010으로 입력하면 010으로 표시됨)

# 2. 해결

SubStr 사용하여 해당 항목의 데이터 첫 글자가 -또는 +로 시작하면 앞에 공백 붙이기

```jsx
// 예시
If(Substr(엔티티1.어트리뷰트1,0,1)="-" or Substr(엔티티1.어트리뷰트1,0,1)="+"
		, " " + 엔티티1.어트리뷰트1,0,1
		, 엔티티1.어트리뷰트1,0,1)
```

다른 방법도 있는 것 같지만 저 공백 붙이기 같은게 제일 깔끔한듯