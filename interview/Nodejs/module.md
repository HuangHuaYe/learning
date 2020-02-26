# module

## CommonJS

`module.exports` 导出模块内容,require读取

## AMD和requireJS

AMD规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。模块加载完之后执行毁掉函数.

    // 先定义模块路径
    require.config({
    	baseUrl: "",
    	paths: {
    		"jq": "jq",
    	}
    }
    // 定义math.js模块
    define(function () {
        var basicNum = 0;
        var add = function (x, y) {
            return x + y;
        };
        return {
            add: add,
            basicNum :basicNum
        };
    });
    // 定义一个依赖underscore.js的模块
    define(['underscore'],function(_){
      var classify = function(list){
        _.countBy(list,function(num){
          return num > 30 ? 'old' : 'young';
        })
      };
      return {
        classify :classify
      };
    })
    
    // 引用模块，将模块放在[]内
    require(['jquery', 'math'],function($, math){
      var sum = math.add(10,20);
      $("#sum").html(sum);
    });

## CMD和seejs

CMD和AMD非常相似,就是声明模块的时候不一致.不同点在于：AMD 推崇依赖前置、提前执行，CMD推崇依赖就近、延迟执行.

    /** AMD写法 **/
    define(["a", "b", "c", "d", "e", "f"], function(a, b, c, d, e, f) { 
         // 等于在最前面声明并初始化了要用到的所有模块
        a.doSomething();
        if (false) {
            // 即便没用到某个模块 b，但 b 还是提前执行了
            b.doSomething()
        } 
    });
    
    /** CMD写法 **/
    define(function(require, exports, module) {
        var a = require('./a'); //在需要时申明
        a.doSomething();
        if (false) {
            var b = require('./b');
            b.doSomething();
        }
    });

## ES6 Module

ES6的模块不是对象，import命令会被 JavaScript 引擎静态分析，在编译时就引入模块代码，而不是在代码运行时加载，所以无法实现条件加载。也正因为这个，使得静态分析成为可能。

    /** export default **/
    //定义输出
    export default { basicNum, add };
    //引入
    import math from './math';
    function test(ele) {
        ele.textContent = math.add(99 + math.basicNum);
    }

## ES6模块与CommonJS的区别

1. CommonJS是值的拷贝,拷贝出去后,模块内部的更改不影响其输出.es6模块则相反
2. CommonJS是运行时加载,ES6是编译时的接口输出.
3. CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。