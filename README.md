sivers.org
==========

My [sivers.org](http://sivers.org/) site.

A 2013 rewrite, moving content from database to static files.

## How it works:

### Writing:

I write my stuff in plain text files in one of the content/{blog,books,pages,presentations,tweets}/ directories.

* The date is in the filename.
* The URI for final publishing is in the filename.
* The title is in the first line of the file.
* Any other metadata needed is at the top.
* The rest is the content body, often written in HTML.

### Templates:

Plain erb Ruby templates are in templates/

Shared header and footer for the whole site.

Much of it is just hard-coded HTML.  (After all these years, I think it's easier to maintain than systems that hide the HTML.)

### Merging:

A Ruby script goes through all the content directories and reads the files.

* It starts an array for the collection of content in each subdirectory.
* It knows how to get the metadata needed for the different types and templates.
* It parses each file, gets the metadata, merges it into the template, and writes it to disk.
* Afterwards, it uses the collection array to merge with the index template, and writes that to disk.
* Finally, it uses all the collections to write the home page, which shows the newest additions of various types.

### Styling:

Styling made by @extend'ing in the SCSS file, instead of adding HTML attributes.

### Serving:

Nginx serves the final static site from the site/ directory.

Nginx passes certain paths by proxy to the dynamic Sinatra server, for dynamic pages, in [50web](https://github.com/50pop/50web)

## Multi-lingual thoughts:

Languages: en, fr, es, pt, zh, ja

What gets translated:

* content/blog
* content/pages (including home)
* template/header.erb will need variable for masthead

What changes in my merging:

* for each langcode, it:
* checks for
