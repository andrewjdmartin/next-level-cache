=== Plugin Name ===
Contributors: verysimple
Donate link: http://verysimple.com/products/nlc/
Tags: cache,next level cache,next level shit,up in your grill,db,drop-in,db.php,database cache,db cache,dropin,verysimple
Requires at least: 2.9
Tested up to: 3.9
Stable tag: trunk

Next Level Cache is a plugin that caches database queries to improve performance.

== Description ==

CAUTION: This is a BETA plugin on which I am actively working. If you use this plugin I would be interesting in hearing feedback on the following issues:

* This cache will most likely perform best on sites that are used as a CMS (ie a finite number of pages that are not being constantly updated throughout the day)
* Sites that have a large number of pages which all receive a reasonable amount of views may not experience performance improvement (I don't have an exact number but perhaps a few hundred pages).
* Multi-site installations share the cache which means it can grow larger.  Cache resets and pruning for one site on the network will affect all others.  This is because the DB Drop-in initializes and begins caching prior to the loading of the multi-site configuration.  As long as the sites meet the above criteria of being CMS-types sites then it shouldn't be a big deal.
* The cache does not ever expire on it's own, but resets automatically when posts or settings are updated.  This could cause performance issues on sites that are constantly being updated all day, every day.
* There are no configuration options for the plugin.

= With all these caveats, why the heck would I use this plugin instead of one of the well-known caching plugins?! =

I've tried all of the usual, popular plugins and I didn't find one that worked exactly the way I wanted. I was interested in DB caching (which I've found to be the weakest link of Wordpress performance) but I didn't care about all of the other speed improvements like script/css minification, gzip support and so on because I handle those at the server level.  Next Level Cache does only one thing which is to quietly reduce DB load and try to keep the caching mechanism totally unnoticeable.

There are many ways to cache output. A popular technique is static HTML caching, which is building a page once, saving it as HTML, and then serving that "static" page on subsequent views. This is an excellent technique because the DB is never even hit, but static page caching has it's trade-offs as well. People may see stale data for one thing.  Dealing with dynamic content on a page such as random items, comments and other things is problematic. Another is that pages may be rendered differently for different devices (for example mobile).  One solution to that I have seen is to simply disable the cache for mobile devices or alternate views, which obviously is not an effective caching strategy.

Another issue with static caching is that it requires building each page from scratch and so if your site does not have tons of traffic, your visitors may experience page after page of cache warm-up. When the cache is empty, a page has to be loaded the normal way first and then saved to the cache to "warm" it up. This is a problem with any cache strategy, however Wordpress makes a lot of queries that are shared all pages of the site.  A static HTML cache will warm up the cache for each and every page. Next Level Cache will cache shared queries on the first page, so subsequent pages may be half-way warmed up already even if they haven't been viewed.

Another caching strategy for Wordpress is "object caching" which is caching data that is obtained through the Wordpress Object API. However I found that not enough data is cached this way and there are still way too many DB calls made.  With DB caching these objects are cached anyway.

The point is that there are trade-offs and certain kinds of caching will be appropriate for certain site. The well-known caching plugins are popular for a reason - because they work great for certain purposes. Next Level Cache does things a little differently that I found to work better for my particular needs of using Wordpress as a CMS. I hope it might work for you as well and I appreciate any feedback that you can provide.

= Overview =

Did you know that a fresh, stock WordPress install with the default theme and no plugins will execute over 30 database queries every single time a visitor views the home page?  After installing an feature-rich theme and a few basic plugins WordPress can easily run 100 or more queries on every single page.  This puts a enormous amount of strain on the database server.

Next Level Cache is a lightweight plugin that intercepts DB queries and selectively caches them. A special type of plugin file called a "Drop-in" is included to override Wordpress's default DB functionality. Every page is still generated dynamically, but WordPress is coerced into using cached data for many of the DB calls. This hybrid approach doesn't eliminate all database queries, but keeps them down to a reasonable number (usually between 1 and 5 queries per page, depending on your theme and plugins).

= Features =

* Zero configuration
* Query debugging options

== Installation ==

Automatic Installation:

1. Go to Admin - Plugins - Add New and search for "next level cache"
2. Click the Install Button
3. Click 'Activate'
4. Copy or soft link the included Drop-in file "db.php" in the root of your wp-content directory

Manual Installation:

1. Download next-level-cache.zip
2. Unzip and upload the 'next-level-cache' folder to your '/wp-content/plugins/' directory
3. Activate the plugin through the 'Plugins' menu in WordPress
4. Copy or soft link the included Drop-in file "db.php" in the root of your wp-content directory

== Frequently Asked Questions ==

= 1. What is NLC (Next Level Cache)? =

Next Level Cache is a plugin that caches database queries to improve performance.

= 2. How does the plugin work? =

Wordpress supports a special type of plugin known as a "Drop-in" which allows overriding of the class that controls access to the database.  Next Level Cache intercepts queries and selectively caches them.

= 3. How to I empty the cache =

Updating any page or Wordpress setting will clear the cache (changing the value isn't necessary, just click an update button somewhere).

= 4. Where does Next Level Cache store it's data? =

The cache is stored in the wp_options table and is loaded upfront with one large query instead of many small ones.

= 5. Will this plugin work in combination with other caching plugins? =

I've minimally experimented with a few other caching plugins and Next Level Cache seems to be compatible with them. However, Wordpress only allows one DB.php Drop-in file to be installed at a time. So if the other plugin requires it's own DB Drop-in then you would have to choose one over the other.  Next Level Cache does not make any attempt to automatically copy or alter the DB.php.  If there is a conflicting DB.php file installed then Next Level Cache will simply not do anything except to show a warning notification on the plugin settings page.

= 6. How can I configure or customize the plugin? =

For the moment there are no configuration options, however there will be some options

== Upgrade Notice ==

= 0.0.5 =
* implement cache pruning and stats for cache activity

== Changelog ==

= 0.0.5 =
* implement cache pruning and stats for cache activity

= 0.0.4 =
* initial release