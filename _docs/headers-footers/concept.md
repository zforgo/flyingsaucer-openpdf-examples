---
title: Concept
category: Headers / Footers
order: 1
---

FlyingSaucer basically supports CSS 2.1, however some parts of the CSS 3 specification is also supported. 
Like [page-margin-boxes](https://www.w3.org/TR/css-page-3/#margin-boxes){:target="_blank"}
and [running elements](https://www.w3.org/TR/css-gcpm-3/#running-headers-and-footers){:target="_blank"}.

{:refdef: style="text-align: center;"}
![image page-margin boxes](/images/css_page_margin_boxes.png)
{: refdef}

> In this example page header is located at the top-center in the document

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <style>
        @page {
            size: letter portrait;
            margin: 2.5cm 1cm;
            @top-center {
                content: element(header);
            }
        }

        header {
            position: running(header);
            padding-bottom: 5pt;
        }
    </style>
    <title>FlyingSaucer OpenPDF example</title>

    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
</head>
<body>
<header>
    Header content
</header>
<!-- all other content -->
</body>
</html>
```
