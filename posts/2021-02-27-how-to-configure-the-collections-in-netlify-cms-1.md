---
layout: layouts/post.njk
title: How to configure the collections in Netlify CMS
description: A brief overview of how collections work and how to fix it for the
  Eleventy blog template
date: 2021-02-27T20:28:50.162Z
tags: Tutorial
---
Using the Netlify CMS for the first time was very confusing. I didn't really know what I was doing and I basically just copied the code from the setup tutorial and hoped it work. In particular, I had no idea what it was actually doing or how to change the template in the CMS to match the pre-existing posts format. After a bit of playing around and reading the docs, I think I've figured it out.

The content displayed in the CMS is defined in the `collections` field of the `config.yml` file. These collections are then displayed in the left sidebar of the Content page of the editor UI. This is what the `collections` setting in my `config.yml` looks like:

```
collections:
    name: "posts" 
    label: "Posts" 
    folder: "posts/" 
    create: true 
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}" 
    fields: # The fields for each document, usually in front matter`
        - {label: "Layout", name: "layout", widget: "hidden", default: "layouts/post.njk"}
        - {label: "Title", name: "title", widget: "string"}
        - {label: "Description", name: "description", widget: "string"}
        - {label: "Publish Date", name: "date", widget: "datetime"}
        - {label: "Tags", name: "tags", widget: "string"}
        - {label: "Body", name: "body", widget: "markdown"}
```