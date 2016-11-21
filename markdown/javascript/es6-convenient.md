# ES6 편리한 기능
 
***
 
### Object [key] setting syntax

 - 기존에는 Object literal 선언에 Variable key's value를 사용할 수 없었다. 
 
        let myKey = 'key3';
        let obj = {
            key1: 'One',
            key2: 'Two'
        };
        obj[myKey] = 'Three';
 
 - ES6는 Object literal 선언에 Variable key's value를 사용할 수 있도록 해준다.
  
        let myKey = 'variableKey';
        let obj = {
          key1: 'One',
          key2: 'Two',
          [myKey]: 'Three' /* yay! */
        };
        
.

### Arrow Functions

 - Function, return 키워드 사용없이 Arrow Function을 제공하여 simple하게 function선언할 수 있도록 해준다.

        // Adds a 10% tax to total
        let calculateTotal = total => total * 1.1;
        calculateTotal(10) // 11
        
        // Cancel an event -- another tiny task
        let brickEvent = e => e.preventDefault();
        document.querySelector('div').addEventListener('click', brickEvent);
   
.
        
### find/findIndex

 - Array에 find/findIndex function을 제공하여, 원하는 조건으로 매칭되는 첫번째 아이템을 찾을 수 있도록 해준다.
 
        let ages = [12, 19, 6, 4];
        
        let firstAdult = ages.find(age => age >= 18); // 19
        let firstAdultIndex = ages.findIndex(age => age >= 18); // 1
        
.

### The Spread Operator: ... 

 - Array 혹은 iterable object가 각각의 item으로 분리되어 전달할 수 있다.

        let numbers = [9, 4, 7, 1];
        Math.min(...numbers); // 1
        
        // Convert NodeList to Array
        let divsArray = [...document.querySelectorAll('div')];
        
        // Convert Arguments to Array
        let argsArray = [...arguments];

.

### Default Argument Values

 - Default Argument value를 설정할 수 있다.
 
         // Basic usage
         function greet(name = 'Anon') {
           console.log(`Hello ${name}!`);
         }
         greet(); // Hello Anon!

.
         
***
 
### 참조
 
  - Six Tiny But Awesome ES6 Features
  
  <https://davidwalsh.name/es6-features>

