Images are way easier than walls of text to explain how uMatrix works. So let's visit [wired.com](https://wired.com).

When you first visit [wired.com](https://www.wired.com), open the matrix:

![Global scope](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/wired-walkthru-1.png)

The top-most left-most cell is the currently selected **scope**. The currently selected scope is just a user interface thing. This allows you to look at, or edit rules in a specific scope. The matrix filtering engine always filter net requests by evaluating rules in the narrowest scope first.

All rules in uMatrix are created in a specific scope. Above in the picture, the `*` is selected. The `*` is the global scope. The global scope contains rules which applies **everywhere**, on every page you visit.

Since uMatrix works in block-all/allow-exceptionally out of the box, pretty much everything is blocked in the global scope, except for CSS-related and image resources.

Let's switch scope to `wired.com`: click the scope cell, and select `wired.com`. The matrix looks different now:

![`wired.com` scope](https://raw.githubusercontent.com/gorhill/uMatrix/master/doc/img/wired-walkthru-2.png)

Here we see that in the `wired.com` scope, net requests which originate from within the `wired.com` domain are all allowed. (Except for `cookie`, that is my personal setting and I forgot to remove it before taking the screenshots.)

This is because of the `1st-party` row: the cells in this row are used to tell what to do with net requests which are 1st-party to the URL address of the current page.

[TODO: complete this walkthrough]