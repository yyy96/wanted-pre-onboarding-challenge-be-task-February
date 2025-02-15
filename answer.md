1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

**RDMS** <br>
RDMS는 관계형 데이터 모델을 기초로 두고 모든 데이터를 2차원 테이블 형태로 관리합니다.
이렇게 테이블 형태로 관리하는 것은 장단점이 존재합니다.
  - **장점**
    - 스키마에 맞춰 데이터를 관리하기 때문에 명확한 데이터 구조와 데이터의 정합성을 보장할 수 있습니다.
  - **단점**
    - 시스템이 커질 수록 (Join 문이 많아져) 쿼리가 복잡해질 수 있습니다.
    - 스키마로 인해 데이터가 유연하지 못하고, 스키마를 변경하게 될 경우 복잡해질 수 있습니다.
    - 성능 향상을 위해서는 서버의 성능을 향상 시켜야하는 Scale-up만을 지원합니다.

**NoSQL** <br>
NoSQL은 RDBMS RDBMS는 Scale-Up으로만 성능이 향상 가능하므로 이를 해결하기 위해 Scale-out을 목표로 등장하였습니다.
때문에 RDMS와 달리 테이블 간 관계를 정의하지 않아 스키마에 맞춰 데이터를 관리하지 않고, 이에 관한 장단점을 지니고 있습니다.
  - **장점**
    - 스키마가 없기 때문에 유연하고 자유로운 데이터 구조를 가질 수 있다. (언제든 저장된 데이터를 조정하고 새로운 필드를 추가할 수 있다.)
    - 데이터 분산이 용이하며 성능 향상을 위한 Saclue-up과 Scale-out이 가능하다.
  - **단점**
    - 데이터 중복이 발생할 수 있으며, 중복된 데이터를 UPDATE 하는 경우 모든 컬렉션에서 수행해야하기 때문에 느리다.
    - 스키마가 존재하지 않기에 명확한 데이터 구조를 보장하지 않으며 데이터 구조 결정이 어려울 수 있다.

<br><br>

2. 트랜잭션(transaction)이란 무엇인가요?

**Transaction** <br>
트랜잭션은 데이터의 정합성을 보장하기 위한 기능입니다.
논리적인 작업 셋 자체가 100% 적용되거나(`COMMIT`) 또는 아무것도 적용되지 않아야 함(`ROLLBACK`)을 보장해줍니다.

- 트랜잭션 **제어어** (TCL/Transaction Control Language)
  - 커밋 (`Commit`) : 트랜잭션의 모든 미결정 데이터를 영구적으로 반영함으로써 트랜잭션을 종료합니다.
  - 롤백 (`Rollback`) : 트랜잭션의 모든 미결정 데이터 변경을 포기함으로써 트랜잭션을 종료합니다.

- 트랜잭션 **특징** <br>
이러한 트랜잭션은 ACID 라 하는 원자성, 일관성, 격리성, 지속성 4가지 성질을 보장해야합니다.
  - 원자성 (`Atomicity`) : 트랜잭션 내에서 실행한 작업들은 마치 하나의 작업인 것처럼 모두 성공 혹은 모두 실패해야합니다.
  - 일관성 (`Consistency`) : 모든 트랜잭션은 일관성있는 데이터베이스 상태를 유지해야합니다.
  - 격리성 (`Isolation`) : 동시에 실행되는 트랜잭션들이 서로에게 영향을 미치지 않도록 격리해야합니다.
  - 지속성 (`Durability`) : 트랜잭션을 성공적으로 끝내면 그 결과가 항상 기록되어야합니다.

<br><br>

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.

**Join** <br>
조인(Join)은 두 개 이상의 테이블을 묶어서 하나의 결과(집합)을 이끌어내는 것입니다.
즉, 서로 다른 테이블에서 데이터를 가져올 때 사용하는 것이 `Join`입니다.

- Join의 다양한 **방식**들
  - `INNER JOIN` : 두 테이블의 교집합 부분에 해당하며, 조인하는 테이블의 조건(`ON절`)이 일치하는 결과를 출력합니다.
  - `OUTER JOIN` : INNER JOIN과 달리 조인하는 테이블에서 한쪽 테이블에만 조건이 일치해도(내용이 존재해도) 결과가 검색됩니다.
  - `LEFT JOIN` : 두 테이블을 Join한다고 할 때, 첫 번째 테이블을 기준으로 두 번째 테이블을 조합하는 Join 입니다.
  - `RIGHT JOIN` : 두 테이블을 Join한다고 할 때, 두 번째 테이블을 기준으로 첫 번째 테이블을 조합하는 Join 입니다.


<br><br>

4. MySQL에서 인덱스(index)란 무엇인가요?

**Index** <br>
Index란 테이블을 처음부터 끝까지 검색하는 방법인 `FTS`(Full Table Scan)이 아니라, 인덱스를 검색하여 해당 자료의 테이블을 엑세스 하는 방법입니다.
즉, 인덱스는 데이터의 저장 성능 보단 데이터의 검색 속도를 높이는 기능이라 볼 수 있습니다.

DBMS는 index를 항상 최신의 정렬된 상태로 유지해야 원하는 값을 빠르게 탐색할 수 있습니다.
이때 왜 항상 정렬된 상태인지 생각해보자면, Index의 **자료구조**에 대해 생각해볼 수 있습니다
 - RDBMS의 Index 자료구조는 주로 `B+Tree` 로 이루어져있는데, 이는 항상 정렬된 상태를 유지하는 자료구조이므로 Index의 부등호(`<`, `>`)를 이용한 순차 검색 연산에 적합합니다.

그렇기 때문에 인덱스가 적용된 컬럼에 INSERT, UPDATE, DELETE가 수행된다면 각각 다음과 같은 연산을 추가적으로 해주어야하며 그에 따른 오버헤드가 발생합니다.

- 인덱스를 **사용해야 하는 경우**
  - 데이터의 양이 많고 검색이 변경보다 빈번한 경우
  - 인덱스를 걸고자 하는 필드의 값이 다양한 값을 가지는 경우

- 인덱스를 사용할 시 **단점**
  - INSERT, DELETE, UPDATE 쿼리문을 실행할 때 별도의 과정이 추가적으로 발생하기 때문에 DB의 변경작업이 잦으면 오버헤드가 발생합니다.
