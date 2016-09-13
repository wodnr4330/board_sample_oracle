## Spring 4 + MyBatis 3 + Oracle 기반 게시판 ##
본 샘플은  Spring 4 + MyBatis 3 + Oracle (Maven) 기반으로  게시판을 만드는 과정을 단계별로 구현한 샘플이다.

자세한 설명은 [이곳에서](http://forest71.tistory.com/2) 얻을 수 있다. 

각 내용은 다음과 같이 구성되었다.

### 1. board Step 1 (board1) ###
- List: 모든 게시물 출력
- Form: 사용자 입력 내용 저장
- Update: 사용자 입력 내용 수정
- Read:   사용자 입력 내용 보기
- Delete: 지정된 게시물 삭제

URL: http://localhost:8080/board/board1List

### 2. board Step 2 (board2) ###
- List: 페이징, 새로운 번호 부여
- Form: 입력/수정을 하나로
- Read: 조회수 
- Delete: 삭제에서 숨기기로

URL: http://localhost:8080/board/board2List


### 3. board Step 3 (board3) ###
- List: 검색, 제목을 한 줄로 표시 ==> 페이징을 공통으로 
- Form: 필수입력, 수정/저장 서비스 하나로
- Read: 스크립트 실행 방지

### 4. board Step 4 (board4) ###
- 자료실

- Step 4.1 (board41)
: CheckStyle, PMD, FindBugs 적용 후 수정

### 5. board Step 5 (board5) ###
- 댓글

### 6. board Step 6 (board6) ###
- 무한 댓글 (계층형)

### 7. board Step 7 (board7) ###
- JQuery 활용


### 8. board Step 8 (board8) ###
- 멀티 게시판

### 9. board Step 9 (board9) ###
- 멀티 게시판 관리자

### 개발 환경 ### 
    Programming Language - Java 1.7
    IDE - Eclipse
    DB - Oracle 
    Framework - MyBatis, Spring 4
    Build Tool - Maven

### 설치 ###

먼저 다음과 같은 테이블을 생성해야 한다.

    CREATE TABLE TBL_BOARD(  
    	BGNO NUMBER(11,0), -- 게시판 그룹번호
    	BRDNO NUMBER(11,0), -- 글번호
    	BRDTITLE VARCHAR2(255 BYTE), -- 글제목
    	BRDWRITER VARCHAR2(20 BYTE), -- 작성자
    	BRDMEMO VARCHAR2(4000 BYTE), -- 글내용
    	BRDDATE DATE, -- 작성일자
    	BRDHIT NUMBER, -- 조회수
    	BRDDELETEFLAG CHAR(1 BYTE), -- 삭제여부 
        CONSTRAINT BRDNO_PK PRIMARY KEY (BRDNO)
    );
    CREATE SEQUENCE BRDNO_SEQ;
      
    CREATE TABLE TBL_BOARDFILE( 
      	FILENO NUMBER(11,0), 
    	BRDNO NUMBER(11,0), 
    	FILENAME VARCHAR2(100 BYTE), 
    	REALNAME VARCHAR2(30 BYTE), 
    	FILESIZE NUMBER, 
    	CONSTRAINT FILENO_PK PRIMARY KEY (FILENO)
    );
    CREATE SEQUENCE FILENO_SEQ;

    CREATE TABLE TBL_BOARDREPLY ( 
    	BRDNO NUMBER(11,0) NOT NULL, 
    	RENO NUMBER(11,0), 
    	REWRITER VARCHAR2(10 BYTE) NOT NULL, 
    	REMEMO VARCHAR2(500 BYTE), 
    	REDATE DATE, 
    	REDELETEFLAG VARCHAR2(1 BYTE) NOT NULL, 
    	REPARENT NUMBER(11,0), 
    	REDEPTH NUMBER, 
    	REORDER NUMBER, 
    	CONSTRAINT RENO_PK PRIMARY KEY (RENO)
    );
    	
    CREATE TABLE TBL_BOARDGROUP (
    	BGNO NUMBER(11,0), 
    	BGNAME VARCHAR2(50 BYTE), 
    	BGPARENT NUMBER(11,0), 
    	BGDELETEFLAG CHAR(1 BYTE), 
    	BGUSED CHAR(1 BYTE), 
    	BGREPLY CHAR(1 BYTE), 
    	BGREADONLY CHAR(1 BYTE), 
    	BGDATE DATE, 
    	CONSTRAINT BGNO_PK PRIMARY KEY (BGNO)
    );
    CREATE SEQUENCE BGNO_SEQ;


\board\src\main\webapp\WEB-INF 폴더에 있는 applicationContext.xml에서 적절한 DB 접속 정보를 입력하고 실행하면 된다.


