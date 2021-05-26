---
title: Different header only on the last page 
category: Headers / Footers 
order: 6
---

If you read other guides such as [header and footer](../header_and_footer) or 
[different header only on the first page](../different_header_on_fisrt_page) then this example would be a trivial exercise.

Let's repeat
* The first ```<header>```  tag before the main content will be attached to the first page header.
* The second ```<header>``` tag before the main content will be attached to all other pages as page header.
* The last ```<header>``` tag will be attached to the first page header. It must be after the last page content.

So, if you have to use same headers on all pages except the last one, just put two ```<header>``` elements in the _HTML_ document.

```html
<!DOCTYPE html>
<html lang="en">
<!-- ... -->
<body>
<header>
    Appears on all pages except the last one
</header>
<div class="newPage">First page content</div>
<div class="newPage">Second page content</div>
<div class="newPage">Third page content</div>
<!-- ... -->
<header>
    Appears only on the last page
</header>
</body>
</html>
```
> NOTE: the last ```<header>``` element must be placed at the bottom of the document.

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
<header>
    This is a custom header only on the last page
</header>

</body>
</html>
```
```java
public class ExampleTest {
    @Test
    void customHeaderOnLast() throws IOException {
        try(final var str = getClass().getResourceAsStream("/headers/different_header_on_the_last_page.html")) {
            final var output = File.createTempFile("openpdf_different_header_on_last_", ".pdf");
            PDFGenerator.of()
                    .withSource(str)
                    .generate(output);
            System.out.println("Output - " + output.getAbsolutePath());
        }
    }
}
```

{% pdf "/files/pdf/headers/different_header_on_the_last_page.pdf" no_link%}