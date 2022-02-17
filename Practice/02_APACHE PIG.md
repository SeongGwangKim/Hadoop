# [ APACHE PIG ]<br>
1. mapper와 reducer를 작성하지 않고도 빠르게 데이터를 분석할 수 있다.<br>
2. PIG 스크립트 실행 방법<br>
   1) 마스터 노드에서 피그로 입력을 하면 Grunt prompt가 뜨고 그 곳에 한 줄씩 피그 스크립트를 입력하고 한 줄씩 실행된다.<br>
cf) Grunt : 명령을 해석하고 처리
   2) Ambari view를 활용.

<br>

## [ Pig를 활용한 실습 ]

### 1. Ambari에서 Pig View를 클릭한다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154437142-dadf9443-21b4-4268-b2be-e8b77825721c.png"  width="70%" height="70%"/><br>

### 2. Scripts로 가서 New Script를 눌러 Name을 작성하고 추가 옵션은 필요에 따라 설정한다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154437145-cbdf4327-d94d-41f9-998c-dfffd5e80ed5.png"  width="70%" height="70%"/><br>

### 3. Script를 작성하고 Execute를 누른다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154437147-b8424df3-5be3-4c32-9b57-d0ff7735e1d4.png"  width="70%" height="70%"/><br>

### 4. 완료되면 COMPLETED가 나오고 하단에 결과, 로그, 스크립트를 확인할 수 있다..<br>
<img src="https://user-images.githubusercontent.com/78336335/154437150-61366b51-75e1-419f-80c4-3593b311ff1f.png"  width="70%" height="70%"/><br>

### 5. cf) Script에서 Execute on Tez를 누르고 Execute를 누르면 스크립트 끝에서부터 최적의 방법으로 결론을 도출하여 속도가 더 빠르게 결과값을 얻을 수 있다.<br>
<img src="https://user-images.githubusercontent.com/78336335/154437155-ee5d854c-d3e6-45b8-b2c4-6e87f59d4e9c.png"  width="70%" height="70%"/><br>

<br>

ratings = LOAD '/user/maria_dev/ml-100k/u.data' AS (userID:int, movieID:int, rating:int, ratingTime:int);<br>
-> u.data에서 구체적인 스키마를 부여해서 ratings를 불러온다.<br>
<br>
metadata = LOAD '/user/maria_dev/ml-100k/u.item' USING PigStorage('|')<br>
	AS (movieID:int, movieTitle:chararray, releaseDate:chararray, videoRealese:chararray, imdblink:chararray);<br>
-> u.item에서 구체적인 파이프 구분자(USING PigStorage('|')) 스키마를 부여해서 metadat를 불러온다.<br>
   <br>
nameLookup = FOREACH metadata GENERATE movieID, movieTitle,<br>
	ToUnixTime(ToDate(releaseDate, 'dd-MMM-yyyy')) AS releaseTime;<br>
-> metadata를 훑어보고 nameLookup이라는 새로운 관계를 바꾸고 movieID, movieTitle, ReleaseTime을 넣는다. <br>
 <br>
ratingsByMovie = GROUP ratings BY movieID;<br>
-> movieID로 모든 평가를 그룹화.<br>
<br>
avgRatings = FOREACH ratingsByMovie GENERATE group as movieID, AVG(ratings.rating) as avgRating;<br>
-> 영화마다 평점의 평균을 avgRating을 avgRatings에 넣는다.<br>
<br>
fiveStarMovies = FILTER avgRatings BY avgRating > 4.0;<br>
-> 평점이 4.0초과인것만 골라낸다.<br>
<br>
fiveStarsWithData = JOIN fiveStarMovies BY movieID, nameLookup BY movieID;<br>
-> JOIN으로 movieID를 기준으로 합친다.<br>
<br>
oldestFiveStarMovies = ORDER fiveStarsWithData BY nameLookup::releaseTime;<br>
-> releaseTime을 기준으로 정렬<br>
<br>
DUMP oldestFiveStarMovies;<br>
-> DUMP로 해당 내용 확인<br>
<br>
<br>
cf) Tez를 체크하면 스크립트의 끝에서부터 최적의 방법으로 결론을 도출해내서 체크를 하지 않았을 때보다 더 빠르다.<br>

