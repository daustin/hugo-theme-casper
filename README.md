# CASPERilla theme for hugo
    
Casperilla is a single-column theme for [Hugo](http://gohugo.io/).
Forked from [Vjeantet's Casper Theme](https://github.com/vjeantet/hugo-theme-casper)

theme source: https://github.com/daustin/hugo-theme-casperilla.git

theme demo blog: https://github.com/daustin/hugo-theme-casperilla-demo.git

![Hugo Casperilla Theme Homepage](https://raw.githubusercontent.com/daustin/hugo-theme-casperilla-demo/master/screenshots/homepage.png)

![Hugo Casperilla Theme Section List](https://raw.githubusercontent.com/daustin/hugo-theme-casperilla-demo/master/screenshots/section.png)

![Hugo Casperilla Theme Tag List](https://raw.githubusercontent.com/daustin/hugo-theme-casperilla-demo/master/screenshots/tag.png)


## Features

* Google Analytics (optional)
* Disqus ( can disable comments by content)
* Share buttons on Facebook, Twitter, Google (can disable share by content)
* Big cover image (optional)
* Custom cover by content (optional)
* Tagging
* Pagination
* Menu
* Custom cover, title, description, and content for section list
* Custom cover, title, description for tag list

# Theme usage and asumptions
* The homepage displays a paginated list of contents from the post Section (other contents may be added to main menu, see below)
* Place content for each section in their respective folders
* Content with type 'index' will be included in the home page
* Content with type 'custom_list_content' in each of the section folders will only be included on the section list page
* Cover, Title, Description vars for section and tag lists are set via Scratch in their respective layouts (see below)

# Installation

## Installing this theme

    mkdir themes
    cd themes
    git clone https://github.com/daustin/hugo-theme-casperilla.git casperilla

## Build your website with this theme

    hugo server -t casperilla

# Configuration

**config.toml**

``` toml

BaseUrl= "http://localhost:1313"
LanguageCode= "en-US"
Title= "City Food"
paginate = 5
canonifyurls = true
pluralizelisttitles = false
paginate = 5
DisqusShortname = "YOUR_SHORT_NAME_HERE"
Copyright = "All rights reserved - 2015"
theme = "casperilla"

[params]
  description = "City Food is Tasty"
  cover = "images/index_cover.jpg"
  author = "Guess Who"
  authorlocation = "Philly, PA"
  authorwebsite = "http://github.com"
  bio= "author bio"
  logo = "images/logo.png"
  googleAnalyticsUserID = "UA-79101-12"
  # Optional RSS-Link, if not provided it defaults to the standard index.xml
  RSSLink = "http://feeds.feedburner.com/..." 
  githubName = "daustin"
  twitterName = "daustin"
  # facebookName = ""
  # linkedinName = ""
  # set true if you are not proud of using Hugo (true will hide the footer note "Proudly published with HUGO.....")
  hideHUGOSupport = false

[[menu.main]]
  name = "Main"
  weight = -110
  identifier = "main"
  url = "/"

[[menu.main]]
  name = "New York"
  weight = -100
  identifier = "new_york"
  url = "/new_york"

[[menu.main]]
  name = "Chicago"
  weight = -95
  identifier = "chicago"
  url = "/chicago"

[[menu.main]]
  name = "Philadelphia"
  weight = -90
  identifier = "phila"
  url = "/philadelphia"

```

Example : [config.toml](https://github.com/vjeantet/vjeantet.fr/blob/master/config.toml)

## Multiple authors configuration

In addition to providing data for a single author as shown in the example above, multiple authors
can be configured via data/authors/\*.(yml, toml, json) entries. If the key provided in
.Site.Params.author matched a data/authors/\* entry, it will be used as the default. Overrides
per page can be done by a simple author = other_author_key entry in the front matter. For those
pages where you want to omit the author block completely, a .Params.noauthor entry is also
available.

Example author definition file:

``` yml
name: John Doe
bio: The most uninteresting man in the world.
location: Normal, IL
website: http://example.com
thumbnail: images/john.png

```

Example override author per page file:
``` toml
+++
author = ""
date = "2014-07-11T10:54:24+02:00"
title = ""
...
+++

Contents here

```

## Menu configuration

On top right of the screen, a "Subscribe" button is displayed with a link to the RSS feed.

When you define a menu in the main config file, Then a menu button is displayed instead of the subscribe button
When the use clicks the menu button, a sidebar appears and shows the subscribe button and all items defined in the main config file

> :information_source: If your added a metadata like ```menu="main"``` in a content file metadata, it will also be displayed in the main menu

Example of a menu definition in main config file.


``` toml
[[menu.main]]
  name = "My Blog"
  weight = -120
  identifier = "blog"
  url = "/"

[[menu.main]]
  name = "About me"
  weight = -110
  identifier = "about"
  url = "/about"
  
```

## Metadata on each content file, example

``` toml
+++
author = ""
date = "2014-07-11T10:54:24+02:00"
draft = false
title = "dotScale 2014 as a sketch"
slug = "dotscale-2014-as-a-sketch"
tags = ["event","dotScale","sketchnote"]
image = "images/2014/Jul/titledotscale.png"
comments = true     # set false to hide Disqus comments
share = true        # set false to share buttons
menu = ""           # set "main" to add this content to the main menu
+++

Contents here
```

## Create a section "mysection" with custom vars and content

Set up list content file and content for a first post
```
hugo new -k custom_list_content mysection/list_content.md
hugo new mysection/first_post.md
cp themes/layouts/section/mysection.html ./layouts/section/mysection.html
```

In the layout you can specify custom cover, title, description for mysection list
```
{{ .Scratch.Set "custom_title" "my custom section title" }}
{{ .Scratch.Set "custom_cover" "images/pic.jpg" }}
{{ .Scratch.Set "custom_description" "my custom section description" }}

{{ partial "list.html" . }}

```

The section list will display content from type custom_list_content in the heading, and treat all other types as normal posts
```
+++
date = "2016-04-15T19:41:40-04:00"
draft = false
type = "custom_list_content"
+++

### Mysection list content

```

## Create a taxonomy (tag) layout

Set up tag layout file
```
cp themes/layouts/taxonomy/mytax.html ./layouts/section/tag.html
```

In the layout you can specify custom cover, title, description for tag list. You can see here there is different info depending on what the tag values are.
```
{{ $tax_value := .Title }}

{{ if eq $tax_value "first" }}
{{ .Scratch.Set "custom_title" "my firsts title" }}
{{ .Scratch.Set "custom_cover" "images/pic.jpg" }}
{{ .Scratch.Set "custom_description" "firsts from each section" }}
{{ end }}

{{ if eq $tax_value "second" }}
{{ .Scratch.Set "custom_title" "my seconds title" }}
{{ .Scratch.Set "custom_cover" "images/pic.jpg" }}
{{ .Scratch.Set "custom_description" "seconds from each section" }}
{{ end }}


{{ partial "list.html" . }}

```


## Create new content based with default metadata from this theme
You can easily create a new content with all metadatas used by this theme, using this command 
```
hugo new -t casperilla post/my-post.md
```

# Contact me

[https://github.com/daustin](https://github.com/daustin)
