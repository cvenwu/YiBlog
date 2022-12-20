---
title: demo
date: 2022-12-09 14:42:30
tags:
updated:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

[参考](https://butterfly.js.org/posts/39b121ef/#Block-Quote)
```

{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}


{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}

{% blockquote David Levithan, Wide Awake %}
Do not just seek happiness for yourself. Seek happiness for all. Through kindness. Through mercy.
{% endblockquote %}


{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io
{% endblockquote %}


{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
Every interaction is both precious and an opportunity to delight.
{% endblockquote %}


{% codeblock [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}

{% codeblock %}
alert('Hello World!');
{% endcodeblock %}


{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}


{% codeblock _.compact http://underscorejs.org/#compact Underscore.js %}
_.compact([0, 1, false, 2, '', 3]);
=> [1, 2, 3]
{% endcodeblock %}


{% pullquote [class] %}
content
{% endpullquote %}

{% pullquote left %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
{% endpullquote %}


{% pullquote right %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
{% endpullquote %}


{% jsfiddle shorttag [tabs] [skin] [width] [height] %}

{% jsfiddle ccWP7 %}

{% gist gist_id [filename] %}

{% gist 996818 %}


{% iframe url [width] [height] %}

{% iframe 'https://butterfly.js.org/' 100% 300px %}

{% img [class names] /path/to/image [width] [height] '"title text" "alt text"' %}


{% link text url [external] [title] %}

{% include_code [title] [lang:language] [from:line] [to:line] path/to/file %}


{% include_code lang:javascript test.js %}


{% include_code lang:javascript from:5 to:8 test.js %}


{% include_code lang:javascript from:5 test.js %}


{% include_code lang:javascript to:8 test.js %}


{% youtube video_id %}


{% vimeo video_id [width] [height] %}


{% post_path filename %}
{% post_link filename [title] [escape] %}


{% post_link 標籤外掛-Tag-Plugins 'How to use <b> tag in title' %}


{% post_link 標籤外掛-Tag-Plugins '<b>bold</b> custom title' false %}


{% asset_path filename %}
{% asset_img filename [title] %}
{% asset_link filename [title] [escape] %}


{% raw %}
content
{% endraw %}
```