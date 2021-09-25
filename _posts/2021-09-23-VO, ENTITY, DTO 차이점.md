<br/><br/>
# 1. Entity :개체

* 실제 db의 테이블과 1:1로 매핑되는 클래스  

* 테이블 내에 존재하는 컬럼만을 필드로 가져야 함  

* 최대한 외부 Entity 클래스의 getter method를 사용하지 않도록 해당 클래스 내에서 필요한 method를 구현한다.  

* Domain Logic만 가능 Presentation Logic은 안됨  

* 구현 method는 주로 Service Layer에서 사용  
<br/><br/>

# 2. DTO

 * Data Transfer Object: 데이터 전송 객체  

* 비동기 처리시 주로 사용  

* 계층간 데이터 교환을 위한 객체(JAVA Beans)  

* DB의 데이터를 Service나 Controller 등으로 보낼 때 사용하는 객체  
->DB의 데이터가 Presentation Logic Tier로 넘어올 때는 DTO로 변환됨  

*  로직 없는 순수 데이터 객체 GETTER SETTER 메서드만 갖는다.  

*  Controller Layer에서 Response DTO형태로 client에 전달  
<br/><br/>
 


# 3. VO

* Value Object: 객체  

* equals(),hashcode() 오버라이딩  

* 필드의 모든 값들이 VO 객체마다 값이 같아야 똑같은 객체로 판별  

* GETTER SETTER, 및 테이블 내 있는 필드 외에 추가적인 필드를 가질 수 있다.   

* 여러테이블에대한 공통 속성을 모아 만든 VO클래스를 상속받는 것도 가능   
<br/><br/><br/><br/>




# 참고

💻  <https://velog.io/@gillog/Entity-DTO-VO-%EB%B0%94%EB%A1%9C-%EC%95%8C%EA%B8%B0>


	