---
title: vue-router的传参方式
date: 2021-09-22 20:26:30
tags:
---



# 今天 向大家介绍的是 vue-router的传参方式和router的使用技巧

## vue-router传参方法一：

- 1.路由配置

```javascript
{
    path:'/describe/:id',
    name:'describe',
    component:()=>import("你写的组件的相对路径")
}
```

> 其中path表示地址栏中的hash值，：id表示传递的参数，它可以写多个，写法是`/describe/:id/:xxx/......`

> component之后的import表示路由使用的是懒加载，这种写法可以防止页面减少过慢的问题。你也可以使用component ：组件名的写法，但要在之间使用import引入

- 2.使用方法

  - 直接调用$router..push()实现携带参数的跳转

  ````javascript
  this.$router.push({
    // 这个id是一个变量，随便什么值都可以
    path:`/describe/${id}`
  })
  ````

- 3.获取方法（在describe页面）

  ````javascript
  this.$route.params.id
  //使用以上方法可以拿到上个页面传递过来的id值或者其他的变量值
  ````

> 注：$router表示当前的整个路由，而$route 表示的是子路由，可以理解为当前页面的路由

## vue-router传参方法二：

- 1.路由配置

````javascript
{
    path:'/describe',
    name:'describe',
    component:()=>import("你写的组件相对路径")
}
````

- 使用方法

````javascript
this.$router.push({
    name:'describe',
    params:{
       id:id
    }
    // query:{
    //	id:id
    //}
})
// 父组件中：通过路由属性中的name来确定匹配的路由，通过params来传递参数
````

> 使用push方式跳转路由有两种写法：
>
> - 基于name跳转，params传递参数
>   - 此方式类似于Ajax请求的post方式，参数较为隐秘，适用于密码或者账号这种需要隐秘性高的
> - 基于path跳转，query传参
>   - 此方式类似于Ajax请求的get方式，参数直接会展示在地址栏上，适用于隐秘性较低或者对安全性要求不高的

- 获取方法（在describe页面）

````javascript
this.$route.params.id
````



## $route适用小技巧

- 1.$route.path

> 类型：**string**
>
> 字符串，对应当前路由的路径，总是解析为绝对路径

- 2.$route.params

> 类型：**object**
>
> 一个key/value对象，包含了动态片段和全局匹配片段，如果没有路由参数，就是一个空对象

- 3.$route.query

> 类型：**Object**
>
> 一个key/value对象，表示URL查询参数。例如，对于路径/foo?user=1,则有$route.query.user ==1，如果没有查询参数，则是个空对象

- 4.$route.hash

> 类型：**string**
>
> 当前路由的hash值（带#号），如果没有hash值，则为空字符串

- 5.$route.fullPath

>类型：**string**
>
>完成解析后的URL，包含查询参数和hash的完整路径





**``新手博客，有错误欢迎纠正``**
