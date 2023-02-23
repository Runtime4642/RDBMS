

# 인덱스

 인덱스란?  - 인간 세상에서 주소

 B*Tree vs hash  
 많을 수록 이득인가?  
 적절한 인덱스의 선택
 
 
 # 트리거  
 <br/>
 <br/>
 <br/>
 
 
 
 # 프로시저  
 <br/>
 <br/>
 <br/>
 
 
 # 안좋은 쿼리란? -> 성능도 물론 중요하지만 - 유지보수  
 <br/>
 <br/>
 <br/>


 ## cluster index vs nonclustered index

 클러스터드 인덱스는 데이터를 재배열 한다.
 넌클러스터드 인덱스는 인덱스 테이블을 생성합니다.


클러스터형 인덱스
- 인덱스를 생성할 때는 데이터 페이지 전체를 다시 정렬한다.
- 대용량의 데이터를 강제로 다시 클러스터 인덱스를 생성하는 건 조심
- 인덱스 자체가 데이터 페이지이다. 인덱스 자체에 데이터가 포함
- 비클러스형 인덱스 보다 검색 속도는 더 빠르다. 하지만 데이터의 입력/수정/삭제는 느리다.
- 테이블에 한 개만 생성할 수 있다.


넌 클러스터형 인덱스
- 별도의 페이지에 인덱스를 구성한다.
- 검색 속도는 느리지만, 데이터의 입력,수정,삭제가 더 빠르다.
- 남용할 경우에는 시스템 성능을 떨어뜨리는 결과를 가져온다.

<br/>
<br/>
<br/>
<br/>


# 옵티마이저

쿼리변환  
비용기반 옵티마이저 - 통계  
힌트


<br/>
<br/>
<br/>
<br/>


# 조인
LEFT
RIGHT
FULL OUTER JOIN
loop join, sort_merge join, hash join => https://lee-mandu.tistory.com/470


https://devuna.tistory.com/36


# SQL

##
1. 조인 및 WHERE 조건에는 항상 인덱스가 존재 할 것
2. 데이터량을 판단하여 쿼리를 작성 할 것
3. IN 보다는 EXISTS
4. 서브쿼리는 주의
5. 대용량 데이터는 조인 전에 GROUP
6. 전체 출력 금지(*) - 인라인 뷰는 예외
7. 쓰지 않아도 될 Having 주의
8. 적절한 임시 테이블
9. ANSI 표준 쿼리 작성(GROUP BY 를 사용하지 않고 집계함수 사용 등.. 금지)   


본인만의 모양이 있어야함.
드라이빙테이블이 왼쪽 드라이븐 테이블을 오른쪽


두개의 사각형을 위 아래로 붙인다 => UNION ALL  

두개의 사각형을 옆으로 붙인다 =>  조인  

데이터를 위 아래로 합친다 -> GROUP BY  

가로로 되어 있는 사각형을 세로로 변경한다 -> CASE  



WITH 문

소계 합계



#격리수준  

@Transactional(isolation = Isolation.READ_UNCOMMITTED, propagation = Propagation.REQUIRED, rollbackFor = Exception.class)


