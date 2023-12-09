# a11y

This repo contains code for testing accessibility.

At the top level you will find master LaTeX documents. Do not compile
these documents. Instead work within the folders. Note, the preamble
for the document may be different in each folder.



## Some notes on Ximera commands

* \answer needs default alt-text of "unanswered" that is replaced with "answered VALUE Correct/Incorrect" after answering. 
* \answer needs optional argument alt={my groovy text} which modifies the default by "'my groovy text' unanswered" or "'my groovy text' answered VALUE"
* Math mode could default to mathml if no alt-text is given
* The text given by accessibility could be the underlying text in the browser DVI
* \wordChoice needs to default to radio buttons
* \multipleChoice needs to default to radio buttons
* \selectAll needs to default to checkboxes
