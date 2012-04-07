---
date: '2008-10-11 19:30:50'
layout: post
slug: part-four-front-end-development
status: publish
title: 'Part Four: Front-End Development'
wordpress_id: '28'
tags:
- CHNM
- CSS
- HTML
- JavaScript
- Omeka
- PHP
- Web Development
- WordPress
---

Front-end development involves codes that deals with how things are displayed in a browser. This includes HTML, CSS, and JavaScript. Back-end development, in contrast, refers to the development on the code and technologies that the end-user hardly ever sees. This includes PHP, MySQL, XML, Perl, or any other languages that affects how a site works underneath. Back-end development usually involves database interaction and programming, installing and modifying any number of content management systems. The lines between front and back-end work can be very blurry. For the purposes of this article I'll be talking about front-end development only; Back-end develop is equally important, but also warrants more space for discussion--perhaps even another post series!

Front-end development usually can't take place until decisions have been made about the front-end design (discussed in the last post). At [CHNM](http://chnm.gmu.edu), we've build projects where there was one designer, one front-end developer, and one back-end developer, all working in concert to build a project. And, we've built projects that had one person doing all three. Whatever your staffing situation, here's what goes on in this phase:

  * Photoshop mockups are translated into working HTML/CSS mockups
  * Naming conventions in code are set and documented.
  * Design is tested in browsers.
  * HTML templates are then used to build out the final version of the site (in CMS, or as static pages)

## 1) Create HTML Mockups

To facilitate faster development of HTML mockups, I've created a "starter kit" that is essentially a directory with a basic file structure and pre-coded files for HTML, CSS, and JavaScript. You can download my [example starter kit](/downloads/starter.zip) and take a look at how I set it up. The file structure I generally follow is:

```
    /starter/
    	index.php
    	/c/
    		screen.css
    		print.css
    		...any other <abbr>CSS</abbr> files.
    
    	/j/
    		global.js
    		...any other necessary javascript files or libraries.
    
    	/i/
    		...any necessary images for the design. Background
                    images, logos, etc.
```

My HTML and CSS files also have a basic structure I usually follow. My starter HTML file looks like this:

```
    <body>
    	<div id="skiplink" class="hide"><a href="#content">Skip to Content</a></div>
    	<div id="wrap">
    		<div id="header">
    			<h1 id="site-title">Site Title</h1>
    			<ul id="sitenav" class="navigation">
    				<li><a href="#">Lorem</a></li>
    				<li><a href="#">Ipsum</a></li>
    				<li><a href="#">Dolor</a></li>
    				<li><a href="#">Amet</a></li>
    			</ul>
    		</div>
    		<div id="content">
    			<div id="primary"></div>
    			<div id="secondary"></div>
    			<div id="tertiary"></div>
    		</div>
    		<div id="footer">
    			<p>Footer Info</p>
    		</div>
    	</div>
```

This is a good point for the front-end developer to come up with (and stick to!) naming conventions for various ids and classes used throughout the site. I've found that using #primary, #secondary, #tertiary, and so on, gets me thinking less about the presentation of that content, and more about its relative importance. Its not a perfect solution, and sometimes I have to ditch this convention in favor of others, but the point is that you have a convention, and you follow it throughout your site.

My CSS file starts with generic styling of basic elements, followed by any global classes I use throughout the site, then moves on to each section of the page (wrap, header, content, footer). Here's an example:

```
    /* == Reset == */
    @import url("reset.css");
    
    /* == Generic styles ======== */
    body {font:62.5% "Helvetica Neue", Helvetica, Arial, sans-serif; color:#222;
        background:#fff;}
    
    /* Headings */
    h1 {font-size:3.6em; line-height:1em; margin-bottom:1em;}
    h2 {font-size:3em; line-height:1em; margin-bottom:1em;}
    h3 {font-size:1.8em; line-height:1em; margin-bottom:1em; font-weight:bold;}
    h4 {font-size:1.5em; line-height:1.2em; margin-bottom:1.2em; font-weight:bold;}
    h5 {font-size:1.5em; line-height:1.2em; margin-bottom:1.2em; color: #999;}
    h6 {font-size:1.2em; line-height:1.5em; margin-bottom:1.5em; font-weight:bold;}
    
    /* Links */
    a:link {}
    a:visited {}
    a:focus {}
    a:hover {}
    a:active {}
    
    h1 a, h2 a, h3 a {text-decoration:none;}
    
    /* Misc Elements */
    p,ul,ol,dl,blockquote,address {font-size:1.2em; line-height:1.5em; 
        margin-bottom:1.5em;}
    ul {}
    ol {}
    dl {}
    blockquote {}
    address {}
    
    /* == Wrap == */
    #wrap {width:882px; margin:0 auto;}
    
    /* == Header == */
    #header {}
    
    /* == Content == */
    #content {}
    
    	#primary {}
    	#secondary {}
    	#tertiary {}
    
    /* == Footer == */
    #footer {}
```

As you can see, I start out with some things already filled in (typography--font sizes, line-heights, margins), but some things I leave blank and fill in as I go. This is a personal preference, and I change things around from project to project. But this gets me started.

