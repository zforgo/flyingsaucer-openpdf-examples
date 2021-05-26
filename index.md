---
title: Getting Started
---

### Overview
Flying Saucer is a pure-Java library for rendering arbitrary well-formed XML (or XHTML) using CSS 2.1 for layout and 
formatting, output to Swing panels, PDF, and images.

> [Visit](https://github.com/flyingsaucerproject/flyingsaucer) official GitHub repository or read [User's Guide](https://flyingsaucerproject.github.io/flyingsaucer/r8/guide/users-guide-R8.html) for more information.

Although FlyingSaucer supports different PDF renderers, the examples based and tested on **flying-saucer-pdf-openpdf** only.
### Conventions used in these examples
Each example should contain source code snippets in _HTML_
```html
<html lang="en">
<head>
    <style>
        body {
            margin: 2px;
        }
    </style>
    <title>FlyingSaucer OpenPDF Examples</title>
</head>
<body>
<h1>Hello World!</h1>
</body>
</html>
```
or in _Java_
```java
public class Foo {
    public static void main(Stirng... args) {
        System.out.println("Hello World!");
    }
}
```
> All Java source codes are in JavaSE 16 but all of those can be downgraded (if you are stuck with it).    

probably PDF output attached
{% pdf "/files/pdf/dummy.pdf" width=50% no_link%}
<br/>
Sometimes when it's necessary a small utility class will be used to generate PDF documents.

```java
public class PDFGenerator {
    private final ITextRenderer renderer;

    private PDFGenerator() {
        renderer = new ITextRenderer();
    }

    public static PDFGenerator of() {
        return new PDFGenerator();
    }

    public final PDFGenerator withSource(InputStream is) {
        Optional.ofNullable(is)
                .map(XMLResource::load)
                .map(XMLResource::getDocument)
                .ifPresentOrElse(doc -> renderer.setDocument(doc, null), () -> {
                    throw new NullPointerException("Something went wrong");
                });
        return this;
    }

    public final void generate(File outputFile) throws IOException {
        try (FileOutputStream fos = new FileOutputStream(outputFile)) {
            renderer.layout();
            renderer.createPDF(fos);
        }
    }
}
```
