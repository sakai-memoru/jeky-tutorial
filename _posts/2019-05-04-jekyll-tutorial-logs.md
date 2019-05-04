---
title: 2019-05-04-jekyll-tutorial-logs
layout: template
---
# 2019-05-04-jekyll-tutorial-logs

## *** overview
- Operating logs with jekyll tutorial

## *** reference
- 30分のチュートリアルでJekyllを理解する 
  - http://melborne.github.io/2012/05/13/first-step-of-jekyll/

## *** environment
### ** working directory
```
(base) g:\workspace\jekyll>mkdir jeky-tutorial
(base) g:\workspace\jekyll>cd jeky-tutorial
```

### ** modules
```
(base) g:\workspace\jekyll\jeky-tutorial>ruby --version
ruby 2.6.3p62 (2019-04-16 revision 67580) [x64-mingw32]

(base) g:\workspace\jekyll\jeky-tutorial>bundler --version
Bundler version 2.0.1

(base) g:\workspace\jekyll\jeky-tutorial>jekyll --version
jekyll 3.8.5
```

## *** git repos

#### * git init and generate .gitignore file by gibo(boiler plate tools)
```
(base) g:\workspace\jekyll\jeky-tutorial>git init
Initialized empty Git repository in g:/workspace/jekyll/jeky-tutorial/.git/

(base) g:\workspace\jekyll\jeky-tutorial>gibo dump vim jekyll > .gitignore

(base) g:\workspace\jekyll\jeky-tutorial>type .gitignore
### vim

# Swap
[._]*.s[a-v][a-z]
[._]*.sw[a-p]
[._]s[a-v][a-z]
[._]sw[a-p]

# Session
Session.vim

# Temporary
.netrwhist
*~
# Auto-generated tag files
tags
# Persistent undo
[._]*.un~


### jekyll

_site/
.sass-cache/
.jekyll-cache/
.jekyll-metadata
```

#### * create README.md
```
(base) g:\workspace\jekyll\jeky-tutorial>vim README.md

(base) g:\workspace\jekyll\jeky-tutorial>type README.md
# jeky-tutorial

## overview
- Repos for operation logs for jekyll's tutorial.

// --- end of README --- //
```

## *** logs

### ** 1. first step：hello jekyll

#### * create index.md

```
(base) g:\workspace\jekyll\jeky-tutorial>vim index.md

(base) g:\workspace\jekyll\jeky-tutorial>type index.md
---
title: 1905-Jekyll-tutorial-logs
---
# 1905-Jekyll-tutorial-logs

// --- end of markdown --- //
```

#### * execute `jekyll serve`
- To stop server , press ctrl-c.

```
(base) g:\workspace\jekyll\jeky-tutorial>jekyll serve
Configuration file: none
            Source: g:/workspace/jekyll/jeky-tutorial
       Destination: g:/workspace/jekyll/jeky-tutorial/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.068 seconds.
 Auto-regeneration: enabled for 'g:/workspace/jekyll/jeky-tutorial'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

[![Image from Gyazo](https://i.gyazo.com/503b1d035fd3d9de4345469d8057829b.png)](https://gyazo.com/503b1d035fd3d9de4345469d8057829b)

```
(base) g:\workspace\jekyll\jeky-tutorial>tree /F
Folder PATH listing for volume Users
Volume serial number is 04A1-7D2F
G:.
│  index.md
│  README.md
│
└─_site
        index.html
        README.md
```
- root配下にあるindex.mdを対象に、_site配下にhtmlが生成される。
- 変換の対象とするには、`YAML Front-Matter`が設定されている必要がある。
- rootのREADME.mdは、 `YAML Front-Matter` がないので、 _site配下にそのままコピーされる。変換の対象とならない。

#### * git commit
```
(base) g:\workspace\jekyll\jeky-tutorial>git add .

(base) g:\workspace\jekyll\jeky-tutorial>git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   .gitignore
        new file:   README.md
        new file:   index.md

(base) g:\workspace\jekyll\jeky-tutorial>git commit -m "first commit"
[master (root-commit) fa455f8] first commit
 3 files changed, 41 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 index.md

(base) g:\workspace\jekyll\jeky-tutorial>git remote add origin https://github.com/sakai-memoru/jeky-tutorial.git

(base) g:\workspace\jekyll\jeky-tutorial>git push -u origin master
fatal: AggregateException encountered.
   One or more errors occurred.
Username for 'https://github.com': sakai-memoru
Password for 'https://sakai-memoru@github.com':
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 614 bytes | 0 bytes/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To https://github.com/sakai-memoru/jeky-tutorial.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

