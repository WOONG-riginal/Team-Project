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
create table bbq_menu(
    menuno number primary key,
    menu varchar2(100) not null,
    img varchar2(200) not null,
    price varchar2(50) not null,
    category varchar2(100) not null,
    info varchar2(2000) not null,
    allergy varchar2(200),
    nutri1 number,
    nutri2 number,
    nutri3 number,
    nutri4 number,
    nutri5 number,
    origin varchar2(100)
);<br>

-- 고객센터 테이블 : bbq_board<br>
create table bbq_board(
    num number primary key,
    store varchar2(50) not null,
    title varchar2(100) not null,
    reg_date varchar2(30) not null,
    type varchar2(100) not null,
    writer varchar2(50) not null,
    contact varchar2(50) not null,
    content varchar2(100) not null,
    ref number,
    re_step number,
    re_level number,
    readcount number,
    writerid varchar2(50) not null
);<br>
-- 시퀀스 만들기
create sequence bbq_board_seq
minvalue 1
maxvalue 9999
increment by 1;

-- 회원 테이블 : bbq_member<br>
create table bbq_member (
    id  varchar2(20) primary key,
    password varchar2(50) not null,
    name varchar2(50) not null,
    tel varchar2(50) not null,
    email varchar2(100) not null,
    point number default 1000,
    coupon number default 1,
    card number default 1,
    role varchar2(10) default 'B',
    address varchar2(200),
    mstore varchar2(200),
    gender varchar2(20),
    birth varchar2(20)
);<br>

-- 주문 테이블 : bbq_order<br>
create table bbq_order (
    ordernum  number primary key,
    ordername varchar2(50) not null,
    ordercontact varchar2(50) not null,
    orderstore varchar2(200) not null,
    orderdate date not null,
    ordermenu varchar2(200) not null,
    orderprice number not null,
    qty number not null,
    delivery number not null,
    orderaddress varchar2(200) not null,
    orderid varchar2(50) not null
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

https://github.com/WOONG-riginal/back-end/tree/a58fcd8a96b8c7d3af1bb861f71f6af38daf2baf/BBQ

<h2>#6. 프로젝트 시연</h2>

  <h3>A. 회원가입 및 온라인 주문</h3>

  https://github.com/WOONG-riginal/test/assets/136036366/cf6fe9df-5a67-4847-a426-b7dfe39a67a3

  <h3>B. 게시판 작성 및 회원정보 수정</h3>

  https://github.com/WOONG-riginal/test/assets/136036366/5aed3d6d-f2ee-49d1-8f9a-a098f0604397

  <h3>C. 게시판 답변 확인하기</h3>

  https://github.com/WOONG-riginal/test/assets/136036366/dc451961-00cc-4e32-9c18-eefb2c5997bc

  <h3>D. 서브 및 콘텐츠 메뉴</h3>

  https://github.com/WOONG-riginal/test/assets/136036366/9bd22c4c-36c9-4cce-a33f-7959e88d4b8d

  <h3>E. 매장찾기</h3>

  https://github.com/WOONG-riginal/test/assets/136036366/ccb12654-5b37-4442-b5ef-ae9839fee811

  <h3>F. 관리자 로그인 및 전용 페이지</h3>

  https://github.com/WOONG-riginal/test/assets/136036366/cfe06943-ca0b-4af0-bc79-21fd24683f94
