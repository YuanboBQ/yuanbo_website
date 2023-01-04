---
title: Citation Style Language (CSL)学习笔记
author: yuanbo
date: 2017-08-05
slug:  csl-notebook
category:   
tags: 
---

最近，试着在 markdown 中进行论文写作，发现可以用 pandoc 进行文献插入工作，而 pandoc(包括 Zotero)进行参考文献的引文样式管理采用的是 csl 引文样式（相当于Endnote采用*.ens样式），因此需要对CSL有一些了解，能够根据期刊的需要自行定义引文及参考书目的样式。

引文样式语言（Citation Style Language ，简称CSL）是一种XML格式的，用于规范行文中的引用、注释及参考书目的格式化语言。

## CSL Style Structure

所有独立的CSL样式都具有相同的基本结构，它们的cs:style中有5种可能的子元素，每个子元素的作用叙述如下：

```
cs:info
该子元素必须作为 cs:style的首个子元素。它包含了描述样式的元数据（样式的名称，样式的唯一的识别码以及样式的作者等）
cs:citation
该元素也是必须的，用来描述文内引用或注释的格式化结构
cs:bibliography (可选)
该元素为可选，用以描述参考书目的格式化结构
cs:macro (宏，可选)
样式可以包含一个或多个cs:macro元素。宏允许重复使用格式化命令，因此有利于保持样式的简洁及易于维护。
cs:locale (区域，可选)
样式可以包含一个或多个 cs:locale 元素。这些元素允许样式基于不同的区域，对默认的区域化数据（术语，日期格式，格式化选项）进行重写。通过 locale 可以实现多语言（比如中英文）混合的参考文献插入和样式管理。

```

后面更详细地介绍上面几个元素。

### info

cs:info 元素包含了样式的所有元数据，它的许多元素借鉴了。虽然它对引用如何格式化没有影响，不过对于要在公共空间传播的样式，完整且准确的元数据无疑非常重要。下面是 cs:info元素的一个例子，再往上是对所有可能包含的元素进行详解。

```
<info>
 <title>Style Title</title>
 <id>http://www.zotero.org/styles/style-title</id>
 <link href="http://www.zotero.org/styles/style-title" rel="self"/>
 <author>
  <name>Author Name</name>
  <email>name@domain.com</email>
  <uri>http://www.domain.com/name</uri>
 </author>
 <category citation-format="author-date"/>
 <category field="zoology"/>
 <updated>2008-10-29T21:01:24+00:00</updated>
 <summary>Style for Some Journal</summary>
 <rights>This work is licensed under a Creative Commons
         Attribution-Share Alike 3.0 Unported License
         http://creativecommons.org/licenses/by-sa/3.0/</rights>
</info>
```

### citation

主要是用来规范参考文献在正文中的样式。

```
  <citation>
    <option name="collapse" value="citation-number"/>
    <sort>
      <key variable="citation-number"/>
    </sort>
    <layout prefix="(" suffix=")" delimiter="; ">
      <text variable="citation-number"/>
    </layout>
  </citation>
```

### bibliography

主要是用来规范文后的参考文献目录。

```
<bibliography>
    <option name="second-field-align" value="true"/>
    <layout>
      <text variable="citation-number" suffix=". "/>
      <text macro="author"/>
      <text macro="title" suffix=". "/>
      <choose>
	<if type="book">
	  <text macro="edition" prefix=" " suffix=" "/>
	  <text macro="publisher" prefix=" " suffix="."/>
	</if>
	<else-if type="chapter">
	  <group prefix=" " suffix=". ">
	    <text term="in" suffix=": " text-case="capitalize-first"/>
	    <text macro="editor"/>
	    <text variable="container-title"/>
	  </group>
	  <text macro="publisher" prefix=" "/>
	  <text variable="page" prefix=" p. " suffix="."/>
	</else-if>
	<else>
	  <text variable="container-title" suffix=" " form="short"/>
	  <text macro="date" suffix=";"/>
	  <text variable="volume"/>
	  <text variable="issue" prefix="(" suffix=")"/>
	  <text variable="page" prefix=":" suffix="."/>
	</else>
      </choose>

          </layout>  
</bibliography>
```

