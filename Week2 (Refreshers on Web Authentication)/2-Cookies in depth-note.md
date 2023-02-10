## Cookies in depth

### 0:00
Hello, and welcome to secure JavaScript programming with Vladimir De Turkheim. As you know, the topic of the video today is about cookies. First of all, I want to apologize for this terrible joke. I had a cookie on my desk and I wanted to show it. Let's talk about cookies. Cookies are very important part of the web. It's the main way of authenticating your user whether by knowing the identity. You can do authorization or authentication based on cookies. You can detect the whole of your user based on the cookies. But also, this is vastly used for user tracking and monitoring who the people are out of marketing reasons. It's at the same time a very important tool in term of authentication management and security but also a very important tool in term of people tracking and privacy. They're everywhere. It's actually very fair to say that even people would have never written any single line of code in their life know about cookies, because they're like the boring banners that can come when they leave in the EU. But I don't want to spoil the end of the video right now. Cookies. Let's go with a simple definition. Right now, I've got two express JS servers. Well, a cookie is just something in a header. You've got first of all, first request header. Let me start again. You have an HTTP request and if in your response, there is a header named Set-Cookie with a value on the right-hand side, then the browser will store that. Each time it will make a new request to that web server, it will actually put that in a header named cookie. Let's start with this first example. I'm running a first server on the port 3000. When you have a request coming in it will actually set the cookie server name, server 1. Let's go there.

### 2:45
Actually this is a web page whose code is to show the cookies, but we'll say that a bit later. If I go into my Debug Console and I show of cookies, I see that there is a cookie named server name, which is exactly what we set into the back-end code. It has the value server 1. Once again, so that's what we set into the code. In terms of domain 127.0.0.1, because that's a URL I've been using, it has a path, it has an expiration, it has a size. Now you've got some diverse fields that we will see later. Now, let's do an HTTP request. We don't really care about its content. We want just to do a request on the same server, on the print endpoint. Here's a print endpoint. What it does, it accept incoming requests, but console.logs are headers of the request. What we have in the console here is the headers of the request. We can see that we have a header that has a named cookie and that has a value server name equals server 1. We don't have more JavaScript code in the web page than that. We did not write anything complex in the console when we did our fetch call. This is just the default behavior of the web browser to spread cookies it has in memory. Now, let's check how to access cookies from JavaScript. Well, that's pretty easy. You can do document.cookie, and you will get to string with the value of the cookies. Let's say that my web server has another cookie.

### 5:09
Let's restart it. Reload the page. If I do document.cookie, I see that I have two values here, which is pretty cool. But because I used for authentication, there are a few things that needs to be taken in account.

### 5:37
If you remember the videos about authentication under management, the previous one, we don't want sessions to run forever, or at least we want to have a way to limit the time of a session. To do that, they're actually primitives that you can use that are Expire or Max-Age. Let's say that I want to over me to have a Max.
Play video starting at :6:10 and follow transcript

### 6:10
Max-Age, is that the correct case? Yes, I don't think it matters a lot. Let's say we want to do that until 20th October, 2021. Let me just check something quickly. New date. Let's do something like that. It will be easier, at least if I'm not mistaken. Let's restart the server and reload and now you can see that on the other cookie, it has an expiration date. It's actually very important when you set either an expiration duration with expire or an expiration date with Max-Age. Let you know that these dates, this expiration, is not based on the server-side time, but on the client-side time. If your clients have clocks that are shifted, these will actually have an impact. Now, let's talk about the scope of a cookie. A cookie is by default available in the exact same domain and an old path. But you can, let me start the second server.
Play video starting at :7:49 and follow transcript

### 7:49
We started a second server and if we check the cookies, we see that this one is on localhost so its domain is localized. You can decide when you set a cookie if it is scoped to the whole world, if it's scoped to sub-domains only, or only to the same domain. The browser will actually know and decide when to send a cookie properly. Also, you have exactly the same thing with the path.
Play video starting at :8:31 and follow transcript

