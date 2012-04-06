---
date: '2006-08-24 18:44:46'
layout: post
slug: listing-pages-with-wordpress
status: publish
title: Listing Pages with WordPress
wordpress_id: '394'
tags:
- code
- PHP
- Projects
- WordPress
---

For you [WordPress](http://wordpress.org) geeks out there: I've recently had the need to list the child pages of a particular page **in addition to** listing those same pages once you visit a child page. In this case, I only have **one level of child pages**. So, my page structure looked like this:



	
  * Main Page

	
    * Subpage One

	
    * Subpage Two

	
    * Subpage Three





You'd want to list the same subpages on _both_ the Main Page and the respective subpages. I came up with a simple solution. First, we need to query the post to get its information. So I set up a PHP variable `$page` and set it equal to `$wp_query->post;`. Then a create another variable called `$parent_id` and do a database query to get the ID of the `$page` variable's `post_parent`. Of course, if `$parent_id` is empty, then that means the page has no parent, and is thus a Main Page. So, for this case, I throw in a simple `if` check that will set an empty `$parent_id` to the page's ID, which is found using `$post->ID`. The full script for finding this info, which I put in the `<head>`, is:



	
  1. <?php

	
  2.    $page = $wp_query->post;

	
  3.    $parent_id = $wpdb->get_var("SELECT ID FROM $wpdb->posts WHERE ID = '$page->post_parent;'");

	
  4.    if(!$parent_id) $parent_id = $post->ID;

	
  5. ?>


**Then**, to actually generate the HTML for the page list, I use the following code in the body of my page template:



	
  1. <?php if(wp_list_pages("child_of=".$parent_id."&echo=0")): ?>

	
  2.    <ul id="subnav">

	
  3.        <?php

        
  4.            wp_list_pages("title_li=&child_of=".$parent_id."&depth=1");

        
  5.        ?>

	
  6.    </ul>

	
  7. <?php endif; ?>


In a nutshell, the second part of the script does two things. First, an `if` statement checks to see if there are in fact subpages for the page's value for `$parent_id`. That's the `<?php if(wp_list_pages("child_of=".$parent_id."&echo=0")): ?>` line. So, if a page doesn't have subpages, it won't generate the unordered list. Remember, if the page is a Main Page, `$parent_id` is the page's ID (see the explanation above). Second, if the first check goes through, then the script will generate the list of pages using the `wp_list_pages()` WordPress template function, using the `$parent_id` in its argument for `child_of`. For more info on how the `wp_list_pages()` works, see the WordPress Codex page [Template Tags/WP List Pages](http://codex.wordpress.org/Template_Tags/wp_list_pages).

There might be better solutions for this kind of problem, but I thought I'd share it and see if there are ways to improve the scripts. It's working pretty well for me, and I think there are multiple ways to use this kind of page query to make page-specific additions to your site. I do need to come up with a solution for multiple levels of pages (two or more levels deep). If anyone has thoughts on that, please leave a comment!
