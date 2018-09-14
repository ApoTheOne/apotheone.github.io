---
title: GitPitch
date: 2018-08-01 19:31:27
tags:
---

Live at [GitPitch](https://gitpitch.com/ApoTheOne/gitpresentation)

---

What is GitPitch?  
GitPitch is a markdown presentation service for everyone on Git. You can use it to promote, pitch or present absolutely anything using the tools you already know and love - Markdown + Git.

---

The service introduces a new convention for Git users, called PITCHME.md. The GitPitch server turns PITCHME.md markdown files found within any public or private repo into online and offline, interactive slideshows.

---

Is GitPitch for you?
If you ever find yourself needing to present a concept, design, library, framework, product, service, training materials, or educational course work:

-   To colleagues, clients or customers
-   At meetups or conferences
-   At training events or teaching sessions

---

Then GitPitch is for you.

Simply capture your ideas in Markdown and let GitPitch automatically turn those ideas into compelling, responsive, online and offline slideshow presentations.

---

How does GitPitch work?  
GitPitch presentations are powered by the amazing reveal.js presentation framework. But with GitPitch there is nothing to download. Nothing to install. All you need is your favorite text editor. And an account on GitHub, GitLab, or Bitbucket. Or a self-hosted instance of GitHub Enterprise, GitLab CE, GitBucket, Gitea, or Gogs.

---

```
git add PITCHME.md
git commit -m "My first presentation"
git push
```

---

#### What is Markdown?

Markdown is a text-to-HTML conversion tool for web writers.  
Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML)

---

#### Why?

Markdown == FAST && EASY

HTML's start and closing tags  
 vs  
Simple text

---

Let's try it out  
Use `**bold**` to make text **bold**.  
Use `*italic*` for _italic_.

Use numbers, \*, or - to create lists.
@ul

-   Plain text list item
-   Rich **markdown** list _item_
-   Link [within](https://gitpitch.com) list item
    @ulend

---

Hyperlinks:

```
[Text] (link)
```

OR

```
[Click here to go to google][url]
[url]: gitPresentation
```

[Click here][g]

[g]: README.md

---

Add Code Snippets:

```
const greetingText = 'Hello';
let name = 'Qwerty';
console.log(`{greetingText}, {name}!`);
```

---

Task Lists

-   [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
-   [x] list syntax required (any unordered or ordered list supported)
-   [x] this is a complete item
-   [ ] this is an incomplete item
        If you include a task list in the first comment of an Issue, you will get a handy progress indicator in your issue list. It also works in Pull Requests!

---

Tables
You can create tables by assembling a list of words and dividing them with hyphens - (for the first row), and then separating each column with a pipe |:

---

| First Header                | Second Header                |
| --------------------------- | ---------------------------- |
| Content from cell 1         | Content from cell 2          |
| Content in the first column | Content in the second column |

Would become:

First Header Second Header
Content from cell 1 Content from cell 2
Content in the first column Content in the second column

---

Strikethrough
Any word wrapped with two tildes (like ~~this~~) will appear crossed out.

Emoji
GitHub supports emoji! :sparkles: :camel: :boom: :smile:

---

Add Images:

```
![Logo](http://spark.apache.org/images/spark-logo-trademark.png)
```

![Logo](http://spark.apache.org/images/spark-logo-trademark.png)

---

Add Videos:

![Video](https://www.youtube.com/embed/mkiDkkdGGAQ)

---

Each slideshow presentation is beautifully rendered, fully responsive, and highly interactive with a rich set of features including:

1 Markdown slides  
2 Code and GIST slides  
3 Image and Video slides  
4 Math Notation and Chart slides  
5 Fragment slides

---

Thank you!