### 8:31
I told you about the scope of cookies, I told you about HTTP only I think. No, I did not. As I told you that you can access cookies in JavaScript. Let's say that you have cross-site scripting, a CSRF, mostly a cross-site scripting, and someone is able to run arbitrary JavaScript on your website. Well, you don't want them to be able to leak the cookie to a third party website. For instance, to do an HTTP request to another website with the cookie in it. To actually limit that, we've got HTTP only primitive in cookies. Lets me create another cookie here and it will be HTTP only.

### 9:29
Now, if I restart server 1, and we check what are the cookies, we see that we have the cookie HTTP only, that is HTTP only. If I do document.cookie, well, it's not there, you can't see it. The cookie HTTP equal only if is not available from the JavaScript code. However, if a do fetch slash prints, once again we don't care about the response, we can see that it has been sent back to the server. Because we prevent it to browser from giving access to this cookie in JavaScript. Let's see what are user traits. A very important one is Secure. Because I'm in [inaudible], it's complicated to setup. But you want all the cookies to be secure, meaning that they are not a load to be sent over HTTP, only HTTPS. That is to prevent someone from eavesdropping the connection and stealing cookies. In prediction, cookies must be secure. Once again, it is just a matter of adding Secure here and the browser will know what to do with it. SameSite is actually a new convention. It's not fully implemented by browser, but it's pretty powerful. It has three potential values. The first one will be Strict.
Play video starting at :11:27 and follow transcript

### 11:27
Let me start that strict, which means it's only for the same domain that can override these values here, and the cookies must never be shared with someone else. The second value will be lax, meaning laxist. You can go under sub-domain of the domain but not outside, and none. None mean, well, no same site policy at all. That's actually dangerous because your cookie will be allowed to leak. Now let's see where we can write cookies from JavaScript. You can actually do that pretty easily, by doing documented cookie equal a equals b. That will not override the cookies, it will just add one here. Let's try to override a cookie. It overrides a cookie. You can actually add cookies by just setting a value for documented cookie. I know it's not the best JavaScript API we have seen in the world, but that's how it works. Also, you can delete a cookie by doing a equal. Now, if I go and document that cookie, there you have the cookie's empty and it's somehow deleted, I guess. That's how you manipulate cookies from JavaScript. Now, let's talk about what is zombie cookie. There are a lot of ways for a user to eventually cancel cookies. One of the easiest one is to actually go there and clear cookies or clean up cookies add-ons. They might want to do that to prevent being tracked. They might have Chrome extension, or Firefox extensions that prevent cookies to be used for tracking and marketing purpose. I'm not recommending anything, but there is a hack that actually enables a developer to force cookies from the front end. That's what's called zombie cookies. Let's say it takes a local storage and I just set item,
Play video starting at :14:5 and follow transcript

### 14:05
sorry, my cookie,
Play video starting at :14:13 and follow transcript

### 14:13
zombie equals cookie.
Play video starting at :14:21 and follow transcript

### 14:21
Now in local storage,
Play video starting at :14:27 and follow transcript

### 14:27
I have an entry for my cookie. That's correct. But what I can do is have a script that each time the page is loaded or from time to time actually reset, I don't know why I can't copy paste.
Play video starting at :14:59 and follow transcript

### 14:59
Actually reset the cookie from the local storage or the local database or the session storage. Because there are many ways of keeping a state under JavaScript side of an application. Well, you can create those evil cookies or zombie cookies that will actually be impossible to get rid of. That was a lot. Before I conclude this video, I have to warn you that there are actually legislation about how you can use cookies. For instance, if your website is available in the European Union, you must comply to GDPR. As long as you are an enterprise, a company and you want to do business in the European Union, and your website is available in the European Union, you must comply with GDPR, which means that you can't have cookies that are not needed for the website to work without explicit user agreement. Usually this goes with banner when you say, hey, this website use cookies for this purpose, please acknowledge that you accept them. This must not be just a banner. You're not allowed you to set up cookies until they have agreed to that. Next show that you know is a legislative framework before using cookies, they're actually very touchy sensitive data in the European Union and as far as I know in the State of California too. You can always decide not to do business with these areas, but the fines might be huge if you miss through that. I will not recommend ignoring this legislative part. Thanks so much for watching these videos. You'll soon know the videos, I hope you enjoyed this well, and that now you are able to tell everything you need to know about cookies to anyone. Have a great day and see you soon.