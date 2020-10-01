# AppleMango

## Project Goal 
인스타그램 활용 맛집 추천 서비스

## Tech Stack
##### Env
- AWS EC2
- Ubuntu 16.04

##### Backend
- Spring Boot
- jdk 13.0.1
- MAVEN
- JPA 

##### FrontEnd
- Vue.js
- Vuetify
- BootStrap

##### Storage
- Docker
- MariaDB

##### Data Processing
- selenium
- BeautifulSoup
- tensorflow
- tensorflow_hub
- keras
- opencv

##### API
- Instagram Graph API 
- Kakao Map API

## Functions

### User
* SignUp (+Daum Adress API)
* Login / Logout
* Security - Spring boot에서 제공하는 SecurityConfig 사용
* Session(in backend) / Cookies(in front) - 기본적인 페이지 이동엔 Cookies, 데이터 수신&송신때 Session의 token과 비교하여 보안 강화
* MyPage - 즐겨찾기 기능 추가(favor) - 자신이 등록한 가게+리뷰를 등록한 가게 favorlist에 자동 저장   

### Rst
* 메뉴 CRUD 기능
* 레스토랑 CRUD 기능
* 레스토랑 위치 Map에 표시
* My Store -> detail 페이지 링크 

### Review
* 리뷰 CRUD 기능
* 리뷰 댓글 CRUD 기능
* 새로운 리뷰 및 댓글 생성시 자동으로 업데이트 

### Instagram

#### Clawling

<시작하기>
* #가게명 입력

<데이터 추출>
1. selenium와 BeautifulSoup라이브러리를 활용하여 인스타그램 데이터 크롤링
2. 크롤링된 데이터에서 인스타그램 계정, 이미지, 좋아요수 등 데이터를 추출

<이미지 전처리>
1. tensorflow-hub를 활용한 이미지간 유사도 측정을 진행, 유사도가 낮은 이미지들 필터링
2. opencv의 haarcascades을 활용한 사람이 나오는 이미지 필터링
3. 추출된 이미지들과 인스타그램 계정데이터를 DB에 저장

#### Instagram API 
* FaceBook Login
* Connect with Instagram business account 
* Send Read Delete Comment 
* Send Read Delete Reply

페이스북에서 앱검수를 안받은 상태이기 때문에 
테스트계정만 엑세스 가능합니다

<시작하기>
1. 페이스북 로그인 클릭
2. 테스트 계정id, password 입력 후 로그인
3. thank you for~  가 게시물 목록 위에 뜨면 로그인 성공한 것! 

<게시물 사진 조회하기>
4. 3번이 성공했다면, 게시물 목록에 select box에서 게시물 id 하나를 선택 (조회 하려는 게시물을 선택하는 겁니다.)
5. 4번 선택시 게시물 사진들이 뜹니다.

<댓글 적는법>(Comment)
1. "댓글을 입력 해주세요" textarea창에 원하는 댓글을 적습니다.
2.  댓글 전송 버튼을 클릭합니다.
3.  댓글 목록 select box 가 갱신된것을 확인 할수 있습니다.
3-1. instagram id @myunggi_moon 에도 성공적으로 댓글이 달린것을 확인할 수 있습니다.

<댓글 지우는 법> 
1. 댓글목록에서 댓글을 선택합니다.
2. 댓글 삭제 버튼을 클릭합니다.
3.  댓글 목록 select box 가 갱신된것을 확인 할수 있습니다.
3-1. instagram id @myunggi_moon 에도 성공적으로 댓글이 삭제된 것을 확인할 수 있습니다.
 
<대댓글 적는법> (Reply)
0. 댓글목록에서 대댓글을 달 댓글을 선택합니다.
1. "댓글을 입력 해주세요" textarea창에 원하는 대댓글을 적습니다.
2.  대댓글 전송 버튼을 클릭합니다. (주의: 댓글 전송 버튼을 누르면 댓글로 들어갑니다.)
3.  대댓글 목록 select box 가 갱신된것을 확인 할수 있습니다.
3-1. instagram id @myunggi_moon 에도 성공적으로 대댓글이 달린것을 확인할 수 있습니다.

<대댓글 지우는 법> 
1. 대댓글목록에서 대댓글을 선택합니다.
2. 대댓글 삭제 버튼을 클릭합니다.
3.  대댓글 목록 select box 가 갱신된것을 확인 할수 있습니다.
3-1. instagram id @myunggi_moon 에도 성공적으로 대댓글이 삭제된 것을 확인할 수 있습니다.


## Member
- 문명기
- 박기훈
- 김연수
- 진소라
- 이은재 