## 4-Node.js refreshers
### قسمت اول:
 نود جی اس محیطیه که میتونیم توش کد های جاوا اسکریپت رو مستقل از بستر وب اجرا کنیم. نود جی اس امکانات زیادی فراهم کرده که مثلا میتونیم به فایل های سیستم دسترسی داشته باشیم. مثلا نمونه کد های زیر رو نگاه کنید:
```node
const fs = require("fs");

fs.readFile(__filename, (err, data) => {
  if (err)
    console.error(err);
  else
    console.log(data.toString());
}
```
### قسمت دوم:
نود جی اس تک ترید(Thread) هست برای همین توی یک لحظه فقط یک کار را می تواند انجام دهد. مثلا به مثال زیر دقت کنید:
```node
fs.readFile(__filename, (err, data) => {
  console.log("file done!");
}

fs.readdir(__dirname, (err, data) => {
  console.log("dir done!");
}
```
اگر برنامه رو اجرا کنیم توی کنسول میبینیم که:
```console
dir done!
file done!
```
اگه در کنار کد هایی که نوشتیم یه لوپ بزرگ هم بنویسیم خواهیم دید که اول لوپ اجرا میشه بعد از اتمام اون بقیه کد ها اجرا میشه.

### قسمت سوم:
ما ماژول های اصلی دیگه ای هم داریم که مثلا میتونیم به صورت زیر بنویسیم:
```node
const http = require("http");

http.createServer((req, res) => {
  res.end("ok");
})
  .listen(8080);
  
process.nextTick(() => {
  http.get("http://localhost:8080", (res) => {
    res.on(data, (dt) => {
      console.log(dt.toString());
    });
  }); 
});
```
