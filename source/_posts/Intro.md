---
title: Intro, build and host your website for free
date: 2017-09-10 02:09:29
tags: Free Static wesite Hosting, Hexo, Github, Markdown, Continuous Deployment
---

# Build and host your site for free

Welcome to learning developer's notes blog.
I build this blog to share my learnings and solution to challenges I face while coding.

While learning or exploring something new, I usually create notes in a mardown file.
Later, I decided to create blog from these notes so that others can also get some benefit out of it.

---

I had to choose a static site generator for building posts quickly and to figure out what is the best fit for me I went to [StaticGen](https://www.staticgen.com/), [Snipcart](https://snipcart.com/blog/choose-best-static-site-generator), [CreativeBloq](https://www.creativebloq.com/features/10-best-static-site-generators) and few more sites.

In order to create blogs from markdown files I chose [Hexo](https://hexo.io/) as it didn't required me to install anything else apart from a npm package 'hexo-cli', as I already have prerequisite node.js installed in my system.
I could have easily went out for other powerful tools out there but I was too lazy to install something and as it required some setup prior actual work.
Although some of them requires special mentions like:

-   Jekyll(GitHubPages), Hugo for blogging,
-   Gitbook, VuePress for documentation
-   Gatsby, Nuxt for e-commerce websites.

I request you try out the one which suits you the most and do share your experience with us.  
The following content is what I have used to generate my blogs, and for reference one might check [github repo](https://github.com/apotheone/apotheone.github.io)

---

**Now let's start with actual work:**
Do refer [Hexo docs](https://hexo.io/docs)  
First, install hexo-cli:

```bash
npm install -g hexo-cli
```

Go to your project folder or create one:

```bash
mkdir devnotes
cd devnotes
```

Inside that directory, initialize your website:

```bash
hexo init
```

Go through config.yml and update it as per your needs.

Create a new post in your website created in previous step:

```bash
$ hexo new "Intro"
```

Enter the content in markdown.
Refer: [Writing](https://hexo.io/docs/writing.html)

Run your server:

```bash
$ hexo server
```

For more details, go to: [Server](https://hexo.io/docs/server.html)

If you are facing any issues then try debugging:

```bash
hexo --debug
```

Generate static files

```bash
$ hexo generate
```

For more details, refer: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

```bash
$ hexo deploy
```

For more details, refer: [Deployment](https://hexo.io/docs/deployment.html

---

As I am using github as source control, I could have hosted this website on [Gihub pages](https://pages.github.com/) but I wanted to explore [Netlify](https://www.netlify.com/)

I created a website in Netlify and did following configuration:

-   Set the repository URL.
-   Set build command as `hexo deploy --generate`
-   Set the publish directory, ex: public.
-   Set your branch, in my case it was 'master'  
Oh yeah, your site is up and running with continous deployment!  
Basic Tip: You might want to work on a different branch and then create a pull request for merging changes into master beanch.
As soon as your pull request is approved and merged, you website/blog will be automatically updated.
