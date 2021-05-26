---
title: Simple header
category: Headers / Footers
order: 2
---

Using headers and footers in any document is essential. Fortunately FlyingSaucer OpenPDF supports
[page-margin-boxes](https://www.w3.org/TR/css-page-3/#margin-boxes){:target="_blank"}
and [running elements](https://www.w3.org/TR/css-gcpm-3/#running-headers-and-footers){:target="_blank"} of the CSS 3 specification.

## ```<header>``` tag as page header
Basically it is not a requirement, but it's strongly recommended to use _HTML_ tags semantically.

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
            border-bottom: 1px solid black;
            font-size: 9pt;
            font-weight: 100;
        }
    </style>
    <!-- ... -->
</head>
<body>
<header>
    Same header on all pages
</header>
<div>page content</div>
</body>
</html>
```

Using only one ```<header>``` tag in the _HTML_ document that ```<header>``` will be used as a page header in the entire document.  
> In the following example the same header content appears on the top of all three pages.

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
    Same header on all pages
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

As you can see there is only one ```<header>``` tag right next to the ```<body>``` tag before any other page content.
Another important stuff is ```.newPage``` CSS rule which forces a page break before that element.
```java
public class ExampleTest {
    @Test
    void simpleHeaders() throws IOException {
        try(final var str = getClass().getResourceAsStream("/headers/simple.html")) {
            final var output = File.createTempFile("openpdf_headers_simple_", ".pdf");
            PDFGenerator.of()
                    .withSource(str)
                    .generate(output);
            System.out.println("Output - " + output.getAbsolutePath());
        }
    }
}
```

Finally, let's run the code above which will generate this output.

{% pdf "/files/pdf/headers/same_header_on_all_pages.pdf" no_link%}

 