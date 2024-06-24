# 27장. 배열 (indexOf, pop, concat, includes, every)

## 📌 Array.prototype.indexOf

- 원본 배열에서 인수로 전달된 **요소를 검색하여 인덱스를 반환**
    - 중복 요소 존재 → 첫 번째로 검색된 요소 반환
    - 존재 X → -1 반환
- 배열에 **특정 요소 존재**하는지 확인할 때 유용함
- indexOf 대신 ES7에 도입된 **includes** 메서드를 사용하는 것이 가독성이 더 좋음
    
    ```jsx
    const arr = [1, 2, 2, 3]
    
    // 요소 2를 검색하여 첫 번째로 검색된 요소의 인덱스 반환
    arr.indexOf(2); // 1
    
    // 두 번째 인수는 검색을 시작할 인덱스
    arr.indexOf(2, 2); // 2
    ```
    

## 📌 Array.prototype.pop

- 원본 배열에서 **마지막 요소를 제거하고 제거한 요소를 반환**함
- 빈 배열이면 **undefined** 반환
- pop, push 메서드를 사용하면 스택 구현 가능
    
    ```jsx
    const arr = [1, 2];
    
    // 원본 배열에서 마지막 요소 제거 후 반환
    let result = arr.pop();
    console.log(result); // 2
    
    // pop 메서드는 원본 배열 직접 변경
    console.log(arr); // [1] 
    ```
    

## 📌 Array.prototype.concat

- 인수로 전달된 값들을 원본 배열의 **마지막 요소로 추가한 새로운 배열을 반환**
- 전달 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가
    - 원본 배열은 변경 X
- push와 unshift 메서드 → concat 메서드로 대체 가능
    
    ```jsx
    const arr1 = [1, 2];
    const arr2 = [3, 4];
    
    let result = arr1.concat(arr2);
    console.log(result); // [1, 2, 3, 4]
    
    result = arr1.concat(arr2, 5);
    console.log(result); // [1, 2, 3, 4, 5]
    ```
    

## 📌 Array.prototype.includes

- 배열 내에 **특정 요소가 포함되어 있는지** 확인하여 true 또는 false를 반환
- 첫 번째 인수로 검색할 대상 지정
    
    ```jsx
    const arr = [1, 2, 4];
    
    // 배열에 요소 2가 포함되어 있는지 확인
    arr.includes(2); // true
    ```
    
- 두 번째 인수는 검색을 시작할 인덱스 위치
    - 두 번째 인수를 생략할 경우는 기본값 0
    - 음수 사용 가능
    
    ```jsx
    const arr = [1, 4, 3];
    
    // 배열 요소 1이 포함되어 있는지 인덱스 1부터 확인
    arr.includes(1, 1); // false
    ```
    

## 📌 Array.prototype.every

- 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수 호출
- 콜백 함수의 반환값이 모두 참이면 **true**, 아니면 **false**
    
    ```jsx
    // 배열의 모든 요소가 3보다 큰지 확인
    [5, 10, 13].every(item => item > 3); // true
    
    // 배열의 모든 요소가 10보다 큰지 확인
    [5, 10, 13].every(item => item > 10); // false
    ```
