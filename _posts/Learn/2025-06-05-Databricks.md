---
layout: single
title: "Pyspark와 Databricks : 클라우드 환경에서 빅데이터 처리 시작하기"
date: 2025-06-05 19:25:49 +0900
category:
  - learn
tags:
  - 테스트
  - 블로그
toc: "true"
toc_sticky: "true"
---
### **[Learn] PySpark와 Databricks: 클라우드 환경에서 빅데이터 처리 시작하기**

---

### **서론: Python과 Pandas의 한계, 그리고 PySpark & Databricks의 필요성**

데이터의 홍수 속에서 데이터 분석가와 엔지니어에게 데이터 처리 능력은 핵심 역량이 되었다. Python의 Pandas 라이브러리는 데이터를 다루는 데 있어 매우 직관적이고 강력한 도구였다. 하지만 Pandas는 단일 서버의 메모리 안에서만 데이터를 처리할 수 있는 한계를 가졌다. 처리할 데이터의 크기가 서버 메모리를 초과하면, 작업은 불가능해지거나 극도로 느려졌다.

데이터의 규모가 수십, 수백 기가바이트를 넘어 테라바이트, 페타바이트 단위로 폭발적으로 증가하면서, 이러한 '단일 머신' 환경의 한계는 빅데이터 분석과 처리에 가장 큰 걸림돌이 되었다. 이러한 문제를 해결하기 위해, 분산 컴퓨팅 환경에서 대규모 데이터를 처리하는 프레임워크인 Apache Spark가 등장했다.

그리고 Python 개발자들에게 익숙한 문법으로 Spark를 다룰 수 있게 해주는 도구가 바로 PySpark이다. PySpark는 Pandas의 한계를 극복하고, 수십, 수백 GB에 달하는 데이터도 분산된 환경에서 효율적으로 처리하는 무기가 된다. 이 PySpark를 클라우드 환경에서 손쉽게 다룰 수 있도록 돕는 플랫폼이 바로 Databricks이다. 본 포스팅에서는 PySpark의 핵심 원리를 파악하고, Databricks 환경에서 이를 어떻게 활용하는지 데이터 엔지니어의 관점에서 설명하고자 한다.

---

### **1. Databricks 환경 이해: 나의 작업 공간**

Databricks는 Apache Spark 기반의 **통합 분석 플랫폼(Unified Analytics Platform)**이다. 데이터 과학자, 데이터 엔지니어, 머신러닝 엔지니어가 데이터 처리, 분석, 모델 개발 및 배포 작업을 한곳에서 수행하도록 설계되었다.

데이터 엔지니어에게 Databricks가 유용한 점은 다음과 같다.

- **관리형 Spark 클러스터**: 복잡한 Spark 클러스터 설정 및 관리를 Databricks가 담당한다. 인프라 관리 부담 없이 데이터 처리 로직에 집중할 수 있다.
    
- **협업용 노트북 환경**: 웹 기반 노트북으로 코드, 시각화, 설명을 통합한다. 팀원들과 실시간으로 협업하며 데이터를 탐색하고 파이프라인을 개발할 수 있다.
    
- **다양한 데이터 소스 연결**: Azure Blob Storage, Azure Data Lake Storage, Azure SQL Database 등 다양한 Azure 데이터 서비스와 쉽게 연결하여 데이터를 읽고 쓸 수 있다.
    
- **확장성 및 효율성**: 필요에 따라 클러스터 크기를 유연하게 조절하여, 대규모 데이터 처리 작업을 효율적으로 수행하고 비용을 최적화할 수 있다.
    

![](2025-06-05-Databricks-2.png)

---

### **2. PySpark 핵심 개념: Databricks 노트북에서 만나다**

PySpark의 강력함을 온전히 활용하려면 몇 가지 핵심 개념을 파악해야 한다. 이 개념들은 Spark가 데이터를 어떻게 처리하고, 분산 환경을 어떻게 관리하는지 보여준다. Databricks 노트북 환경에서 이 개념들을 직접 실습하며 이해할 수 있다.

#### **2.1 SparkSession: 분산 환경의 진입점**

