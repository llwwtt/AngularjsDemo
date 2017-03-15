##angularjs的四大核心特性
   1 MVC
   model-view-controller
   数据模型-视图（眼睛能看到的）-业务逻辑和控制逻辑
   2 模块化
   Module 一切都是从模块开始的
   3 指令系统
   directive
   4 双向数据绑定
   view 和 viewmodel
   当视图上的东西变化，视图模型上的数据也会变化，相反，最常见的应用是表单

   代码编辑工具：足够强大灵活 sublime webstrom(可以实时运行浏览器找出兼容性)
   断点调试工具：batarang(针对按gularjs设计的)
   版本管理工具：git tortoisegit(小乌龟)在系统的右键出现很多菜单
   代码合并和混淆工具：grunt (配置的太多) gulp(推荐使用)
   依赖管理工具：bower(自动安装依赖的组件、组件之间的依赖检测、版本兼容性自动检测)
   单元测试工具：karma jasmine(茉莉花)
   集成测试工具：模拟用户的操作 让代码整体跑起来


   为什么需要mvc？

   前台代码规模越来越大 切分职责是大势所趋
   很多逻辑一模一样，这时需要复用
   为了后期维护方便，修改一块不影响其他功能
   mvc只是手段，终极目标是模块化和复用

   前端mvc的困难

   操作dom的代码必须等待页面全部加载完成
   多个js文件之间如果相互依赖，程序员必须自己解决
   js的原型继承也给前端编程带来了很多困难
   

   Angularjs中的controller

   控制器由一个函数充当
   视图和控制器进行交互，控制器再跟数据交互，视图不可能和数据直接交互，
  一个控制器可以控制多个视图，如果多个视图之间没有任何逻辑上的关系，那控制器的角色就会很尴尬
  所以完美的方法是一个控制器控制一个视图 如果多个控制器都有相同的功能，如果你说再写一个通用的控制器让其他控制器去继承它那就错了
  angularjs中的做法是提供了一个service

  注意点

  不要试图去复用controller 一个控制器只能负责一个模块
  不要在controller中操作dom 这不是控制器的职责 而是封装到另一个叫做指令模块中
  不要在controller里面做数据格式化，ng有很好用的表单控件
  不要在controller里面做数据过滤操作，ng有$filter服务
  一般来说，controller是不会互相调用的，控制器之间的交互通过事件进行

  如何复用model

  ```
  <div ng-app='mainapp' ng-controller='maincontroller'>
    	<!-- input标签为view -->
    	<input ng-model='greeting.text'>
    	<!-- p标签为viewmodel -->
    	<p>{{greeting.text}},angularjs</p>
    </div>
  ```
  angularjs启动以后会首先去找ng-app属性 并创建一个根作用域$rootscope上
  认为ng-app中的所有指令都归angularjs管 找到ng-model以后，就会生成一个$scope 这个对象挂载在$rootscope上 并且在当前ng-model属性下的所有标签都可以去访问里面的方法和属性
  因为这些方法和属性是绑定在当前$scope下的

  如何复用view
  利用directive实现视图的复用 
  angularjs的mvc都是借助$scope实现的
  作用域 $scope和原型链差不多 本身没有的就会去上一级去查找 直到找到$rootscope

  $scope
  $scope是一个对象
  是表达式的执行环境（或者叫作用域）
  是一个树形结构，与dom平行
  每一个angular都有一个跟$scope对象，位于ng-app上
  可以传播事件，类似dom事件，可以向上也可以向下
  是mvc的实现基础

  angularjs是如何实现模块化的？ 

  使用ngRoute进行视图之间的路由，也就是切换模块
  angular.module('mainapp',[])
    .controller('maincontroller',['$scope',function(){

  }])
  任何一个ng应用都是由控制器、指令、服务、路由、过滤器等有限的模块类型构成的
  控制器、指令、服务、路由、过滤器分别放在一个模块里面
  用一个总的app模块作为入口点，它依赖其他所有模块

依赖注入
 var bookStoreApp = angular.module('bookStoreApp',['ngRoute','ngAnimate','bookStoreCtrls','bookStoreFilters','bookStoreServices','bookStoreDirectives']);
 ng在启动时，会检测有没有依赖的模块 ng开头的是ng提供的

 ng没实现异步加载 因为已经有工具了 比如require.js


  books {
    book{
       [title:'aa',author:'bb'],
       [title:'aa',author:'bb'],
       [title:'aa',author:'bb'],
       [title:'aa',author:'bb'],
       [title:'aa',author:'bb'],
    },
    city{

      },
      

  }