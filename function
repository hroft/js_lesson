#Функции:
## псевдомассив arguments
В js может быть только одна функция с определенным именем с неограниченным числом аргументов. Неиспользованные аргументы будут находится в псевдомассиве **arguments**
Например: имеется функция без входных параметров. При вызове передадим туда некие параметры и просмотрим внутри функции псевдомассив **arguments**
```javascript
function setAlphabet(){
    console.log(arguments);
}
setAlphabet('a','b','c','d','e');
```
В консоле будет **["a", "b", "c", "d", "e"]**
**arguments** является объектом хотя у него и имеется свойство light
```javascript
function setAlphabet(){
    console.log(arguments.length);
    console.log(typeof(arguments));
}
setAlphabet('a','b','c','d','e');
```
Результат **5 object**
Напишем функцию которая будет принимать на вход неограниченное количество аргументов и на выходе отдавать строку из котактенированных аргументов. Для етого преобразуем псевдомассив **arguments** в массив.
```javascript

function setAlphabet(){
    var arr =[];
    for(var i = 0; i< arguments.length; i++){
        arr[i] = arguments[i];
    }
    console.log(arr);
}
setAlphabet('a','b','c','d','e');
```
Результат** ["a", "b", "c", "d", "e"]**
Передадим первым параметром разделитель(separator)
```javascript
function setAlphabet(separator){
    var arr =[];
    for(var i = 1; i< arguments.length; i++){
        arr[i-1] = arguments[i];
    }
    return arr.join(separator);
}
console.log(setAlphabet(',','a','b','c','d','e'));
console.log(setAlphabet('-','a','b','c','d','e'));
console.log(setAlphabet('+','a','b','c','d','e'));
```
Результат: 
a,b,c,d,e
 a-b-c-d-e
a+b+c+d+e
Или спользуя **spread ES6**
```javascript
function setAlphabet(separator){
    var arr =[...arguments];
    return arr.join(separator);
}
console.log(setAlphabet(',','a','b','c','d','e'));
console.log(setAlphabet('-','a','b','c','d','e'));
console.log(setAlphabet('+','a','b','c','d','e'));
```