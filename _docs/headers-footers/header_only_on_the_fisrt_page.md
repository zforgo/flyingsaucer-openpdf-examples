---
title: Header only on the first page 
category: Headers / Footers 
order: 4
---
Now, you can use headers and footers in any PDF document. If you can't, please take a look at the [previous example](../header_and_footer)
In some (not so) special cases you have to use header (or footer) only on the first page in the document. This is tricky
a little, but it is easy.

> The important part is the order of the _HTML_ elements.

Using different ```<header>``` and ```<footer>``` tags are available in the _HTML_ document. There are some rules that
you have keep in mind.

* If only one ```<header>``` tag exists in the _HTML_ document, that will be used on all pages as a page header.
* If multiple ```<header>``` tag exists in the _HTML_ document.
    * The first ```<header>``` tag will be attached to the first page header.
    * The second ```<header>``` tag will be attached to all other pages as page header.
    * The last ```<header>``` tag will be attached to the first page header. It must be after the last page content.

It sounds difficult, but it isn't. Let me explain, how it works.

```html
<!DOCTYPE html>
<html lang="en">
<!-- ... -->
<body>
<header>
    Appears on first page header
</header>
<header>
    Appears on all other pages except first and last page if the third header tag exists
</header>
<div class="newPage">First page content</div>
<div class="newPage">Second page content</div>
<div class="newPage">Third page content</div>
<header>
    Appears on the last page header
</header>
<!-- ... -->
</body>
</html>
```
What do you think how could you display header only on the first page? Assumed solution is:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- ... -->
  <style>
    @page {
      size: letter portrait;
      margin: 2.5cm 1cm;
      @top-center {
        content: element(header);
      }
    }

    .newPage {
      page-break-before: always
    }

    header {
      position: running(header);
      padding-bottom: 5pt;
      border-bottom: 1px solid black;
      font-size: 9pt;
      font-weight: 100;
    }

    header.hidden {
      display: none;
    }
  </style>
  <!-- ... -->
</head>
<body>
<header>
    Appears on first page header
</header>
<header class="hidden">
    Appears on all other pages except first and last page if the third header tag exists
</header>
<div class="newPage">First page content</div>
<div class="newPage">Second page content</div>
<div class="newPage">Third page content</div>
<!-- ... -->
</body>
</html>
```
It's a nice try, but it's wrong.
> ```display: none``` CSS rule will be ignored.

Simply you should use
```css
header.hidden {
    border: none;
    content: none;
}
```
instead of
```css
header.hidden {
    display: none;
}
```

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

        body {
            background-color: beige;
        }

        .newPage {
            page-break-before: always
        }

        header {
            position: running(header);
            padding-bottom: 5pt;
            border-bottom: 1px solid black;
            font-size: 9pt;
            font-weight: 100;
        }

        header.nextPages {
            border: none;
            content: none;
        }
    </style>
    <title>FlyingSaucer OpenPDF example</title>

    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
</head>
<body>
<header>
    Visit: <a href="https://flyingsaucer-openpdf-examples.github.io" target="_blank">https://flyingsaucer-openpdf-examples.github.io</a>
    or get involved with contributing guides
    <a href="https://github.com/zforgo/flyingsaucer-openpdf-examples" target="_blank">https://github.com/zforgo/flyingsaucer-openpdf-examples</a>
</header>
<header class="nextPages">
</header>
<div>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ultrices risus eu risus placerat dignissim. Quisque
    tincidunt lectus non rutrum tempor. Proin finibus, urna quis mattis cursus, lacus ex elementum nunc, a volutpat
    metus tellus ac turpis. Nulla nisi ex, ultricies eu magna eu, sagittis pulvinar turpis. Duis eget leo dolor. Vivamus
    elit magna, ultricies a massa non, mattis bibendum velit. Curabitur ac vestibulum nunc. Cras laoreet turpis odio,
    vitae tempus felis pharetra pretium. Pellentesque non cursus ipsum, quis bibendum arcu. Fusce vel sapien varius,
    facilisis risus non, tincidunt mauris.
</div>

<div class="newPage">
    Sed sed sapien sed turpis pulvinar pretium. Orci varius natoque penatibus et magnis dis parturient montes, nascetur
    ridiculus mus. Ut commodo neque non tellus pretium, quis lacinia velit porttitor. Maecenas lorem magna, vulputate
    sed sollicitudin nec, pulvinar a ligula. Cras interdum tempor leo. Fusce sed sem nec lacus iaculis faucibus. Lorem
    ipsum dolor sit amet, consectetur adipiscing elit.
</div>

<div class="newPage">
    Praesent nulla enim, venenatis sit amet ligula at, commodo viverra metus. Vivamus congue felis vel libero
    scelerisque, eu tempor tortor rutrum. Proin vitae tincidunt nunc. In hac habitasse platea dictumst. Fusce a placerat
    metus. Cras dolor dolor, tristique nec efficitur venenatis, venenatis et ante. Pellentesque varius massa ac
    convallis commodo. In at consequat est. Pellentesque habitant morbi tristique senectus et netus et malesuada fames
    ac turpis egestas. Vestibulum rutrum felis eleifend, mattis purus at, lacinia metus. Duis sit amet feugiat sapien,
    commodo tincidunt dui. Integer fringilla risus quis risus tempus dignissim. Nulla tempus vel turpis id lacinia.
</div>

</body>
</html>
```

```java
public class ExampleTest {
    @Test
    void firstPageHeader() throws IOException {
        try (final var str = getClass().getResourceAsStream("/headers/header_only_on_first_page.html")) {
            final var output = File.createTempFile("openpdf_headers_first_only_", ".pdf");
            PDFGenerator.of()
                    .withSource(str)
                    .generate(output);
            System.out.println("Output - " + output.getAbsolutePath());
        }
    }
}
```

{% pdf "/files/pdf/headers/header_only_on_the_first_page.pdf" no_link%}