(base) g:\workspace\jekyll\jeky-tutorial>
```

### ** 2. second step: apply layout template
#### * template for html layout

- view gerated html of index.html

```
(base) g:\workspace\jekyll\jeky-tutorial>cd _site

(base) g:\workspace\jekyll\jeky-tutorial\_site>type index.html
<h1 id="1905-jekyll-tutorial-logs">1905-Jekyll-tutorial-logs</h1>

<p>// --- end of markdown --- //</p>
```

- create template layout

```
(base) G:\workspace\jekyll\jeky-tutorial>mkdir _layouts
(base) G:\workspace\jekyll\jeky-tutorial>cd _layouts
(base) G:\workspace\jekyll\jeky-tutorial\_layouts>gvim template.html

(base) G:\workspace\jekyll\jeky-tutorial\_layouts>type template.html
<!DOCTYPE html>
<head>
  <meta http-equiv="Content-type" content="text/html; charset=utf-8">
  <title>{{ page.title }}</title>
</head>
<body>
  {{ content }}
  <p>- rendered with layout template -</p>
</body>
```
- set layout using config into markdown file in YAML Front-Matter.
```
(base) G:\workspace\jekyll\jeky-tutorial>vim index.md

(base) G:\workspace\jekyll\jeky-tutorial>type index.md
---
title: 1905-Jekyll-tutorial-logs
layout: template
---
# 1905-Jekyll-tutorial-logs

// --- end of markdown --- //
```

#### * execute `jekyll build`
```
(base) G:\workspace\jekyll\jeky-tutorial>jekyll build
Configuration file: none
            Source: G:/workspace/jekyll/jeky-tutorial
       Destination: G:/workspace/jekyll/jeky-tutorial/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.177 seconds.
 Auto-regeneration: disabled. Use --watch to enable.
```


[![Image from Gyazo](https://i.gyazo.com/e8dea73e01cf46024452428b0937d1d3.png)](https://gyazo.com/e8dea73e01cf46024452428b0937d1d3)

```
(base) g:\workspace\jekyll\jeky-tutorial\_site>type index.html
<!DOCTYPE html>
<head>
  <meta http-equiv="Content-type" content="text/html; charset=utf-8">
  <title>1905-Jekyll-tutorial-logs</title>
</head>
<body>
  <h1 id="1905-jekyll-tutorial-logs">1905-Jekyll-tutorial-logs</h1>

<p>// --- end of markdown --- //</p>

  <p>- rendered with layout template -</p>
</body>

```

### ** 3. third step : post blog with markdown
#### * create post file

```
(base) g:\workspace\jekyll\jeky-tutorial>mkdir _posts

(base) g:\workspace\jekyll\jeky-tutorial>cd _posts

(base) g:\workspace\jekyll\jeky-tutorial\_posts>gvim 2019-05-04-jekyll-tutorial-logs.md

(base) g:\workspace\jekyll\jeky-tutorial\_posts>dir
 Volume in drive G is Users
 Volume Serial Number is 04A1-7D2F

 Directory of g:\workspace\jekyll\jeky-tutorial\_posts

05/04/2019  10:31 AM    <DIR>          .
05/04/2019  10:31 AM    <DIR>          ..
05/04/2019  10:31 AM               541 .2019-05-04-jekyll-tutorial-logs.md.un~
05/04/2019  10:31 AM             6,583 2019-05-04-jekyll-tutorial-logs.md
               2 File(s)          7,124 bytes
               2 Dir(s)  40,309,084,160 bytes free

(base) g:\workspace\jekyll\jeky-tutorial\_posts>
```

- tree
```
(base) g:\workspace\jekyll\jeky-tutorial>jekyll build
Configuration file: g:/workspace/jekyll/jeky-tutorial/_config.yml
            Source: g:/workspace/jekyll/jeky-tutorial
       Destination: g:/workspace/jekyll/jeky-tutorial/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 1.25 seconds.
 Auto-regeneration: disabled. Use --watch to enable.

(base) g:\workspace\jekyll\jeky-tutorial>tree /F
Folder PATH listing for volume Users
Volume serial number is 04A1-7D2F
G:.
│  .gitignore
│  index.md
│  README.md
│  _config.yml
│
├─_layouts
│      template.html
│
├─_posts
│      2019-05-04-jekyll-tutorial-logs.md
│
└─_site
    │  index.html
    │  README.md
    │
    └─2019
        └─05
            └─04
                    jekyll-tutorial-logs.html
```

[![Image from Gyazo](https://i.gyazo.com/741ba09e1bd8d5e855fd07055c6d71d6.png)](https://gyazo.com/741ba09e1bd8d5e855fd07055c6d71d6)

// --- end of markdown --- //