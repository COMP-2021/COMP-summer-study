# HTML

---

## 표 tabel

```jsx
<table border="2">
	<tr>
		<td>이름</td>   <td>성별</td>
	</tr>
  <tr>
		<td>최진혁</td> <td>남</td>
	</tr>
</table>
```

- tr 태그는 table row로 행을 구분
- td 태그는 table data로 열을 구분

```jsx
<table border="2">
	<tr>
		<td>이름</td>   <td>성별</td>
	</tr>
  <tr>
		<td>최진혁</td> <td>남</td>
	</tr>
</table><table border="2">
	<tr>
		<td>이름</td>   <td>성별</td>
	</tr>
  <tr>
		<td>최진혁</td> <td>남</td>
	</tr>
</table>
```

- <thead> 태그는 표의 항목명을 지정하는 태그로써 <th> 태그와 함께 사용
- <tbody> 태그는 표의 내용을 지정하는 태그
- <tfoot> 태그는 표의 마지막 행을 지정하는 태그
- <thead>와 <tfoot> 태그는 코드 위치와 상관없이 표의 처음과 끝에 위치

- <td> 태그의 속성으로 rowspan, colspan을 지정하여 행과 열을 병합할 수 있음 ex) <td rowspan="2"></td>

---

## 입력양식 form

: 사용자가 입력한 데이터를 전송하기 위한 목적

- action 속성 값에 데이터를 보낼 목적지를 적어줌
- 전송 받은 데이터는 각 태그의 name 속성으로 구분

### form 태그의 종류

1. 텍스트 입력
- <input> 태그의 속성 중 type="text" 를 통해 문자를 입력 받을 수 있음
- value 속성은 텍스트 입력 태그의 디폴트 문자를 설정 가능

- <textarea> 태그를 통해 긴 글을 입력 받을 수 있음
- 속성으로 cols과 rows로 크기 조정 가능
- 디폴트 문자는 속성으로 지정 대신 textarea 태그 사이에 넣어줌으로써 설정 가능

1. 선택
- <select> 태그 내에 <option> 태그를 넣어줌으로써 dropdown list /  combo box 생성
- multiple 속성을 넣어주면 ctrl를 이용하여 옵션 다중 선택 가능

- <input> 태그의 type="radio" 속성으로 라디오 버튼 생성
- name 속성이 같은 태그끼리 그룹 지을 수 있음
- <input> 태그의 type="checkbox" 속성으로 다중 선택 가능한 체크박스 생성
- checked 속성으로 디폴트 값으로 미리 체크 가능

1. 버튼
- <input> 태그의 type="submit" 속성은 데이터를 form 태그를 동작 시키게끔 제출하는 역할
- value 속성으로 텍스트 바꿀 수 있음

- submit과는 다르게 type="button"은 버튼을 생성하여 js와 연동하여 사용 가능

- type="reset" form 태그 내에 있는 사용자가 입력한 모든 정보를 초기화

1. 데이터 전송 - hidden
- <input> 태그의 type="hidden" 속성은 UI 없이 데이터를 전송할 때 사용

1. 컨트롤의 제목 - label

```jsx
<label for="id_txt">text</label> : 
<input id="id_txt" type="text" name="id">
```

- 2번 째 줄의 input 태그의 이름이 text라는 것을 명시하기 위해 <label> 태그로 감싸주었고, for 속성으로 누구의 label인지를 알려줌
- input 태그를 label 태그로 감싸주어도 label 내에 있는 태그와 매칭 가능

1. method
- form 태그가 서버에 정보를 전달할 때 url에 정보를 노출하면 안되는 경우가 존재하는데, 이때 post 방식을 사용
- form 태그의 속성으로 method="get" 으로 하여 데이터를 전송하는 방식이 디폴트 동작
- method="post" 로 하여 데이터를 전송하면 url에 데이터가 노출되지 않음

1. 파일 업로드 - upload
- <input> 태그의 속성으로 type="file"을 지정하면 파일을 선택할 수 있는 버튼 생성
- 파일을 전송할 때는 form 태그의 속성으로 enctype="multipart/form-data" 를 지정해야 함

---
