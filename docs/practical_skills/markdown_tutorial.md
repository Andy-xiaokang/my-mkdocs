# this is a practice for learning markdown
## markdown标题语法
# Heading level 1
## Heading lever 2
### Heading lever 3
#### Heading lever 4
##### Heading lever 5
###### Heading lever 6


## markdown 段落语法
空行且段首不要空格
I really like using markdown.

I think I'll use it to format all of my documents from now on.
Don't put tabs or spaces in front of your paragraphs

Keep lines left-aligned like this

## Markdown换行语法
在一行末尾添加两个或多个空格，然后回车键，即可创建一个换行；至少有两种轻量级标记语言支持无需在行尾添加任何内容，只需键入回车键（return）即可实现换行
This is the first line.  
And this is the second line

## Markdown 强调语法
粗体（bold)在单词或短语前后各添加两个星号*cd
I just love **bold text**.
love**is**bold
斜体在单词短语前后添加一个星号
Italicized text is the *cat's meow*
A*cat*meow
粗斜体单词或短语前各添加三个星号
This text is ***really important***.
This is really ***very*** imporant

## markdown 引用语法
创建块引用，在段落前添加一个`>`符号
> Dorothy followed her though many of the beautiful rooms in her castle.

多个段落的块引用,块引用可以包含多个段落。为段落之间的空白行添加一个`>`符号
> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean pots and kettles and sweep the floor and keep the fire fed with wood.

嵌套块引用，在要嵌套的段落前添加一个`>>`符号
> dorothy followed her through many of the beautiful rooms in her castle.
>
> >The witch bade her clean the pots and kettles and sweep the floor and keep the fire with wood

带有其他元素的块引用
> ### the quarterly results look great!
>
> * Revenue was off the chart.
> * profits were higher than ever.
>
> *Everything* is going according to **plan**

## markdown 列表语法
有序列表，列表项前添加数字并紧跟一个英文句点，数字不必按数学顺序排列，但列表应当以数字1起始

1. first item
2. second item
3. third item
   
   1. first item
   2. second

4. fourth item

无序列表

*  first item
  
  * indented item
  * indented item


在列表中嵌套其他元素，请将该元素缩进四个空格或一个制表符
* first item
* second item
    I need to add another paragraph below the second list item
* third item


* first item
* second item
    > A blockquote would look great below the second list item.
* third item

******

1. first item
2. second item 
    ```c
    #include<stdio.h>
    {
        printf()
    }
    ```
3. third item
***
1. first item
2. second item 
    ![截屏2023-04-12 20.44.12](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-04-12%2020.44.12.png)
3. third item

列表

1. first item
2. second item 
    * indented item
    * indented item
3. third item

## markdown 代码语法
行内代码
若将单词或短语表示为代码，请将其包裹在反引号中 
at the command prompt, type `nano`
转义反引号
如果你要表示为代码的单词或短语中包含一个或多个反引号，则可以通过将单词或短语包裹在双反引号(``)中。

``Use `code` in your markdown file``

markdown 围栏式代码块(在代码块的反引号旁指定一种语言即可语法突出显示)
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
## 分割线语法
单独一行上使用三个或多个星号（`***`）
try to put a blank line before...
***
...and after put a horizontal rule.

## 链接语法
[apple](https://www.apple.com.cn/)
使用尖括号可以很方便地把URL或者email变成可点击的链接
<https://www.apple.com.cn/>
<2177877404@qq.com>
带格式化的链接
This is the *[Markdown Guide](https://markdown.com.cn)*


## 图片语法
![gardon](https://markdown.com.cn/assets/img/philly-magic-garden.9c0b4415.jpg)

## Markdown转义字符语法
在字符前面添加反斜杠字符\
\* Without the backslash, this would be a bullet in an unordered list

## markdown 扩展语法
Markdown 表格

| syntax  | description| test text|
|:--- | :---: | ---: |
|Header|title|here's this|
|paragraph |text|and more|

围栏代码块
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
Markdown脚注
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.
indented paragraphs to include them in the footnote.
`{my code}`
add as many paragraphs as you like

Markdown删除线
~~世界是平坦的~~，我们现在知道是圆的

Markdown任务列表语法

- [x] write the press release
- [ ] update the website
- [ ] contact the media 

Markdown 高亮语法
==高亮==

1.  Vivamus id mi enim. Integer id turpis sapien. Ut condimentum lobortis
    sagittis. Aliquam purus tellus, faucibus eget urna at, iaculis venenatis
    nulla. Vivamus a pharetra leo.

    1.  Vivamus venenatis porttitor tortor sit amet rutrum. Pellentesque aliquet
        quam enim, eu volutpat urna rutrum a. Nam vehicula nunc mauris, a
        ultricies libero efficitur sed.

    2.  Morbi eget dapibus felis. Vivamus venenatis porttitor tortor sit amet
        rutrum. Pellentesque aliquet quam enim, eu volutpat urna rutrum a.

        1.  Mauris dictum mi lacus
        2.  Ut sit amet placerat ante
        3.  Suspendisse ac eros arcu

