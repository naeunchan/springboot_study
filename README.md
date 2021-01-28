# 테스트 주도 개발(Test-driven development, TDD)
## 단위 테스트
1. 단위 테스트는 개발 단계 초기에 문제 발견 가능
2. 회귀 테스트 가능
3. 기능에 대한 불확실성 감소
4. 빠른 피드백

# Code

## ./web/HelloController
### @RestController
-> 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줌.

### @GetMapping
-> HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 줌.

## ./web/HelloControllerTest
### @RunWith(SpringRunner.class)
-> 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행.
   스프링 부트 테스트와 JUnit 사이에 연결자 역할

### @WebMvcTest
-> 여러 스프링 테스트 어노테이션 중, Web(Spring MVC)에 집중할 수 있는 어노테이션.
   선언할 경우 @Controller, @ControllerAdvice 등 사용 가능.
   단, @Service, @Component, @Repository 등은 사용 불가.

### @Autowired
-> 스프링이 관리하는 빈(Bean)을 주입 받음.

### private MockMvc mvc
-> 웹 API를 테스트 할 때 사용.
   스프링 MVC 테스트의 시작점.
   이 클래스를 통해 HTTP GET, POST 등에 대한 API 테스트 가능.

### mvc.perform(get("/hello"))
-> MockMvc를 통해 /hello 주소로 HTTP GET 요청.
   체이닝이 지원되어 여러 검증 기능을 이어서 선언 가능.

### .andExpect(status().isOk())
-> mvc.perform의 결과 검증.
   HTTP Header의 Status 검증.
   200, 404, 500 등의 상태 점검.
   isOk => 200.

### .andExpect(content().string(hello))
-> mvc.perform의 결과 검증.
   응답 본문의 내용 검증.

##  ./web/dto/HelloResponseDto
### @Getter
-> 선언된 모든 필드의 get 메소드 생성.

### @RequiredArgsConstructor
-> 선언된 모든 final 필드가 포함된 생성자 생성.
   final이 없는 필드는 생성자에 포함되지 않음.

## ./web/dto/HelloResponseDtoTest
### assertThat()
-> assertj라는 테스트 검증 라이브러리의 검증 메소드.
   검증하고 싶은 대상을 메소드 인자로 받는다.
   메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용 가능.

### isEqualTo()
-> assertj의 동등 비교 메소드.
   assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공.