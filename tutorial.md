---
layout: base
title: Tutorial Jekyll
---

### 0. Requirements

```
$ ruby    --version 2.5.1
$ gem     --version 2.7.6
$ bundler --version 1.16.1
```

### 1. Create directory

```shell
git init tutorialjekyll
cd tutorialjekyll
```

### 2. Create Gemfile

```shell
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

### 3. Install gems

```shell
bundler install --path=vendor/bundler
Fetching gem metadata from https://rubygems.org/............
Fetching version metadata from https://rubygems.org/...
Fetching dependency metadata from https://rubygems.org/..
Resolving dependencies...
```

### 4. Run server

#### 4.1 `_config.yml` setup

```yml
# Mandatory
repository: mathforprogramming/mathforprogramming.github.io

# Some optional configs
encoding: UTF-8
highlighter: rouge
markdown: kramdown
kramdown:
  input: GFM
  hard_wrap: false

# ...
```

#### 4.2 Run server

```shell
bundler exec jekyll serve
```


### 5. Render basic page

#### 5.1 Create `_layouts/base.html`

```html
<!-- [_layouts/base.html] Begin -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>mathforprogramming | {{page.title}}</title>

    <!-- GENERATED JEKYLL CSS -->
    <link rel="stylesheet" href="/assets/css/style.css"/>

    <!-- MATHJAX LIBRARY CONFIG -->
    <script>
    // Config mathjax - @doc http://docs.mathjax.org/en/latest/configuration.html#using-plain-javascript - 12.01.18
    window.MathJax = {
        tex2jax: {
            inlineMath: [["$","$"], ["\\(","\\)"]],
            processEscapes: true
        }  
    };
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-MML-AM_CHTML"></script>

</head>
<body>
<div class="container-lg px-3 my-5 markdown-body">

    <h1> mathforprogramming | {{page.title}}</h1>

    <!-- [_layouts/base.html] Content begin -->
{ content }
    <!-- [_layouts/base.html] Content end -->

</div>
</body>
</html>
<!-- [_layouts/base.html] End  -->
```

#### 5.2 Create page/basic.html

```md
---
layout: base
title: Basic page example
---
<h1> Page 1</h1>

# hei
## hei
### hei
#### hei
##### hei
```


### 6. Code highlighting


```md
---
layout: base
title: Different code examples
---

#### Javasript code example

    ```javascript
    function hei() {    
        window.addEventListener(e => console.log(e); 
    }

    ```

<br>

#### Python code example

    ```python
    def myfunction(a, b):
        a = a + b + b + b + b**5
        return a + b
    ```

<br>

#### C++ code example

    ```cpp

    int main() {
        std::cout << "Hello world\n";
    }

    ```
```


### 7. Mathjax example

```md
---
layout: base
title: Mathjax example
---


$$\begin{pmatrix} & 1 & 2 & 3 & 4 & 5 & 6 \\
1 & x & x & x & x & x & x \\
2 & x & x & x & x & x & x \\
3 & x & x & x & x & x & x \\
4 & x & x & x & x & x & x \\
5 & x & x & x & x & x & x \\
6 & x & x & x & x & x & x\end{pmatrix}$$
```


### 8. Video include example

#### 8.1 Create `_includes/video.html`

```html

<!-- begin _includes/video.html -->
<!-- include.id = { include.id} -->
<!-- include.url = { include.url} -->

<div class="expand">

  <input id="video{  include.id }button1" 
         style="display: block;" 
         type="image" 
         src="/img/play.png" 
         height="25" 
         width="25"/>

  <input id="video{  include.id }button2" 
         style="display: none;" 
         type="image" 
         src="/img/minus.png" 
         height="25" 
         width="25"/>   

</div>

<iframe id="insertvideo{  include.id }" 
        style="display: none;" 
        width="660" 
        height="380" 
        src="" 
        frameborder="0" 
        allowfullscreen>
</iframe>

<script>
    
window.addEventListener('load', () => {

    let video     = document.getElementById('insertvideo{  include.id }');
    let videobtn1 = document.getElementById('video{  include.id }button1');
    let videobtn2 = document.getElementById('video{  include.id }button2');

    videobtn1.addEventListener('click', (function () {
        return function () {
            video.setAttribute('src', "{  include.url }");
            video.style.display = 'block';
            videobtn1.style.display = 'none';
            videobtn2.style.display = 'block';
        }
    })());

    videobtn2.addEventListener('click', (function () {
        return function () {
            video.style.display = 'none';
            videobtn1.style.display = 'block';
            videobtn2.style.display = 'none';
            video.setAttribute('src', '');
        }
    })());
});
</script>

<!-- end _includes/video.html -->
```

#### 7.2 Include from example

```
---
layout: base
title: Video include example
---

%  include video.html
        id="01"
        url="https://www.youtube.com/embed/UsnRQJxanVM?rel=0&autoplay=1" %

%  include video.html
        id="02"
        url="https://www.youtube.com/embed/-OTryGzS-G8?rel=0&autoplay=1" %

%  include video.html
        id="03"
        url="https://www.youtube.com/embed/dQw4w9WgXcQ?rel=0&autoplay=1" %


```


#### 7.3 Get png files

```
img/minus.png
img/play.png
```
