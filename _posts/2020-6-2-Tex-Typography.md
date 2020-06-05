---
published: true
---
Some years ago I had to write my PhD thesis using a LaTeX template provided by the univeristy. It was a half-ready tempalte; and I was very obsessive. Consequently, I spent same amount of time on styling as I spent on writing the actual content :D. There were two issues with the existing style: a) the official graphical style of the university was not present in the LaTeX template; and b) typesetting for mathematics and some other environments were quite limitted and basic.

Let's fist discuss the second issue. I suumarize what I learned about Typography in LaTeX in this post.

Coming back to the first issue of overal graphical style, the main problem was the absence of official fonts in the LaTeX template. There is no easy way to use Sentinel and Nimbus Sans as text and math fonts in LaTeX. To adress this issue, I eventually switched from LaTeX to XeLaTeX to use OpenType fonts freely for text and math. This document, however, is about LaTeX or applicable to both LaTeX and XeLaTeX unless exlicitly specified. A separate discussion about font setting in XeTeX is included as well. 

Before diving in TeX detail, I have a comment. Follow an style guide. There are few comprehensive guides [The Chicago Manual of Style](https://www.chicagomanualofstyle.org/home.html) is the one that I use. You may not need to read it cover to cover, but having a style book on my desk while writing my dissertation a tremendous help to check whenever in doubt.

## Matching Fonts 
TeX has two main fornt families used for text 'Serif' and 'Non Serif'. There is also 'Type Writer' family. For math environment, there is normal math font and 'Match Caligraphy' font. Other font shapes might be also used in math, including 'Math Blackboard' and 'Math Script'. Ideally all these font families should have matching shapes. Matching menas that they have relatively simillar size, weight and shape, such that they look to complement each other.  

If a basic TeX template is used the default font/typeface is Computer Modern. This has matching fonts for all font families.

### Better Math
Use `AMS` packages.

    % AMS packages
    \usepackage{mathtools,amsfonts,amssymb,amsthm,amsbsy} 
    \interdisplaylinepenalty=2500 % after amsmath to restore bad page breaks
    
### Times Font
The `newtx` package has exceptionally good text and math typesetting for `Times New Roman` family of fonts. It is comparable to the default Computer Modern font in terms of typesetting quality.

	\usepackage{newtxtext} % newtx Times font
	\usepackage[cmintegrals,cmbraces,vvarbb]{newtxmath}  % newtx Times font, math symbols

The actual serif font is a modified version of Adobe Times. It has all the maths symbols of the Computer Modern and AMS fonts and more. There are complementing sans-serif font based on Helvetica, and a monospace set. The package also provides a libertine and garamondx options that uses Libertine or garamond-alike math symbols to match the corresponding text.

The order in which you load packages is important. For example you may need to load `newtxmath` after `AMS` to make sure that you end up with correct font setting.



### More Math Alphabet

	\usepackage[scr=rsfso]{mathalfa}
    \usepackage{textcomp} % more symbols


### Bolds, Italics

	\usepackage{bm} % poor man's bold	

### Upright Greek
For some reason LaTeX does not have upright greek letters, they are all italic. It is common in many disciplines to typeset vectors and matrices with upright letters in math mode.

### XeTeX

## Spacing, Kerning, Typesetting

Always use microtype

	\usepackage[protrusion=true,expansion=true]{microtype}

Some fine tuning for typesetting, french standard!
	\frenchspacing
	\usepackage{impnattypo}



## Floats
You probably use `graphicx` to include images.

### Figures
	\usepackage{float}
	\usepackage{dblfloatfix}
	\usepackage[caption=false,font=footnotesize]{subfig}

### Tables

### Other Environments
 	\usepackage{algorithm}
	\usepackage[noend]{algpseudocode}
	\floatname{algorithm}{Table}
 
## References

You need to reffer to figures, sections, equasations, citations, etc. in the text. All of such items need to be labeled for consistent reffering. Use prefix in your labels, eg \label{sec:introduction}. 

	\usepackage{cite}
	\let\labelindent\relax % needed for compatibility with IEEtran
	

	


	\usepackage[acronym,shortcuts,nowarn,smallcaps]{glossaries}
	\glsdisablehyper
	\makeglossaries

## Lists

	\usepackage[inline]{enumitem}
	\setlist{nolistsep}