`SparkSession`은 PySpark의 모든 작업이 시작되는 진입점이다. SparkSession 객체는 분산 환경의 자원을 관리하고, 개발자가 작성한 코드를 실행 가능한 계획으로 전환한다. 클러스터에 연결하고, 데이터를 읽어 들이며, DataFrame을 생성하는 등 모든 작업은 SparkSession 객체를 통해 이루어진다.

Databricks 환경에서는 `SparkSession` 객체가 `spark`라는 이름으로 자동으로 생성되어 제공된다. 따라서 별도의 설정 없이 바로 PySpark 코드를 시작할 수 있다.

![](2025-06-05-Databricks-4.png)



![](2025-06-05-Databricks-5.png)


![](2025-06-05-Databricks-6.png)




![](2025-06-05-Databricks-7.png)

![](2025-06-05-Databricks-8.png)


![](2025-06-05-Databricks-9.png)




![](2025-06-05-Databricks-10.png)

![](2025-06-05-Databricks-11.png)




Python

```
# Databricks 노트북에서는 SparkSession이 'spark' 이름으로 자동 생성된다.
# 따라서 별도로 SparkSession을 생성할 필요 없이 바로 사용 가능하다.

# 예시: 간단한 데이터로 DataFrame 생성하기
data = [("Alice", 1), ("Bob", 2), ("Cathy", 3)]
columns = ["Name", "Age"]
df = spark.createDataFrame(data, columns)

# DataFrame 내용 확인
df.show()
# 결과:
# +-----+---+
# | Name|Age|
# +-----+---+
# |Alice|  1|
# |  Bob|  2|
# |Cathy|  3|
# +-----+---+

# DataFrame의 스키마 확인
df.printSchema()
# 결과:
# root
#  |-- Name: string (nullable = true)
#  |-- Age: long (nullable = true)
```

**[여기에 `spark.createDataFrame` 코드 실행 결과가 보이는 Databricks 노트북 스크린샷을 추가해야 합니다.]**

#### **2.2 DataFrame: 대규모 데이터를 위한 분산된 구조**

PySpark의 `DataFrame`은 Pandas의 DataFrame과 유사하게 테이블 형태의 데이터를 제공한다. 그러나 결정적인 차이가 있다. Pandas DataFrame이 단일 머신 메모리에 모든 데이터를 저장한다면, PySpark DataFrame은 데이터를 클러스터의 여러 노드에 분산하여 저장한다. 이 덕분에 대용량 데이터를 처리하는 과정에서 메모리 부족 현상을 겪지 않는다.

DataFrame은 데이터를 분산 저장할 뿐만 아니라, `지연 연산(Lazy Evaluation)`이라는 특성을 가진다. 이는 개발자가 DataFrame에 대해 어떤 연산을 지시하더라도, 실제 데이터 처리(연산)는 해당 결과가 필요할 때(예: `show()`, `count()`, `write()` 등) 비로소 시작된다는 의미이다. 불필요한 연산을 줄여 성능을 최적화하는 데 도움이 된다.

Python

```
# 예시: DataFrame 기본 연산 (지연 연산 확인)
from pyspark.sql.functions import col

# 가상의 주문 데이터 DataFrame 생성
order_data = [
    ("CustA", "ProdX", 100, "2023-01-01"),
    ("CustB", "ProdY", 150, "2023-01-02"),
    ("CustA", "ProdZ", 200, "2023-01-03"),
    ("CustC", "ProdX", 50, "2023-01-04"),
    ("CustB", "ProdX", None, "2023-01-05") # 결측치 포함
]
order_columns = ["CustomerID", "Product", "Amount", "OrderDate"]
orders_df = spark.createDataFrame(order_data, order_columns)

print("원본 DataFrame 스키마:")
orders_df.printSchema()

# 'Amount'가 100 이상인 주문만 필터링 (Transformation - 지연 연산)
filtered_df = orders_df.filter(col("Amount") >= 100)

# 'Amount' 컬럼의 결측치를 0으로 채우기 (Transformation - 지연 연산)
filled_df = filtered_df.na.fill(0, subset=['Amount'])

print("\n필터링 및 결측치 처리된 DataFrame (show()를 통해 Action 발생):")
filled_df.show() # show() 액션이 발생해야 위의 Transformation이 실행됨
```

