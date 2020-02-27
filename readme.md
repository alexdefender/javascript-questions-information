## Вопросы и интересная информация по JavaScript

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
