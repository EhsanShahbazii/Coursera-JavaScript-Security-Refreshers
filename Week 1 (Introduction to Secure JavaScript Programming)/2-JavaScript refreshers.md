## 2-JavaScript refreshers

### قسمت اول
قراره که یه مروری در مورد جاوااسکریپت داشته باشیم. یه مثال در مورد اینکه میتونیم مقدار یه متغیر رو نزاریم تغییر کنه یا نه.
```js
const x = {};

Object.defineProperty(x, 'foo', {
  value: 10,
  writable: false
});

console.log(x.foo); // 10
x.foo = 11;
console.log(x.foo); // 10
```
می بینیم که تغییر نکرد، در حالیکه با منطق خیلی کار درستی نیست. اینجاست که تو جاوااسکریپت `use strict` هست که سخت می گیره و این نوع موارد رو ارور نشون میده.
```console
Type error: cannot assign to read only property 'foo' of object '#<Object>'
```

### قسمت دوم
حالا به متغیر ها و تعریف اونها توجه می کنیم. مثلا اگه به `var` دقت کنیم می بینیم که:
```js
x = 10;
var x;
console.log(x); // 10
```
متغیر رو قبل از اینکه تعریف کنیم مقدار دادیم بهش و کار کرد. اگه `use strict` اضافه کنیم داریم:
```js
'use strict';
x = 10;
var x;
console.log(x); // 10
```
باز هم بدون مشکل کار می کنه. این به خاطر اینه که `var` در اول کار به بالاترین سطح کد ها میره و انگار یک متغیر گلوبال هست.

برای اینکه از ارور ها و باگ های پیشگیری کنیم از `let` و `const` استفاده می کنیم.

### قسمت سوم
روش های مختلفی برای تعریف تابع وجود داره که به صورت زیر هستن:
```js
function f1( ) { }

const x = function f2( ) { }

const arrow1 = (e) =>  e++ ;
const arrow2 = (e) => {
  return e++;
}

const newFunction = new Function('a', 'b', 'return a + b');
```
و اگه این مدل آخری `newFunction` رو با متد `( )toString` فراخوانی کنیم به صورت یک رشته تمام کد تابع به دست می آید.

### قسمت چهارم
اینجا هم قراره تایپ های دیتا های جاوااسکریپت رو مرور کنیم.
```js
console.log(typeof {}); // object
console.log(typeof []); // object
console.log(typeof ''); // string
console.log(typeof 10); // number
console.log(typeof null); // object
console.log(typeof undefined); // undefined
```

### قسمت پنجم
و در آخر قراره که مساوی و برابری دیتا هارو به دست بیاریم. توی جاوااسکریپت ما دو نوع برابری داریم: `==` و `===` که به صورت زیر است:
```js
console.log(1 == '1'); // true
console.log(1 === '1'); // false
```
دلیل اینکه `==` برابر شد و دیگری نه اینه که `==` فقط برابری مقادیر رو در نظر می گیره و به نوع داده اهمیتی نمیده. ولی `===` نوع داده و رفرنس اون رو هم در نظر می گیره.

حالا قراره مقادیر هایی که تو زبان جاوااسکریپت `false` هستند رو ببینیم:
```js
console.log(!!false); // false
console.log(!!0); // false
console.log(!!''); // false
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!!NaN); // false
```

