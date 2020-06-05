---
published: true
---
Some years ago I had to write my PhD thesis using a LaTeX template provided by the univeristy. It was a half-ready tempalte; and I was very obsessive. Consequently, I spent same amount of time on styling as I spent on writing the actual content :D. There were two issues with the existing style: a) the official graphical style of the university was not present in the LaTeX template; and b) typesetting for mathematics and some other environments were quite limitted and basic.

Let's fist discuss the second issue. I suumarize what I learned about Typography in LaTeX in this post.

Coming back to the first issue of overal graphical style, the main problem was the absence of official fonts in the LaTeX template. There is no easy way to use Sentinel and Nimbus Sans as text and math fonts in LaTeX. To adress this issue, I eventually switched from LaTeX to XeLaTeX to use OpenType fonts freely for text and math. This document, however, is about LaTeX or applicable to both LaTeX and XeLaTeX unless exlicitly specified. A separate discussion about font setting in XeTeX is included as well. 

Before diving in TeX detail, I have a comment. This post is not a comprehensive guide on styling, but a mere collection of random notes. 

Ideally you should have a well constructed LaTeX template to start with and do not worry about anything else. In fact most institutes and publishers would recommend against changing anything in their provided template. However, it is not usually the case for an obsessive person! I would like to strees the importance of following a style guide. There are few comprehensive style guides out there, but only use one of them. [The Chicago Manual of Style](https://www.chicagomanualofstyle.org/home.html) is the one that I use. You may not need to read it cover to cover, but having a style book on my desk while writing my dissertation a tremendous help to check whenever in doubt. And if you are still in doubt, do some googling. A valuable resource for me was [english.stackexchange.com](https://english.stackexchange.com/).

##  Fonts 
A short excuse before we start. To keep things simple, the word `font` is used loosely in this document, and interchangably with word `typeface`. 

TeX has two main fornt families used for text 'Serif' and 'Non Serif'. There is also 'Type Writer' family. For math environment, there is normal math font and 'Match Caligraphy' font. Other font shapes might be also used in math, including 'Math Blackboard' and 'Math Script'. Ideally all these font families should have matching shapes. Matching menas that they have relatively simillar size, weight and shape, such that they look to complement each other. 

To me, the foremost component of typesetting is the consistent use of matching fonts throughout the document. One can write a whole book with perfect tyepsetting using only one font, but it is hard to compose a profesional looking document with a handfull of fonts. 

If a basic TeX template is used the default font/typeface is Computer Modern. This has matching fonts for all font families.

### Better Math
Use `AMS` packages.

    % AMS packages
    \usepackage{mathtools,amsfonts,amssymb,amsthm,amsbsy} 
    \interdisplaylinepenalty=2500 % after amsmath to restore bad page breaks

There are plenty of other packages for example `nicefrac` creates better looking fractions.

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

RequirePackage{amsmath,amssymb,amsthm,trace}
\interdisplaylinepenalty=2500 % after amsmath to restore bad page breaks
\usepackage{mathtools}
\RequirePackage{accents} % accents package should be loaded before unicode-math
% XeLaTeX
\RequirePackage{microtype}
% Set fonts
\RequirePackage{fontspec}
% Set text font
\setmainfont[Ligatures=TeX,Numbers={OldStyle,Proportional},Scale=0.95,WordSpace=1.2]{Sentinel Book} % Set the serif font
\setsansfont[Scale=0.95]{Nimbus Sans} % Set the sans serif font
%
%	% Set math font
\RequirePackage[math-style=TeX]{unicode-math}
%	%%\setmathfont{XITS Math}
%	\setmathfont[Scale=MatchLowercase]{Asana-Math.otf}
\setmathfont{latinmodern-math.otf}[FakeBold=0.05,Scale=0.9]
\setmathfont{latinmodern-math.otf}[range=bb,Scale=1]
\AtBeginDocument{% Needed by unicode-math for a bug related to mathbf
	\renewcommand{\mathbf}[1]{\symbf{#1}}
}

\setmonofont[Scale=0.85]{Consolas}
%\setmathrm{Optima}
%\setboldmathrm[BoldFont={Optima ExtraBlack}]{Optima Bold}
% Load polyglossia package for multi-language support
\RequirePackage{polyglossia}



\setmathfont[range=\mathbb,Scale=MatchUppercase]{texgyrepagella-math.otf}

\newfontfamily\thfont{Sentinel Book}[
WordSpace={2}
]
% Declare theorem environments
\usepackage{thmtools}
\declaretheoremstyle[
	numberwithin=chapter,
	bodyfont=\thfont\itshape,
]{mythstyle}
\declaretheorem[style=mythstyle]{theorem}


## Spacing, Kerning, Typesetting

Always use microtype

	\usepackage[protrusion=true,expansion=true]{microtype}

The `microtype` works best if loaded before other packages.

Spacing is mainly adjusted by TeX itself and by your font packages.

### Text spacing
Some fine tuning for typesetting, french standard!

	\frenchspacing
	\usepackage{impnattypo}

### Math spacing
 % Adjust math line spacing
 
 \usepackage{array}
 
\renewcommand*{\arraystretch}{1.1} % for array/matrix environments
\setlength{\jot}{8pt} % for split environment

### Line Breaks and Hyphenation
This is also something that you use TeX to do it.

	\setlength{\emergencystretch}{1em}

	\usepackage{ragged2e}


## Floats
You probably use `graphicx` to include images.

### Figures
	\usepackage{float}
	\usepackage{dblfloatfix}
	

	\usepackage{float, wrapfig}
	\usepackage[format=plain]{caption}
	\usepackage{subcaption}
	\captionsetup[subfigure]{justification=centering}

If you have an old template that is not compatible with `subcaption` you may use `subfig` instead.

	\usepackage[caption=false,font=footnotesize]{subfig}

### Tables
\usepackage{tabu}

\usepackage{multirow, multicol, makecell}
\usepackage{rotating}
\renewcommand\theadfont{\bfseries}

Define one table styles and stick to it for consistency.

### Other Environments
 	\usepackage{algorithm}
	\usepackage[noend]{algpseudocode}
	\floatname{algorithm}{Table}
    
    \usepackage{listings}
 
	\colorlet{commentColor}{aaltoGray!60!black}%
	\usepackage[algoruled,linesnumbered,algochapter,noline,displayblockmarkers]{algorithm2e}%
	\newcommand\mycommfont[1]{\ttfamily\bfseries\textcolor{commentColor}{#1}}%
	\SetCommentSty{mycommfont}%
	\renewcommand{\algorithmcfname}{Table}%
	\SetAlgoBlockMarkers{}{}%
	\SetKwProg{Fn}{}{\{}{}%
	\SetEndCharOfAlgoLine{}%
	\DontPrintSemicolon%
	\SetNlSty{}{}{:}%

## References

You need to reffer to figures, sections, equasations, citations, etc. in the text. All of such items need to be labeled for consistent reffering. Use prefix in your labels, eg \label{sec:introduction}. 

Use BibTeX or Biber

	\usepackage{cite}
	\let\labelindent\relax % needed for compatibility with IEEtran
	
	\renewcommand\citeleft{{\small[}}
	\renewcommand\citeright{{\small]}} 
	\bibliographystyle{../support/IEEEtran}
	\usepackage{url}


### Acronyms and Glosaries
Use this for list of symbols and acronyms

	\usepackage[acronym,shortcuts,nowarn,smallcaps]{glossaries}
	\glsdisablehyper
	\makeglossaries

	% Load glossaries package to manage glossaries and acronyms
	\usepackage[xindy,acronym,shortcuts,nosuper,nonumberlist]{glossaries}
	\usepackage{glossary-longragged}
	\usepackage{glossary-tree}
	%
	\newglossarystyle{longuc}%
	{%
		\setglossarystyle{long}%
		\renewcommand{\glossentry}[2]{%
			\glsentryitem{##1}\glstarget{##1}{\glossentryname{##1}} &
			\Glossentrydesc{##1}\glspostdescription\space ##2\tabularnewline
		}%
	}
	\setacronymstyle{long-short}
	\glsdisablehyper
	%
	\makeglossaries
	\renewcommand*{\acronymfont}[1]{\mbox{#1}}



## Lists

	\usepackage[inline]{enumitem}
	\setlist{nolistsep}

	\usepackage[shortlabels, inline]{enumitem}

	\SetEnumitemKey{midsep}{topsep=5pt, partopsep=1pt, parsep=1pt, itemsep=5pt}
	\SetEnumitemKey{hang-1}{topsep=3pt, partopsep=1pt, parsep=0pt, itemsep=2pt, 
		leftmargin=!, labelindent=\parindent+1em, labelsep=0.5em, labelwidth=1em}
	\SetEnumitemKey{hang-2}{topsep=3pt, partopsep=1pt, parsep=0pt, itemsep=2pt,
		leftmargin=!, labelindent=\parindent, labelsep=0.5em, labelwidth=\parindent}
	\SetEnumitemKey{alph}{label=\emph{\alph*}\textbf{.}}
	\SetEnumitemKey{Alph}{label=\emph{\Alph*}\textbf{.}}


## Better PDF


Standard PDF:
	\usepackage[x-1a]{pdfx}
    
 Use only vector graphics. SVG, PSD, and PDF formats work best as importing vector graphics.
 You can also craete impressive things inside TeX if you are patient.
 
	\usepackage{tikz}
	\usetikzlibrary{arrows,calc,positioning}   

If you want to have a navigation pane for your long PDF, then use `hyperref`. But not that, this package is notorious for causing issues.
	\usepackage[pdfpagelabels]{hyperref}

