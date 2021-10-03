
# controller에서 해야 할일

## 1. 객체를 개체화(Object -> Entity)

1. 콘트롤러 Art art = bdto.toEntity();

2. Art 클래스 생성 위에 @Entity해주고 bdto와 같이 변수 생성 후 
		id위엔  @GeneratedValue @Id어노테이션(import javax.persistence.Id;)

3. BDTO에 toEntity() 함수 생성

	
		public Art toEntity() {

      		  	long id=0;
   	    	 	return new Art(id,name,title,content);
  		  }

## 2. 개체들을 db에 저장(repository)
1.  콘트롤러 전역
		 @Autowired
    		private ArtRepository artRepository;
	 	
out해주는 함수 안에 

		Art saved = artRepository.save(art);

2. ArtRepository 인터페이스 만들고 상속

		public interface ArtRepository extends CrudRepository<Art, Long> {

		}

## 3. application.properties 안에 작성 

	spring.h2.console.enabled :true
	spring.jpa.show-sql : true

## 4. 실행-> 주소창에 http://localhost:8446/h2-console 입력

## 5. JDBC URL에 콘솔창에 ctrl +f +jdbc해서 찾은 값 복붙 -> sql 입력 가능 (insert폼에서 받은 값 select 가능)

# 개체 하나로 쓰는법


## 1. School 개체 클래스 생성 

1. 디폴트 생성자, getter setter 생성자 추가 , 위에 @NoargsConstructor @Getter @Setter 써줘도 됨

2. 나머지는 위랑 같음 

## 2.  SchoolRepository CRUD 인터페이스 생성
	위와 같음

## 3. 홈컨트롤러 (커맨드 방식 가능)

	@AllArgsConstructor
	@Controller
	public class SchoolController {

    	@Autowired
    	private SchoolRepository schoolRepository;
    	
	/*위에 @AllArgsConstructor 해주면 아래처럼 생성자 안해도 갖다 쓸 수 있음
        	public SchoolController(SchoolRepository schoolRepository) {
            this.schoolRepository = schoolRepository;
        	}
     	*/

    	@PutMapping("/school/save")
    	@ResponseBody
    	public School School( School school){

      	  return  schoolRepository.save(school);
    	}
	}

## 4. application.properties 에 다음처럼 입력

	server.port =8446
	spring.h2.console.enabled=true
	spring.datasource.url= jdbc:h2:mem:demo

