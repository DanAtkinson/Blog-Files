title: How to hack a trusting Windows developer's machine
author: Dan Atkinson
tags: []
categories: []
date: 2017-01-26 22:49:00
---
This is based on a post on [Life Plus Linux](https://lifepluslinux.blogspot.co.uk/2017/01/look-before-you-paste-from-website-to.html) entitled *"Look before you paste from website to terminal"*. It details a very simple but cleverly crafted method of giving the user a seemingly benign string to execute into their Linux terminal window with [CSS](https://en.wikipedia.org/wiki/CSS) used to hide extra commands.

In this instance, the command looked like `ls -lat`. This shows all files in the current directory ordered by date. However, between `ls` and `-lat` was some text, hidden by some fairly simple CSS. When the text is pasted directly into the terminal, did something the user probably didn't expect, or indeed want.

I wondered to myself whether this was possible on Windows and so I set about doing exactly that. Not long after, I came up with the following [example](https://gist.github.com/DanAtkinson/e4e333e1fa40f18a565974481fdced34) which you can try out for yourself.

**Go ahead and copy and paste the below into your command prompt:**

<code style="padding:10px;"><span>dir</span> <span style="color:#EEE;  position:absolute; left:-1000px; top:-1000px; height:0px; z-index:-100; display:inline-block;">&amp;
  cls &amp; echo Haha! You gave me access to your computer! &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking ##                        (10%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking ###                       (20%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking #####                     (33%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking #######                   (40%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking ##########                (50%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking #############             (66%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking #####################     (99%) &amp;
      ping 127.0.0.1 -n 2 &gt; nul &amp;
      cls &amp; echo h4cking #######################   (100%) &amp;
      cls &amp; echo Hacking complete. &amp;
      echo Use GUI interface using visual basic to track my IP &amp;
      ping 127.0.0.1 -n 5 &gt; nul &amp;
      cls 
      dir </span><span>/w /p<br></span></code>

I assure you that ***this*** example is safe and will do no harm to your computer, but you should check the contents of your clipboard just to be sure. Below is how it should look if my Markdown blog doesn't fluff the HTML too much.

![](https://i.imgur.com/XpkoqnJ.gif)

Apart from the fact that your command window started spitting out text you weren't expecting, you might also notice that you didn't have to press enter/return - Windows actually interprets the line breaks as new lines and executes it accordingly. So, unless you examine your clipboard contents first in a text editor like Notepad, you could be executing something that can cause ***very serious damage*** to your machine.

Whilst, that little example above is jokey, it's not difficult to craft yourself with some basic CSS, and then turn it into something far more [malicious](https://en.wikipedia.org/wiki/Fork_bomb). Given that many developers (including myself) use a command prompt with administrative privileges, the possibilities are somewhat worrying.

***And so here, it the rant...***

It's far too easy for a lazy, novice or trusting developer to simply paste code pulled from a website like [Stack Overflow](https://www.stackoverflow.com)\* into a command prompt and execute it without understanding what it could do. Furthermore, Windows offers absolutely **no guidance** whatsoever when it comes to pasting potentially dangerous commands into the prompt.

This is especially true when there are sites like [Chocolatey](https://chocolatey.org/)\** that tell you to do exactly this!

If you run [Cmder](http://cmder.net/) and try to paste the above example in, you'll actually get two warnings, you lucky bugger! The [first](https://i.imgur.com/D5tTktH.png) will let you know that it's been given multi-line contents which will force the command prompt to execute them. The [second](https://i.imgur.com/B7H1pMd.png) informs you that you're pasting a long clipboard entry into the console and executing the command may lock the console. Both should be red flags given that you should have a reasonable idea that the 10-character long sample is actually nearly 1000 characters! In both cases, you can choose to cancel, which would prevent this from happening.

If you're interested, I created a fully-functioning [Plunker](https://plnkr.co/2DrRyq) and [Github Gist](https://gist.github.com/DanAtkinson/e4e333e1fa40f18a565974481fdced34) example which you can try for yourself. And here is the HTML for the `dir /w /p` example.

    <code style="padding:10px;">
      <span>dir</span>
      <!-- Here, you can see that: -->
      <!-- The text colour is the same as my blog background and it's also positioned way off the page. -->
      <span style="color:#EEE; position:absolute; left:-1000px; top:-1000px; height:0px; z-index:-100; display:inline-block;">&amp;
        cls &amp; echo Haha! You gave me access to your computer! &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking ##                        (10%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking ###                       (20%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking #####                     (33%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking #######                   (40%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking ##########                (50%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking #############             (66%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking #####################     (99%) &amp;
        ping 127.0.0.1 -n 2 &gt; nul &amp;
        cls &amp; echo h4cking #######################   (100%) &amp;
        cls &amp; echo Hacking complete. &amp;
        echo Use GUI interface using visual basic to track my IP &amp;
        ping 127.0.0.1 -n 5 &gt; nul &amp;
        cls 
        <br>dir
      </span>
      <span>/w /p<br></span>
    </code>

##### Tl:dr Do not copy/paste commands from websites into your command prompt without examining the clipboard contents FIRST!

\* I singled out Stack Overflow here as an example of a site which developers frequently copy and execute code from. I'm ***not*** suggesting that the Stack Overflow website allows malicious users to craft code samples in such a way as above in order to execute this. That being said, Plunker is often used to provide a more complete answer when HTML, CSS and JS are involved. As shown above, this 'problem' can and will occur on Plunker.

\*\* Full disclosure: I'm a member of the [Chocolatey organisation](https://github.com/orgs/chocolatey/people).