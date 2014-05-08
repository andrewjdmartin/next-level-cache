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
* Multi-site installations share the cache which means it can grow larger.  Cache resets and prunning for one site on the network will affect all others.  This is because the DB Drop-in initializes and begins caching prior to the loading of the multi-site configuration.  As long as the sites meet the above criteria of being CMS-types sites then it shouldn't be a big deal.
* The cache does not ever expire on it's own, but resets automatically when posts or settings are updated.  This could cause performance issues on sites that are constantly being updated all day, every day.
* There are no configuration options for the plugin.

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