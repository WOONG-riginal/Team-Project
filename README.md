<h1>조별 풀스택 프로젝트 CRUD</h1>

<h2>#1. 개요</h2>

> HTML, CSS, JS을 활용해 BBQ 사이트를 클론코딩하고, WEB JAVA를 통해 CRUD 기능을 구현하였습니다.<br>
> C - 회원가입, 문의글 작성, 온라인 주문<br>
> R - 서브페이지 및 콘텐츠페이지 메뉴 조회, 회원정보 조회, 문의글 조회, 주문내역 조회, 회원목록 불러오기<br>
> U - 회원정보 수정, 문의글 수정, 포인트 누적<br>
> D - 회원탈퇴, 문의글 삭제
<br><br>


<h2>#2. DB 구성</h2>

> 프로젝트명 : Floatleft_Project_BBQ<br>
> 작업명 : BBQ 웹자바 구현<br>
> 메뉴 테이블명 : bbq_menu<br>
> 고객센터 테이블명 : bbq_board<br>
> 회원 테이블명 : bbq_member<br>
> 주문 테이블명 : bbq_order<br>
<br>

-- 메뉴 테이블명 : bbq_menu<br>
create table bbq_menu(<br>
    menuno number primary key,<br>
    menu varchar2(100) not null,<br>
    img varchar2(200) not null,<br>
    price varchar2(50) not null,<br>
    category varchar2(100) not null,<br>
    info varchar2(2000) not null,<br>
    allergy varchar2(200),<br>
    nutri1 number,<br>
    nutri2 number,<br>
    nutri3 number,<br>
    nutri4 number,<br>
    nutri5 number,<br>
    origin varchar2(100)<br>
);<br><br>

-- 고객센터 테이블 : bbq_board<br>
create table bbq_board(<br>
    num number primary key,<br>
    store varchar2(50) not null,<br>
    title varchar2(100) not null,<br>
    reg_date varchar2(30) not null,<br>
    type varchar2(100) not null,<br>
    writer varchar2(50) not null,<br>
    contact varchar2(50) not null,<br>
    content varchar2(100) not null,<br>
    ref number,<br>
    re_step number,<br>
    re_level number,<br>
    readcount number,<br>
    writerid varchar2(50) not null<br>
);<br>
-- 시퀀스 만들기<br>
create sequence bbq_board_seq minvalue 1 maxvalue 9999 increment by 1;<br><br>

-- 회원 테이블 : bbq_member<br>
create table bbq_member (<br>
    id  varchar2(20) primary key,<br>
    password varchar2(50) not null,<br>
    name varchar2(50) not null,<br>
    tel varchar2(50) not null,<br>
    email varchar2(100) not null,<br>
    point number default 1000,<br>
    coupon number default 1,<br>
    card number default 1,<br>
    role varchar2(10) default 'B',<br>
    address varchar2(200),<br>
    mstore varchar2(200),<br>
    gender varchar2(20),<br>
    birth varchar2(20)<br>
);<br><br>

-- 주문 테이블 : bbq_order<br>
create table bbq_order (<br>
    ordernum  number primary key,<br>
    ordername varchar2(50) not null,<br>
    ordercontact varchar2(50) not null,<br>
    orderstore varchar2(200) not null,<br>
    orderdate date not null,<br>
    ordermenu varchar2(200) not null,<br>
    orderprice number not null,<br>
    qty number not null,<br>
    delivery number not null,<br>
    orderaddress varchar2(200) not null,<br>
    orderid varchar2(50) not null<br>
);<br><br>


<h2>#3. 구성</h2>

> 메인 페이지<br>
> 서브 페이지(메뉴 소개)<br>
> 콘텐츠 페이지(메뉴 정보)<br>
> 마이 페이지 및 관리자 페이지<br>
> 회원가입 페이지<br>
> 로그인 페이지<br>
> 온라인주문 페이지<br>
> 고객문의 페이지
<br><br>


<h2>#4. Work-Flow</h2>

