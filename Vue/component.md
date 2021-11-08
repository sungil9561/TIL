# Component

> Vue의 컴포넌트 개념, 컴포넌트 간 통신, 상-하위 컴포넌트 간 데이터 전달 방법



## Component 개념

### Component

![component](img/component.png)

- Vue의 가장 강력한 기능 중 하나
- Html 코드를 재사용할 수 있도록 캡슐화
- Life cycle hook 사용 가능
- 전역 컴포넌트, 지역 컴포넌트
- 'template'를 이용



### 컴포넌트 스타일 가이드

https://v3.ko.vuejs.org/style-guide/

- 컴포넌트 이름에 합성어 사용 (ex. `<todo>` 대신에 `<todo-list>`)
- 컴포넌트의 data는 반드시 함수



### 전역 컴포넌트 등록

```vue
Vue.component(<tagname>, <options>)
```

##### 이름 표기법

- kebab-case
- PascalCase
- DOM에서는 케밥 케이스만 쓸 수 있고, 파스칼 표기가 DOM객체와 연결될 때는 Vue가 파스칼 케이스를 케밥 케이스로 바꿔준다



### 로컬 컴포넌트 등록

```vue
components: {
	MyComponent1: {...}
}
```



## Component 간 통신

![img](img/Screenshot_25-16363857367742.png)

- 상위(부모) - 하위(자식) 컴포넌트 간의 data 전달 방법
- 부모에서 자식으로 : props라는 특별한 속성을 전달
- 자식에서 부모로 : event로만 전달 가능 ($emit)



### 상위에서 하위 컴포넌트로 data 전달

- 하위 컴포넌트는 상위 컴포넌트 데이터에 직접 접근할 수 없다.

- props 속성을 이용한다

  ```vue
  <div id="app">
      <child-component region="seoul" msg="안녕하세요"></child-component>
  </div>
  <script>
  Vue.component('ChildComponent', {
    props: {
      'region': String,
      'msg': {
        type: String, require: true,
      }
    },
    template: `
      <span>{{ msg }}, {{ region }}</span>
    `
  });
  new Vue({
      el: '#app',
  });
  ...
  </script>
  ```

  - v-bind 속성을 이용해 상위 컴포넌트의 data의 key에 접근할 수도 있다

    ```vue
    <div>
      <input v-model="parentMsg">
      <child-component :my-message="parentMsg"></child-component>
    </div>
    ```



### 상위에서 하위 컴포넌트로 object 전달



### 사용자 정의 이벤트

```vue
// 이벤트 발생
vm.$emit("<eventname>", [...parameter])
// 이벤트 수신
vm.$on("<eventname>", callback(){...});
```

- 이벤트의 경우에는 자동 대소문자 변환을 제공하지 않아 되도록 kebab-case를 쓰는것이 좋다



### 하위에서 상위 컴포넌트로 event 전달



### 비 상하위간 통신 