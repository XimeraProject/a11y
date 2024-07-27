# a11y

This repo is for the development and testing of accessible components in Ximera.


## Our intial strategy

We are not opiniated concerning the technical background; however, in our disucssions, ARIA has been brought up quite a bit. **Note** some of the links below dispute this and suggest we "should prefer using the correct semantic HTML element over using ARIA."
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA
- https://www.w3.org/TR/html-aria/


## Four cases

I believe there are four cases for Ximera Accessibility.

## Navigating BETWEEN sections

OSU has cards and KU Leuven has a more traditional "table of contents." Out plan is to adopt KU Leuven's format.

## Navigating WITHIN an activity

Ximera documents are already "somewhat" accessible in this domain. However, it could surely be improved.

## `\answer`

The command `\answer` first needs to be implemented in a modern version of TeX4ht/MathJax.
It needs to automatically have
- "Blank answer box"
- "Answered with TYPED-ANSWER not evaluated."
- "Answered with TYPED-ANSWER incorrect."
- "Answered with TYPED-ANSWER complete."
After that, it will need an additional optional argument `alt='STRING'` that will give
additional information about the answer, for example:
```
\[
\begin{pmatrix}
3           &   2 \\
\answer[alt='entry 2 1']{1}  &   1
\end{pmatrix}
\]

```
This additional text would be **prepended** to the previous statement, so in this example it would read
- "entry 2 1 Blank answer box"
- "entry 2 1 Answered with TYPED-ANSWER not evaluated."
- "entry 2 1 Answered with TYPED-ANSWER incorrect."
- "entry 2 1 Answered with TYPED-ANSWER complete."

## Math and Images

All "4-function calculator math" should be read. However, when math becomes much more complicated (or is an image), it should be given a **static** alternative description.
At the level of LaTeX, we would like to handle this in the following way: `\alt{}` within an environment (including math-mode, and display-math) will obliterate all content within that envirnment except for:
- other `\alt` and
- `\answer`
So for example, we would like to be able to write:
```
\[
\alt{a 2 by 2 matrix with answer boxes in each entry}
\begin{pmatrix}
\answer[alt='entry 1 1']{3}  &   \answer[alt='entry 1 2']{2} \\
\answer[alt='entry 2 1']{1}  &   \answer[alt='entry 2 2']{1}
\end{pmatrix}
\]
```
Multiple `\alt` are allowed, with the `\alt` and `\answer` being read left to right, top to bottom. The example above would be read:

"a 2 by 2 matrix with answer boxes in each entry, entry 1 1 blank answer box, entry 1 2 blank answer box, entry 2 1 blank answer box, entry 2 2 blank answer box."




## Other 

For some (perhaps) helpful links/discussions, see:

* https://github.com/latex3/tagging-project/discussions/72
* https://ctan.org/pkg/catdvi?lang=en  (catdvi)
* https://ctan.org/pkg/srcltx?lang=en  (srcltx)
* https://ctan.org/pkg/dvi2tty?lang=en (dvi2tty)
* https://unplannedobsolescence.com/blog/behavior-belongs-in-html/
* https://stackoverflow.com/questions/26007744/image-overlay-on-site-but-keeping-content-clickable
* https://jacobbartlett.substack.com/p/oh-sht-my-app-is-successful-and-i (a11y discussion)
* https://ctan.org/pkg/axessibility?lang=en
### For PDF

See
* https://docs.google.com/presentation/d/1H1fNuuSVnwgtKONojRLZvUpWPvfV__avWT_rpYZR-Ro/edit#slide=id.p
* https://mirror.mwt.me/ctan/macros/latex/contrib/accsupp/accsupp.pdf
* Try built-in screen readers.

### Some notes on Ximera commands

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

\[
\alt{two plus two equals}
2+2 = \answer{4} %% answer would have its own alt manifestation
\]
```
A different model (though perhaps impractical) is:
```latex
\alt{Text to be shown}
\alt{Some message in the middle of the text}

%% and

\alt[Text to be replaced]{text to be shown}
\alt[\[ 2+2=\answer{4} \]]{two plus two}
```

A different model yet
```latex
%% use options for environments like so:

\begin{environment}[alt]
Something complicated
\end{environment}`
%% Here, we would have a file, that has all the "alt" text of the document.
%% Math mode and answer would automatically be included.
```

Another idea
We implemnet `\alt` for injecting random text. Then all math mode, `\answer`, `\tabular`, `image`
automatically get alt entires in some document.
