---
title: 在国内加载reCAPTCHA的绝妙方式
author: 千里扯淡
layout: post
---
>众所周知，谷歌的reCAPTCHA验证码在国内是无法正常加载的。  
>同样众所周知的是，其不能加载的原因是因为使用它需要加载 https://www.google.com/recaptcha/api.js 这个文件。然后！ google.com 在国内是无法正常访问的，然后整个reCAPTCHA都没法用了(；´д｀)ゞ  
>不过， https://recaptcha.net/recaptcha/api.js 可以起到同样的功能，并且 recaptcha.net 是可以正常在国内访问到的ヽ(￣▽￣)ﾉ  
>所以，我们只要想办法加载https://recaptcha.net/recaptcha/api.js就行了。  

--------------
--------------
--------------

>我们可以好好利用浏览器中的“检查”（就是 右键--检查 那个）的“控制台（Console）”功能（如图）  
>![图片](https://files.qlchedan.tk/file/filesssss/20210802/pic0.PNG)  
>它允许你直接在浏览器中输入JavaScript命令。而说起加载外部的js文件，我想到的就是使用jQuery的 $.getScript() 方法。所以，理论上来说，只要在控制台中加载jQuery，接着使用 $.getScript() 方法岂不是就解决问题了？  
>直接开干！

-------------
-------------
-------------

>在浏览器控制台中输入:  
>```JavaScript
>var importJs=document.createElement('script')
>importJs.setAttribute("type","text/javascript")
>importJs.setAttribute("src", 'https://cdn.jsdelivr.net/npm/jquery@3.2.1/dist/jquery.min.js')
>document.getElementsByTagName("head")[0].appendChild(importJs)
>```
>导入jQuery，然后输入：
>```jQuery
>$.getScript("https://recaptcha.net/recaptcha/api.js?onload=grecaptchaOnload")
>```
>![图片](https://files.qlchedan.tk/file/filesssss/20210802/pic1.PNG)  
>接着，你应该就可以发现这个图标了：  
>![图片](https://files.qlchedan.tk/file/filesssss/20210802/pic2.PNG)  

------------
------------
------------

>大功告成！
