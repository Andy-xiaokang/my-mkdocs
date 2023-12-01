---
comments: true
---

# Reference
Here are some markdown_extensions from [reference](https://squidfunk.github.io/mkdocs-material/reference/) page, I think it may be enough for me to build my online docs. for more extensions visit [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/). a design principle from philosophy from getting started page draw my attention. 
> **It's just markdown**: ==focus on the content of your documentation== and create a professional static site in minutes.

That's what I need, so I explore some simple but useful extensions and want to write a markdown file to test. I think my docs may accompany me to record future study. The docs is designed for myself to record daily study, something interesting and something easily forgotten. If I get strong enough in the future, I believe what I get from Internet I will return to the Internet. My English level is so poor but I think practice makes perfect so I will write in English as much as possible.
***
## Admonitions
### configuration 
```yaml
markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences
```
### usage
```markdown title="admonition"
!!! note 
    this is a note 
```
!!! note 
    this is a note 
#### changing the title 
```markdown title="Admonition with custom title"
!!! note "custom title"
    note with a custom title
```
!!! note "custom title"
    note with a custom title
#### collapsible blocks
```markdown title="collapsible admonition"
??? note "collapsible admonitions and initially collapsed"
    this is a collapsible admonitions and initially collapsed
```
??? note "collapsible admonitions and initially collapsed"
    this is a collapsible admonitions and initially collapsed

```markdown title="collapsible admonition and initially expanded"
???+ note "collapsible admonitions and initially expanded"
    this is a collapsible admonitions and initially expanded
```
???+ note "collapsible admonitions and initially expanded"
    this is a collapsible admonitions and initially expanded

```markdown
=== "inline end"
    !!! info inline end "a info in line end"
        this is a test for info admonition 
        in line end
    ```markdown
    !!! info inline end "a info in line end"
        this is a test for info admonition 
        in line end
    ```
=== "inline front"
    !!! info inline "a info in line front"
        this is a test for info admonition in 
        line front

    ```markdown
    !!! info inline "a info in line front"
        this is a test for info admonition in 
        line front
    ```
```

=== "inline end"
    !!! info inline end "a info in line end"
        this is a test for info admonition 
        in line end
    ```markdown
    !!! info inline end "a info in line end"
        this is a test for info admonition 
        in line end
    ```
=== "inline front"
    !!! info inline "a info in line front"
        this is a test for info admonition in 
        line front

    ```markdown
    !!! info inline "a info in line front"
        this is a test for info admonition in 
        line front
    ```
==important==: admonitions that use `inline` modifiers must be declared prior to the content block you want to place them beside. If there's insufficient space to render the admonition next to the block, the admonition will stretch to the full width of the viewport, e.g., on mobile viewports.

#### supported types
!!! abstract
    this is abstract type
!!! tip
    this is tip type
!!! success
    this is success type
!!! question
    this is question type
!!! warning
    this is warning type
!!! failure
    this is failure type
!!! danger
    this is danger type
!!! bug
    this is bug type
!!! example
    this is example type
!!! quote
    this is quote type
***
## Code blocks
### Configuration
```yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
```
```yaml
theme:
  features:
    - content.code.copy
```
### Usage
```markdown title="code block"
    ``` py
    import tensorflow as tf
    ```
```
``` py
import tensorflow as tf
```
#### adding title
```markdown title="code block with title"
    ``` py title="bubble_sort.py"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
```
``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
#### add line numbers
```markdown title="code block with line numbers"
    ``` py linenums="1"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
```
``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
#### Highlighting specific lines
```markdown title="code blocks with highlighted specific lines"
    ``` py hl_lines="2 3"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
```
``` py hl_lines="2 3" linenums="1" title="bubble_sort"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
***
## Content tabs
### Configuration
```yaml
markdown_extensions:
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true 
```
```yaml
theme:
  features:
    - content.tabs.link
```
### Usage
#### grouping code blocks
=== "C"
    ```c
    #include<stdio.h>
    int main(void)
    {
        printf("Hello World!\n");
        return 0;
    }
    ```
=== "C++"
    ``` c++
    #include <iostream>
    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```
#### grouping other content
```markdown title="content list"
=== "content unordered list"
    * first unordered item
    * second unordered item
    * third unordered item

=== "ordered list"
    1. first ordered item
    2. second ordered item
    3. third ordered item

``` 
=== "content unordered list"
    * ==first unordered item==
    * second unordered item
    * third unordered item

=== "ordered list"
    1. first ordered item
    2. second ordered item
    3. third ordered item

#### Embedded content
```markdown title="content tabs in admonition"
!!! example 
    === "content unordered list"
        * ==first unordered item==
        * second unordered item
        * third unordered item

    === "ordered list"
        1. first ordered item
        2. second ordered item
        3. third ordered item
```
!!! example 
    === "content unordered list"
        * ==first unordered item==
        * second unordered item
        * third unordered item

    === "ordered list"
        1. first ordered item
        2. second ordered item
        3. third ordered item
   
## Data Tables
### Configuration
```yaml
markdown_extensions:
  - tables
```
### Usage
```markdown title="data table"
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       |     Fetch resource  |
| `PUT`       |  Update resource |
| `DELETE`    |      Delete resource |
```

| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       |    Fetch resource  |
| `PUT`       | Update resource |
| `DELETE`    |     Delete resource |

place`:`on the left, both side or right to align a specific column
***
## Footnote
### Configuration
```yaml
markdown_extensions:
  - footnotes
```
```markdown title="text with footnote"
this is footnote1[^1], and this is footnote2[^2]
[^1]: I am xiaokang
[^2]: I am practicing some extensions for mkdown
```
this is footnote1[^1], and this is footnote2[^2]
[^1]: I am xiaokang
[^2]: I am practicing some extensions for mkdown, this test footnote be paragraphs what will happen. nothing happen and everything is normal. nothing change.
*** 
## formatting
### Configuration
```yaml
markdown_extensions:
  - pymdownx.critic
  - pymdownx.caret
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.tilde
```
### Usage 
```markdown title="text with highlighting"
* ==This was marked==
* ^^This was inserted^^
* ~~This was deleted~~
```

* ==This was marked==
* ^^This was inserted^^
* ~~This was deleted~~

#### sub and superscripts
```markdown title="text with sub and superscripts"
- H~2~O
- A^T^A
```

- H~2~O
- A^T^A
***
## Lists
### configuration
```yaml
markdown_extensions:
  - def_list
  - pymdownx.tasklist:
      custom_checkbox: true
```
### Usage
#### using unordered lists
```markdown title="unordered list"
* unordered list item1
* unordered list item2
    * nested unordered list item1
    * nested unordered list item2
* unordered list item3
```

* unordered list item1
* unordered list item2
    * nested unordered list item1
    * nested unordered list item2
* unordered list item3
#### using ordered lists

```markdown title="ordered list"
1. first ordered item
2. second ordered item
    1. first nested item
    2. second nested item
        1. nested nested item
        2. second nested nested item
3. third ordered item
```

1. first ordered item
2. second ordered item
    1. first nested item
    2. second nested item
        1. nested nested item
        2. second nested nested item
3. third ordered item
#### task lists
```markdown title="task list"
- [x] Lorem ipsum dolor sit amet, consectetur adipiscing elit
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    * [x] In hac habitasse platea dictumst
    * [x] In scelerisque nibh non dolor mollis congue sed et metus
    * [ ] Praesent sed risus massa
- [ ] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque

```

- [x] Lorem ipsum dolor sit amet, consectetur adipiscing elit
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    * [x] In hac habitasse platea dictumst
    * [x] In scelerisque nibh non dolor mollis congue sed et metus
    * [ ] Praesent sed risus massa
- [ ] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque

caution: there need four spaces or a tab for nested item; and there mustn't text in front of list 
***
## MathJax
### Configuration
=== "docs/javascripts/mathjax.js"
    ```js
    window.MathJax = {
    tex: {
        inlineMath: [["\\(", "\\)"]],
        displayMath: [["\\[", "\\]"]],
        processEscapes: true,
        processEnvironments: true
    },
    options: {
        ignoreHtmlClass: ".*|",
        processHtmlClass: "arithmatex"
    }
    };

    document$.subscribe(() => { 
    MathJax.typesetPromise()
    })
    ```
=== "mkdocs.yml"
    ```yaml
    markdown_extensions:
    - pymdownx.arithmatex:
        generic: true

    extra_javascript:
    - javascripts/mathjax.js
    - https://polyfill.io/v3/polyfill.min.js?features=es6
    - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js

    ```
### Usage
```markdown title="mathjax"
$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$
The homomorphism $f$ is injective if and only if its kernel is only the 
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such 
that $f(a)=f(b)$.

```

$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$

The homomorphism $f$ is injective if and only if its kernel is only the 
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such 
that $f(a)=f(b)$.

