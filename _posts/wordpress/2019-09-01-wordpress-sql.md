---
layout: post
title: "Wordpress Cheat Sheet"
tags: ["Wordpress", "cheat sheet"]
---

## Domain change upadte

Replace the old domain `__SEARCH__` with a new one `__REPLACE__`

```sql
UPDATE wp_options SET option_value = replace(option_value, '__SEARCH__', '__REPLACE__');
UPDATE wp_posts SET guid = replace(guid, '__SEARCH__','__REPLACE__');
UPDATE wp_posts SET post_content = replace(post_content, '__SEARCH__', '__REPLACE__');
UPDATE wp_postmeta SET meta_value = replace(meta_value, '__SEARCH__', '__REPLACE__');
```

update wp_users set user_pass = MD5('wAXMRV05x8iMaAoW5BsNewa') where ID = 3;

## Theme Files

- **style.css** – This is your theme’s stylesheet file.
- **index.php** – This is the main body template for your theme.
- **header.php** – Is the <head> section of your site (metadata, stylesheet).
- **sidebar.php** – Everything in you sidebar goes in this file, like widgets, categories, additional menus, search form, etc.
- **footer.php** – This file contains your footer information, such as copyright details, widgets, and social icons.
- **single.php** – This file displays just one post.
- **page.php** – When you create a page on your site, this is the template responsible.
- **comments.php** – This file is responsible for displaying comments.
- **404.php** – When visitors try to visit a page on your site that doesn’t exist, this file will general an error page.
- **functions.php** – This file is where you can place special functions. We always recommend creating a child theme rather than edit this file directly.
- **archive.php** – Display an archive with this file so visitors to your site can go way back when and read your Hello World! post.
- **search.php** – Help your visitors search your site with this page.
- **searchform.php** – Display a search form for your visitors with this template file.

## Template Include Tags

- **get_header()** – Includes the header.php file
- **get_sidebar()** – Includes the sidebar.php file
- **get_footer()** – Includes the footer.php file
- **comments_template()** – Includes your comments

##  Template Header/Bloginfo Tags

These are functions you'll find in your theme’s header.php file, though you’ll also find them in other theme files:

```php
bloginfo('name'); – The title of your site, or blog name
bloginfo('url'); – Your site’s URL
bloginfo('stylesheet_url'); – Link to your themes’s stylesheet file
bloginfo('template_url'); – Location of your site’s theme file
bloginfo('description'); – Displays the tagline of your blog as set in Settings > General.
bloginfo('atom_url'); – Link to your site’s atom URL
bloginfo('rss2_url'); – RSS feed URL for your site
bloginfo('pingback_url'); – Pingback URL for your site
bloginfo('version'); – WordPress version number
bloginfo('html_type'); – The HTML version your site is using
site_url(); – The root URL for your site
get_stylesheet_directory(); – Location of your stylesheet folder
wp_title(); – Title of a specific page
```

## Template Tags

These tags can be used across all of your template files, such as index.php or page.php, making it easy to display specific information anywhere you want on your site:

```php
the_content(); – Displays the content of a post
the_excerpt(); – Displays the excerpt used in posts
the_title(); – Title of the specific post
the_permalink() – Link of a specific post
the_category(', ') – Category of a specific post
the_author(); – Author of a specific post
the_ID(); – ID of a specific post
edit_post_link(); – Edit link for a post
next_post_link(' %link ') – URL of the next page
previous_post_link('%link') – URL of the previous page
get_links_list(); – Lists all links in blogroll
wp_list_pages(); – Lists all pages
wp_get_archives() – List archive for the site
wp_list_cats(); – Lists all categories
get_calendar(); – Displays the built-in calendar
wp_register(); – Displays register link
wp_loginout(); – Displays login/logout link only to registered users
```

### The Loop

The Loop is the default mechanism in WordPress for displaying all of your posts.

```php
    if ( have_posts() ) :
        while ( have_posts() ) :
            the_post();
            //
            // Post Content here
            //
        endwhile; // end while
    endif; // end if
```

- next_post_link() – A link to the post published chronologically after the current post
- previous_post_link() – A link to the post published chronologically before the current post
- the_category() – The category or categories associated with the post or page being viewed
- the_author() – The author of the post or page
- the_content() – The main content for a post or page
- the_excerpt() – The first 55 words of a post's main content followed by an ellipsis (…) or read more link that goes to the full post. You may also use the "Excerpt" field of a post to customize the length of a particular excerpt.
- the_ID() – The ID for the post or page
- the_meta() – The custom fields associated with the post or page
- the_shortlink() – A link to the page or post using the URL of the site and the ID of the post or page
- the_tags() – The tag or tags associated with the post
- the_title() – The title of the post or page
- the_time() – The time or date for the post or page. This can be customized using standard php date function formatting.
You can also use conditional tags, such as:

- `is_home()` – Returns true if the current page is the homepage
- `is_admin()` – Returns true if an administrator is logged in and visiting the site
- `is_single()` – Returns true if the page is currently displaying a single post
- `is_page()` – Returns true if the page is currently displaying a single page
- `is_page_template()` – Can be used to determine if a page is using a specific template, for example: is_page_template('about-page.php')
- `is_category()` – Returns true if page or post has the specified category, for example is_category('news')
- `is_tag()` – Returns true if a page or post has the specified tag
- `is_author()` – Returns true if a specific author is logged in and visiting the site
- `is_search()` – Returns true if the current page is a search results page
- `is_404()` – Returns true if the current page does not exist
- `has_excerpt()` – Returns true if the post or page has an excerpt