Using this starter kit, I build out HTML/CSS mockups based on the Photoshop mockups created in the last stage. I generally try to build the same pages that were presented to the project team, and strive to make the HTML version look and feel the same as the color mockups as much as possible. But, its important to remember than a design will never completely look the same in Photoshop and in the browser, and will rarely look the same across different browsers. Striving for pixel perfection to the color mockup across browsers, while sounding noble, ends up being a significant waste of time. The goal should be to make the HTML mockups look like the color mockups as much as possible, but also be usable and useful to the end-user. If one section of a site is bigger by one point on one browser, its probably not worth the time to figure out why.  If its using a completely different typeface, then maybe you have a problem.

## 2) Test Mockups in Browsers

The advantage to doing HTML mockups before diving straight into the entire project is that you can 1) do the prototypes quickly, and 2) test the design in browsers before doing all the work to apply the design to dynamic content. At CHNM, we test in the following browsers:

**Windows**

  * Firefox 3
  * Internet Explorer 6
  * Internet Explorer 7
  * Opera

**Macintosh**

  * Firefox 3
  * Opera
  * Safari

I try my best to test every single page, but I usually miss a few pages, so its good to have one or more people test your site on different browsers. When taking notes, I generally make a list that starts with the browse in quest, then a subheadings with the title and path of the page I'm looking at, and then specific issues for that page. For example:

> ### Internet Explorer 6
>
> #### Items Browse page - example.com/items/browse/
>
> * Items content extends past page boundary
> * Individual item titles not showing up
> * Layout for main column and sidebar is broken (aren't showing up side by side)

This allows me to first focus on a particular browser, then focus on a particular page (and know what its URL is), and get those issues working for that browser. I've found that a lot of issues on one page are similar to other pages, so solving it once usually fixes it globally. But, I like to note each problem on each page, because there may be other issues at play.

## 3) Applying to Dynamic Content

After you've completed HTML mockups and tested them in various browser, its time to use them when working with dynamic content. If your project is just going to be static pages, simply keep building out HTML pages as you did for the HTML mockups. But if you'll be working with data in a database, now's the time to learn a little bit about the kind of code you'll be using to pull data into your HTML dynamically.

One piece of advice I can give on back-end development is: avoid reinventing the wheel as much as possible. That is to say, look to see if there are solutions available to make your development process easier before deciding to write something from scratch. With [Omeka](http://omeka.org), the project team met early on and explored options for doing the kinds of things with wanted to do with other content management systems ([Drupal](http://drupal.org), [WordPress](http://wordpress.org)), and determined that the problems we wanted to solve required that we write something new. But even then, we did completely start from scratch. We use a PHP framework, [Zend](http://zend.com), as the base for the application, which makes development much more rapid and stable than if we wrote our own framework from scratch.

The data needs for a project can greatly impact the kinds of technology a project will need to use (or can't use). I recommend that the development person/team make a list of any available content management systems, frameworks, and libraries and rate their qualities based on what your project needs to accomplish. For example, at CHNM we've use Drupal, Omeka, and WordPress for different projects based on their needs. We build Omeka, and we think it rocks, but its not right for every site. Neither is Drupal or WordPress, or any other CMS out there.

When I'm choosing a CMS or library or framework, I like to give myself some time to figure out how I would build the site with each one (if possible), determine which is most efficient and maintainable, and then go with the best choice. Some examples:

**Content Management Systems**

  * [Drupal](http://drupal.org)
  * [ExpressionEngine](http://expressionengine.com)
  * [Joomla](http://joomla.org)
  * [Moodle](http://moodle.org)
  * [Omeka](http://omeka.org)
  * [WordPress](http://wordpress.org)

**PHP Frameworks**

  * [CakePHP](http://cakephp.org)
  * [CodeIgniter](http://codeigniter.com)
  * [Symfony](http://symfony-project.org)
  * [Zend](http://zend.com)

**JavaScript frameworks and libraries**

  * [Dojo](http://dojotoolkit.org)
  * [jQuery](http://jquery.com)
  * [Prototype](http://prototypejs.org)
  * [MooTools](http://mootools.net)
  * [Yahoo UI](http://developer.yahoo.com/yui/)

Many of you will be developing projects that rely on some kind of content management system that employs a theme API to pull content from a database. WordPress and Omeka are two such systems that I've worked with very closely, but other such as Drupal, [Joomla](http://joomla.org), and [ExpressionEngine](http://expressionengine.com) are others that you might be using. One of the final jobs of the front-end developer is take the static HTML mockups she/he has created, and apply the HTML structure to the template files used in one of those systems. In some cases your front-end and back-end developer (if they're two different people) will need to work together to make sure their individual contributions to the project can work together. A back-end developer, for example, may need to explain to a front-end developer about how certain theme API calls work and where to put them in the HTML template, while a front-end developer may need to explain to a back-end developer than the content a plugin generates needs to be in an unordered list with a specific `id` and `class` attribute. In short, there's a point where the two types of development merge, usually a few weeks before the site launches.

This will also be a time when the front-end developer will have to account for specific kinds of content not covered in the HTML mockups. This will happen as content for the site gradually gets added to the database, and all the sections and pages for the site outlined in the site map emerge. You may have to add some specific styles for certain content. But the work you've already done will make this process much faster. Once you've done all of this, maybe run some more browser testing for anything new you've added since the HTML mockups, your site should be ready for launch!

  *[XML]: Extensible Markup Language
  *[API]: Application Programming Interface
  *[URL]: Uniform Resource Locator
  *[CHNM]: Center for History and New Media
  *[HTML]: Hypertext Markup Language
  *[PHP]: Hypertext Pre-Processor
  *[CSS]: Cascading Style Sheets
