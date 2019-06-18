# Markdown


* [Markdown](https://daringfireball.net/projects/markdown/) is a text-to-HTML conversion tool for web writers. Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML).
* Markdown is a lightweight and easy-to-use syntax for styling all forms of writing on the GitHub platform.
* Files with the `.md` or `.markdown` extension


* References
   * GitHub Help > [Writing on GitHub](https://help.github.com/categories/writing-on-github/)
   * [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
   * [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#images)


---


## Contents


- [Markdown](#markdown)
  - [Contents](#contents)
  - [Headings](#headings)
- [Heading 1](#heading-1)
  - [Heading 2](#heading-2)
    - [Heading 3](#heading-3)
      - [Heading 4](#heading-4)
        - [Heading 5](#heading-5)
          - [Heading 6](#heading-6)
  - [Styling Text](#styling-text)
  - [Blockquotes (Quoting Text)](#blockquotes-quoting-text)
  - [Quoting Code](#quoting-code)
  - [Links](#links)
  - [Reference Links](#reference-links)
  - [Section Links and Anchors](#section-links-and-anchors)
  - [Lists](#lists)
  - [Task Lists](#task-lists)
  - [Image](#image)
  - [Table](#table)
  - [Comments](#comments)
  - [Math](#math)
  - [HTML Tags](#html-tags)
  - [Emoji](#emoji)


---


## Headings


**Markdown code:**


```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```


**Output:**


# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6


---


## Styling Text


**Markdown code:**


```markdown
**Bold**  
_Italic_  
***Bold and italic***  
~~Strikethrough~~
```


**Output:**


**Bold**  
_Italic_  
***Bold and italic***  
~~Strikethrough~~


---


## Blockquotes (Quoting Text)


**Markdown code:**


```markdown
> Quote
>    * 1
>       * 2


> Quote 1
>
>> Quote 2
>>
>>> Quote 3
>>
>>>> Quote 4
```


**Output:**  


> Quote
>    * 1
>       * 2


> Quote 1
>
>> Quote 2
>>
>>> Quote 3
>>
>>>> Quote 4


---


## Quoting Code


**Markdown code:**


* Within a sentence


```markdown
Hello `Quote` world!
```


* Distinct block


```markdown
\```python
import numpy as np
\```
```


※ Use triple backticks only without backslashs.


**Output:**  


* Within a sentence


Hello `Quote` world!


* Distinct block


```python
import numpy as np
```


---


## Links


**Markdown code:**


```markdown
https://github.com/ktj9279/jin_study


<https://github.com/ktj9279/jin_study>


[Jin's GitHub](https://github.com/ktj9279/jin_study)


[Jin's GitHub (w/ title)](https://github.com/ktj9279/jin_study "마우스 커서를 올리면 나타나는 타이틀")
```


**Output:**


https://github.com/ktj9279/jin_study


<https://github.com/ktj9279/jin_study>


[Jin's GitHub](https://github.com/ktj9279/jin_study)


[Jin's GitHub (w/ title)](https://github.com/ktj9279/jin_study "마우스 커서를 올리면 나타나는 타이틀")


---


## Reference Links


**Markdown code:**


```markdown
[Jin's GitHub][1]  
[TensorFlow][2]  
[PyTorch][3]  
[Jin's GitHub][1]  
[Jin's GitHub w/ title][jin_study]  


[1]: https://github.com/ktj9279/jin_study
[2]: https://www.tensorflow.org/
[3]: https://pytorch.org/
[jin_study]: https://github.com/ktj9279/jin_study "https://github.com/ktj9279/jin_study"
```


**Output:**


[Jin's GitHub][1]  
[TensorFlow][2]  
[PyTorch][3]  
[Jin's GitHub][1]  
[Jin's GitHub w/ title][jin_study]  


[1]: https://github.com/ktj9279/jin_study
[2]: https://www.tensorflow.org/
[3]: https://pytorch.org/
[jin_study]: https://github.com/ktj9279/jin_study "https://github.com/ktj9279/jin_study"


---


## Section Links and Anchors


* You can link directly to a section in a rendered file by hovering over the section heading to expose the link. (section heading 위에 마우스를 올렸을 때 좌측 또는 우측에 뜨는 링크 아이콘을 클릭하면 해당 section의 시작 위치로 스크롤이 이동된다.)
* 또한 anchors를 사용하여 목차 또는 특정 section의 위치로 이동하는 링크를 만들 수 있다.


**Markdown code:**


```markdown
1. [Headings](#Headings)
2. [Styling Text](#Styling-Text)
3. [Blockquotes (Quoting Text)](#Blockquotes-Quoting-Text)


[↑ Go to the top](#Markdown)  
[↑ Go to the contents](#Markdown)  
```


**Output:**


1. [Headings](#Headings)
2. [Styling Text](#Styling-Text)
3. [Blockquotes (Quoting Text)](#Blockquotes-Quoting-Text)


[↑ Go to the top](#Markdown)  
[↑ Go to the contents](#Markdown)  


---


## Lists


**Markdown code:**


* Unordered list

```markdown
* list 1
   * list 1-1
      * list 1-1-1
      * list 1-1-2
   * list 1-2
   * list 1-3
* list 2
* list 3
```


or


```markdown
- list 1
   - list 1-1
      - list 1-1-1
      - list 1-1-2
   - list 1-2
   - list 1-3
- list 2
- list 3
```


* Oredered list

```markdown
1. list 1
   1. list 1-1
      1. list 1-1-1
      2. list 1-1-2
   2. list 1-2
2. list 2
3. list 3
```


**Output:**  


* Unordered list


* list 1
   * list 1-1
      * list 1-1-1
      * list 1-1-2
   * list 1-2
   * list 1-3
* list 2
* list 3


* Oredered list


1. list 1
   1. list 1-1
      1. list 1-1-1
      2. list 1-1-2
   2. list 1-2
2. list 2
3. list 3


---


## Task Lists


**Markdown code:**


```markdown
* [ ] Task 1
* [ ] Task 2
* [x] Task 3
* [x] Task 4
```


**Output:**  


* [ ] Task 1
* [ ] Task 2
* [x] Task 3
* [x] Task 4


---


## Image


* References
   * [[GitHub] 이미지 사이즈 조절 & 정렬](https://blog.yena.io/studynote/2017/11/23/Github-resize-image.html)
   * [HTML Images](https://www.w3schools.com/html/html_images.asp)
   * [CSS Image Gallery](https://www.w3schools.com/css/css_image_gallery.asp)


**Markdown code:**


```markdown
1. 기본 형태


![Octocat](./figures/Octocat.png)


<img src="./figures/Octocat.png" alt="Octocat">


2. 제목 추가


![Octocat](./figures/Octocat.png "Octocat")


<img src="./figures/Octocat.png" alt="Octocat" title="Octocat">


3. 사이즈 조절 및 링크 추가


<img src="./figures/Octocat.png" alt="Octocat" style="width:200px;height:200px;">


<img src="./figures/Octocat.png" alt="Octocat" width="200" height="200">


[<img src="./figures/Octocat.png" alt="Octocat" title="Octocat" width="200">](https://github.com/ktj9279/jin_study)
```


**Output:**  


[<img src="./figures/Octocat.png" alt="Octocat" title="Octocat" width="200">](https://github.com/ktj9279/jin_study)


---


## Table


* A balnk line before a table
* Hyphens `-` to create each column's header
* Pipes `|` to separate each column


**Markdown code:**


```markdown
| Header 1 | Header 2 | Header 3 | Header 4 |
| -------- | :------- | :------: | -------: |
| (1, 1) | (1, 2) | (1, 3) | (1, 4) |
| (2, 1) | (2, 2) | (2, 3) | (2, 4) |
```


**Output:**  


| Header 1 | Header 2 | Header 3 | Header 4 |
| -------- | :------- | :------: | -------: |
| (1, 1) | (1, 2) | (1, 3) | (1, 4) |
| (2, 1) | (2, 2) | (2, 3) | (2, 4) |


---


## Comments


**Markdown code:**


```markdown
<!--
마크다운 주석
-->
```


**Output:**  


<!--
마크다운 주석
-->


※ No output


---


## Math


LaTeX 문법을 사용하여 수식 입력


* References
   * [위키독스 수식입력](https://wikidocs.net/1679)
   * [마크다운과 수학 표현식이 만나다.](http://pad.haroopress.com/page.html?f=mathematics-expression)
   * [깃헙 블로그에 수식 입력하기](https://cameliaovo.github.io/2018/04/12/write-equation-in-blog/)
   * [Daum Equation Editor](http://s1.daumcdn.net/editor/fp/service_nc/pencil/Pencil_chromestore.html)
   * [LaTeX-Tutorial.com](https://www.latex-tutorial.com/)
   * tutorialspoint > [tex - Tutorial](https://www.tutorialspoint.com/tex_commands/index.htm)


**Markdown code:**


```markdown
Eq. 1-1. Inline: ${{MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}$


Eq. 1-2. Inline with some options: ${\displaystyle \operatorname {MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}$


Eq. 2-1. Block:
$$
{{MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}
$$


Eq. 2-2. Block with some options:
$$
{\displaystyle \operatorname {MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}
$$
```


※ `\displaystyle`: The displaystyle affects the amount of vertical space used to lay out a formula: when true, the more spacious layout of displayed equations is used, whereas when false a more compact layout of inline formula is used.


**Output:**  


Eq. 1-1. Inline: ${{MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}$


Eq. 1-2. Inline with some options: ${\displaystyle \operatorname {MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}$


Eq. 2-1. Block:
$$
{{MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}
$$


Eq. 2-2. Block with some options:
$$
{\displaystyle \operatorname {MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}}
$$


---


## HTML Tags


* References
   * [글쓰기, 마크다운의 모든 것! <고급과정>](https://steemit.com/kr/@newiz/3)


**Markdown code:**


```markdown
공백 여러 개&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;삽입

---

개행 위<br>개행 아래

---

m<sup>2</sup>, m<sup>3</sup>

---

x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>

---

<center>가운데 정렬</center>

---

&copy;

---

<q>큰따옴표</q>
```


**Output:**  


공백 여러 개&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;삽입

---

개행 위<br>개행 아래

---

m<sup>2</sup>, m<sup>3</sup>

---

x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>

---

<center>가운데 정렬</center>

---

&copy;

---

<q>큰따옴표</q>


---


## Emoji


* [Emoji](https://help.github.com/en/articles/basic-writing-and-formatting-syntax#using-emoji)
* [Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md)
* [Emoji Unicode Tables](https://apps.timwhitlock.info/emoji/tables/unicode)