---
title: angular中定义全局变量的3种方法
date: 2016-05-02 00:34:52
tags:
---
angularjs自身有二种，设置全局变量的方法，在加上js的设置全局变量的方法，总共有三种。要实现的功能是，在ng-app中定义的全局变量，在不同的ng-controller里都可以使用。

1. 通过var 直接定义global variable，这根纯js是一样的。

2. 用angularjs value来设置全局变量 。

3. 用angularjs constant来设置全局变量 。

下面用一个例子，来说明，上面3种方法：

实例：

####1. 在app模块中，定义全局变量

    'use strict';  
      
    /* App Module */  
      
    var test2 = 'tank';         //方法1，定义全局变量  
      
    var phonecatApp = angular.module('phonecatApp', [     //定义一个ng-app  
      'ngRoute',  
      'phonecatControllers',  
      'tanktest'  
    ]);  
      
    phonecatApp.value('test',{"test":"test222","test1":"test111"});  //方法2定义全局变量  
      
    phonecatApp.constant('constanttest', 'this is constanttest');    //方法3定义全局变量  
      
    phonecatApp.config(['$routeProvider',                //设置路由  
      function($routeProvider) {  
        $routeProvider.  
          when('/phones', {  
            templateUrl: 'partials/phone-list.html'      //这里没有设置controller，可以在模块中加上ng-controller  
          }).  
          when('/phones/:phoneId', {  
            templateUrl: 'partials/phone-detail.html',  
            controller: 'PhoneDetailCtrl'  
          }).  
          when('/login', {  
            templateUrl: 'partials/login.html',  
            controller: 'loginctrl'  
          }).  
          otherwise({  
            redirectTo: '/login'  
          });  
      }]);  

####2. 在controller中调用全局变量


    'use strict';  
      
    /* Controllers */  
      
    var phonecatControllers = angular.module('phonecatControllers', []);  
      
    phonecatControllers.controller('PhoneListCtrl', ['$scope','test','constanttest',  
      function($scope,test,constanttest) {  
        $scope.test = test;                   //方法2，将全局变量赋值给$scope.test  
        $scope.constanttest = constanttest;   //方法3，赋值  
        $scope.test2 = test2;                 //方法1，赋值  
      }]);  

####3. 在html中看一下效果


    <div data-ng-controller="PhoneListCtrl">  
        {{test.test1}}  
        {{constanttest}}  
        {{test2}}  
    </div>  
      
    结果：test111 this is constanttest tank  

其实我们可以通过其他方法来实现全局变量，例如：angularjs factory的功能。
