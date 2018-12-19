<!-- TOC -->

- [编程规约](#编程规约)
    - [命名风格](#命名风格)
        - [通用](#通用)
        - [类名](#类名)
        - [方法名、参数名、成员变量、局部变量](#方法名参数名成员变量局部变量)
        - [常量](#常量)
        - [包名](#包名)
    - [常量定义](#常量定义)
    - [代码格式](#代码格式)
- [参考资料](#参考资料)

<!-- /TOC -->


# 编程规约 
## 命名风格 
### 通用

1、代码中的命名均不能以下划线或美元符号开始，也不能以下划线或美元符号结束。 

反例：`_name / __name / $name / name_ / name$ / name__ `

2、严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。

正例：`alibaba / taobao / youku / hangzhou` 等国际通用的名称，可视同英文。 

反例：`DaZhePromotion [打折] / getPingfenByName() [评分] / int 某变量 = 3` 

3、杜绝完全不规范的缩写，随意缩写严重降低了代码的可阅读性。 

反例：`AbstractClass` 缩写成 `AbsClass`；`condition` 缩写成 `condi`

### 类名

1、类名使用 UpperCamelCase 风格，但以下情形例外：DO / BO / DTO / VO / AO / PO / UID 等。 

正例：`MarcoPolo / UserDO / XmlService / TcpUdpDeal / TaPromotion` 

反例：`macroPolo / UserDo / XMLService / TCPUDPDeal / TAPromotion`

2、抽象类命名使用 Abstract 或 Base 开头；异常类命名使用 Exception 结尾；测试类命名以它要测试的类的名称开始，以 Test 结尾。

### 方法名、参数名、成员变量、局部变量

1、 统一使用 lowerCamelCase 风格，遵从驼峰形式。 

正例： `localValue / getHttpMessage() / inputUserId `

### 常量

1、常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚，不要嫌名字长。

### 包名
1、包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式。 

## 常量定义

1、不允许任何魔法值（即未经预先定义的常量）直接出现在代码中。

2、在 long 或者 Long 赋值时，数值后使用大写的 L，不能是小写的 l，小写容易跟数字 1 混淆，造成误解。 

说明：Long a = 2l; 写的是数字的 21，还是 Long 型的 2? 

3、【推荐】不要使用一个常量类维护所有常量，要按常量功能进行归类，分开维护。 

说明：大而全的常量类，杂乱无章，使用查找功能才能定位到修改的常量，不利于理解和维护。 

正例：缓存相关常量放在类 CacheConsts 下；系统配置相关常量放在类 ConfigConsts 下。 

4、【推荐】如果变量值仅在一个固定范围内变化用 enum 类型来定义。 

说明：如果存在名称之外的延伸属性应使用 enum 类型，下面正例中的数字就是延伸信息，表示一年中的第几个季节。 

正例： 
```java
public enum SeasonEnum {     
    SPRING(1), SUMMER(2), AUTUMN(3), WINTER(4);     private int seq;     
    SeasonEnum(int seq){
        this.seq = seq;     
        } 
    }
```

## 代码格式
1、**大括号**的使用约定。如果是大括号内为空，则简洁地写成`{}`即可，不需要换行；如果是非空代码块则：  
- 左大括号前不换行。 
- 左大括号后换行。  
- 右大括号前换行。  
- 右大括号后还有 else 等代码则不换行；表示终止的右大括号后必须换行。 

2、**左小括号**和字符之间不出现空格；同样，右小括号和字符之间也不出现空格；而左大括号前需要空格。详见第 5 条下方正例提示。

3、需要加空格的情况：
- `if/for/while/switch/do` 等保留字与括号之间都必须加空格。 
- 任何二目、三目运算符的左右两边都需要加一个空格。
- 方法参数在定义和传入时，多个参数逗号后边必须加空格。如`method(args1, args2, args3)`
- 注释的双斜线与注释内容之间有且仅有一个空格。

4、采用 4 个空格缩进，禁止使用 tab 字符。

 说明：如果使用 tab 缩进，必须设置 1 个 tab 为 4 个空格。IDEA 设置 tab 为 4 个空格时， 请勿勾选 Use tab character；而在 eclipse 中，必须勾选 insert spaces for tabs。 

5、【推荐】不同逻辑、不同语义、不同业务的代码之间插入一个空行分隔开来以提升可读性。 任何情形，没有必要插入多个空行进行隔开。

正例：（涉及 1-5 点）
```java 
public static void main(String[] args) {      
 
    // 缩进 4 个空格      
    String say = "hello";      
    // 运算符的左右必须有一个空格      
    int flag = 0;     
    // 关键词 if 与括号之间必须有一个空格，括号内的 f 与左括号，0 与右括号不需要空格      
    if (flag == 0) {          
        System.out.println(say);      
    }               
        
    // 左大括号前加空格且不换行；左大括号后换行      
    if (flag == 1) {          
        System.out.println("world");      
    // 右大括号前换行，右大括号后有 else，不用换行      
    } else {            
        System.out.println("ok");      
        // 在右大括号后直接结束，则必须换行      
    }  
}
```

6、**单行字符数限制**不超过 120 个，超出需要换行，换行时遵循如下原则：  
- 第二行相对第一行缩进 4 个空格，从第三行开始，不再继续缩进.
- 运算符与下文一起换行。  
- 方法调用的点符号与下文一起换行。  
- 方法调用中的多个参数需要换行时，在逗号后进行。  
- 在括号前不要换行，见反例。

正例： 
```java
StringBuffer sb = new StringBuffer();  
// 超过 120 个字符的情况下，换行缩进 4 个空格，点号和方法名称一起换行  
sb.append("zi").append("xin")...    
    .append("huang")...  
    .append("huang")...  
    .append("huang");  
```
反例： 
```java
StringBuffer sb = new StringBuffer();  
// 超过 120 个字符的情况下，不要在括号前换行  
sb.append("zi").append("xin")...append      
    ("huang");   
 
// 参数很多的方法调用可能超过 120 个字符，不要在逗号前换行
method(args1, args2, args3, ...      
    , argsX);  
```

7、【推荐】单个方法的总行数不超过 80 行。 

 说明：包括方法签名、结束右大括号、方法内代码、注释、空行、回车及任何不可见字符的总 行数不超过 80 行。 

代码逻辑分清红花和绿叶，个性和共性，绿叶逻辑单独出来成为额外方法，使主干代码 更加清晰；共性逻辑抽取成为共性方法，便于复用和维护。 

8、【推荐】没有必要增加若干空格来使某一行的字符与上一行对应位置的字符对齐。 

9、IDE 的 text file encoding 设置为 **UTF-8**; IDE 中文件的换行符使用 **Unix** 格式， 不要使用 Windows 格式。

# 参考资料
- [阿里巴巴Java开发手册](https://github.com/alibaba/p3c/blob/master/%E9%98%BF%E9%87%8C%E5%B7%B4%E5%B7%B4Java%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C%EF%BC%88%E8%AF%A6%E5%B0%BD%E7%89%88%EF%BC%89.pdf)




