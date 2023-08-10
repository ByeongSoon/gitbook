---
description: MySQL에서 여러 테이블 또는 쿼리의 데이터를 결합하는 데 사용되는 두 가지 다른 작업인 Join과 UNION의 차이점에 대해 알아본다.
---

# MySQL에서 Join과 UNION의 차이점은?

### Join

JOIN 작업은 두 개 이상의 테이블 사이의 관련 열을 기반으로 행을 결합하는 데 사용됩니다. 여러 테이블 간의 관계를 지정하여 여러 테이블에서 데이터를 검색할 수 있습니다. 다음과 같은 다양한 유형의 JOIN 작업이 있습니다.

* INNER JOIN: 지정된 조인 조건에 따라 두 테이블에서 일치하는 행만 반환합니다.
* LEFT JOIN: 조인 조건에 따라 왼쪽 테이블의 모든 행과 오른쪽 테이블의 일치하는 행을 반환합니다. 일치하는 항목이 없으면 오른쪽 테이블의 열에 대해 NULL 값이 반환됩니다.
* RIGHT JOIN: 조인 조건에 따라 오른쪽 테이블의 모든 행과 왼쪽 테이블의 일치하는 행을 반환합니다. 일치하는 항목이 없으면 왼쪽 테이블의 열에 대해 NULL 값이 반환됩니다.
* FULL JOIN: 일치하지 않는 행을 포함하여 두 테이블의 모든 행을 반환합니다. 일치하는 항목이 없으면 각 테이블의 열에 대해 NULL 값이 반환됩니다.

조인 조건은 일반적으로 ON 키워드를 사용하여 정의되며 테이블 간의 관계를 설정하는 데 사용되는 열 또는 표현식을 지정합니다.

```sql
SELECT Employees.Name, Departments.Dept_Name
FROM Employees
JOIN Departments ON Employees.Dept_ID = Departments.Dept_ID;
```

### UNION

UNION 연산자는 둘 이상의 SELECT 문의 결과 집합을 단일 결과 집합으로 결합하는 데 사용됩니다. 열의 수와 데이터 유형이 일치하는 한 서로 다른 쿼리의 행을 세로로 쌓을 수 있습니다. UNION에 대해 주목해야 할 중요한 사항은 다음과 같습니다.

* 결과 집합의 열 이름은 UNION의 첫 번째 SELECT 문에 의해 결정됩니다.
* SELECT 문에서 해당 열의 데이터 유형이 호환되어야 합니다.
* 기본적으로 UNION은 최종 결과 집합에서 중복 행을 제거합니다. 중복을 포함하려면 UNION ALL 연산자를 대신 사용할 수 있습니다.
* 모든 SELECT 문의 열의 개수와 순서는 동일해야 합니다.

UNION은 구조가 동일하고 단일 결과 집합으로 처리해야 하는 여러 쿼리의 결과를 결합하려는 경우에 유용합니다.

```sql
SELECT Name
FROM Employees
WHERE Dept_ID = 1
UNION
SELECT Name
FROM Employees
WHERE Dept_ID = 3;
```



요약하면 JOIN은 관계를 기반으로 여러 테이블의 행을 결합하는 데 사용되는 반면 UNION은 여러 쿼리의 결과 집합을 세로로 쌓는 데 사용됩니다.&#x20;

JOIN은 열을 가로로 결합하고 UNION은 행을 세로로 결합합니다.
