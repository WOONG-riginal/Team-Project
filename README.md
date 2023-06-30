<h1>조별 풀스택 프로젝트 CRUD</h1>

<h2>#1. 개요</h2>

> HTML, CSS, JS을 활용해 BBQ 사이트를 클론코딩하고, WEB JAVA를 통해 CRUD 기능을 구현하였습니다.<br>
> C - 회원가입, 문의글 작성, 온라인 주문<br>
> R - 서브페이지 및 콘텐츠페이지 메뉴 조회, 회원정보 조회, 문의글 조회, 주문내역 조회, 회원목록 불러오기<br>
> U - 회원정보 수정, 문의글 수정, 포인트 누적<br>
> D - 회원탈퇴, 문의글 삭제
<br><br>


<h2>#2. DB 구성</h2>

<button>열기</button>
<script>
  $('button').click(function(){
    $(this).next().toggle();
  })
</script>
<p>
  /*
   프로젝트명 : Floatleft_Project_BBQ
   작업명 : BBQ 웹자바 구현
   메뉴 테이블명 : bbq_menu
   고객센터 테이블명 : bbq_board
   회원 테이블명 : bbq_member
   주문 테이블명 : bbq_order
*/


-- 기존 테이블 있는지 확인 후 존재하면 삭제
drop table bbq_menu;
drop table bbq_board;
drop table bbq_member;
drop table bbq_order;

-- 메뉴 테이블명 : bbq_menu 테이블
drop table bbq_menu;

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
);



--=========================== 고객센터 테이블 ===========================
-- 고객센터 테이블
drop table bbq_board;
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
);


select * from bbq_board;

drop sequence bbq_board_seq;
-- 시퀀스 만들기
create sequence bbq_board_seq
minvalue 1
maxvalue 9999
increment by 1;

commit;

--고객의 소리 쓰기
insert into bbq_board values(bbq_board_seq.nextval,'BBQ노원구','글제목',sysdate,'주문거부','송승현','010-1111-1111','글내용',1,0,0,0,'ezen');
commit;

select max(ref) from bbq_board;

--계층형 게시판 쿼리문
select * from bbq_board order by ref desc, re_step asc;

--글가져오기 로직
select * from bbq_board where num=1;

--글상세보기
select  * from bbq_board where num=1 ;

--비밀번호 비지니스 로직
select password from bbq_board where num=1;

--글수정 로직??
UPDATE bbq_board SET content='점심시간아와라' WHERE num=1;

--글 삭제 로직
DELETE FROM bbq_board WHERE num=1;

-- 관리자페이지 문의내역 조회 로직
select * from bbq_board order by ref desc, re_level asc, re_step asc;

-- 관리자페이지 답변 등록 로직
update bbq_board set re_level=re_level+1 where ref=? and re_level>?;
insert into bbq_board values(bbq_board_seq.nextval,?,'[답변] '||?,sysdate,?,?,?,?,?,?,?,0);

-- 관리자페이지 답변여부 확인 로직
select count(*) from bbq_board where ref=?;

-- 답변글 조회 로직
select * from bbq_board where ref=? and re_step>1;


--=========================== 회원 테이블 ===========================
drop table bbq_member;
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
);
insert into bbq_member(id,password,name,tel,email,role) 
values ('ezen','1111','김이젠','01023456789','ezen@ezen.com','A');

commit;
update bbq_member set point=(point+19000) where id='ezen';

select * from bbq_member;

-- 로그인 확인 쿼리문
select count(*) from bbq_member where id='ezen' and password=1111;

-- id 중복 확인 쿼리문
select count(*) from bbq_member where id='ezen';

-- 비밀번호 확인 쿼리문
select password from bbq_member where id='ezen';

-- 마이페이지 쿼리문
select * from bbq_member where id='ezen';

-- 비밀번호 변경 쿼리문
update bbq_member set password='2222' where id='ezen';

-- 회원정보 변경 쿼리문
update bbq_member set birth='19920528', tel='01012341234', email='ez@eez.com', address='다른주소' where id='ezen';

-- 회원탈퇴 쿼리문
delete from bbq_member where id='ezen';


commit;

------------------------------------------------------------------------------

drop table bbq_order;
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
);
select * from bbq_order;

select *
from bbq_member mem, bbq_board brd
where mem.name=brd.writer
and mem.id='asdf12' and brd.writer='김이름';

select * from bbq_member mem, bbq_order ord where mem.id=ord.orderid and ord.orderid='asdf1234';
</p>


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
