0. pom.xml   
   
 ##### javax.validation은 최신버전에서 지원하지 않아서 아래 코드를 넣어줘야 한다
   ```<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
  ``` 



1. VO설정 (검증 어노테이션)

  ```java
  public class MemberVO {
	@NotBlank(message = "빈칸이 올 수 없습니다!")
	@Size(min=4)
	private String id;
	@Size(min=4)
	private String pw;
  ```
    @NotNull  : null 허용X   
    @NotEmpty : null, "" 허용X   
    @NotBlank : null,""," " 허용X   
    @Max(value=지정값)  : 최대값 지정   
    @Min(value=지정값)	: 최소값 지정   
    @Size(max=, min=) : 문자열 또는 배열등의 길이 판단 (글자수)   
    @Pattern(regex="정규표현식", flag="")	: 정규표현식   

	  Hibernate 제공 Annotation
	  @Email   
	  @Length(min=, max=)	: 문자열 길이 검증   
	  @Range(min=, max=)	: 숫자 범위 검증   
	  @URL			: URL 형식   


  2. Controller 설정

- Get : view의 form 에서 컨트롤러로 오는 VO객체를, 컨트롤러에서 모델에 담아야한다
  ```java
  @GetMapping("join")
	public void memberJoin(Model model) throws Exception{
		model.addAttribute("memberVO", new MemberVO());
	}
  ```

- Post : @Valid, BindingResult 사용
- ❗️❗️❗️❗️❗️@valid 바로 뒤에 BindingResult를 선언해야한다❗️❗️❗️❗️❗
- 검증 결과를 담는곳이 BindingResult
```java	
@PostMapping("join")
	public String setJoin(@Valid MemberVO memberVO,BindingResult bindingResult)throws Exception{
		if(bindingResult.hasErrors()) {
		return "member/join";	
		}		
		
		int result= memberService.setJoin(memberVO);
		return "redirect:../";
	}
```

3. 뷰 : jsp 설정
   ```xml
   <%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
    <form:form action="./join" modelAttribute="memberVO" method="post">

    
      <form:input path="name" class="form-control" placeholder="name" ></form:input>
	    <form:errors cssClass="c1" path="name"></form:errors>
   
    <!--form:input : name 대신 path, type="text" 내장 -->
    <!-- 태그명으로는 Css 못건다 ,, -->
   ```
 - spring form 태그 사용해야한다
- modelAttribute : Controller에서 Model에  추가한 Bean객체의 속성명
- path는 bean의 멤버변수명, 일반 Form의 name속성의 용도
- 검증 메세지 출력 :  <form:errors path="password"> </form:errors>
