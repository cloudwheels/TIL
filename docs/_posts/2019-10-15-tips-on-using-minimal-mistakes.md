---
tags:
  - jekyll
  - websites
categories:
  - development
excerpt: >-
    Tips on using the minimal mistakes jekyll theme this
    website is built with
---

Some useful tips here, courtesy of [Jack Dougherty](https://jackdougherty.org/site-info/)

Copyright (c) 2019 Jack Dougherty, used under [MIT License](https://raw.githubusercontent.com/JackDougherty/jack-site/master/LICENSE)

## Formatting Guide

### Link types
- Visible link uses angle brackets <http://google.com>
- [Embedded link: place text in brackets, URL in parentheses](http://google.com)
- But an embedded link to an internal page or post on this site requires the full URL

### Footnote
Write the main text and insert a bracketed footnote symbol with a unique number or keyword.[^keyword] Then somewhere else in the main text, write the same bracketed footnote symbol and number/keyword, followed by a colon, and the footnote text.

[^keyword]: Here's the footnote text.

### Markdown image with pre-slash pathname (no baseurl because custom domain), actual size, but no caption
![root image caption](../assets/images/sample-300x200.jpg)

### [Liquid templating](https://jekyllrb.com/docs/liquid/) image in root no-slash images  
{% include figure image_path="../assets/images/sample-300x200.jpg" alt="sample image" caption="here's the sample image" %}

### Liquid image in root no-slash aligned with caption
{% include figure image_path="../assets/images/sample-300x200.jpg" alt="sample image" caption="sample caption" %}{: .align-right}
This sample text demonstrates the wrap-around feature with aligned images. This sample text demonstrates the wrap-around feature with aligned images. This sample text demonstrates the wrap-around feature with aligned images. This sample text demonstrates the wrap-around feature with aligned images. This sample text demonstrates the wrap-around feature with aligned images.

### HTML iframe, with quote marks around with and height, whether percentages or pixels
Code:
```html
<iframe src="https://jackdougherty.youcanbook.me/" width="100%" height="600px"></iframe>
```
Demo:
<iframe src="https://jackdougherty.youcanbook.me/" width="100%" height="600px"></iframe>

### YouTube embed
Code:
{% raw %}
```markdown
{% include video id="3sK7-g0otGM" provider="youtube" %}
```
{% endraw %}

Demo:
{% include video id="3sK7-g0otGM" provider="youtube" %}

### Redirect
I modified config.yml to accept jekyll-redirect-from plugin for GitHub Pages, but have only succeeded with the redirect_to option. See <https://github.com/jekyll/jekyll-redirect-from#redirect-to>



