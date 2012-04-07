---
date: '2004-09-27 21:51:48'
layout: post
slug: photolog-for-clioweb
status: publish
title: Photolog for ClioWeb
wordpress_id: '23'

---

I've been working on a few different photolog systems, and I think I've found a fairly useful one (for my purposes anyways). It uses a slightly modified version of the [PHP Slide Show](http://www.zinkwazi.com/pages.php?page_name=scripts) from [zinkwazi.com](http://www.zinkwazi.com). Basically, this script calls images from a directory or folder instead of putting them in a database like MySQL. Right now I only have one album called [Dragon's Tooth](http://www.clioweb.org/photolog/dragons_tooth/index.php) with two pictures of a hike Jill and I took to Dragon's Tooth, an awesome outcropping of rocks near the [Appalachian Trail](http://www.appalachiantrail.org/) in the Roanoke, VA area.




What's really nice about this script is that I can simply put new images in the individual album's folder and it will automatically add a link to that new image. Essentially, the directory for my photoalbums will look like this:


{% img /i/photodir.jpg Directory of ClioWeb's photolog %}


In the `photolog` folder there is a folder titled `inc`, which stands for "includes". In the `inc` folder there is a file called `album.php`. This file contains the scripts for the albums. I then have an `index.php` page for each individual album, which I place in the respective album folders. I "include" the `album.php` using the `include()` PHP function. The `index.html` file is identical in each individual album, but it calls up the photos located alongside it in the album folder.




I'm sure there's a much better way to do a photo album, but this method seems pretty simple to me. I'm not sure if I've explained it properly, but I'm actually happy that I understand what I've done, moreso than usual. I'm still debating the size of images, which I have to do manually instead of declaring `width` and `height` in the script. Right now I'm resizing the images so that their width (whether portrait or landscape) is 500px. I'm sure I'll tinker with that in the near-future.




**Update 09/27/04:** My album for [Dragon's Tooth](http://www.clioweb.org/photolog/dragons_tooth/) now has 12 images, with one of my [favorite pictures of Jill](http://www.clioweb.org/photolog/dragons_tooth/index.php?directory=.&currentPic=4).
