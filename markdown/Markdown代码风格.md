# Markdown代码风格

## 标题

    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题
    ###### 六级标题

## 文本

语法 | 效果 
---- | -----
`_斜体_`| _斜体_
`**粗体**` | **粗体**
`~~删除线~~` | ~~删除线~~
`**_斜粗体_**` | **_斜粗体_**
`~~**_斜粗体删除线_**~~` | ~~**_斜粗体删除线_**~~

换行

    ---

---

## 代码

    ``` java
        public class HelloWorld {
            public static void main(String[] args) {
                System.out.println("Hello World!");
            }
        }
    ```

``` java
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("Hello World!");
        }
    }
```

## 链接

    [text](url "title")
    
    [Link To Google](https://www.google.com "Google")

[Link To Google](https://www.google.com "Google")

## 图片

    ![Alt Text](image url "title")
    
    图片增加链接
    [![Alt Text](image url "title")](url)
    
    [![Build Status](https://secure.travis-ci.org/HuangRongjun/i-blog.png)](https://travis-ci.org/HuangRongjun/i-blog)

[![Build Status](https://secure.travis-ci.org/HuangRongjun/i-blog.png)](https://travis-ci.org/HuangRongjun/i-blog)

## 锚点

    [标题](#标题)  
    [文本](#文本)
    [代码](#代码)
    [链接](#链接)
    [图片](#图片)
    [列表](#列表)  

转到 [标题](#标题)  
转到 [文本](#文本)
转到 [代码](#代码)
转到 [链接](#链接)
转到 [图片](#图片)
转到 [列表](#列表)  

## 列表

有序列表

    1. Item 1
    2. Item 2
    3. Item 3
        1. Item 3a
        1. Item 3b

1. Item 1
2. Item 2
3. Item 3
    1. Item 3a
    1. Item 3b

---

无序列表

    - Item 1
    - Item 2
        - Item 2a
        - Item 2b

- Item 1
- Item 2
    - Item 2a
    - Item 2b

## 引用

常用

    > 最美的不是下雨天  
    > 是曾与你躲过雨的屋檐

> 最美的不是下雨天  
> 是曾与你躲过雨的屋檐

---

嵌套

    > 张老三，我问你，
    > 你的家乡在哪里？
    
    >> 我的家，在山西，
    >> 过河还有三百里。
    
    >>> 我问你，在家里，
    >>> 种田还是做生意？
    
    >>>> 拿锄头，耕田地，
    >>>> 种的高梁和小米。

> 张老三，我问你，
> 你的家乡在哪里？

>> 我的家，在山西，
>> 过河还有三百里。

>>> 我问你，在家里，
>>> 种田还是做生意？

>>>> 拿锄头，耕田地，
>>>> 种的高梁和小米。

## 表格

    First Header | Second Header | Third Header
    :----------- | :-----------: | -----------:
    Content from cell 1 | Content from cell 2 | Content from cell 3
    Content in the first column | Content in the second column | Content in the third column

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Content from cell 1 | Content from cell 2 | Content from cell 3
Content in the first column | Content in the second column | Content in the third column
