# a11y

This repo contains code for testing accessibility.

At the top level you will find master LaTeX documents. Do not compile
these documents. Instead work within the folders. Note, the preamble
for the document may be different in each folder.

## For the web

For some (perhaps) helpful links/discussions, see:


* https://ctan.org/pkg/catdvi?lang=en  (catdvi)
* https://ctan.org/pkg/srcltx?lang=en  (srcltx)
* https://ctan.org/pkg/dvi2tty?lang=en (dvi2tty)
* https://unplannedobsolescence.com/blog/behavior-belongs-in-html/
* https://stackoverflow.com/questions/26007744/image-overlay-on-site-but-keeping-content-clickable
* https://jacobbartlett.substack.com/p/oh-sht-my-app-is-successful-and-i (a11y discussion)

## For PDF

See 
* https://docs.google.com/presentation/d/1H1fNuuSVnwgtKONojRLZvUpWPvfV__avWT_rpYZR-Ro/edit#slide=id.p
* https://mirror.mwt.me/ctan/macros/latex/contrib/accsupp/accsupp.pdf
* Try built-in screen readers. 

## Some notes on Ximera commands

* `\answer` needs default alt-text of "unanswered" that is replaced with "answered VALUE Correct/Incorrect" after answering. 
* `\answer` needs optional argument `alt={my groovy text}` which modifies the default by "'my groovy text' unanswered" or "'my groovy text' answered VALUE"
* Math mode could default to mathml if no alt-text is given
* The text given by accessibility could be the underlying text in the browser DVI
* `\wordChoice` needs to default to radio buttons
* `\multipleChoice` needs to default to radio buttons
* `\selectAll` needs to default to checkboxes
* Is it even possible (within latex) to compile in such a way that a model such as:
```latex
\[
\alt{here}
Text to be replaced?
\]
```
A different model (though perhaps impractical) is:
```latex
\alt{Text to be shown} %% and 

\alt[Text to be replaced]{text to be shown}
```
The second syntx seems problematic with examples where the `\answer` boxes are within content that must be alt-ed out. For example, a large array/table with answer boxes, or a tikz picture with answer boxes.
