---
title: Creating Clean Amazon Affiliate Links in WordPress
date: 2011-04-02 00:00:00 -04:00
categories:
- Miscellany
tags:
- Blogging
- PHP
- Wordpress
author: Nathaniel Ward
excerpt: Automatically generate simple, cruft-free Amazon affiliate links in Wordpress.
layout: post
---

One way bloggers can earn incremental income is through affiliate marketing programs, among which [Amazon’s ][1]is perhaps the most popular. Bloggers simply link to Amazon products, adding a special referral code, and they are given credit for the sales they generate.

Generating these tracking codes can be something of a pain. [Amazon’s own utility][2] is clumsy and offers up a long, clunky URL. [Ragaskar’s WordPress plugin][3] aims to fill the void by automatically appending tracking codes to Amazon links in posts, but this can still generate clunky links.

Based on Ragaskar’s plugin, I whipped up the following code:

```php

    add_filter('the_content','filter_amazon_associate_filter');

    add_filter('comment_text','filter_amazon_associate_filter');

    

    function filter_amazon_associate_filter($content) {

        $affiliate_code="YOURCODEHERE";

    

        $content=preg_replace(

            '/http:\/\/[^>]*?amazon.([^\/]*)\/([^>]*?ASIN|gp\/product|exec\/obidos\/tg\/detail\/-|[^>]*?dp)\/([0-9a-zA-Z]{10})[a-zA-Z0-9#\/\*\-\?\&#038;\%\=\,\._;]*/i',

            'http://www.amazon.$1/exec/obidos/ASIN/$3/'.$affiliate_code,

            $content

        );

        return $content;

    }
```

Very simply, this code scans through your posts and comments and replaces ugly Amazon links with somthing like `http://www.amazon.com/exec/obidos/ASIN/B0048EJXCK/nathward-20`.

To add this to your site, simply place the above code in your WordPress template’s `functions.php` file and replace `YOURCODEHERE` with your Amazon affiliate code.

 [1]: https://affiliate-program.amazon.com/
 [2]: https://affiliate-program.amazon.com/gp/associates/network/build-links/individual/main.html
 [3]: http://wordpress.org/extend/plugins/amazon-associate-filter/