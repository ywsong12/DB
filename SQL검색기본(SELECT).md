# SQL 검색의 기본
### SELECT
`SELECT 뒤에는 찾고자하는 대상(Column)들을 입력`
### FROM
`FROM 뒤에는 찾을 대상이 현재 있는 공간(Table)을 입력`
### WHERE
`WHERE 뒤에는 찾고자하는 대상에 대한 구체적인 조건을 추가하여 입력`
`조건을 더 주고 싶은 경우 AND를 활용`  

---
#### SELECT, FROM, WHERE 활용 예제
- 옷장에 있는 길이 110cm이상의 바지를 찾아라
```
SELECT 바지 FROM 옷장 WHERE 길이 >= 110cm;
```
- A마트에서 파는 사과중에 색은 초록색이고 크기는10cm 이하인 것을 찾아라
```
SELECT A마트 FROM 사과 WHERE 색 = "초록색" AND 크기 <= 10;
```
---
### 







