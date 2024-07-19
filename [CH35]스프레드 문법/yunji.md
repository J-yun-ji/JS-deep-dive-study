# 35장. 스프레드 문법

### 📍 스프레드 문법 사용 대상

- Array
- String
- Map
- Set
- DOM 컬렉션
- arguments와 같이 for … of 문으로 순회할 수 있는 이터러블에 한정됨
    
    ```jsx
    console.log(...[1, 2, 3]); // 1 2 3
    console.log(...'Hello'); // H e l l o
    ****console.log(...new Map([['a', '1']], ['b', '2']])); // ['a', '1'], ['b', '2']
    ****console.log(...{ a: 1, b: 2 }); // 일반 객체이므로 TypeError
    ```
    
- 스프에드 문법의 결과는 값이 아닌 **값들의 목록**
    - 즉, 값을 생성하는 연산자가 아니므로 변수에 할당할 수 없음
- 쉼표로 구분한 값의 목록을 사용하는 문맥에서만 사용 가능
    - 함수 호출문이 인수 목록
    - 배열 리터럴의 요소 목록
    - 객체 리터럴의 프로퍼티 목록

## 📌 함수 호출문의 인수 목록에서 사용하는 경우

- Math.max 메서드 예제
    
    ```jsx
    const arr = [1, 2, 3];
    
    // 배열을 인수로 전달
    const max = Math.max(arr); // NaN
    
    // 스프레드 문법 제공 이전 -> Function.prototype.apply
    const max = Math.max.apply(null, arr); // 3
    
    // 스프레드 문법
    const max = Math.max(...arr); // 3
    ```
    
- Rest 파라미터와 형태가 동일하므로 혼동할 수 있음
    - Rest 파라미터
        
        → 함수에 전달된 인수들의 목록을 배열로 전달받기 위해 매개변수 이름 앞에 …을 붙이는 것
        
    - 스프레드 문법
        
        → 여러 개의 값이 하나로 뭉쳐 있는 배열과 같은 이터러블을 펼쳐서 개별적인 값들의 목록을 만드는 것
        
    - 즉, 서로 상반된 개념

## 📌 배열 리터럴 내부에서 사용하는 경우

- 스프레드 문법을 **배열 리터럴**에서 사용하면 ES5에서 사용하던 기존 방식보다 더욱 간결하고 가독성 좋게 표현 가능
    
    ### 📍 concat
    
    - 2개의 배열을 1개의 배열로 결합하고 싶은 경우 사용
        
        ```jsx
        // ES5 -> concat
        var arr = [1, 2].concat([3, 4]);
        console.log(arr); // [1, 2, 3, 4]
        
        // ES6 -> spread
        
        const arr = [...[1, 2], ...[3, 4]];
        console.log(arr); // [1, 2, 3, 4]
        ```
        
    
    ### 📍 splice
    
    - 어떤 배열의 중간에 다른 배열의 요소들을 추가하거나 제거할 때 사용
        - 세 번째 인수로 배열 전달 시 배열 자체 추가됨
        
        ```jsx
        // ES5
        var arr1 = [1, 4];
        var arr2 = [2, 3];
        
        arr1.splice(1, 0, arr2);
        console.log(arr1); // [1, [2, 3], 4] 원하는 결과 = [1, 2, 3, 4]
        
        // apply() 사용
        Array.prototype.splice.apply(arr1, [1, 0].concat(arr2));
        console.log(arr1); // [1, 2, 3, 4]
        
        // ES6
        arr1.splice(1, 0, ...arr2); 
        console.log(arr1); // [1, 2, 3, 4]
        ```
        
    
    ### 📍 배열 복사
    
    - ES5에서 배열 복사 ⇒ slice 메서드 사용
        
        ```jsx
        // ES5
        
        var origin = [1, 2];
        var copy = origin.slice();
        
        console.log(copy); // [1, 2]
        console.log(copy === origin); // false
        
        // ES6 
        const origin = [1, 2];
        const copy = [...origin];
        
        console.log(copy); // [1, 2]
        console.log(copy === origin); // false
        ```
        
    - 얕은 복사하여 새로운 복사본 생성

## 📌 객체 리터럴 내부에서 사용하는 경우

- Rest 프로퍼티와 스프레드 프로퍼티를 사용하면 객체 리터럴의 프로퍼티 목록에서도 스프레드 문법 사용 가능
    - 일반 객체도 허용
    
    ```jsx
    // 스프레드 프로퍼티
    // 객체 복사(얕은 복사)
    const obj = { x: 1, y: 2 };
    const copy = { ...obj };
    
    console.log(copy); // { x: 1, y: 2 }
    console.log(copy === origin); // false
    
    // 객체 병합 -> ES5 (중복되면 뒤에 위치한 프로퍼티가 우선권 가짐)
    const merged = Object.assign({}, { x: 1, y: 2 }, { y: 10, z: 3 }};
    console.log(merged); // { x: 1, y: 10, z: 3 }
    
    // 객체 병합 -> ES6
    const merged = { x: 1, y: 2, ...{ a: 3, b: 4 } };
    console.log(merged); // { x: 1, y: 2, a: 3, b: 4 }
    ```