![워크플로우](https://github.com/WOONG-riginal/Team-Project/assets/136036366/bfc6ba18-0ed0-4342-a5d6-71a06e568851)



<h2>#5. 소스코드</h2>

https://github.com/WOONG-riginal/back-end/tree/a58fcd8a96b8c7d3af1bb861f71f6af38daf2baf/BBQ/src/main/webapp

<h2>#6. 프로젝트 시연</h2>

  <h3>A. 페이지 소개</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/cd8cdb58-fd81-4a16-aea6-44a241ac238a

  1. 메인페이지 : 실시간 인기메뉴 슬라이드 및 이미지 슬라이드 구성
  2. 온라인주문 및 고객센터 페이지는 로그인이 필요한 서비스
  3. 서브페이지(메뉴소개) : DB에 입력된 정보를 카테고리 별로 출력
  4. 콘텐츠페이지(메뉴상세정보) : 서브페이지에서 선택된 메뉴에 대한 DB에 입력된 정보를 출력


  <h3>B. 매장찾기</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/012977db-77c9-4ed8-9797-316887d43e6d

  1. 전국 BBQ매장 조회
  2. 키워드 검색 시 해당 매장 조회
  3. 메인페이지에서 키워드 입력 가능
  4. 매장 위치를 전용 마커로 표시
  5. 마커 및 검색목록 클릭 시 해당 매장 정보 조회
  

  <h3>C. 회원가입</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/1fa21483-3adb-48c6-9ebd-c6de7e709813

  1. 필수약관 동의 시에만 회원가입 가능
  2. 아이디 및 비밀번호는 조건에 맞게 기입
  3. 비밀번호 확인 시 동일한 비밀번호 입력
  4. 추천매장 검색 후 클릭으로 입력
  5. 주소지는 도로명 및 지번으로 검색, 입력 후 상세주소 추가기입 가능
  6. 회원가입 완료 시 마케팅수신동의(선택시) 알림문구 출력
  
  https://github.com/WOONG-riginal/Team-Project/assets/136036366/9259736d-6ef4-451e-834a-2d4c3590d078

  1. 아이디 중복 시 가입불가
  2. 선택사항은 입력하지 않아도 회원가입 가능


  <h3>D. 로그인 로그아웃</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/01c0d3ed-70ec-44a3-a6cf-765114430a9c
  
  
  <h3>E. 주문하기</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/c59b3c4a-5126-473d-a78a-dad41df154a6

  1. 먼저 주문매장 필수로 선택, 회원가입 시 등록한 추천매장이 있다면 사용 가능, 다른 매장 선택도 가능
  2. DB에 입력된 메뉴정보를 통해 메뉴목록 제공
  3. 배달/포장 선택

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/7f7f364e-57c5-4fff-a8b8-e9d2d51b9298

  1. 배달 주문시 배달지 입력 필요
  2. 포장주문에는 주소지 입력이 필요하지 않음
  3. 주문내역은 마이페이지에서 확인
  

  <h3>F. 문의글 작성</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/e0228352-e1e3-4141-8596-b831c592a5b1

  1. 해당 작성글 내용 및 답변여부는 마이페이지에서 확인 가능


  <h3>G. 마이페이지</h3>

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/31100a5b-e607-4157-af44-05a46723156f

  https://github.com/WOONG-riginal/Team-Project/assets/136036366/11cf43d1-2046-4faf-b946-df32c5eda382

  1. 회원가입 시 기본 포인트 1000P 제공, 이후 주문금액의 10% 적립
  2. 개인정보 조회 및 변경 : 먼저 비밀번호를 확인하고 페이지 연결
  3. 입력한 정보 변경 가능 (단, 이름과 아이디는 변경 불가)
  4. 입력하지 않은 선택정보 입력 가능, 주소지의 경우 변경 및 삭제 가능
  5. 비밀번호 변경은 추가적인 페이지에서 진행
  6. 로그인 된 회원의 주문내역 및 문의내역 확인 가능
  7. 문의글에 대한 답변만 조회 가능
  
  https://github.com/WOONG-riginal/Team-Project/assets/136036366/d25b48ca-66ac-4e21-80e8-0819b160b030

  1. 답변 이전의 문의글에 대해서만 수정 및 삭제 가능

  
<h3>H. 관리자페이지</h3>

https://github.com/WOONG-riginal/Team-Project/assets/136036366/1e203c31-fb02-47aa-ad74-478e94a3c42e

1. 관리자로 로그인 시 관리자페이지 사용 가능
2. 회원목록 확인, 가입 시 입력하지 않은 항목은 미기입으로 표기
3. 모든 주문내역 확인, 주문자 ID를 같이 표기해 동명이인의 경우 구분
4. 모든 문의내역 확인 및 답변 등록
