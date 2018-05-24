---
title: 记录碰到的移动端BUG
date: 2018-04-24 11:12:09
tags:
---
<p>记录下自己开发过程中碰到的一些移动端的坑，方便以后使用</p>

<div>
<h3>1.Vue构建的SPA在安卓微信端分享问题</h3>
<article>
特别注意：在Hash模式下，安卓中会遇到分享到朋友圈之后，点击跳转会首页的情况，此时分享的路径与商品的真实路径是不一致的。需要在服务器端稍微处理一下。即把index文件，重新建一个文件夹，例如static，放进去。此时分享之后的路径，与真实路径才是一致的，也不会发生跳回首页的情况。苹果手机则不会有这个问题。
</article>
</div>

<div>
<h3>2.移动端没有Control属性的视频无法在IOS播放及Video标签占页面层级最高级</h3>
<article>
解决办法：目前暂无好的办法，不建议使用原生Video标签，建议自己写一个Video标签样式，可以避免这个问题
</article>
</div>

<div>
<h3>3.Vue spa页面在同一个页面下切换不同的Query，页面不刷新</h3>
<article>
解决办法：解决办法：监听页面Query变化
</article>
{% codeblock %}
watch: {
    $route: function (route) {
      var query = route.query
      this.page = query.page
      location.reload()
    }
  }
{% endcodeblock %}
</div>
<div>
<h3>4.IOS 无法使用20XX-XX-XX XX:XX:XX类时间格式</h3>
<article>
解决办法：转换成20XX/XX/XX XX:XX:XX或时间戳
</article>
</div>

<div>
<h3>5.IOS 点击页面会有300ms延迟</h3>
<article>
解决办法：引入fastclick.js文件解决
</article>
{% codeblock %}
npm install fastclick -S
{% endcodeblock %}
</div>

<div>
<h3>6.某些Android border-radius属性无效</h3>
<article>
解决办法：设置CSS的background-clip属性
</article>
{% codeblock %}
background-clip: padding-box;
{% endcodeblock %}
</div>