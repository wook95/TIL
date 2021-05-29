0. 설정
    - spring security api 추가
    - 프로젝트 생성시 api 선택 혹은 pom.xml 에 api 선언
  ```
  <dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
```



jsp에서 사용시
```
<dependency>
<groupId>org.springframework.security</groupId>
<artifactId>spring-security-taglibs</artifactId>
</dependency>

```
타임리프에서 사용시
```
<dependency>
<groupId>org.thymeleaf.extras</groupId>
<artifactId>thymeleaf-extras-springsecurity5</artifactId>
</dependency>
```

1. 기본 용어

    a. 인증 (Authentication)

    - 예를 들어 이 회사에 들어갈 수 있는 사람인가 (회사 출입문)
    - 로그인
    - 유저 식별 (관리자니?)

    b. 인가, 권한부여 (Authorization)

    - 예를들어 회사에 들어왔어도 이 사람이 들어갈 수 있는곳들이 구별 되어있다
    - 접근 권한
    - 인증된 유저의 권한 (판매자니 소비자니?)

    c. 접근 주체 (principal)

    - Security에서 사용하는 인증, 인가정보가 있는 유저

2. DB
  
  1)) member     : 사용자 정보 (기존 테이블 사용) 

           enabled 칼럼 추가(BIT) - 계정 사용 유무

2)) Role    :  권한 정보를 저장

             roleName 데이터 저장시 접두어로 'ROLE_' 추가

             PK(roleNum), roleName 2개 칼럼

             

 3)) member_role   : 어떤 유저가 role을 가지는지 저장

            N:M 관계이므로 member와 role의 pk를 저장하는 테이블
           member_role 생성





3. VO : userDetail 인터페이스 구현
    	//role 저장	
	```java
      @Override
      public Collection<? extends GrantedAuthority> getAuthorities() {
        //그랜티드어써리티를 상속받는 어떤 애들 타입이 이거다
      List<GrantedAuthority> authorities = new ArrayList<GrantedAuthority>();

      for(RoleVO roleVO:this.roles) {
        authorities.add(new SimpleGrantedAuthority(roleVO.getRoleName()));
      }
      return authorities;
	}```

4. Service: UserDetailsService 인터페이스 구현

❗️회원가입시 passwordEncoder.encode를 통해 비밀번호 암호화해야된다. 인터페이스 구현해서 필요한 메소드 오버라이딩
```java 
@Override
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

		//스프링 시큐리티에서 알아서 로그인 처리해줌
		MemberVO memberVO = new MemberVO();
		memberVO.setUsername(username);
		memberVO=memberMapper.getLogin(memberVO);		
		return memberVO;
	}
```





   5. config

```java
public class WebSecurityConfig extends  WebSecurityConfigurerAdapter{

	@Bean
	public PasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}//인터페이스라 바로 객체 못 만들고 구현된 객체 사용
	
	
	
	@Override
	public void configure(WebSecurity web) throws Exception {

		//security를 무시(제외)
		web.ignoring()
		.antMatchers("/resources/**")
		.antMatchers("/images/**")
		.antMatchers("/css/**")
		.antMatchers("/js/**")
		.antMatchers("/vendor/**")
		.antMatchers("/favicon/**")
		;
	}
	
	@Override
	protected void configure(HttpSecurity http) throws Exception {

		http
			.exceptionHandling()
				//사용하지 않으면 기본 제공 에러 처리 방법 사용 403.html
				.accessDeniedPage("/member/error")	//url주소로 보내는 방법
				//accessDeniedHandler(new SecurityException()) //전문 처리 객체 만드느법
				.and()
			.cors().and()
			.csrf().disable()
			.authorizeRequests()
			.antMatchers("/").permitAll()
			.antMatchers("/notice/list","/notice/select").permitAll()
			.antMatchers("/notice/**").hasRole("ADMIN")
			.antMatchers("/qna/list").permitAll()
			.antMatchers("qna/**").hasAnyRole("ADMIN","MEMBER")		
			.antMatchers("/member/join").permitAll()
			.antMatchers("/member/**").hasAnyRole("ADMIN","MEMBER")
			.anyRequest().authenticated()
			.and()
		.formLogin()
			//로그인 페이지 따로 안 만들어도 기본 폼으로 이동하는데
			//내가 만든 폼으로 이동하고 싶으면 이렇게 !
			//어서라이즈 리퀘스트 한덩어리,, 폼 로그인은 다르 덩어리
			//and 쓰기 싫으면 http. 쓰면 된다
			.loginPage("/member/login")
			.defaultSuccessUrl("/member/memberLoginResult")
			//로그인 실패시 처리 - 안해도 되지만 할수있어!~! / 에러 파라미터는 컨트롤러에서 조정
			//.failureUrl("/member/loginFail?error")		
			//failureHandler(null)
			.permitAll()
			.and()
		.logout()
			.logoutUrl("/member/logout")	 //로그아웃
			.logoutSuccessUrl("/")			//로그아웃 후 가는 주소
			.invalidateHttpSession(true)	//세션 삭제, 밑은 쿠키 삭제
			.deleteCookies("JSESSIONID")
			.permitAll()
			.and()
		.exceptionHandling()
			.accessDeniedPage(null) 		//권한 에러 발생(403)
			.accessDeniedHandler(null) 		//에러 처리 클래스선언 - 우리가 만들어야됨
			;
		

	}
```


