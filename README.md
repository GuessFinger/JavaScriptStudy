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

    
