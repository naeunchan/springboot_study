# 테스트 주도 개발(Test-driven development, TDD)
## 단위 테스트
1. 단위 테스트는 개발 단계 초기에 문제 발견 가능
2. 회귀 테스트 가능
3. 기능에 대한 불확실성 감소
4. 빠른 피드백

# Code

## ./web/HelloController
### @RestController
-> 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줌.<br>

### @GetMapping
-> HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 줌.<br>

### @RequestParam
-> 외부에서 API로 넘긴 파라미터를 가져오는 어노테이션.<br>

### .param
-> API 테스트 시 사용될 요청 파라미터 설정.<br>
값은 String만 허용.<br>
숫자/날짜 등의 데이터를 등록할 때는 문자열로 변경하여 저장.<br>

### jsonPath
-> JSON 응답값을 필드별로 검증할 수 있는 메소드.<br>
$를 기준으로 필드명 명시.<br>

## ./web/HelloControllerTest
### @RunWith(SpringRunner.class)
-> 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행.<br>
스프링 부트 테스트와 JUnit 사이에 연결자 역할.<br>

### @WebMvcTest
-> 여러 스프링 테스트 어노테이션 중, Web(Spring MVC)에 집중할 수 있는 어노테이션.<br>
선언할 경우 @Controller, @ControllerAdvice 등 사용 가능.<br>
단, @Service, @Component, @Repository 등은 사용 불가.<br>

### @Autowired
-> 스프링이 관리하는 빈(Bean)을 주입 받음.<br>

### private MockMvc mvc
-> 웹 API를 테스트 할 때 사용.<br>
스프링 MVC 테스트의 시작점.<br>
이 클래스를 통해 HTTP GET, POST 등에 대한 API 테스트 가능.<br>

### mvc.perform(get("/hello"))
-> MockMvc를 통해 /hello 주소로 HTTP GET 요청.<br>
체이닝이 지원되어 여러 검증 기능을 이어서 선언 가능.<br>

### .andExpect(status().isOk())
-> mvc.perform의 결과 검증.<br>
HTTP Header의 Status 검증.<br>
200, 404, 500 등의 상태 점검.<br>
isOk => 200.<br>

### .andExpect(content().string(hello))
-> mvc.perform의 결과 검증.<br>
응답 본문의 내용 검증.<br>

##  ./web/dto/HelloResponseDto
### @Getter
-> 선언된 모든 필드의 get 메소드 생성.<br>

### @RequiredArgsConstructor
-> 선언된 모든 final 필드가 포함된 생성자 생성.<br>
final이 없는 필드는 생성자에 포함되지 않음.<br>

## ./web/dto/HelloResponseDtoTest
### assertThat()
-> assertj라는 테스트 검증 라이브러리의 검증 메소드.<br>
검증하고 싶은 대상을 메소드 인자로 받는다.<br>
메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용 가능.<br>

### isEqualTo()
-> assertj의 동등 비교 메소드.<br>
assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공.<br>

### asertj의 장점
-> 추가적인 라이브러리가 필요하지 않고, 자동 완성이 좀 더 확실하게 지원된다.<br>

