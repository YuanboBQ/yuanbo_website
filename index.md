---
layout: page
title: About me and Blogs!
tagline: Supporting tagline
---
{% include JB/setup %}

一个心理学与计算机的爱好者，比郭敬明高，比博尔特白，比郭德纲帅，比刘欢脖子长，比巩汉林结实，比刘翔痘少，比曾哥唱歌在调，比周杰伦吐字清楚，比布拉德皮特中文说得好……作为一俗人，我喜欢看这些片子：《疯狂的石头》《大话西游之仙履奇缘》《十全九美》《九阴真经》《武林外传》《樱桃小丸子》《士兵突击》《Father and Daughter》《The Danish Poet》《沉静如海》等等。我对美非常没有抵抗力，看到美的东西我就会拼命研究。有时候我很不靠谱，尤其是我发现了一件值得做的事情之后，就会归隐若干天把其它的事撂一边。总的来说，我还是想基于统计做一番事业。

## 博客文章

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## To-Do

This theme is still unfinished. If you'd like to be added as a contributor, [please fork](http://github.com/plusjade/jekyll-bootstrap)!
We need to clean up the themes, make theme usage guides with theme-specific markup examples.


