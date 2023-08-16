# wanted-pre-onboarding-backend
지원자: 박민주

## 구현한 API의 동작을 촬영한 데모 영상 링크
- https://youtu.be/Noo2s7UyB_w
<hr/>

## 애플리케이션의 실행 방법 (엔드포인트 호출 방법 포함)
- 과제 1. 사용자 회원가입 엔드포인트
  - 홈 화면의 [회원가입] 버튼 클릭 -> 회원가입 폼 화면으로 이동
- 과제 2. 사용자 로그인 엔드포인트
  - 홈 화면의 [로그인] 버튼 클릭 -> 로그인 폼 화면
- 과제 3. 새로운 게시글을 생성하는 엔드포인트
  - 로그인 한 상태에서 홈 화면의 [새 글쓰기] 버튼 클릭
- 과제 4. 게시글 목록을 조회하는 엔드포인트
  - 홈 화면에 게시글 목록
- 과제 5. 특정 게시글을 조회하는 엔드포인트
  - 홈 화면에서 게시물 제목 클릭시 조회 화면으로 넘어감, 
- 과제 6. 특정 게시글을 수정하는 엔드포인트
  - 로그인 한 상태에서 상세 페이지 접속 시 [수정]버튼 보임, 클릭 시 수정화면 진입
- 과제 7. 특정 게시글을 삭제하는 엔드포인트
  - 로그인 한 상태에서 상세 페이지 접속 시 [삭제]버튼 보임, 클릭 시 해당 게시물 삭제

<hr/>

## 데이터베이스 테이블 구조
### site_user 테이블
![image](https://github.com/minjuaaa/wanted-pre-onboarding-backend/assets/51702223/24d119d8-267e-430c-ad32-e8948622d93d)

<br/>

### question 테이블
#### author_id는 외래키(fk)로 site_user테이블의 id 값과 연결

![image](https://github.com/minjuaaa/wanted-pre-onboarding-backend/assets/51702223/ac5ccb02-d75c-4a6d-be18-2ae4387f836e)



## 구현 방법 및 이유에 대한 간략한 설명
- jwt 토큰 발행 과정에서 오류가 발생하여 form로그인, 회원가입 방식으로 구현

## API 명세(request/response 포함)

![image](https://github.com/minjuaaa/wanted-pre-onboarding-backend/assets/51702223/9b15d541-46ed-4c28-a27b-af01439153de)


## docker-compose 실행방법
1. 윈도우 개발 환경에서 Dokerfile, docker-compose.yml 작성
2. 도커 설정파일을 포함한 스프링 프로젝트 github에 push & commit
3. AWS EC2 ubuntu 실행
4. gitclone으로 프로젝트 다운받음
5. ubuntu에서 docker, docker-compose 설치 후 명령어 입력
6. 도커 mysql, 스프링 컨테이너 실행
```
services:
  mysql:
    image: mysql:latest
    ports:
      - 3306:3306  # MySQL 포트 매핑 (호스트 포트:컨테이너 포트)
    environment:
      - MYSQL_ROOT_PASSWORD=0000  # MySQL 루트 비밀번호
    volumes:
      - mysql_data:/var/lib/mysql  # MySQL 데이터 볼륨

  app:
    build: .
    ports:
      - 8080:8080  # 스프링 애플리케이션의 포트 매핑 (호스트 포트:컨테이너 포트)
    environment:
      - SPRING_DATASOURCE_URL=jdbc:mysql://mysql:3306/bootex?useSSL=false&useUnicode=true&serverTimezone=Asia/Seoul&allowPublicKeyRetrieval=true
      - SPRING_DATASOURCE_USERNAME=root
      - SPRING_DATASOURCE_PASSWORD=0000
    depends_on:
      - mysql
```
