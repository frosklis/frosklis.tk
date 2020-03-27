---
draft: false
date: 2014-12-08
title: Jekyll is so nice!
tags: Jekyll, web development
---
I have moved my blog from a custom based solution to [jekyll]. What I was using was [appengine] and before that I had used [wordpress].

Wordpress doesn't give you too much control. Of course you can configure it but it is so hard to do, I find PHP a nightmare and Wordpress' API difficult to interact with. It was a pain doing plugins. It has one big advange though: it is easy to use for any user. They have done a great job doing that.

Then I moved to Google's app engine. You can check the blog I have with my girlfriend there, [kmc2]. It is so much nicer to program because you get to use python and you can control absolutely evrything. It is a really powerful tool and simpler to use than [aws]. Managing users and providing a user interface *ala Wordpress* was difficult to program but I learned a lot of python, html, css and javascript during the process. Specially the python part is helping my in my job (I do have one!) as a data scientist, as my scripting abilities have improved a lot.

On to [jekyll]. I am not going to migrate to jekyll my other blog ([kmc2]), at least no any time soon:

- It would be a lot of work.
- I would have to teach my girlfriend how to use it and it is difficult.

It is difficult but so easy at the same time. Provided you know git and are not affraid of command lines, there is nothing new to learn. Right to my workflow is: I (create a new post)[https://jekyllrb.com/docs/posts/] in a plain text file with a text editor (I use [sublime]), add it to the repo and commit it. Done.

There is something goind behind the scene. I created a post-commit hook that takes advantage of the [parse] command line tools so that when I commit the site is generated and uploaded to parse.

My post-commit hook:

<pre><code>#!/bin/bash

echo Generating site with jekyll
cd jekyll
jekyll build --destination ../public
echo Uploading to parse
parse deploy
</code></pre>

Jekyll is so nice!

Update 2019: I now use [hugo], which is even better. Using it already for [kmc2] and here too.

[jekyll]: https://jekyllrb.com/  "jekyll"
[kmc2]: https://www.kmc2.tk/  "km c2"
[aws]: https://aws.amazon.com/ "Amazon Web Services"
[parse]: https://www.parse.com/ "parse"
[sublime]: https://www.sublimetext.com/ "sublime text"
[appengine]: https://cloud.google.com/appengine/ "Google App Engine"
[wordpress]: https://www.wordpress.org/ "Wordpress"
