#Функции: 
##Типы функций Function expression, Function declaration & Name Function Expression
Функции решают проблему дублирования кода. Рассмотрим различные виды функций:
###function declaration
создается на этапе транслирования и её вызов доступен до объявления:
```javascript
// function declaration
console.log(sum(1,4));
function sum(a, b){
    return a+b;
}
```
Результат **5**
###function expression
```javascript
// function expression
//console.log(sum1(2,4));
var sum1 = function(a, b){
    return a+ b;
}
console.log(sum1(2,4));
```
Вызов функции до её объявления вызовит ошибку!!!
Вызывать такой тип функций можно только после её объявления!
###named funstion expression
Данный тип функций нужен для вызова функции из её тела.
```javascript
//named function expression
var fuc = function sum(a, b){
    return a+ b;
}
console.log(fuc(5,5));
```
Пример использования такой функции - рекурсия(вычисление факториала):
```javascript
//factorial
function f(n){
    return n ? n*f(n-1) : 1; //тернарный оператор
}
console.log(f(5));
```
Ответ будет **120**
Функция в JS является объектом и доступна по ссылке.
```javascript
//factorial
function f(n){
    return n ? n*f(n-1) : 1; //тернарный оператор
}
var g=f;
console.log(g(5));
```
Ответ будет **120**
Но если уничтожить f - то будет ошибка:
```javascript
......
var g = f;
f = null;
console.log(g(5));
```
Чтобы этого не происходило - перепишем нашу функцию:
```javascript
//factorial
var f = function factorial(n){
    return n ? n*factorial(n-1) : 1; //тернарный оператор
}
var g=f;
f= null;
console.log(g(5));
```
Ответ будет **120**