引文格式的差异通常会很小，你可以找一个类似的格式，只需要做些许改动，就可以得到你想要的格式。 一般情况下，你只需要改动参考文献目录中的标点符号，各个项目（作者，题目，年份等）的位置就可以了。

在 Zotero 中，分别以prefix, suffix 和 (group) delimiter属性来标识。例如，下列改动将会将卷号由格式(9)变动为[9]。

可以将`<text variable="issue" prefix="(" suffix=")"/>` 改为 `<text variable="issue" prefix="[" suffix="]"/>`。

当一篇引文的作者有多个的时候，常常需要显示 et al. 的缩写，这需要一个option参数。这个设置在CSL 0.8.1 和 1.0 中有所不同。


In CSL 1.0, the same options - and several new ones - exist, but they are not listed separately, but included in the <citation> and <bibliography> lines, e.g.
```
<citation et-al-min="4" et-al-use-first="1" disambiguate-add-year-suffix="true" disambiguate-add-names="true">
```

##  中文混排

在Zotero首选项-引用-样式中已经预装了很多样式，导出参考文献时在word-zotero-document preference中也可以设置导出参考文献的格式。 
另外在 http://editor.citationstyles.org/about/ 可以下载需要的样式，网站提供了search by name, search by example, visual editor和code editor等功能，可以方便搜索样式和修改样式。 

