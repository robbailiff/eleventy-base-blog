---
layout: layouts/post.njk
title: How to configure the collections in Netlify CMS
description: A brief overview of how collections work and how to fix it for the
  Eleventy blog template
date: 2021-02-27T20:28:50.162Z
tags: Tutorial
---
## Introduction

Using the Netlify CMS for the first time was very confusing. I didn't really know what I was doing and I just copied the code from the setup tutorial and hoped it work. In particular, I had no idea what was going on behind the scenes or how to change the template in the CMS user interface (UI) to match the pre-existing posts format. I finally got to the bottom of it after a bit of playing around and reading the Netlify CMS documentation [here](https://www.netlifycms.org/docs/configuration-options).

## Collections

The content displayed in the CMS editor UI is defined in the `collections` field of the `config.yml` file and these collections are then displayed in the left sidebar of the Content page of the editor UI. This is what the `collections` setting in my `config.yml` looks like:

```
collections:
    name: "posts" 
    label: "Posts" 
    folder: "posts/" 
    create: true 
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}"
    preview_path: "posts/{{slug}}" 
    fields: # The fields for each document, usually in front matter`
        - {label: "Layout", name: "layout", widget: "hidden", default: "layouts/post.njk"}
        - {label: "Title", name: "title", widget: "string"}
        - {label: "Description", name: "description", widget: "string"}
        - {label: "Publish Date", name: "date", widget: "datetime"}
        - {label: "Tags", name: "tags", widget: "string"}
        - {label: "Body", name: "body", widget: "markdown"}
```

The first collections option is `name`, which acts as the collection identifier and is used when referenced, such as the collection URL. So in this case the name is posts and the URL of this collections in the Netlify CMS is `admin/collections/posts`. 

Next is `label`, which is simply the name for the collection in admin user interface as shown below. If no value is given it defaults to the `name` value. 

![Picture of the Netlify CMS editor UI](/img/posts/collection-ui-md.png "The Netlify CMS Editor User Interface")

The `folder` option specifies the location of the collection items within the site structure relative to the root.

The `create` option is a boolean value which determines whether a new item in this collection can be created. It is set to false by default.

The `slug` option specifies a template for generating new filenames of the collection document type. A slug is a human readable, unique identifier and in the example below it specifies a template for generating new filenames based on a file's creation date and title field.


```slug: "{{year}}-{{month}}-{{day}}-{{slug}}"```


The first 3 template tags are for the date and the last tag ```{{slug}}``` is a url-safe version of the title field for the file. If the title of the post was "My new post" and it was posted on 21st February 2021, the `slug` option would output `2021-02-25-my-new-post.md` as the name of the new document.

The `preview_path` option is a string denoting where the collection documents are found on the deployed site to allow a preview of the document. If it is not set, the "View Preview" button in the editor UI will take you to the root of the site. In this example `posts/{{slug}}` is the folder location of the collection, followed by the {{slug}} tag. In this case, the ```{{slug}}``` is the **entire** slug for the current entry defined in the `slug` option above, and not just the url-safe identifier.

## Fields

The `fields` option allows the definition of attribute fields that each correspond to a widget in the editor UI. Each of these attribute fields is nested in the fields option and placed within curly braces. In a nutshell, the `fields` option allows the user to build a template, and the field attributes in the `fields` option should be the same as the attributes in the front matter of the corresponding document type. Below is an image which shows the `config.yml` for the editor UI on the left, and a markdown file (a blog post) on the right.

![Comparison of config and posts templates](/img/posts/vs-code-md.png "Comparison of config and posts templates")

Like the `collections` options, the `name` option is the field identifier, and the `label` option is the name for the field in the editor UI. 

The `widget` option determines the data type of the attribute field and the corresponding editor UI. Most of the data types are fairly self explanatory but there are a lot of options. The one that is perhaps less obvious is for the layout field. 

`{label: "Layout", name: "layout", widget: "hidden", default: "layouts/post.njk"}`

The widget option of `hidden`, hides it from view meaning it cannot be changed in the editor UI. The `default` option sets the default value of the field as the path to the template for the document, in this example `layouts/post.njk`.  

There are numerous options for fields and if you want to know more check out the widgets section of the Netlify CMS documentation [here](https://www.netlifycms.org/docs/widgets).

The `required` option is a boolean value which is enabled as true by default, making all fields required. It must be set as false to make a field optional.

**Important!** It is worth noting that order of the fields in your Netlify CMS `config.yml` file determines their order in the editor UI.

## Conclusion

I found going through the code, reading the docs and trying to understand what I had done a really useful exercise, and hopefully this can be useful to someone else too. You view my GitHub repository for the project [here](https://github.com/robbailiff/eleventy-base-blog), and the Netlify CMS documentation [here](https://www.netlifycms.org/docs/configuration-options).