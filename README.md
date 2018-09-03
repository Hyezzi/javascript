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
  - 화살표 함수는 항상 익명 함수 
  - 매개변수가 하나뿐인 경우 괄호는 선택사항
  - 매개변수가 없는 함수는 괄호가 필요
  - 예제 코드 1
       ```
      (param1, param2, …, paramN) => { statements }
      (param1, param2, …, paramN) => expression
      // 다음과 동일함:  => { return expression; }

      // 매개변수가 하나뿐인 경우 괄호는 선택사항:
      (singleParam) => { statements }
      singleParam => { statements }

      // 매개변수가 없는 함수는 괄호가 필요:
      () => { statements }
      ```
  - 예제코드 2
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
1. **기본 메소드**
  - Array.from() : 유사 배열 또는 반복 가능한 객체로부터 새로운 배열 인스턴스를 생성합니다.
  - Array.isArray() : 만약 변수가 배열이면 true를 아니면 false를 반환합니다.
  - Array.observe() : 객체의 Object.observe()와 유사하게 배열에 대한 변경점을 비동기로 관찰합니다. 이것은 발생한 순서대로 변경 스트림을 제공합니다.
  - Array.of() : 전달인자의 개수나 데이터 타입에 관계없이 새 배열 인스턴스를 생성합니다.
  
2. **변경자 메서드** : 변경자 메서드는 배열 수정.
  - Array.prototype.copyWithin() : 배열 내의 지정된 요소들을 동일한 배열 내에서 복사합니다.
  - Array.prototype.fill() : 배열 안의 시작 인덱스부터 끝 인덱스까지의 요소값을 지정된 정적 값으로 채웁니다.
  - Array.prototype.pop() : 배열에서 마지막 요소를 뽑아내고, 그 요소를 반환합니다.
  - Array.prototype.push() : 배열의 끝에 하나 이상의 요소를 추가하고, 변경된 배열의 길이를 반환합니다.
  - Array.prototype.reverse() : 배열의 요소 순서를 반전시킵니다. - 첫 번째가 마지막이 되고 마지막이 첫 번째가 됩니다.
  - Array.prototype.shift() : 배열에서 첫 번째 요소를 삭제하고 그 요소를 반환합니다.
  - Array.prototype.sort() : 배열의 요소를 정렬하고 그 배열을 반환합니다.
  - Array.prototype.splice() : 배열에서 요소를 추가/삭제합니다.
  - Array.prototype.unshift() : 배열의 앞에 하나 이상의 요소를 추가하고 새로운 길이를 반환합니다.
3. **접근자 메서드** : 배열을 수정하지 않고 배열 일부를 반환합니다.
  - Array.prototype.concat() : 배열과, 인자로 주어진 배열/값을 결합해 새로운 배열을 만들고, 이 새 배열을 반환합니다.
  - Array.prototype.includes() : 배열에 특정 요소가 포함돼있는지 알아내어 true 또는 false를 적절히 반환합니다.
  - Array.prototype.indexOf() : 배열에서 지정한 값과 같은 요소의 첫 인덱스를 반환합니다. 없으면 -1을 반환합니다.
  - Array.prototype.join() : 배열의 모든 요소를 문자열로 변환하여 합칩니다.
  - Array.prototype.lastIndexOf() : 배열에서 지정한 값과 같은 요소의 마지막 인덱스를 반환합니다. 없으면 -1을 반환합니다.
  - Array.prototype.slice() : 배열의 일부를 추출한 새 배열을 반환합니다.
  - Array.prototype.toSource() : 지정한 배열을 나타내는 배열 리터럴을 반환합니다.새로운 배열을 만들기 위해 이 값을 사용할 수 있습니다.
  - Array.prototype.toString() : 배열과 요소를 반환하는 문자열을 반환합니다. Object.prototype.toString() 메서드를 재정의합니다.
  - Array.prototype.toLocaleString() : 배열과 요소를 나타내는 지역화된 문자열을 반환합니다. Object.prototype.toLocaleString() 메서드를 재정의합니다.
   4. **반복 메서드**
    배열을 처리하는 동안, 각각의 배열요소에 대해 (인자로 주어진) 콜백 함수를 호출하는 메서드가 몇 개 있습니다. 이러한 메서드들은 메서드의 호출시점에 배열의 길이를 확인한 후, 그 길이까지의 배열요소에 대해서만 콜백을 수행하며,  콜백 중에 추가된 배열 요소(메서드 호출시점에 확인된 길이보다 더 큰 인덱스값을 갖는 요소들)에 대해서는 콜백을 수행하지 않습니다. 만약 메서드의 실행 도중에  배열의 변경(요소의 값 설정 또는 배열요소를 삭제하는 등)이 발생하고, 이런 변경이후에 메서드가 해당 배열 요소에 대해 콜백을 호출하게 되면  작업 결과에 영향을 줄 수도 있습니다. 이러한 사례들에 있어 메서드들의 구체적인 동작은 잘 정의되어 있지만, 당신의 코드를 읽을 다른 사람들이 혼란스럽지 않게 해야 합니다. 만약 이런 메서드를 이용해 배열을 변경해야한다면, 원본 배열 대신 새로운 배열로 값을 복사하는 방식으로 처리하십시오.

    Array.prototype.entries()
    배열의 각 인덱스에 대한 키/값 쌍을 포함하는 새로운 배열 반복자 객체를 반환합니다.
    Array.prototype.every()
    만약 배열의 모든 요소가 제공된 검사 함수를 만족하면 true를 반환합니다.
    Array.prototype.filter()
    주어진 필터링 함수의 값의 결과가 참인 경우의 배열 요소들만으로 새로운 배열을 생성하여 반환합니다
    Array.prototype.find()
    주어진 테스팅 함수의 요구조건을 만족하는 배열 요소를 반환합니다. 그러한 배열요 요소가 없으면  undefined를 반환합니다.
    Array.prototype.findIndex()
    주어진 테스트 함수를 만족하는 배열의 첫 번째 요소에 대한 인덱스를 반환합니다. 그렇지 않으면 -1이 리턴됩니다.
    Array.prototype.forEach()
    배열의 각각의 요소에 함수를 호출합니다.
    Array.prototype.keys()
    배열의 각 인덱스에 대한 key들을 가지는 새로운 Array Iterator 객체를 반환합니다.
    Array.prototype.map()
    배열 내의 모든 요소 각각에 대하여  제공된 함수(callback)를 호출하고, 그 결과를 모아서  만든 새로운 배열을 반환합니다.
    Array.prototype.reduce()
    배열의 각 값에 대해 왼쪽에서 오른쪽으로 함수를 적용하여 단일 값으로 줄입니다.
    Array.prototype.reduceRight()
    배열의 각 값에 대해 오른쪽에서 왼쪽으로 함수를 적용하여 단일 값으로 줄입니다.
    Array.prototype.some()
    R배열중의 적어도 한 요소가 테스팅 함수를 만족시킨 다면 true를 반환합니다.
    Array.prototype.values()
    배열의 요소값들에 대한 Array Iterator 객체를 반환합니다.
    Array.prototype[@@iterator]()
    배열의 요소값들에 대한 Array Iterator 객체를 반환합니다.


## Spread Operator (Array/Object Spread)
## Export / import



*참고페이지 https://developer.mozilla.org/ko/*
