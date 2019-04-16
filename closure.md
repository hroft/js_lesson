#Функции
###Замыкания, области видимости, ликсическое окружение
Замыкание - это функция со всеми переменными которые ей достпны. Механиз работы функций:

Все переменные внутри функции свойства внутреннего объекта** LexicalEnvironment ** котсоздается при её запуске. Этот объект внутренний и скрыт от прямого доступа. Создается при запуске и записывает в себя аргументы, функции и переменные.
```javascript
function sayHi(name){
 // LexicalEnvironment = {name: 'Jack, phrase = 'undefined'}
    var phrase = 'Hello, '+name;
 // LexicalEnvironment = {name: 'Jack, phrase = 'Hello, Jack'}
    console.log(phrase);
}
sayHi('Jack');
```
После вполнения функции объект с переменными обычно уничтожается **"сборщиком мусора"**
Из функции мы можем обратиться не только к локальной переменной но и к внешеней:
```javascript
var userName = 'Jack';
function sayHi(){
    console.log(userName);
}
sayHi();
```
В консоли будет **Jack**
Интерпретатор, при доступе к переменной, сначала пытается найти переменную в текущем **LexicalEnvironment**, а затем, если её нет – ищет во внешнем объекте переменных. В данном случае им является **window**.
**При создании функция получает скрытое свойство [[Scope]], которое ссылается на лексическое окружение, в котором она была создана.**
Если обобщить:
- Каждая функция при создании получает ссылку [[Scope]] на объект с переменными, в контексте которого была создана.
- При запуске функции создаётся новый объект с переменными LexicalEnvironment. Он получает ссылку на внешний объект переменных из [[Scope]].
- При поиске переменных он осуществляется сначала в текущем объекте переменных, а потом – по этой ссылке.
```javascript
function makeCounter(){
    var currentCounter = 1;
    return function(){
        return currentCounter++;
    }
}
var counter = makeCounter();
console.log(counter());
console.log(counter());
console.log(counter());
console.log(counter());
console.log('=========================')
var m3 = makeCounter();
console.log(m3());
console.log(m3());
console.log(m3());
console.log(m3());
```
Счетчики не зависят друг от друга.
Практический пример с **замыканием**

```html
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
    <button></button>
```
```javascript
var buttons = document.querySelectorAll('button');
for(var i=0; i<buttons.length; i++){
    buttons[i].innerHTML = i;
    buttons[i].onclick = function(x){
        return function(){
    	console.log(x);
        }
    }(i)
}
```
Создается 10 объектов **LexicalEnvironment** 

```javascript

 function(x){
        return function(){
    	console.log(x);
        }
    }(i);
```
**На момент вызова x=i **