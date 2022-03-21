# React Hook Form

기존 html과 ,js를 가지고 Input Validation, Form Submit, onChange Event Listener 등 폼 관리를 하기엔 너무 힘들다. 이러한 문제점을 위해 보다 적은 코드 양으로 쉽게 작성할 수 있는 라이브러리가 생겼는게 그게 바로 **React-Hook-Form**이다.

### 설치하기

```
> npm install react-hook-form
```

React 버전 충돌 에러가 뜬다면

```
> npm install react-hook-form --legacy-peer-deps
```

### 불러오기

```JSX
import { useForm } from "react-hook-form";

const {} = useForm();
```

### register

input을 바로 state와 연결시켜줌

```JSX
const { register } = useForm();
{...register("값이름")}
```

register 적용 전

```JSX
<input  onChange={()=>{
            const {currentTarget: { value }} = event;
            setEmail(value);
        }}>
```

적용 후

```JSX
<input {...register("username")}>
```

### watch

말 그대로 form을 '보게해주는'함수

```JSX
const { watch } = useForm();
console.log(watch()); // { username: "example" }
```

### js 로 html input 속성 넣기 ( required, minLength ... )

```JSX
<input {...register("username", {
    required: true,
    minLength: 5,
})}>
```

### handleSubmit

handleSubmit은 event.PreventDefault 같은 걸 할 함수임

```JSX
const { handleSubmit } = useForm();

<input
onSubmit={ handleSubmit(form이 유효할 때만 실행되는 함수, 유효하지 않을 때 실행되는 함수) }>
```

```JSX
interface EnterForm {
    type
    type
    type
}
const onValid = (validForm: EnterForm) => {
    console.log(validForm);
}
const onInvalid = (errors: FieldErrors) => {
    console.log(errors);
}

<input onSubmit={
    handleSubmit(onValid, onInvalid)
}>
```

### error message 관리

```JSX
<input {...register("username", {
    required: "Username is required",
    minLength: {
        message: "The username should be longer than 5 chars",
        value: 5,
    }
})}>
```

나만의 특별한 validation 규칙을 지정해줄 수 있음

### validate 관리하기

이메일에 @gmail.com이 포함되어 있으면 오류 발생

```JSX
<input {...register("username", {
    required: true,
    minLength: 5,
    validate: {
        notGmail : (value) => !value.includes("@gmail.com")
    }
})}>
```

메시지 관리하기

```JSX
validate: {
    notGmail : (value) => !value.includes("@gmail.com")
    : "" ? "Gmail is not allowed"
}

validate: {
    notGmail : (value) => !value.includes("@gmail.com") || "Gmail is not allowed"
}
```

### error 메시지 UI 띄우기

```JSX
{errors.[값 이름]?.message}
```

### useForm mode

종류

- all
- onBlur : input 바깥쪽을 클릭했을 때 일어남
- onChange : input이 변화할 때 일어남
- onSubmit : Submit 버튼을 누를 때 validation이 일어남
- onTouched

```JSX
const { handleSubmit } = useForm({
    mode:"[모드종류]"
});
```
