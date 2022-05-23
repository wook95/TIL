
#  템플릿 기반 폼

템플릿에서, 디렉티브를 이용해 폼 구성  
NgForm, NgModel, NgModelGroup 이용  
(FormsModule을 사용하는 모듈에 임포트한다)  

## NgModel

ngModel은 유효성 검증 상태, 값의 추적 기능을 제공하는 FormControl 인스턴스를 생성한다.
html의 인풋에 ngModel 디렉티브와 name을 지정해준다.  
디폴트로 값을 지정해주고 싶을땐, 단방향 바인딩 `[ngModel] = "'디폴트값'"`을 사용한다.  
ngModelGroup 로컬참조를 통해 그룹화하고, valid를 확인할 수 있다.  
라디오버튼의 경우 value의 프로퍼티 바인딩을 통해 동적으로 쉽게 value를 결정해 줄 수 있다.  


## NgForm

폼 전체를 관리하는 디렉티브.  
루트 모듈에 FormsModule을 추가하면 NgForm 디렉티브 없이도 form에 자동으로 있는것처럼 적용된다.  
(html 유효성 검증 안할것이므로 .. form에 novalidate 어트리뷰트 추가 요망)  

submit 이벤트는 ngSubmit이벤트로 대체된다.  
`<form (ngSubmit)="onSubmit(f) #f="ngForm">`  
로컬참조에 ngForm을 대입해주면 자바스크립트 폼 객체를 조작할 수 있게 된다.  
로컬참조이기에 onSUbmit의 인자로 f를 넘겨주지 않고 컴포넌트 안에서 ViewChild를 이용해 접근할 수도 있다.  

### 패칭

`viewChild를-통한-로컬참조.setValue`의 경우 전체 폼을 덮어쓴다.
`viewChild를-통한-로컬참조.form.patchValue({})`의 경우 업데이트 하고 싶은 value만 업데이트. 



## 유효성 검사 -> 스타일 적용  

1. ngForm의 로컬참조의 valid값을 통해
2. angular에서 부여해주는 css 클래스를 통해 (ng-invalid, ng-touched)  
3. ngForm의 로컬참조처럼 input에도 ngModel의 로컬참조를 부여, valid값을 활용한다  






#  리액티브 폼

컴포넌트에서 폼 조작   

1. 사용하는 모듈에서 ReactiveFormsModule 임포트  
2. onInit에서 FormGroup초기화  
3. FormGroup안에 FormControl을 넣어줌 


```jsx
ngOnInit() {
    this.signUpForm = new FormGroup({
        username: new FormControl(null),
        gender: new FormControl('male')
    })
}
```

4. html의 폼에 [formGroup]="변수"로 폼그룹 알려줌  
5. html의 인풋에 formControlName을 통해 프로퍼티명 알려줌  
6. html의 폼에 ngSubmit을 달아주고 컴포넌트에서 조작 (컴포넌트에서 만든 formGroup 변수를 통해)  
7. 유효성 검사가 필요하다면 FormGroup 생성시 formControl 안에 두번째 파라미터로 validator 추가  
8. ngIf를 사용해 경고문을 띄워주고 싶다면, FormGroup변수.get('프로퍼티명').valid 활용  
9. formGroup안에 formGroup을 넣어준다. 해당 그룹을 div로 감싸고, formGroupName을 지정해준다.  
10. 동적으로 폼을 추가하고 싶을땐 FormArray  
11. 폼 값의 변화 감지는 formGroup변수.valueChanges 옵저버블 이용, 폼의 유효와 무효의 구독은 statusChanges 
12. 폼변수.setValue로 전체 업데이트, 폼변수.patchValue로 일부 값 업데이트  
