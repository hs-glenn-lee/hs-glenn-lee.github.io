---
layout: post
title:  "액티브 레코드 패턴"
author: "이희수"
---

Django ORM이 Active Record Pattern으로 구현되어있다하여, 마틴 파울러의 엔터프라이즈 어플리케이션 아키텍쳐에서 관련 내용을 정리해본다.

[장고 공식 Documentation, 디자인 철학](https://docs.djangoproject.com/en/2.2/misc/design-philosophies/#include-all-relevant-domain-logic) 중 에서

> Include all relevant domain logic¶
Models should encapsulate every aspect of an “object,” following Martin Fowler’s Active Record design pattern.
> 모델은 객체의 모든 측면을 캡슐화 해야한다.
> This is why both the data represented by a model and information about it (its human-readable name, options like default ordering, etc.) are defined in the model class; all the information needed to understand a given model should be stored in the model.
> 따라서 모델이 나타내는 데이터와 모델에 관한 정보(사람이 읽을 값, default 정렬 방법 등)은 모델 클래스에 정의되어야 한다. 주어진 모델을 이해하는데 필요한 정보는 모델 안에 있어야 한다.


## 액티브 레코드 패턴
> An object that wraps a row in a database table or view, encapsulates the database access, and adds domain logic on that data.
> 데이터베이스 테이블이나 뷰의 행을 래핑하고, 데이터베이스 접근을 캡슐화하여, 해당 데이터에 대한 도메인 논리를 추가하는 객체

![액티브 레코드 패턴 uml]({{site.url}}/assets/postimages/activeRecordSketch.gif )



### 정의와 특징
Persistent Data를 다루는 패턴 중에 하나다.

활성 레코드의 핵심은 도메인 모델이며, 도메인 모델 안에서 활성 레코드 클래스는 데이터 베이스의 레코드 구조와 거의 일치하게 된다.

각 활성 레코드는 데이터베이스에 **데이터를 저장 및 로드**하고 해당 **데이터를 대상으로 하는 모든 도메인 논리**를 담당한다.

활성 레코드가 어플리케이션의 모든 도메인 논리를 포함할 수도 있지만,?? 일부 도메인 논리는 트랜잭션 스크립트에 포함되고 공용 및 데이터 기반 코드는 활성 레코드에 포함될 수도 있다.

활성 레코드의 자료구조는 데이터베이스의 구조와 정확하게 일치해야 한다.

이 패턴에서 클래스는 편의를 제공하지만, 관계형 데이터베이스가 있다는 사실을 감출 수는 없다. 따라서 활성 레코드를 사용할 때는 그렇지 않을 때보다 일반적으로 다른 객체-관계형 매핑(ORM) 패턴이 적게 사용된다?.

활성 레코드 클래스에는 일반적으로 다음과 같은 일을 하는 메서드가 있다.

- SQL 결과 집합 행을 이용해 활성 레코드의 인스턴스를 생성
- 테이블에 삽입할 새로운 인스턴스 생성
- 자주 사용되는 SQL 쿼리를 래핑하고 활성 레코드 객체를 반환하는 정적 검색기 메서드
- 데이터베이스를 업데이트하고 활성 레코드의 데이터를 삽입
- 필드 얻기 및 설정
- 비즈니스 논리의 일부를 구현

**활성 레코드**는 행 데이터 **게이트웨이?**와 아주 비슷하다. 가장 큰 차이는 게이트 웨이는 데이터 베이스 접근만 포함하지만, **활성 레코드는 데이터 원본과 도메인 논리를 모두 포함한다는 것이다.**

활성레코드와 데이터베이스 간의 밀접한 결합 떄문에 이 패턴에는 정적 검색 메서드가 사용되는 경우를 자주 보게 된다. 그러나 검색 메서드를 별도의 클래스로 분리하지 못할 이유는 없으며, 행 데이터 게이트 웨이 에서도 설명 했지만 이렇게 하는 편이 테스트하는 데 편리하다.
=> ModelManager!

*궁금점1 대체 활성 레코드 클래스는 테이블이냐 레코드냐?*

좀 생각해보니 당연하게도 .. **활성 레코드 클래스의 인스턴스는 하나의 데이터베이스 레코드다.**

특징적인 부분은 행 데이터 베이스 게이트웨이 패턴과는 다르게, save, update 등 CRUD를 레코드 인스턴스 메소드로 수행한다는 것이다. **Person(...field values...).save()**

이래서 active record인 것 같다. 레코드 값만 담고 있는 객체인 것이 아니라 실제 동작을 수행하기 때문에..

*궁금점1-2* 어떤것을 클래스 메소드에 정의하고, 어떤 것을 인스턴스 메소드에 정의 할까.

예제 코드를 보고 추측한다.
```text
class Person...
    private static String findStatementString = "SELECT id, ... FROM people WHERE id = ?";

    public static Person find(Long id) {
        ... 생략 ...
        rs = findStatement.executeQuery(); // select 쿼리 수행
        rs.next();
        result = load(rs); // ResultSet을 Person() 객체로 초기화 하는 동작
        return result;
    }...
```

정적 검색기 메소드 find(id), Django ORM으로 치면 .get(pk="ID_VALUE")는 클래스의 스태틱 메소드(public static method. 장고로 치면 @classmethod)다.

Django ORM에서 정적 검색기는 **Person.objects**에 할당된 **ModelManager**다. 클래스 변수 **objects** 에 할당 되므로 ModelManager는 위에서 처럼 다른 클래스로 분리된 활성 레코드 클래스의 클래스 메소드다.

다음 에제 코드와 설명

> 모든 비즈니스 논리(예: 공제액 계산)는 인물 클래스 자체에 포함된다. p.173
```text
class Person...

    public Money getExemption() {
        Monney baseExemption = Money.dollars(1500);
        Money dependentExepmtion = Money.dollars(750);
        return baseExemption.add(dependentExemption.multiply(this.getNumberOfDependents()));
    }
```

아직 잘 모르겠지만.. 비즈니스 로직은 인스턴스 메소드로, 정적 메소드에는 활성 레코드 인스턴스 값과 무관한 검색과 같은 정적 동작을 정의하면 되는 것 같다.

*궁금점1-3 일부의 비즈니스 논리는 어떻게 구현되나? 전체의 비즈니스의 논리중 어떤 일부가 활성 레코드에 구현되나*
***결론 적으로 활성 레코드는 도메인 모델의 일부.. 데이터베이스를 조작하는 부분이니.. 잘 모르는 도메인 모델 섹션을 더 공부해야.. 전체적인 결론을 구할 수 있을 것 같다.***

## 사용 시점
#### 장점
활성 레코드는 생성, 읽기, 갱신 같은 기본적인 도메인 논리를 처리하는 데 적합하다. 단일 레코드 기반의 파생과 유효성 검사는 이 구조에서 아주 잘 동작한다.

활성 레코드의 핵심 장점은 단순성이다. 활성 레코드는 작성하기 쉽고, 이해하기도 쉽다.

#### 단점
활성 레코드의 주된 문제는 활성 레코드 객체가 데이터베이스 테이블과 일대일로 대응 되는 동형 스키마일 때만 잘 동작한다는 것이다. 비즈니스 논리가 복잡한 경우 객체의 직접관계, 컬렉션, 상속 등을 사용하고 싶어진다. 이러한 개념은 활성 레코드에 어울리지 않으며 억지로 적용하다 보면 엉망진창이 될 수 있다.

=> *SQL을 직접 쓰는 것이 불편해 지면 적용하기 좋은 단순한 패턴, 쉽지만 비즈니스 논리가 복잡한 경우에 다른 객체지향적 요소를 사용한 디자인이 어렵다.*


