---
published: true
---
Over the years I have been setting up many weblogs and CMS sites for people. When WordPress came out and everyone was migrating to it, I also created a blog for myself. I did so with Drupal and few other platforms, but none of those weblogs survived beyond couple of posts. You see the pattern here; the focus has been on technology rather than the content. Some days ago, I got interested in Jekyll and decided to give it a go after many years of no web development. Meanwhile I started writing some notes about typesetting in TeX for a colleague, which looked like a good material for publishing. Seeing a promotion from GoDaddy for $2 domain registration completed the picture. I registered "randomdoctor.com" and started yet another blog. Hopefully this one will last for a while :) I wrote a short [biography of myself](/about) that you may read, or continue with the following notes about setting up the blog.


## Blog  Setup
I used GitHub to host the blog. GitHub Pages is magical in its automatic building of Jekyll websites. I followed the instructions given [in this well written blog post](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/). Afterwards, I installed Jekyll on my MacBook, and started experimenting with it locally. All in all, I liked this exercise very much :). Here are some notes regarding my experience.

- The use of [MarkDown](https://en.wikipedia.org/wiki/Markdown) language for technology/science blogging is awesome. I enjoy its easy and nice typesetting for text, code, and math formulas. 
- Jekyll is many times better than WordPress if you want a simple weblog. It is minimal; The workflow is sophisticated; and you have great control over everything.
- Despite being quick to setup, it is highly customizable and extendible through plugins. 
- DNS setup was not very smooth, but I finally managed to read [this guide](https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site) and configure the apex for "randomdoctor.com".
- Jekyll works like a charm when installed on local machine. You run `bundle exec jekyll serve`; and afterwards every change that you make instantly appears in the browser. This is very helpful while styling a website.
- I did some styling, including changing colors, fonts, and a bit of the template. I summarize some steps that may work as examples for the next amateur :)
    - I started with the default theme `midnight`. The gem package for this is named `jekyll-theme-midnight`, which can be modified in `/Gemfile`.
    - Configuration begins with `/_config.yml` file. Other than usual setup, I added few plugins under `plugins:` section, including `jekyll-email-protect`. This requires adding the gem package `jekyll-email-protect` to `/Gemfile`.
    - You define the colors such as `$bgcolor` in `/_sass/_variables.scss` and apply them in `/style.scss`.
    - I used Adobe Fonts (Typekit) to create font-face css file for serif font Adobe Caslon. I also downloaded the sans-serif font Linux Biolinum into `/fonts` folder and put its font-face css file there. These two css files are imported in `/_sass/_variables.scss`, and variables such as `$body-font` are defined there. You may indeed modify the use of those font variables in `/style.scss` if needed.
    - I added date tag for posts in the index page. Open `/index.html` and add 
    {% raw %} {{ post.date | date: "%B %e, %Y" }}  {% endraw %}
    inside a new div block `<div class="date">` under the title line. I also moved the same tag in `_layouts/post.html` from bottom to the top.


