---
layout: post
title:  "My little website now uses WordPress"
categories: site
---
<b>Spoiler alert:</b> it doesn't any more.

My little vanity-website has been through many changes. I’ve found that the way to get the most enjoyment of it and to make sure that it remains active, is to make it easy for me to update and to make sure the design isn’t too strong. This website has had some hideous designs over the years, all of which I thought were beautiful at the time and all of which put me off from ever using it.

I’ve had this very basic design for a little over a year now and **I don’t hate it**. I’ve actually added content which is quite a big deal for me, I usually get cross and redo the entire thing each time I want to add a new project.

However, the blog has been difficult. I first made the decision to point the blog subdomain to [Tumblr](http://blog.steveguntrip.co.uk/). I did this in anticipation of my dinosaur project going viral and causing me a horrendous bandwidth bill; I was right about that, the dinosaur project was hugely popular and if I had hosted all of those photographs on this little server the internet would have certainly [hugged it to death](http://en.wikipedia.org/wiki/Slashdot_effect).

But now I have a popular post on Tumblr and I can never move it or do anything with it. Even though I’ll repost it here, it will forever be stuck on Tumblr. I realise now that I should just be hosting image content on Imgur (or somewhere similar).

I was initially going to spend the evening coding a little bespoke blog tool for myself. Things are quite manic and up in the air at the moment and in those situations a little geeky project is nice. Instead, I decided to finally get to grips with WordPress.

This is a theme I’ve created called Stevecat.

I’ve always been put off of WordPress as I find it quite slow, especially as my website has a lot of content that has no need for WordPress to be in memory, so I’ve replaced the WordPress index.php with my own. This creates the header, design and loads any CSS and JS (this is the major change to the normal WP flow). If the homepage is requested or my own URI analyser can’t find a match (i.e. /photography/), it hands over to wp-header.php which will then either deliver the main blog or analyse the URI itself to deliver a sub-page.

I’ve found WordPress theme creation intimidating in the past; The Loop sounded a little scary and it’s really difficult to find an overview of how it works. I found a [site](https://www.siteground.com/tutorials/wordpress/wordpress_create_theme.htm) detailing the file structure and how to create a very basic theme and from there, using the [WordPress Codex](https://codex.wordpress.org/), I figured the rest out. I already had the design from the main site, so it was just a case of styling the blog elements, sidebar and creating any features I wanted
.
I decided to make use of tags. The sidebar uses get_tags() to grab all current tags and the individual posts show their specific tags using wp_get_post_tags(get_the_ID()) and looping through that. I’ve also made a few headers using the is_tag() and is_date() conditions and a “Return to blog” will appear on tag, date or single views. The site was already responsive and it only took an additional six lines of CSS to make the blog act the same!

All in all, I’m happy to have gone from zero WordPress knowledge at 9pm to making my first post on my own custom theme at 1am. I will probably fiddle more and maybe even play with creating some plugins that could be useful for people.

I’m hoping I can have dinner now but I reckon I’ll probably be fixing whatever errors pop up now that I’ve made my fanfare-post.