<br><br>
## [ pig 명령어들 ]
1. 로드 및 저장
- LOAD : 파일 시스템/저장소로부터 데이터를 관계자로 로드.
- STORE : 관계자를 파일 시스템/저장소에 저장.
- DUMP : 콘솔에 관계자의 내용을 출력.

2. 필터링
- FILTER : 관계자에서 언하지 않는 행을 삭제.
-DISTINCT : 관계자에서 중복된 행을 삭제
- FOREACH/GENERATE : 관계자에 항목을 추가 또는 삭제.
- MAPREDUCE : 관계자를 입력으로 사용하여 맵리듀스 잡을 실행
- STREAM : 외부 프로그램을 사용하여 관계자를 변환.
- SAMPLE : 관계자에서 무작위 샘플을 추출.
- ASSERT : 관계자의 모든 행의 조건이 true인지 검증.

3. 그룹화, 조인
- JOIN : 두 개 이상의 관계자를 조인.
- COGROUP : 두 개이 상의 관계자의 데이터를 그룹화.
- GROUP : 단일 관계자의 데이터를 그룹화.
- CROSS : 두 개 이상의 관계자에 대한 교차곱을 생성 즉, 모든 조합을 생성.
- CUBE : 단일 관계자의 특정 컬럼을 기준으로 모든 조합을 구한 후 집계를 생성.

4. 정렬
- ORDER : 한 개 이상의 항목을 기준으로 관계자를 정렬
- RANK : 단일 관계자의 각 튜플의 순위를 매기고 첫 번째 항목을 기준으로 정렬.
- LIMIT : 튜플의 최대 개수를 지정하여 관계자의 크기를 제한, 디버깅시 유용

5. 결합, 분할
- UNION : 두 개 이상의 관계자를 하나로 결합
- SPLIT : 단일 관계자를 두 개이상의 관계자로 분할.

6. 진단
- DESCRIBE : 관계자의 스키마를 출력 즉, 이름과 종류 등을 확인할 수 있음.
- EXPLAIN : 논리 및 물리 계획을 출력 즉, PIG가 어떻게 계획을 실행할지를 보여줌.
- ILLUSTRATE : 입력의 부분 집합을 이용하여 논리 계획에 대한 단순한 실행 결과를 보여줌 즉, PIG가 무엇을 하는지 더 자세하게 보여줌.

7. UDF'S(사용자 정의 함수)
- REGISTER : 피그 실행 시에 사용할 JAR 파일을 등록.
- DEFINE : 매크로, UDF, 스트리밍, 스크립트, 명령어에 대한 별칭을 생성.
- IMPORT : 외부 파일에 정의된 매크로를 스크립트로 가져옴.

8. 피그 내장 함수
1) 평가
- AVG : 백(BAG) 내의 개체의 평균값을 계산.
- SUM : 백(BAG) 내의 개체의 합을 계산.
- CONCAT : 백(BAG) 내의 배열을 연결.
- COUNT : 백(BAG) 내의 null이 아닌 개체의 수를 카운트.
- COUNT_STAR : 백(BAG) 내의 null을 포함한 개체의 수를 카운트.
- DIFF : 백(BAG) 내의 두 집합의 차이를 계산.
- MAX/MIN : 백(BAG) 내의 개체의 최댓값/최솟값을 계산.
- SIZE : 자료형의 크기를 계산.(숫자=1, 문자=문자 수, 바이트=바이트 수...)
- TOBAG : 한 개 이상의 표현식을 개별 튜플로 변환 후 백(BAG)에 넣음.
- TOKENIZE : 문자 배열을 단어로 분리 후 백(BAG)에 넣음.
- TOMAP : 짝수 개의 값을 key-value의 맵으로 변환.
- TOP : 백(BAG) 내의 상위 n개의 튜플을 계산.
- TOTUPLE : 한 개 이상의 표현식을 튜플로 변환.

2) 필터
- IsEmpty : 백(BAG)이나 맵이 비어 있는지 검증.

3) 로드/세이브
- PigStorate
- TextLoader
- JsonLoader
- JsonStorage
- AvroStorage
- ParquetLoader, ParquetStorer
- OrcStorage
- HBaseStorage
