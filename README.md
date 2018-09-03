# Javascript ES5 Essentials
## Promises
  - **promise** : 자바 스크립트 비동기(특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행함) 처리에 사용되는 객체. 비동기적 특성으로 인해, 데이터를 받아오기도 전에 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜨는 상황 발생할 수 있음. 이를 방지하기 위한 방법이 promise.
            : promise가 fulfilled / rejected 여부에 따라 부가적인 method를 연결할 수 있다. 
  - **promise 타입**
    1. Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
    2. Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
    3. Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태
  - **promise method**
    1. **Promise.all(iterable)**
       : iterable 내의 모든 프로미스가 이행한 뒤 이행하고, 어떤 프로미스가 거부하면 즉시 거부하는 프로미스를 반환합니다. 반환된 프로미스가 이행하는 경우 iterable 내의 프로미스가 결정한 값을 모은 배열이 이행 값입니다. 반환된 프로미스가 거부하는 경우 iterable 내의 거부한 프로미스의 이유를 그대로 사용합니다. 이 메서드는 여러 프로미스의 결과를 모을 때 유용합니다.

    2. **Promise.race(iterable)**
        : iterable 내의 어떤 프로미스가 이행하거나 거부하는 즉시 스스로 이행하거나 거부하는 프로미스를 반환합니다. 이행 값이나 거부 이유는 원 프로미스의 값이나 이유를 그대로 사용합니다.

    3. **Promise.reject(reason)**
        : 주어진 이유로 거부하는 Promise 객체를 반환합니다.
    4. **Promise.resolve(value)**
        : 주어진 값으로 이행하는 Promise 객체를 반환합니다. 값이 then 가능한 (즉, then 메서드가 있는) 경우, 반환된 프로미스는 then 메서드를 따라가고 마지막 상태를 취합니다. 그렇지 않은 경우 반환된 프로미스는 주어진 값으로 이행합니다. 어떤 값이 프로미스인지 아닌지 알 수 없는 경우, Promise.resolve(value) 후 반환값을 프로미스로 처리할 수 있습니다.
  - **예제 코드**
    ```
    //fetch()는 promise 객체를 반환함
    fetch('https://api-to-call.com/endpoint').then(response=>{
      if (response.ok){
        return response.json();
      }
      throw new Error('Request failed!');
    }, networkError=>{
      console.log(networkError.message);
    }).then(jsonResponse=>jsonResponse)
    ```
    
    
![프로미스 프로세스](https://joshua1988.github.io/images/posts/web/javascript/promise.svg)

## Const / Let
  - 자바스크립트에는 세가지 형태의 변수가 있다; **const, let, var**
  - **const** (block scoped)
    - 변수 재선언 불가능
    - immutable
    - 참조형(Complex type: array, object, function)의 경우 const가 보다 적합하다다. (참조형은 const로 선언하더라도 멤버값을 조작하는 것이 가능)
  - **let** (block scoped)
    - 변수 재선언 불가능
    - mutable
  - **var** (function scoped)
    - 변수 재선언 가능
      ```
      // 이미 만들어진 변수이름으로 재선언해도 문제가 없음. 
      var a = 'hi'
      var a = 'hello'

      // hoisting으로 인해 ReferenceError에러가 없음. 
      c = 'no error'
      var c
      ```
## Arrow Functions
  - 화살표 함수는 항상 익명. 
  - 예제코드
    ```
      var materials = [
      'Hydrogen',
      'Helium',
      'Lithium',
      'Beryllium'
    ];

    console.log(materials.map(material => material.length));
    // expected output: Array [8, 6, 7, 9]

    ```

## Array Methods (map, reduce, filter, slice, splice)
## Spread Operator (Array/Object Spread)
## Export / import
