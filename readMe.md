

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

클러스터 인덱스 vs 비클러스터 인덱스에서의 정렬 작업 차이
클러스터 인덱스:

클러스터 인덱스는 실제 데이터가 정렬된 상태로 저장돼 있어요. 따라서 삽입, 수정, 삭제 작업이 일어나면, 데이터 자체를 다시 정렬해야 할 수도 있어요.
데이터가 물리적으로 테이블 내에서 재배치되기 때문에, 디스크 I/O가 더 많이 발생하고 성능에 영향을 미칠 수 있어요.
비클러스터 인덱스:

비클러스터 인덱스는 리프 노드에 **데이터의 위치(포인터)**만 저장해요. 즉, 포인터들만 정렬해야 하지, 실제 데이터 자체는 그대로 유지돼요.
삽입, 수정, 삭제 작업이 있을 때 트리의 균형을 맞추기 위해 포인터를 재정렬하는 작업은 필요하지만, 데이터 자체를 이동시키지 않으므로 클러스터 인덱스보다는 디스크 I/O가 적고 성능 부담이 덜해요.
중요한 차이
클러스터 인덱스에서는 데이터 자체가 정렬되어야 하기 때문에, 삽입이나 수정이 있을 때 데이터를 이동시키고 재정렬하는 작업이 크고 비용이 많이 듭니다.
비클러스터 인덱스에서는 포인터(주소 정보)만 정렬하면 되기 때문에, 트리 구조 안에서 정렬 작업이 일어나는 것이고 실제 데이터는 그대로입니다. 트리의 일부 노드를 분할하거나 병합하면서 트리 구조를 유지하는 것이지, 데이터 자체를 이동시키지는 않아요.
따라서, 정렬 작업 자체는 비클러스터 인덱스에서도 발생하지만, 실제 데이터 자체가 이동하지 않는다는 점에서 비용이 훨씬 적게 든다고 볼 수 있습니다. 이 점 때문에 삽입, 수정, 삭제가 많은 테이블에서는 비클러스터 인덱스가 더 효율적일 수 있는 거예요.

요약:
비클러스터 인덱스에서도 포인터를 정렬해야 하니 정렬 작업은 일어납니다.
하지만 데이터 자체를 이동하거나 재정렬하지 않으므로, 클러스터 인덱스보다 성능 부담이 적어요.
비클러스터 인덱스는 포인터만 정렬하므로 삽입, 수정, 삭제 작업에서 효율적입니다.

<br/>
<br/>
<br/>
<br/>


# 옵티마이저

쿼리변환  
비용기반 옵티마이저 - 통계  

비용 기반 옵티마이저는 여러 경로의 비용을 계산해 가장 효율적인 경로를 선택해.
규칙 기반 옵티마이저는 미리 정해진 규칙을 따르기 때문에 유연성이 떨어져.


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


