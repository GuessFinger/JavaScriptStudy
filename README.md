- 把JavaScript这本书，这本书总共28章，一周7章，一周的最后一天把之前学习的内容再复习下，这个计划还是有点偏理想，尽量按照这个计划进行

- **第1章**
- 完整的JavaScript包含的部分
    - 核心（ECMAScript） 欧洲计算机管理协会Script
    - 文档对象模型 DOM   提供与网页内容交互的方法和接口
    - 浏览器对象模型 BOM  提供与浏览器交互的方法和接口
    
- **第2章**
- \<script\>标签有哪些属性
    - 属性名  是否必须  干什么用的？
    - async 
    - charset 
    - crossorigin  
    - defer 
    - integrity 
    
- script 最大的一个争议点就是 它可以包含外部域的JavaScript文件，即使这个文件和html不再相同的域中  也就是引入文件的时候，不会出现跨域的问题
- 标签的位置
    - 把script标签放到head中间，页面加载的时候 需要先把script标签中的内容下载，解析和解释完成后，才开始渲染页面 所以一般放到body结束标签的上面
- 推迟脚本执行
    - 给引入的脚本文件添加属性 defer属性 告诉浏览器立即下载 但是延迟执行
- 异步执行脚本
    - 给引入的外部脚本文件添加 async属性 告诉浏览器立即下载，但是延迟执行，添加多个属性 脚本之间么有依赖关系的 有可能第二个脚本先执行
- 动态加载脚本(这个之前看过)
    ```javascript 1.8
          let script = document.createElement('script')
          script.scr = 'common.js'
          document.head.appendChild(script)
          // 不是所有的浏览器都支持async属性 统一加载行为  进行下面的设置
          script.async = false
          // 使用这种方式 对浏览器的预加载器是不可见的 也就是它不知道你加载了这个文件 需要在文档头部显式声明
          // <link rel="preload" href="common.js"></link> 
    ```
 - 行内代码和外部文件  基本上都选择外部文件的方式
    - 可维护性
    - 缓存  相同文件的话
    - 适应未来 
- 文档模式  混杂模式和标准模式  可以通过doctype 来进行切换

- 定义变量的方式let var const  
    ```javascript 1.8
        //  使用var可以这样使用
        hello = 'world'
        var hello;
        // 你这个变量定义在函数里面  外面就会报错的  如果不添加var 就不会报错
        function test(){var message = 'hello world';}  console.log(message)
    ```
    - let var
        - var 声明提升 就是把所有变量声明都拉到函数作用域的顶部 后面的代码正常执行 undefined `function test(){console.log(age);var age = 26}`
        - 暂时性死区  let 声明的变量不会再作用域中被提升 大概的意思就是 使用let定义变量  不能再没有定义之前使用
        - 全局变量  使用 var message = 'hello world' window.message 也会找到这个值  let就不会出现
        - let是快级作用域
        - for循环  
        ```javascript
              for(var i = 0; i < 5 ; i++) {
                console.log('hello world')
              }
              // 这里打印的i就是5  变量渗透到变量体之外了  使用let的话 迭代的变量会限制在for循环内部
              console.log(i)
              // 下面的例子是非常经典的面试题  最后打印的结果是多少  如果换成let声明会怎么样？  
              for(var j = 0; j < 5 ; i++) {
                setTimeout(() => console.log(j))
              }
        ```
    - const  和let使用规则是一样的  重点是const在声明变量的时候 一定要进行初始化 且尝试修改const定义的变量会报错

- 数据类型(Undefined Null Boolean Number String Symbol Object)
    - 怎么判断类型 `typeof 123;typeof '123'` typeof的结果有哪些(undefined,boolean,string,number,object,function,symbol)
    
    - Undefined类型 就一个值undefined 声明变量但是没有赋值 
    - Null类型  也就一个值null 表示一个空对象指针  typeof null  ==> object  
        - 在定义*对象*的时候 使用let obj = null;这样的方式定义 一般let obj;这样obj默认等于的哦就是undefined
        - null == undefined  ==> true 
    - Boolean类型
        - 说过JavaScript是区分大小写的 所以 true/false 和True/False是不一样的
        - ![Boolean的默认转换规则](./images/Boolean的默认转换规则.png) 
        - 根据上面的语法，才可以写 `if(message){console.log(true)}` 这样的语法
    - Number类型
        - 永远不要测试某个特定的浮点值  `if(0.1+0.2 == 0.3){console.log(false)}` 
        - 最大值 Number.MAX_VALUE  最小值 Number.MIN_VALUE 如果一个数不在这个范围之内的话 用-Infinity/Infinity来表示负无穷大/正无穷大
            这样的值不能再进行运算 判断是否是无穷大的方式 isFinite()    
        - NaN  not a number  表示本来要返回数值的操作失败了 `0/0;-0/+0`   任何涉及NaN的操作始终返回NaN, NaN不等于包括NaN在内的任何值
            NaN == NaN ==> false  如果要判断的话 isNaN() 这种方式
        - 数字的转换 true -> 1;false -> 0;'' -> 0;'hello' -> 0;'00011' -> 11
        - parseInt('123abc') => 123 这个结果我是没想到的如果第一个字符不是数值字符、加号或减号，parseInt()立即
            返回 NaN。这意味着空字符串也会返回 NaN（这一点跟 Number()不一样，它返回 0）。如果第一个字符
           是数值字符、加号或减号，则继续依次检测每个字符，直到字符串末尾，或碰到非数值字符。  它还可以接受第二个参数 表示进行几进制转换 parseFloat一样效果
           
        - 字符串  一旦创建，他们的值不能发生变化了 要求改某个变量中的字符串，必须销毁员原来的哦字符串       
            
