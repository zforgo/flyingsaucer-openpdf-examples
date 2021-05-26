---
title: Header and footer 
category: Headers / Footers 
order: 3
---

Extending the [previous example](../simple_header) this post shows how to use both ```<header>``` and ```<footer>``` in
the same document. Methodology is same. 

```<header>``` element attached to page header and ```<footer>``` will be used as page footer.

```html
<!-- ... -->
    <style>
        @page {
            size: letter portrait;
            margin: 2.5cm 1cm;
            @top-center {
                content: element(header);
            }
            @bottom-center {
                content: element(footer);
            }
        }
        </style>
<!-- ... -->
```
... and related _HTML_ part is:
```html
<!DOCTYPE html>
<html lang="en">
<!-- ... -->
<body>
<header>
    Same header on all pages
</header>
<footer>
    Visit: <a href="https://flyingsaucer-openpdf-examples.github.io" target="_blank">https://flyingsaucer-openpdf-examples.github.io</a>
    or get involved with contributing guides
    <a href="https://github.com/zforgo/flyingsaucer-openpdf-examples" target="_blank">https://github.com/zforgo/flyingsaucer-openpdf-examples</a>
</footer>
<div>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ultrices risus eu risus placerat dignissim. Quisque
    tincidunt lectus non rutrum tempor. Proin finibus, urna quis mattis cursus, lacus ex elementum nunc, a volutpat
    metus tellus ac turpis. Nulla nisi ex, ultricies eu magna eu, sagittis pulvinar turpis. Duis eget leo dolor. Vivamus
    elit magna, ultricies a massa non, mattis bibendum velit. Curabitur ac vestibulum nunc. Cras laoreet turpis odio,
    vitae tempus felis pharetra pretium. Pellentesque non cursus ipsum, quis bibendum arcu. Fusce vel sapien varius,
    facilisis risus non, tincidunt mauris.
</div>
<!-- ... -->
</body>
</html>
```
## Let's put together

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
            @bottom-center {
                content: element(footer);
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
        footer {
            position: running(footer);
            padding-top: 5pt;
            border-top: 1px solid black;
            font-size: 9pt;
            font-weight: 100;
        }
    </style>
    <title>FlyingSaucer OpenPDF example</title>

    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
</head>
<body>
<header>
    Same header on all pages
</header>
<footer>
    Visit: <a href="https://flyingsaucer-openpdf-examples.github.io" target="_blank">https://flyingsaucer-openpdf-examples.github.io</a>
    or get involved with contributing guides
    <a href="https://github.com/zforgo/flyingsaucer-openpdf-examples" target="_blank">https://github.com/zforgo/flyingsaucer-openpdf-examples</a>
</footer>
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
    void headerAndFooter() throws IOException {
        try (final var str = getClass().getResourceAsStream("/headers/header_and_footer.html")) {
            final var output = File.createTempFile("openpdf_header_and_footer_", ".pdf");
            PDFGenerator.of()
                    .withSource(str)
                    .generate(output);
            System.out.println("Output - " + output.getAbsolutePath());
        }
    }
}
```

Finally, let's run the code above which will generate this output.

{% pdf "/files/pdf/headers/header_and_footer.pdf" no_link%}