写中文论文时，不可避免地会涉及到中文参考文献混排的问题，之前在 endnote 中很难完美的解决这个问题。但是现在在 Zotero 中可以解决这个问题了。能够实现中英文参考文献混排，得归功于CSL-M格式中可以指定的<layout>与其locale属性。原本在CSL 1.0.1语言标准中并没有详细介绍<layout>，是CSL-M扩充了CSL 1.0.1之后才有这<layout>等功能，而Zotero使用的是CSL-M。<layout>是使用于设定文中引用的<citation>与文后参考文献的<bibliography>所使用的标签。<layout>里面可以设定locale属性，例如<layout locale=”zh- cn”>。locale属性会参考书目本身的“语言”(language)栏位。我参考了这个 [blog](http://blog.pulipuli.info/2014/08/zoteroapa-zotero-citation-style-apa.html)，并在作者提供的一份 [csl 样式](https://raw.githubusercontent.com/pulipulichen/blogger/master/project/zotero/apa_zh_pulipuli.csl)上进行了修改，目前可以解决中文混排的问题。

修改 csl 涉及的主要的 code 如下：

```
<bibliography hanging-indent="true"      
              et-al-min="8"       
              et-al-use-first="6"       
              et-al-use-last="true"       
              entry-spacing="0"       
              line-spacing="1.5">       
  <sort>       
    <key macro="chinese-sort" sort="ascending"/>       
    <key macro="author"/>       
    <key macro="issued-sort" sort="ascending"/>       
    <key macro="title"/>       
  </sort>       
  
  <!-- 中文的格式 -->       
  <layout locale="zh-tw">       
    <text macro="chinese-bibliography"/>       
  </layout>       
  <layout locale="zh-cn">       
    <text macro="chinese-bibliography"/>       
  </layout>       
  <layout locale="zh-Hant">       
    <text macro="chinese-bibliography"/>       
  </layout>       
  <layout locale="Chinese">       
    <text macro="chinese-bibliography"/>       
  </layout>       
  <layout locale="chi">       
    <text macro="chinese-bibliography"/>       
  </layout>       
      
  <!-- 英文的格式 -->

    
  <layout>      
     
    <group suffix=".">       
      <group delimiter=". ">       
        <text macro="author"/>       
        <text macro="issued"/>       
        <text macro="title" prefix=" "/>       
        <text macro="container"/>       
      </group>       
      <text macro="locators"/>       
      <group delimiter=", " prefix=". ">       
        <text macro="event"/>       
        <text macro="publisher"/>       
      </group>       
    </group>       
    <text macro="access" prefix=" "/>       
  </layout>       
</bibliography>

```


----
## CSL Style Structure

All CSL styles share the same basic structure: only five different XML elements can be nested directly in the style root element: info, citation, bibliography, macro and terms. 

* info: contains metadata describing the style (name of the style, authors of the style, etc)   
* citation: describes how in-text citations should be formatted      
* bibliography: describes how bibliographies should be formatted   
* macro: allows for reuse of formatting instructions, allowing for more compact styles   
* terms: allows for the modification of locale-specific strings (e.g. “edited by” can be changed in “ed. by”)  

### info

### citation
The cs:citation element describes the formatting of citations, which consist of one or more references (“cites”) to bibliographic sources. Citations appear in the form of either in-text citations (in the author (e.g. “[Doe]”), author-date (“[Doe 1999]”), label (“[doe99]”) or number (“[1]”) format) or notes. The required cs:layout child element describes what, and how, bibliographic data should be included in the citations (see Layout). cs:layout may be preceded by a cs:sort element, which can be used to specify how cites within a citation should be sorted (see Sorting). The cs:citation element may carry attributes for Citation-specific Options and Inheritable Name Options. An example of a cs:citation element:
```
<citation>
  <sort>
    <key variable="citation-number"/>
  </sort>
  <layout>
    <text variable="citation-number"/>
  </layout>
</citation>
```

### bibliography
The cs:bibliography element describes the formatting of bibliographies, which list one or more bibliographic sources. The required cs:layout child element describes how each bibliographic entry should be formatted. cs:layout may be preceded by a cs:sort element, which can be used to specify how references within the bibliography should be sorted (see Sorting). The cs:bibliography element may carry attributes for Bibliography-specific Options and Inheritable Name Options. An example of a cs:bibliography element:
```
<bibliography>
  <sort>
    <key macro="author"/>
  </sort>
  <layout>
    <group delimiter=". ">
      <text macro="author"/>
      <text variable="title"/>
    </group>
  </layout>
</bibliography>
```
### Locale
Localization data, by default drawn from the “locales-xx-XX.xml” locale files, may be redefined or supplemented with cs:locale elements, which should be placed directly after the cs:info element.

The value of the optional xml:lang attribute on cs:locale, which must be set to an xsd:language locale code, determines which languages or language dialects are affected (see Locale Fallback).

See Terms, Localized Date Formats and Localized Options for further details on the use of cs:locale.

```
<style>
  <locale xml:lang="en">
    <terms>
      <term name="editortranslator" form="short">
        <single>ed. &amp; trans.</single>
        <multiple>eds. &amp; trans.</multiple>
      </term>
    </terms>
  </locale>
</style>
```


### Macros

A list of macro definitions is usually included between the info and citation sections. These are sort of like subroutines that can be called later in the description to make similar styles for parts. Effective use of macros is a key to making good styles. Ideally, in fact, the main layout sections for the citation and bibliography should be quite simple, and simply call a series of macro

### What do these elements do?

The required cs:info element fulfills the same function in independent styles as it does in dependent styles: it stores the style metadata.
The optional cs:locale elements can be used to overwrite the locale data from the locale files.
The optional cs:macro elements can be used to store CSL code for use by cs:citation, cs:bibliography, or other cs:macro elements.
The required cs:citation element defines the format of citations.
The optional cs:bibliography element defines the format of the bibliography.


How were we able to define this format? First, the structure of cs:bibliography is very similar to that of cs:citation, but here cs:layout defines the format of each individual bibliographic entry. In addition to the “author” and “issued-year” macro, the bibliographic entries also show each item’s “title” and “container-title” (for journal articles, the “container-title” is the title of the journal), the “volume” and “issue” in which the article was printed, and the pages (“page”) on which the article appeared. 



# 参考资料
http://docs.citationstyles.org/en/stable/specification.html  
http://blog.sina.com.cn/s/blog_565e747c0101537z.html  
http://blog.pulipuli.info/2014/08/zoteroapa-zotero-citation-style-apa.html