**[여기에 `DataFrame` 생성 및 기본 연산(`filter`, `na.fill`, `show` 등) 결과가 보이는 Databricks 노트북 스크린샷을 추가해야 합니다.]**

#### **2.3 카탈리스트 옵티마이저 (Catalyst Optimizer): PySpark의 두뇌**

PySpark가 대규모 데이터를 빠르게 처리하는 가장 큰 이유 중 하나는 **카탈리스트 옵티마이저**에 있다. 이것은 Spark의 쿼리 최적화 엔진으로, 개발자가 작성한 코드를 보고 가장 효율적인 실행 계획을 스스로 수립한다.

카탈리스트 옵티마이저는 크게 세 가지 단계에 걸쳐 작동한다.

1. **논리적 계획(Logical Plan) 생성**: 개발자가 작성한 코드(예: `df.filter().join()`)를 받아서, 어떤 연산을 수행해야 하는지 논리적인 구조를 만든다. 이때는 아직 실제 연산이 시작되지 않는다.
    
2. **논리적 최적화**: 논리적 계획을 분석하여 더 효율적인 연산 순서를 찾는다. 예를 들어, 조인(Join) 전에 불필요한 데이터를 미리 필터링하여 데이터의 양을 줄이는 '필터 푸시다운(Filter Pushdown)' 같은 최적화를 수행한다.
    
3. **물리적 계획(Physical Plan) 생성**: 최적화된 논리적 계획을 바탕으로, Spark 클러스터에서 실제로 연산을 수행할 가장 효율적인 방법을 결정한다.
    

이러한 과정을 통해 PySpark는 개발자가 작성한 코드를 그대로 실행하는 것이 아니라, 내부적으로 가장 빠르고 효율적인 실행 계획을 만들어내어 처리 속도를 혁신적으로 향상시킨다. `explain()` 메서드를 사용하여 PySpark가 생성하는 실행 계획을 직접 확인할 수 있다.

Python

```
# 예시: explain()을 통해 카탈리스트 옵티마이저의 작동 확인
# 위에서 생성한 orders_df를 사용

# Amount가 100 이상인 주문을 필터링하고 Product별로 합계를 계산하는 연산
optimized_plan_df = orders_df.filter(col("Amount") >= 100).groupBy("Product").sum("Amount")

# explain()을 사용하여 최적화된 실행 계획 확인
optimized_plan_df.explain(extended=True)
# 결과는 복잡한 텍스트로 나타나지만, 'Filter', 'HashAggregate', 'Exchange' 등
# Spark가 어떤 단계를 거쳐 최적화했는지 보여준다.
```

**[여기에 `explain()` 메서드 실행 결과의 일부 또는 주요 단계가 보이는 Databricks 노트북 스크린샷을 추가해야 합니다.]**

---

### **3. PySpark로 배우는 데이터 전처리 실습 (Databricks 활용)**

이 섹션은 PySpark가 실제 데이터 전처리 과정에서 어떻게 활용되는지 보여주는 실습 예제로 구성된다. 군주가 Databricks 노트북 환경에서 가상의 데이터를 활용하여 기본적인 전처리 파이프라인을 구축하는 과정을 설명한다.



#### **3.1 데이터 로드 및 초기 탐색: 데이터 불러오기**

데이터 엔지니어링의 첫 단계는 데이터를 불러오는 것이다. PySpark는 다양한 데이터 소스로부터 데이터를 `DataFrame`으로 로드하는 강력한 기능을 제공한다. 여기서는 가장 흔한 형태인 CSV 파일을 로드하는 예시를 사용한다.



























