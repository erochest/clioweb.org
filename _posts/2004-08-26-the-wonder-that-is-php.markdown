---
date: '2004-08-26 15:54:05'
layout: post
slug: the-wonder-that-is-php
status: publish
title: The Wonder that is PHP
wordpress_id: '9'

---

I've fallen in love with PHP. Even though I only know a little, and use even less, it seems like a very powerful tool for web development. Besides the PHP that's included in [Wordpress](http://wordpress.org), I've also used the `<?php include()>` feature in the header, the site navigation, and the footer. The site navigation is especially cool, because it chooses which navigation link is "selected". See below:




> `<?php if($PHP_SELF=="/index.php") { echo '<li><a href="/index.php" class="selected">Home</a>'; } else{ echo '<li><a href="/index.php">Home</a></li>'; } ?>`




This snippet is for the index page. If the page you're on is the index page, then it will "echo" the first part, with the `class="selected"` and put a little arrow image on the left. If you're on another page, like say the contact page, then it will just make the home link a regular link without the arrow. There's a script just like this one for each of my main pages. I'm sure I didn't explain this too well, mostly because I don't know it well enough to explain it properly. Many thanks to Marty Andolino for writing this, and to Rikk Mulligan for pointing it out to me and expaining to me how it works.
  *[PHP]: Hypertext Pre-Processor
