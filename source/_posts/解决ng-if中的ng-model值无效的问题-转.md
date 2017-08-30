---
title: 解决ng-if中的ng-model值无效的问题
date: 2017-08-30 16:42:28
tags:
---

<p class="text-indent">在写分销2.0的购物车部分是遇到了这个问题，纠结了好久，开始以为是哪里绑定出了问题，再三确认，觉得可能是遇到angular的Bug，一搜，发现其实是ngif的作用域问题。</p>
<p class="text-indent">作者：abloume &nbsp;&nbsp; 转自：http://blog.csdn.net/u013451157/article/details/60866210 </p>
<p class="text-indent">与其他指令一样，ng-if指令也会创建一个子级作用域，因此，如果在ng-if指令中添加了元素，并向元素属性增加 ng-model指令，那么ng-model指令对应的作用域属性子级作用域，而并非控制器注入的$scope作用域对象，这点在进行双向数据绑定时，需要引起注意。</p>
{% codeblock %}
<!DOCTYPE html>    
<html ng-app="myApp">    
<head>    
<meta charset="UTF-8">    
<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script>    
<style>  
  .frame{  
    padding: 5px 8px;  
    margin: 0px;  
    font-size: 12px;  
    width: 320px;  
    background-color: #eee;  
  }  
  .frame div{  
    margin: 5px 0px;  
  }  
</style>   
</head>    
<body>    
  <div ng-controller="myCtrl" class="frame">  
    <div>  
      a 的值： {{a}}  <br>  
      b 的值： {{b}}  
    </div>  
    <div>  
      普通方式： <input type="checkbox" ng-model="a">  
    </div>  
    <div ng-if="!a">  
      ngIf方式：<input type="checkbox" ng-model="$parent.b">  
    </div>  
  </div>  
  
  <script>  
    angular.module('myApp', [])  
      .controller('myCtrl', function($scope){  
        $scope.a = false;  
        $scope.b = false;  
      })  
  </script>  
</body>    
</html>
{% endcodeblock %}
<p class="text-indent">在ng-if方式中，每个包含的元素都拥有自己的作用域，因此，复选框元素也拥有自己的$scope作用域。相对于控制器作用域来说，这个作用域属于一个子级作用域，所以，如果它想绑定控制器中的变量值，必须添加$parent标识，只有这样才能访问到控制器中的变量。</p>
<p class="text-indent">因此，解决ng-if中ng-model值无效的问题，主要方法就是在绑定值时添加$parent标识，或者用ng-show指令代替ng-if指令，这两种方法都可以达到同样的页面效果。</p>
<p class="text-indent">因为我将ng-if修改成ng-show后，ng-model的值我明明赋的是false，判断时却变成了true,所以姑且使用了添加$parent方法，实测有效！</p>