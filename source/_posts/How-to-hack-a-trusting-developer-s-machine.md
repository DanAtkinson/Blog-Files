title: How to hack a trusting Windows developer's machine
author: Dan Atkinson
date: 2017-01-26 22:49:14
tags:
---
This is based on a post on [Life Plus Linux](https://lifepluslinux.blogspot.co.uk/2017/01/look-before-you-paste-from-website-to.html) entitled `Look before you paste from website to terminal`.

The post detailed a very simple but cleverly crafted method of giving the user a seemingly benign string to execute into their Linux terminal window.

In this instance, the command looked like `ls -lat`. This shows all files in the current directory ordered by date. However, between `ls` and `-lat` was some hidden text which, when pasted directly into the terminal, did something quite interesting.

![](https://i.imgur.com/wAsCWqP.gif)

I wondered to myself whether this was possible on Windows and so I set about doing exactly that. About 5 minutes later (yes, it wasn't that hard) I came up with the following [example](https://gist.github.com/DanAtkinson/e4e333e1fa40f18a565974481fdced34) which you can try out for yourself. Go ahead and copy and paste the below code sample into your command prompt!

<code style="padding:10px;"><span>dir</span> <span style="color:#EEE;position:absolute;left:-1000px;top:-1000px;height:0px;z-index:-100;display:inline-block;">&amp;
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

I promise you that ***this*** example is benign, but you should check the contents of your clipboard just to be sure.

Below is how it should look if Markdown doesn't fluff the HTML too much.

![](http://i.imgur.com/XpkoqnJ.gif)

My blog uses Markdown, so the markup might be a bit iffy, so I created a fully-working  [Github Gist](https://gist.github.com/DanAtkinson/e4e333e1fa40f18a565974481fdced34) example.

### Tl;dr Always check the command being pasted is actually the command you're expecting to execute