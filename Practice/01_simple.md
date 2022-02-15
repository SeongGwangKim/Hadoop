# 01_Hadoop_Practice - Hive(mk-100k : 영화 평점 데이터)

### 1. Hive View 들어간다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017786-7852dd5e-e437-4303-a934-6fea3cc42c3c.png"  width="70%" height="70%"/>

<br>

### 2. 사용할 파일을 업로드하기 위하여Upload Table에 들어간다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017795-55788a32-eade-4033-b2fb-11c67af00499.png"  width="70%" height="70%"/>

<br>

### 3. 환경설정 버튼을 눌러서 업로드할 파일의 타입을 설정한다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017798-a683bd7a-b3f2-4a9e-af79-f8acde003667.png"  width="70%" height="70%"/>

<br>

### 4. 우리가 받은 mk-100k의 데이터의 u.data의 데이터 구분이 TAB으로 되어 있기 때문에 TAB을 설정하고 Close를 누른다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017802-c2220d9b-76d3-444d-9541-3d353df3586c.png"  width="70%" height="70%"/>

<br>

### 5. Select from local의 파일 선택을 누르고 내가 업로드하려는 파일의 경로로 가서 파일을 선택하고 열기를 누른다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017805-d5b98fc7-d8f3-43c4-95d1-437cc82b8cb1.png"  width="70%" height="70%"/>

<br>

### 6. u.data의 파일에서 내가 Hive에서 사용할 설정들을 다음과 같이 바꾸고 Upload Table을 누르면 업로드가 된다. <br>
<img src="https://user-images.githubusercontent.com/78336335/154017808-b6038047-717c-4462-bdf9-c5486dd2774b.png"  width="70%" height="70%"/>

<br>

### 7. 업로드가 완료가 되면 다음과 같이 창이 뜨게 된다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017813-e0c257a1-a64e-45df-8206-bba08c27519e.png"  width="70%" height="70%"/>

<br>

### 8. 영화에 대한 정보가 들어있는 u.item의 데이터 구분은 |로 되어 있기 때문에 |를 설정해주고 Close를 누른다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017815-48abf3d6-4f00-47d3-a16e-27fa5f20914e.png"  width="70%" height="70%"/>

<br>

### 9. u.item이 존재하는 경로에 가서 파일을 선택하고 열기를 누른다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017819-6c0e6cf9-c8e3-4816-9557-6e280a95e06a.png"  width="70%" height="70%"/>

<br>

### 10. u.item의 파일에서 내가 Hive에서 사용할 설정들을 다음과 같이 바꾸고 Upload Table을 누르면 업로드가 된다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017822-ea1e2216-4522-4ce3-8fb8-1c05c95cd956.png"  width="70%" height="70%"/>

<br>

### 11. 업로드가 완료가 되면 다음과 같이 창이 뜨게 된다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017824-96b9ff72-5e47-486d-961f-21feefe43a5d.png"  width="70%" height="70%"/>

<br>

### 12. Query를 사용하여 데이터를 불러오는 실습을 하기 위해 Query 탭을 눌러 이동한다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017828-e2645ebf-b6d5-4549-9381-962e69de280f.png"  width="70%" height="70%"/>

<br>

### 13. 데이터를 업로드할 때, 따로 설정을 해주지 않으면 default에 저장이 된다.<br>
### cf) 만약 Upload를 했는데, 보이지 않는다면 다른 탭을 갔다오거나 껐다가 켜면 들어와 있다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017830-8e4d21ca-a4db-467b-ab84-50919a5db21c.png"  width="70%" height="70%"/>

### Worksheet에 다음과 같은 쿼리를 입력하고 실행을 하면<br> 영화의 Index와 해당 영화를 평점 매긴 사람 수를 카운트해서<br> 카운트한 것을 기준으로 내림차순으로 정렬하여 하단에 보여준다.

<br>

### 14. 오른쪽에 그래프 모양의 아이콘을 누르면 다음과 같은 창이 뜨고 각각을 설정해주면 하단에 그래프로 보여준다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017831-0cfd69f6-fffc-4d99-a6ec-b5e087464b05.png"  width="70%" height="70%"/>

<br>


### 15. Worksheet에 다음과 같은 쿼리를 입력하고 실행을 하면<br> 영화의 이름 테이블에서 영화의 Index가 50인 데이터의 이름을 보여준다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154017832-5c2c4fde-04cc-48c0-884b-e82a120818b0.png"  width="70%" height="70%"/>

<br>



