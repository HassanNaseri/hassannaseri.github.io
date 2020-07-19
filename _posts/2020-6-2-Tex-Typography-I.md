---
published: true
---
Some years ago I had to write my PhD thesis using a LaTeX template provided by the univeristy. Sometimes I become obsessed with how things look like, and that template did not look right. Consequently, I spent same amount of time on styling as I spent on writing the actual thesis :D, hoping that it may benefit others as well. Two major problems of the provided template were: a) the official visual style of the university was not present in the LaTeX template; and b) the typesetting for mathematics and some other environments were quite limitted and basic.

Addressing the first problem, required enabling Sentinel and Nimbus Sans fonts in LaTeX for both text and math, which can only end in despair. I eventually switched from [pdfTeX](https://en.wikipedia.org/wiki/PdfTeX) to [XeTeX](https://en.wikipedia.org/wiki/XeTeX) to use OpenType fonts freely for text and math. The second problem, was adressed using a pletora of new packages, settings and definitions applicable to both LaTeX and XeLaTex. I am now publishing the highlights of what I learned in this process in a couple of blog posts. The first part covers LaTeX and more generic considerations regarding typesetting. The second part will cover XeTeX stuff and a long list of custom setiings and definitions.


Before diving into TeX detail, I need to emphasize that this post is not a comprehensive guide on styling, but a mere collection of random notes. Ideally you have a well constructed LaTeX template to start with, and do not worry about anything other than writing. In fact most institutes and publishers would recommend against changing anything in their provided template. However, it is not usually the case for an obsessive mind :) I would also like to strees the importance of following a style guide. There are few comprehensive style guides out there. Choose one and stick to it. [The Chicago Manual of Style](https://www.chicagomanualofstyle.org/home.html) is the one that I use. You may not read it cover to cover, but having a style book on your desk is a huge releif whenever in doubt. There is also a pletora of very good websites to search for writing tips that you don't find in an style guide. I extensively used [english.stackexchange.com](https://english.stackexchange.com/) and [tex.stackexchange.com](https://tex.stackexchange.com/).


##  Fonts 
A short excuse before we start. To keep things simple, the word "font" is used loosely in this document, and interchangably with word typeface. TeX has two main fornt families used for text [serif](https://en.wikipedia.org/wiki/Serif) and [sans-serif](https://en.wikipedia.org/wiki/Sans-serif). There is also a [monospaced](https://en.wikipedia.org/wiki/Monospaced_font) familiy, known as typewriter in TeX. For math typesetting, there is normal math font and and math caligraphy font (known as *mathcal*). Other font shapes might be also used in math, including *math blackboard* and *math script*. Ideally all these font families should have matching shapes. That is, they have relatively simillar size, weight and shape, so they complement each other. 

To me, the foremost feature of good typesetting is consistency, which cannot be achieved without  matching fonts throughout the whole document. One can write a whole book with perfect tyepsetting using only one font, but it is hard to compose a good document with a handfull of different fonts. 

When a standard TeX templates is used, the [Computer Modern](https://en.wikipedia.org/wiki/Computer_Modern) family of typefaces (actually the updated Latin Modern) gets applied by default. It comes with matching shapes for serif, non-serif, typewriter, math, etc., and guarantees an almost perfect typesetting for all text and math throughout the document.

### The Problem
TeX has a quite sophisticated font system [Metafont](https://en.wikipedia.org/wiki/Metafont), created alongside TeX itself. It generates scalable fonts with non-rivaled typesetting features. However, there are only few fonts with extensive symbols to choose from. In fact, any font other than Computer Modern may come with some sacrifices or complications somewhere if you start nit picking. The introduction of TrueType and OpenType fonts, made scalable and good looking fonts available for a much wider range of applications. However, standard TeX cannot easily use such fonts and even if used it does not guarantee the professional typesetting that you expect from TeX out of the box. Hence, the problem arises when you want or asked to use a font other than Computer Modern and you still want a comparable quality for typesetting text and more critically math equation.

There are two solutions, a) switch from TeX/LaTeX to something newer like XeTeX or LuaTeX, b) be lucky and find a very good LaTeX package for the font that you want and workaround remaining issues. In this post we are covering the second option. 

### Times Font
Most font packages for LaTeX will not give you the quality of typesetting that you get with default fonts. However, there are few good packages as well. If you wish to typeset your document with Times New Roman, because you want to be different, then there is a good option for you. The [newtx](https://ctan.org/pkg/newtx?lang=en) package has exceptionally good text and math typesetting for Times New Roman family of fonts. The actual serif font in `newtx` is a modified version of Adobe Times. It has all the maths symbols of the Computer Modern and AMS fonts and more. There are complementing sans-serif font based on Helvetica, and a matching monospace (typewriter) set. The package also provides a libertine and garamondx options that uses Libertine or garamond-alike math symbols to match the corresponding text. Here is how to load `newtx` for text and math.

    {% highlight tex %}
    {% raw %}
    \usepackage{newtxtext} % newtx Times font for text
    \usepackage[cmintegrals,cmbraces,vvarbb]{newtxmath}  % newtx Times font for math
    {% endraw %}
    {% endhighlight %}

As seen above `newtx` comes in two packages for text and math. The second line loads `newtxmath` for math, but uses integral and brace symbols from Computer Modern font for better typesetting if you prefer them. The order in which you load packages is important. For example you may need to load `newtxmath` after AMS packages (discussed next) to make sure that you end up with correct font setting.


### Better Math and More Symbols

[AMS-LaTeX](https://en.wikipedia.org/wiki/AMS-LaTeX) is a collection of packages that provide an extensive set of math symbols, macros and environments. Use the following lines to load them if you have math in your document.
	
    {% highlight tex %}
    {% raw %}
    % AMS packages
    \usepackage{mathtools,amsfonts,amssymb,amsthm}
    \interdisplaylinepenalty=2500 % after amsmath to restore bad page breaks
    {% endraw %}
    {% endhighlight %}

Note that we load `mathtools` instead of `amsmath` to fix some minor issues. There are plenty of other packages to provide additional math symbols or different typesetting for certain equations. Fo example, [nicefrac](https://ctan.org/pkg/nicefrac?lang=en) creates better looking fractions. The follwing two packages might be loaded if you need additional math symbols not available in AMS packages.

    {% highlight tex %}
    {% raw %}
    \usepackage[scr=rsfso]{mathalfa}
    \usepackage{textcomp} % more symbols
    {% endraw %}
    {% endhighlight %}


### Bolds, Italics, Small Caps, etc.
Different shapes/styles of a font are accessible using the commands `\textit{}`, `\textbf{}`, and `\textsc{}` or using
    {% highlight tex %}
    {% raw %}
    {\itshape ...} # Italic shape
    {\bfseries ...} # Bold shape
    {\scshape ...} # Small caps
    {% endraw %}
    {% endhighlight %}
In order to use these commnads, one needs to have a corresponding font shape available. However, most fonts don't include all the comibinations of these shapes. For example, slanted or bold small capitals are rarely found in fonts. If for a given font, small capitals are available in slanted or bold shapes, then the package [slantsc](https://ctan.org/pkg/slantsc?lang=en) enables the use of them. 

Bold shapes of symbols may be particularly important for math typesetting. If some symbols don't have bold shape, then a fake bold symbol may be created by just increasing the weight of a normal glyph. You may use the package [bm](https://ctan.org/pkg/bm?lang=en) to do so. However, this should be only used very sparingly, and certainly not for body text. 
    {% highlight tex %}
    {% raw %}
    \usepackage{bm} % poor man's bold	
    {% endraw %}
    {% endhighlight %}


### Upright Bold Greek Letters
For some reason LaTeX does not have upright greek letters, they are all italic. It is common in many disciplines to typeset vectors and matrices with upright letters in math mode.

    {% highlight tex %}
    {% raw %}
    \makeatletter
    \def\changegreek{\@for\next:={%
        alpha,beta,gamma,delta,epsilon,zeta,eta,theta,kappa,lambda,mu,nu,xi,pi,rho,sigma,%
        tau,upsilon,chi,psi,omega,varepsilon,vartheta,varpi,varrho,varsigma,varphi}%
        \do{\expandafter\let\csname\next\expandafter\endcsname\csname\next up\endcsname}}
    \def\changegreekbf{\@for\next:={%
        alpha,beta,gamma,delta,epsilon,zeta,eta,theta,kappa,lambda,mu,nu,xi,pi,rho,sigma,%
        tau,upsilon,chi,psi,omega,varepsilon,vartheta,varpi,varrho,varsigma,varphi}%
        \do{\expandafter\def\csname\next\expandafter\endcsname\expandafter{%
        \expandafter\bm\expandafter{\csname\next up\endcsname}}}}
    \makeatother
    {% endraw %}
    {% endhighlight %}



## Spacing, Kerning, and Microtypography

The most amazing LaTeX package that automatically solves your microtypography concerns in [microtype](https://ctan.org/pkg/microtype?lang=en). It also partially works in XeTeX and LuaTeX. I recommend you always load it as your first package in any document (before other packkages). 
    {% highlight tex %}
    {% raw %}
	\usepackage[protrusion=true,expansion=true]{microtype}
    {% endraw %}
    {% endhighlight %}

### Text Spacing, Hyphenation, and Line Breaks

Correct spacing between symbols, words and sentences is a key component of good typesetting. TeX is designed to solve this issue out of the box in an almost perfect manner. However, some fine tuning always help, specially if you use anything other than default Computer Modern font family. Hyphenation has also the same story. You can tweek it if you are not happy with what comes out of the box. Hyphenation is a delicate matter that keeps balance between how the words are aligned at the end of each row, and how fragmented the text looks like in each line. 

I prefer to have follwing commands in the preamble (before `\begin{document}` where you load all other packages) to tweek sentence spacing and hyphenation.

    {% highlight tex %}
    {% raw %}
	\frenchspacing
	\usepackage{impnattypo}
	\setlength{\emergencystretch}{1em}
    {% endraw %}
    {% endhighlight %}

If you need some ragged text in your document, for example in certain environments, then load [ragged2e](https://ctan.org/pkg/ragged2e?lang=en) package as well. It gives you some flexible and tunable ragged text environments.

We do not discuss letter spacing and [kerning](https://en.wikipedia.org/wiki/Kerning) here for two reasons. First, if you already know what is kkerning then you may not need this guide at all :), and second, those microtypographic details should be automatically handled by proper packages that you load, such as `microtype` and `newtx`.

### Math Spacing
Good spacing in math is way more complex than text. No matter, how good your math packages are, there might be still room to apply your own modifications. You can pretty much adjust any type space that does not look good. Here I just give two examples to adjust vertical spacing.

You are most likely to use `array` environment for multiline math equations and matrices. Often with large symbols, array environment looks crammed. You can use the follwing command to strech that out:

	\renewcommand*{\arraystretch}{1.1} % for array/matrix environments

Similarly, the follwing command doubles the line spacing in `split` and `align` environments of `amsmath`:
	
	\setlength{\jot}{8pt} % for split environment	

More detailed spacing. If you want to only reduce the spacing in inline math without affecting display math mode. 

    {% highlight tex %}
    {% raw %}
    \everymath{
        \thinmuskip=0.5\medmuskip
        \medmuskip=0.5\medmuskip
        \thickmuskip=0.5\thickmuskip
    }
    {% highlight tex %}
    {% raw %}

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
	{% highlight tex %}
	{% raw %}
	\usepackage{cite}
	\let\labelindent\relax % needed for compatibility with IEEtran
	
	\renewcommand\citeleft{{\small[}}
	\renewcommand\citeright{{\small]}} 
	\bibliographystyle{../support/IEEEtran}
	\usepackage{url}
	{% endraw %}
	{% endhighlight %}


### Acronyms and Glosaries
Use this for list of symbols and acronyms

    {% highlight tex %}
    {% raw %}
    \usepackage[acronym,shortcuts,nowarn,smallcaps]{glossaries}
    \glsdisablehyper
    \makeglossaries
    \immediate\write18{makeglossaries \jobname} % run (pdf)latex twice with --shell-escape
    \makeglossaries
	{% endraw %}
	{% endhighlight %}

This uses small caps, if you want normal caps for the glossaries list and still small caps for acronyms in the body text, then use this command after loading glossaries package.
    \renewcommand{\glsnamefont}[1]{\MakeUppercase{#1}}

	{% highlight tex %}
	{% raw %}
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
	{% endraw %}
	{% endhighlight %}

    \usepackage{soul}
    \usepackage[acronym,shortcuts=ac]{glossaries-extra}
    \makeglossaries
    \renewcommand{\glsabbrvscfont}[1]{\textsc{\MakeTextLowercase{\caps{#1}}}}
    \setabbreviationstyle[acronym]{long-short-sc}

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



	

	



