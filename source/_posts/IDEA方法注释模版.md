---
title: IDEA方法注释模版
copyright: true
date: 2019-04-06 21:39:44
tags: [Java,IDEA]
categories: Java
top:
---

JAVA注释模版

```java
*
 * $TODO$
 * @author caiguoyu
 * @date $time$ $date$
 $param$
 * @return $return$
 */
```

<!--more-->

 > 第一行*必须顶格，这样才能正确显示注释   
 > 第二行之所以用一个空的TODO，是为了生成注释后光标自动显示在第一行   
 > $param$通过函数生成，如果存在多个参数，生成时可能会串行，一路回车下去即可。
![img](https://oss.caiguoyu.cn/pictures/olds/1.jpg)
![img](https://oss.caiguoyu.cn/pictures/olds/2.jpg)
 其中，paramw为:   
 `groovyScript("def result=''; def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList(); for(i = 0; i < params.size(); i++) {result+='* @param ' + params[i] + ((i < params.size() - 1) ? '\\n ' : '')};return result", methodParameters())
 `    

 >用/**+`Enter`即可    

 **效果：**   
![img](https://oss.caiguoyu.cn/pictures/olds/3.jpg)


 头部注释在    

![img](https://oss.caiguoyu.cn/pictures/olds/4.jpg)

 ```java
 /**
 * @Author caiguoyu
 * @Date ${DATE} ${TIME} 
 * @Description TODO
 * @Version 1.0
 * 
 */
 ```

