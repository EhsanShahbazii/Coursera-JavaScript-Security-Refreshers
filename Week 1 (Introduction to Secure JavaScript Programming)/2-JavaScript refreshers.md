## 2-JavaScript refreshers
قراره که یه مروری در مورد جاوااسکریپت داشته باشیم. یه مثال در مورد اینکه میتونیم مقدار یه متغیر رو نزاریم تغییر کنه یا نه.
```js
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
