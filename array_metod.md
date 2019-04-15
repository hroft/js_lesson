#  Массив перебирающие методы:
Понедельник, 15. апреля 2019 12:25 
##Оглавление:
[forEach](#forEarch)
[map](#map)
[filter](#filter)
[every и some](#every_some)
[reduce и reduceRight](#reduce_reduceRight)

<a name="forEarch"></a>
###  **forEarch**

```javascript
 var array = [1,2,3,4,5,6,7,8,9,10];
var newArray = [];
newArray = array.forEach(function(elem){
    return elem *= elem;
});
```
 Не возращает значение! Return вернет **undifine**
```javascript
array.forEach(function(elem){
    newArray.push(elem *= elem);
});
console.log(newArray);
```
 А так вернет массив каждый элемент которого возведен в квадрат

***[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]***

Просчитаем для примера ссумму элементов массива array
```javascript
var array = [1,2,3,4,5,6,7,8,9,10];
var newArray = [];
var counter = 0;

array.forEach(function(elem){
    counter += elem; 
});
console.log(counter);
```
 ответ составит ***55***

**forEarch** удобно применять при обработке данных из ***json***
<a name="json"></a>
```javascript
var resnonse = [
    {
        "index":0,
        "isActive": true,
        "age":20,
        "name":"Ivan Ivanov",
        "gender":"male",
        "email": "ivanov@mail.ru"
    },
    {
        "index":1,
        "isActive": true,
        "age":20,
        "name":"Irina Sidorova",
        "gender":"female",
        "email": "sidorova@mail.ru"
    },
    {
        "index":0,
        "isActive": true,
        "age":36,
        "name":"Petr Petrov",
        "gender":"male",
        "email": "petrov@mail.ru"
    }
];
```
перенесем calback function из forEarch и присвоим переменной

```javascript
var getNames = function(elem){
    newArray.push(elem.name);
};

response.forEach(getNames);
console.log(newArray);
```
 Результат - массив с именами 
***["Ivan Ivanov", "Irina Sidorova", "Petr Petrov"]***
<a name="map"></a>
## map
map может возвращать результат своей работы:
```javascritpt
var array = [1,2,3,4,5,6,7,8,9,10];
var newArray = [];

newArray = array.map(function(elem){
    return elem *=elem;
});
console.log(newArray);
```
результатом работы будет ***[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]***
сделаем то же самое переписывая мсходный массив:
```javascript
array.map(function(elem){
    elem *= elem;
});
console.log(array);
```
результат ***[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]***
Допустим нам в пришедшем [JSON](#json) файле нужны не все данные а только name и age.
```javascript
array = response.map(function(elem){
    return {
        name: elem.name,
        age: elem.age
    };
});
console.log(array);
```
результат работы : 
0: {name: "Ivan Ivanov", age: 20}
1: {name: "Irina Sidorova", age: 20}
2: {name: "Petr Petrov", age: 36}
<a name="filter"></a>
## Filter
Производит фильтрацию массива по заднным параметрам
Выведем не четные элементы массива:
```javascript
var array = [1,2,3,4,5,6,7,8,9,10];

array = array.filter(function(elem){
    return elem %2;
});
console.log(array);
```
результат работы: ***[1, 3, 5, 7, 9]***
Для вывода четных элементов массива:
```javascript
var array = [1,2,3,4,5,6,7,8,9,10];

array = array.filter(function(elem){
    return elem %3 && elem !==1;
});
console.log(array);
```
результат работы: ***[2, 4, 5, 7, 8, 10]***
Например мы хотим получить из  [JSON](#json) файла только тех пользователей, у которых возраст меньше 30 лет:
```javascritpt
array = response.filter(function(elem){
    return elem.age < 30;
});
console.log(array);
```
результат работы: 
0: {index: 0, isActive: true, age: 20, name: "Ivan Ivanov", gender: "male", …}
1: {index: 1, isActive: true, age: 20, name: "Irina Sidorova", gender: "female", …}
<a name="every_some"></a>
##every и some
Данные методы используют для проверки (валидации) элементов масства
***every*** вернет true усли все элементы массива удовлетворяют условию.
***some*** вернет true если хотя бы один элемент удовлетворяет условию.
Например, мы хотим узнать все ли элементы массива положительные
```javascript
var array = [1,2,3,4,5,6,7,8,9,10,-1,-2,-3]; 

array = array.every(function(elem){
    return elem > 0;
});
console.log(array);
```
вернет false
```javascript
var array = [1,2,3,4,5,6,7,8,9,10,-1,-2,-3]; 

array = array.some(function(elem){
    return elem > 0;
});
console.log(array);
```
вернет true
Проверим есть ли у всех в  [JSON](#json) файле email:

```javascript
 array = response.every(function(elem){
    return elem.email;
});
console.log(array);
```
ответ true

<a name="reduce_reduceRight"></a>

##reduce и reduceRight
Используются для вычисления единственного значения из массива (свертка массива).Применяют callback function к каждому элементу массива сохраняя промежуточный результат. Так же функции можно передать начальное значение. Отличаются направлением обработки данных.

```javascript
var array = [1,2,3,4,5,6,7,8,9,10,-1,-2,-3];
var flattened = [[0,1],[2,3],[4,5]];

array = array.reduce(function(sum, elem){
    return sum +=elem;
});
console.log(array);
```
В sum будут прибаляться значения элементов массива. В итоге получим сумму элементов ***49*** 
Так же можно указать значение инициализации. Если его нет, то оно будет равно значению первого элемента массива.
```javascritpt
var array = [1,2,3,4,5,6,7,8,9,10,-1,-2,-3];
var flattened = [[0,1],[2,3],[4,5]];

array = array.reduce(function(sum, elem){
    return sum +=elem;
},10);
console.log(array);
```
В примере выше значение инициализации равно 10. Соответственно результат будет  ***59***
Приобразуем двумерный массив ***flattened*** в одномерный массив. Примаеним функцию ***concat***.
```javascript
var flattened = [[0,1],[2,3],[4,5]];

array = flattened.reduce(function(sum, elem){
    return sum.concat(elem);
});
console.log(array);
```
Получим массив ***[0, 1, 2, 3, 4, 5]***
Еще один пример:
Мы получили новый JSON файл - список друзей и книг которые у них есть. В данном примере неоходимо передать значение инициализации(["1984"]) - название первой книги в списке. Иначе произойдет ошибка, так как reduce получит не первый элемент массива а объект.
```javascript
var friends = [
    {name: "Anna",books:["Bible, Harry Potter"]},
    {name:"Bob",books:["War and peace","Romeo and Juliet"]},
    {name:"Alice",books:["The Lord of the Rings","The Shining"]}
];
array = friends.reduce(function(sum, elem){
    return sum.concat(elem.books);
},["1984"]);
console.log(array);
```
Результат ***["1984", "Bible, Harry Potter", "War and peace", "Romeo and Juliet", "The Lord of the Rings", "The Shining"]***
При использовании вместо reduce - reduceRight 
```javascript
var friends = [
    {name: "Anna",books:["Bible, Harry Potter"]},
    {name:"Bob",books:["War and peace","Romeo and Juliet"]},
    {name:"Alice",books:["The Lord of the Rings","The Shining"]}
];
array = friends.reduceRight(function(sum, elem){
    /* spread ES6 8 */
    return [...sum, ...elem.books];
},["1984"]);
console.log(array);
```
Результат будет следующим :***["1984", "The Lord of the Rings", "The Shining", "War and peace", "Romeo and Juliet", "Bible, Harry Potter"]***
