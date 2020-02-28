## Вопросы и [информация по JavaScript](#%d0%98%d0%bd%d1%84%d0%be%d1%80%d0%bc%d0%b0%d1%86%d0%b8%d1%8f-%d0%bf%d0%be-javascript)

##### 1. Что выведет консоль?

```javascript
console.log(true | 0)
```

- a: `true`
- b: `1`
- c: `0`
- d: `false`

<details><summary><b>Результат</b></summary>

#### Ответ: b

</details>

##### 2. Что выведет консоль?

```javascript
console.log(Number(null));
console.log(Number(undefined));
console.log(Number('\n'));
console.log(Number(' 12s '));
```

- a: `null` `undefined` `0` `12` 
- b: `false` `false` `false` `true`
- c: `true` `true` `true` `false`
- d: `0` `NaN` `0` `NaN`

<details><summary><b>Результат</b></summary>

#### Ответ: d

При преобразовании строки в число, движок сначала отсекает все пробельные символы, символы `\n`, и `\t` в начале и в конце строки, и возвращает `NaN` если обрезанная строка не представляет из себя корректное число. Если строка окажется пустой, то результатом будет `0`.

`null` и `undefined` обрабатываются по разному: `null` станет `0`, в то время как `undefined` станет `NaN`.

</details>

##### 3. Что выведет консоль?

```javascript
console.log(null == 0);
console.log(undefined == NaN);
```

- a: `true` `true`
- b: `false` `false`

<details><summary><b>Результат</b></summary>

#### Ответ: b

При применении `==` к `null` или `undefined`, численное преобразование не происходит, так как `null` может равняться только `null` или `undefined`, и ничему другому.

</details>

##### 4. Что выведет консоль?

```javascript
function foo() {
  console.log( this.a );
}
var a = 2;
var o = { a: 3, foo: foo };
var p = { a: 4 };

o.foo();
(p.foo = o.foo)();
```

- a: `3` `2`
- b: `3` `4`
- c: `3` `3`

<details><summary><b>Результат</b></summary>

#### Ответ: a

Результирующим значением выражения присваивания `p.foo = o.foo` является ссылка на нижележащий объект функции. Отсюда 
следует, что фактическим местом вызова будет просто `foo()`, а не `p.foo()` или `o.foo()`, как можно было ожидать. Согласно системе правил, упомянутых ранее, применяется правило связывания по умолчанию.

</details>

##### 5. Что выведет консоль?

```javascript
'use strict'

var myObject = {
    name: 'alex',
};

Object.preventExtensions(myObject);
myObject.age = 20;

console.log(myObject.age)
```

- a: `undefined`
- b: `20`
- c: `TypeError`
- d: `ReferenceError`

<details><summary><b>Результат</b></summary>

#### Ответ: c

`Object.preventExtensions(..)` запрещает возможность добавления новых свойств в объект, оставляя остальные свойства объекта без изменений. Если не действует режим strict, попытка создания b завершается неудачей без выдачи ошибки, обращение к свойству вернет  `undefined`. В режиме `strict` выдается ошибка `TypeError`.

Еще несколько полезных функций:

* `Object.seal(..)` - делает тоже самое, что и `Object.preventExtensions(..)`, но также все существующие свойства получают пометку `configurable:false`. Таким образом, к объекту не только нельзя добавлять новые свойства, но и также нельзя изменять конфигурацию или удалять cуществующие свойства (хотя вы можете изменять их значения).
* `Object.freeze(..)` создает «замороженный» объект; функция получает существующий объект и фактически вызывает для него `Object.seal(..)`, но также все свойства доступа к данным получают пометку `writable:false`, так что их значения не могут быть изменены.

</details>

##### 6. Что выведет консоль?

```javascript
var myObject = {};

console.log('name' in Object);
console.log(myObject.hasOwnProperty('name'));
```

- a: `true` `false`
- b: `false` `false`
- c: `true` `true`
- d: `false` `true`

<details><summary><b>Результат</b></summary>

#### Ответ: a

Оператор `in` проверяет, присутствует ли заданное свойство в объекте или на одном из более высоких уровней обхода цепочки `[[Prototype]]`. `hasOwnProperty(..)` только проверяет, присутствует ли свойство в объекте `myObject` или нет и не обращается к цепочке `[[Prototype]]`.

</details>

## Информация по JavaScript

#### Объявление геттеров и сеттеров в объектах:

```javascript
var myObject = {
    get name() {
        return this._name;
    },
    set name(name) {
        this._name = name;
    }

};
myObject.name = 'bobi'
console.log(myObject.name)
```


