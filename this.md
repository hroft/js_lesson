#Контекст вызова
##this
Не привязывается статически к объекту. Зависит только от контекста вызова.
Создадим объекты user, user2 и метод объекта sayHi:
```javascript
var user = { name: 'Max'};
var user2 = { name: 'Bob'};

 user.sayHi = function(){
     console.log('Hello!'+this.name);
 };
 user.sayHi();
```
Результат **Hello! Max**
Контекстом для **this** будет объект **user**. То есть **this.name** равносильно **user.name**
Если вызвать:
```javascript
var user = { name: 'Max'};
var user2 = { name: 'Bob'};

 user2.sayHi = function(){
     console.log('Hello!'+this.name);
 };
 user2.sayHi();
```
Результат **Hello! Bob**
Контекстом для **this** будет объект **user2**. То есть **this.name** равносильно **user2.name**

Если произошла ошибка и **this** не получила контекст, то контекстом будет объект **Window**. В режиме **'use strict'** **this** будет равна **undefined**.

На практике **this** используют что бы узнать элемент который вызвал обработчик
```html
<button>Button</button>
```
```javascritpt
var btn = document.querySelector('button');
btn.onclick = function(){
    console.log(this);
}
```
При нажатии на кнопку в консоли будет: 
```html
<button>Button</button>
```
