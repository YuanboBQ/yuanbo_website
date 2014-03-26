---
layout: page
title: About me and Blogs

---
{% include JB/setup %}

**一个心理学与计算机的爱好者，比郭敬明高，比博尔特白，比郭德纲帅，比刘欢脖子长，比巩汉林结实，比刘翔痘少，比曾哥唱歌在调，比周杰伦吐字清楚，比布拉德皮特中文说得好……作为一俗人，我喜欢看这些片子：《疯狂的石头》《大话西游之仙履奇缘》《十全九美》《九阴真经》《武林外传》《樱桃小丸子》《士兵突击》《Father and Daughter》《The Danish Poet》《沉静如海》等等。我对美非常没有抵抗力，看到美的东西我就会拼命研究。有时候我很不靠谱，尤其是我发现了一件值得做的事情之后，就会归隐若干天把其它的事撂一边。总的来说，我还是想基于统计做一番事业。**

**最近，一直在想博客应该写些什么内容，最初是想像日记似的写博客，写了几篇也一直没有贴上来，总觉得这样的博客意义不大。经过一段时间的思考，我觉得这个博客应该记录一些自己学习专业知识以及其他知识的思考，尤其是对这些知识思考和探索的过程。因为，从小学到现在的教育总是让我被动的接受太多，独立思考的却很少，所以导致现在自己的思维能力很差!
因此，我想以后博客的内容主要是关于心理学尤其是认知神经科学方面的专业知识，以及自己比较感兴趣的计算机编程和统计方面的知识。这些知识也大多也是我在Coursera上学习的课程，我希望记录学习这些知识的过程和疑惑，而不仅仅是从网络上搜索到这些知识。以后主要将博客的内容分为以下几类：**

>1. 社会认知神经科学
>2. 生物学以及脑科学
>3. 心理统计 (R software）
>4. 实验编程（Matlab & E-prime）
>5. 文献阅读
>6. 生活絮语

## 博客目录

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## To-Do

This theme is still unfinished. If you'd like to be added as a contributor, [please fork](http://github.com/plusjade/jekyll-bootstrap)!
We need to clean up the themes, make theme usage guides with theme-specific markup examples.


