---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: id_PPA
title: Visual Representation of Path Planning Algorithms

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Tanay Ranjan
# multiple category is not supported
category: Projects
# multiple tag entries are possible
tags: [Arduino, Processing IDE, HCSR-04, HC-05]
# thumbnail image for post
img: ":PPA/ppa.jpg"
# disable comments on this page
#comments_disable: true

# publish date
date: 2021-09-16 08:11:06 +0900

# seo
# if not specified, date will be used.
#meta_modify_date: 2022-02-10 08:11:06 +0900
# check the meta_common_description in _data/owner/[language].yml
#meta_description: ""

# optional
# please use the "image_viewer_on" below to enable image viewer for individual pages or posts (_posts/ or [language]/_posts folders).
# image viewer can be enabled or disabled for all posts using the "image_viewer_posts: true" setting in _data/conf/main.yml.
#image_viewer_on: true
# please use the "image_lazy_loader_on" below to enable image lazy loader for individual pages or posts (_posts/ or [language]/_posts folders).
# image lazy loader can be enabled or disabled for all posts using the "image_lazy_loader_posts: true" setting in _data/conf/main.yml.
#image_lazy_loader_on: true
# exclude from on site search
#on_site_search_exclude: true
# exclude from search engines
#search_engine_exclude: true
# to disable this page, simply set published: false or delete this file
# published: false
---

# Aim

To implement Path Planning Algorithms for gaining better experience about it.

# Methodology

The application was written in **Python**, and the library used for designing GUI was **PyGame Library**.

There are 3 files:

- **nodes.py :** Contains class which has suitable functions for creating and operating the GUI, like changing status of nodes or getting status of nodes, etc.

- **dijkstra.py :** Contains function for appyling Dikstra's Path Planning Algorithm.

- **main.py :** This file uses functions and classes from above 2 files, and execute them in mannered way to get the desired outcome.

# How to Operate
1) Run main.py, a grid will appear

2) Hold `s` and left-click a cell in the grid using mouse. It will create a starting point

3) Hold `e` and left-click a cell in the grid using mouse. It will create a ending point

4) Hold `o` and left-click a cell in the grid using mouse. It will create obstacles

5) Now press enter, it will solve grid automatically using Dijkstra's Algorithm

![ice_video_20210925-232819.gif](:PPA/ice_video_20210925-232819.gif)

# [GITHUB Code](https://github.com/tanayranjan/Grid-based-Visual-Representation-of-Path-Planning-Algorithm)