- **가상의 데이터셋 로드**: 가상의 고객 주문 데이터, 판매 데이터 등 간단한 시나리오를 설정하고, 이 데이터를 Databricks 노트북으로 로드하는 과정을 보여줍니다. `spark.read`를 사용하여 CSV, JSON 등 일반적인 파일 형식의 데이터를 로드하는 예시가 좋습니다.
    
    Python
    
    ```
    # 예시: 가상 CSV 파일에서 데이터 로드
    # 이 코드는 Databricks 환경에 업로드된 가상 CSV 파일을 읽는다고 가정합니다.
    # 예: '/databricks-datasets/retail-org/customers/customers.csv' 같은 경로
    
    # 가상의 데이터 (실제 파일이 없다면 PySpark로 직접 생성해도 됨)
    sample_data = [
        (1, "ProductA", 10.5, "Electronics", "2023-01-01"),
        (2, "ProductB", 20.0, "Food", "2023-01-01"),
        (1, "ProductC", None, "Electronics", "2023-01-02"),
        (3, "ProductD", 5.0, "Books", "2023-01-02"),
        (2, "ProductA", 12.0, "Electronics", "2023-01-03")
    ]
    sample_columns = ["OrderID", "ProductName", "Price", "Category", "OrderDate"]
    sample_df = spark.createDataFrame(sample_data, sample_columns)
    sample_df.show()
    sample_df.printSchema()
    
    # 실제 파일 로드 예시 (주석 처리)
    # df_loaded = spark.read.format("csv") \
    #     .option("header", "true") \
    #     .option("inferSchema", "true") \
    #     .load("dbfs:/path/to/your/virtual_data.csv")
    ```
    
    **[여기에 가상 데이터를 `DataFrame`으로 로드하는 코드와 결과 스크린샷을 추가해야 합니다.]**
    
- **핵심 전처리 작업**: 위에서 로드한 가상 데이터셋을 활용하여 다음 전처리 작업들을 PySpark 코드로 보여줍니다. 각 작업마다 짧은 코드와 그 코드의 역할을 설명해야 합니다.
    
    - **결측치 처리**: `None` 값(`null`)을 `0`이나 다른 값으로 채우거나 해당 행을 제거하는 예시 (예: `df.na.fill()`, `df.dropna()`).
        
    - **데이터 타입 변환**: 컬럼의 데이터 타입을 정확하게 맞춰주는 예시 (예: `df.withColumn("Price", col("Price").cast("double"))`).
        
    - **데이터 통합 (Join)**: 두 개의 가상 `DataFrame`을 만들어 `join()` 연산을 통해 데이터를 통합하는 예시. (예: 고객 정보 DataFrame과 주문 정보 DataFrame 조인)
        
    - **데이터 필터링 및 선택**: 특정 조건을 만족하는 데이터만 필터링하고 필요한 컬럼만 선택하는 예시.
        
    - **데이터 집계 (Aggregation)**: `groupBy()`와 `agg()`를 사용하여 특정 기준(예: 카테고리별 총 판매액)으로 데이터를 집계하는 예시.
        
    - **(선택 사항) UDFs**: `SQL UDFs`나 `Python UDFs`를 활용하여 사용자 정의 함수로 데이터를 변환하는 간단한 예시를 추가할 수 있다면 좋습니다.
        

**[위의 각 전처리 작업별로, 해당 기능을 시연하는 PySpark 코드 예제와 실행 결과 스크린샷을 추가해야 합니다. 랩 파일을 참고하여 가장 간결하고 명확한 예시를 선택하십시오.]**

---

### **4. 결론: PySpark와 Databricks, 나의 데이터 엔지니어링 여정**

이 포스팅에서 다룬 PySpark의 핵심 개념과 Databricks 환경에서의 실습은 데이터 엔지니어링의 중요한 기본기를 제공한다. Python의 유연성과 Spark의 분산 처리 능력이 Databricks의 관리형 플랫폼 안에서 시너지를 발휘하여, 대규모 데이터 처리의 복잡성을 효과적으로 해결할 수 있음을 확인했다.

군주는 이 학습 경험을 통해 데이터의 '양'에 짓눌리지 않고, 데이터를 정제하고 변환하며 분석 가능한 형태로 제공하는 데이터 엔지니어의 핵심 역량을 이해하고 있다. 이 지식은 향후 더 복잡한 데이터 파이프라인을 설계하고 구축하는 데 든든한 기반이 될 것이다.