---
published: true
---
Around four years ago I started the writing of my PhD thesis using a [LaTeX](https://en.wikipedia.org/wiki/LaTeX) template provided by the university. 
But the template was far from perfect - sometimes I get obsessed with how things look like. 
There were two major issues with the template: a) the official visual style of the university was not present in the LaTeX template; and b) the typesetting for mathematics and some other environments were quite limited and basic.
Consequently, I spent same amount of time on styling the thesis as I spent on writing the actual content :D. 

<div style="width: 80%;
            padding-left: 3px; padding-right: 3px;" >
<a href="http://phdcomics.com/comics.php?f=1756">
<img style="display: block" src="/images/phd102914s.gif" alt="PHD Comic"/>
</a>
</div>

Addressing the first issue required enabling Sentinel and Nimbus Sans fonts in LaTeX for both text and math, which can only end in despair. I eventually switched from [pdfTeX](https://en.wikipedia.org/wiki/PdfTeX) to [XeTeX](https://en.wikipedia.org/wiki/XeTeX) to use OpenType fonts freely for text and math. The second issue, was addressed using a plethora of new packages, settings and definitions applicable to both LaTeX and XeLaTex. 
Hence, I considerably modified the university template, and also created a new XeLaTex template, hoping that it may benefit others as well.
Here, I am publishing the highlights of what I learned in this process in a couple of blog posts. The first part, that you are reading now, covers LaTeX and more generic considerations regarding typesetting. 
The second part will cover XeTeX together with a long list of custom settings and definitions.

 
Before diving into TeX detail, I need to emphasize that this post is not a comprehensive guide on styling, but a mere collection of random notes. Ideally you have a well constructed LaTeX template to start with, and do not worry about anything other than writing. In fact, most institutes and publishers would recommend against changing anything in their provided template. However, it is not usually the case for an obsessive mind :) 
Moreover, this series is not about writing style, except for few tips. I would like to stress the importance of following a style guide for writing. There are few comprehensive style guides out there. Choose one and stick to it. [The Chicago Manual of Style](https://www.chicagomanualofstyle.org/home.html) is the one that I use. You may not read it cover to cover, but having a style book on your desk is a huge relief whenever in doubt. 
There are also many very good websites to search for or ask about things that you don't find in a style guide. I extensively used [english.stackexchange.com](https://english.stackexchange.com/) and [tex.stackexchange.com](https://tex.stackexchange.com/).


##  Fonts 
First, a quick disclaimer: in order to keep things simple, the word "font" is used loosely in this document, and interchangeably with the word typeface. 
TeX has two main font families used for text [serif](https://en.wikipedia.org/wiki/Serif) and [sans-serif](https://en.wikipedia.org/wiki/Sans-serif). There is also a [monospaced](https://en.wikipedia.org/wiki/Monospaced_font) family, known as *typewriter* in TeX. 
For math typesetting, there is normal math font and a math calligraphy font (known as *mathcal*). Other typefaces might be also used in math, including *math blackboard* and *math script*. Ideally all these font families should have matching shapes. That is, they have relatively similar size, weight and shape, so they complement each other. 

To me, the principal of good typesetting is consistency, which cannot be achieved without  matching fonts throughout the whole document. One can write a whole book with perfect typesetting using only one font. This gets exceedingly impractical once you have a handful of different fonts. 
If one of the default TeX templates is used, the [Computer Modern](https://en.wikipedia.org/wiki/Computer_Modern) family of typefaces (actually the updated Latin Modern) gets applied. It comes with matching shapes for serif, non-serif, typewriter, math, etc., and guarantees an almost perfect typesetting for all text and math throughout the document.

### The Problem
TeX has quite a sophisticated font system [Metafont](https://en.wikipedia.org/wiki/Metafont), created alongside TeX itself. It generates scalable fonts with non-rivaled typesetting features. However, there are only few fonts with extensive symbols to choose from. 
In fact, any font other than Computer Modern will show some limitations or complications if you start nit picking. The introduction of TrueType and OpenType fonts, made scalable and elegant fonts available to a much wider range of applications. However, standard TeX cannot easily use such fonts; and even if used it does not guarantee the professional typesetting that you expect from TeX out of the box. Hence, the problem arises when you want or asked to use a font other than Computer Modern but you still want a comparable quality for typesetting text and more critically math equations.

There are two solutions, a) switch from TeX/LaTeX to something newer like XeTeX or LuaTeX, b) be lucky and find a very good LaTeX package for the font that you want and workaround remaining issues. In this post we are covering the second option. 

### Times Font
As discussed above, most font packages for LaTeX will not give you the quality of typesetting that you get with default fonts. However, there are few good packages out there. If you wish to typeset your document in Times New Roman, because you want to be different, then there is a good option for you. The [newtx](https://ctan.org/pkg/newtx?lang=en) package has exceptionally good text and math typesetting. The actual serif font in `newtx` is a modified version of Adobe Times. If you really want to know the minute differences between Times and Times New Modern, [you may start from here](https://creativepro.com/times-roman-vs-times-new-roman/#:~:text=The%20Times%20(Roman)%20and%20Times,a%20theme%2C%20so%20to%20speak.).
The `newtx` has all the math symbols of the Computer Modern and AMS fonts and more. There are complementing sans-serif font based on Helvetica, and a matching monospace (typewriter) set. The package also provides a libertine and garamondx options that uses Libertine or garamond-alike math symbols to match the corresponding text. Here is an example of loading `newtx` for text and math.

    {% highlight tex %}
    {% raw %}
    \usepackage{newtxtext} % newtx Times font for text
    \usepackage[cmintegrals,cmbraces,vvarbb]{newtxmath}  % newtx Times font for math
    {% endraw %}
    {% endhighlight %}

As seen above `newtx` comes in two packages for text and math. The second line loads `newtxmath` for math, but uses integral and brace symbols from Computer Modern font for better typesetting if you prefer them. The order in which you load packages is important. For example, you may need to load `newtxmath` after AMS packages (discussed next) to make sure that you end up with correct font settings.


### Better Math and More Symbols

[AMS-LaTeX](https://en.wikipedia.org/wiki/AMS-LaTeX) is a collection of packages that provide an extensive set of math symbols, macros and environments. Use the following lines to load them if you have mathematics in your document.
	
    {% highlight tex %}
    {% raw %}
    \usepackage{mathtools,amsfonts,amssymb,amsthm}
    \interdisplaylinepenalty=2500 % after amsmath to restore bad page breaks
    {% endraw %}
    {% endhighlight %}

Note that, we load `mathtools` instead of `amsmath` to fix some minor issues. There are plenty of other packages that provide additional math symbols or different typesetting for certain equations. Fo example, [nicefrac](https://ctan.org/pkg/nicefrac?lang=en) creates better looking fractions. 
The following two packages might be loaded if you need additional math symbols that are not available in AMS packages.

    {% highlight tex %}
    {% raw %}
    \usepackage[scr=rsfso]{mathalfa}
    \usepackage{textcomp} % more symbols
    {% endraw %}
    {% endhighlight %}


### Bolds, Italics, Small Caps, etc.
In LaTeX, different shapes/styles of a font are accessible using the commands `\textit{}`, `\textbf{}`, and `\textsc{}` or using

    {% highlight tex %}
    {% raw %}
    {\itshape ...} # Italic shape
    {\bfseries ...} # Bold shape
    {\scshape ...} # Small caps
    {% endraw %}
    {% endhighlight %}

In order to use these, their corresponding font shapes must be available. However, most fonts don't include all the combinations of these shapes. For example, slanted or bold small capitals are rarely found in fonts. If for a given font, small capitals are available in slanted or bold shapes, then the package [slantsc](https://ctan.org/pkg/slantsc?lang=en) enables the use of them. 

Bold shapes of symbols may be particularly important for math typesetting. If some symbols don't have bold shape, then a fake bold symbol may be created by just increasing the weight of a normal glyph. You may use the package [bm](https://ctan.org/pkg/bm?lang=en) to do so. However, this should be only used very sparingly, and certainly not for body text. 

    {% highlight tex %}
    {% raw %}
    \usepackage{bm} % poor man's bold	
    {% endraw %}
    {% endhighlight %}


## Spacing, Kerning, and Microtypography

The most impressive LaTeX package that automatically solves your microtypography concerns is [microtype](https://ctan.org/pkg/microtype?lang=en). It also partially works in XeTeX and LuaTeX. I recommend you always load it as your first package in any document (before other packages). 

    {% highlight tex %}
    {% raw %}
    \usepackage[protrusion=true,expansion=true]{microtype}
    {% endraw %}
    {% endhighlight %}

### Text Spacing, Hyphenation, and Line Breaks

TeX is designed to create perfect spacing between symbols, words and sentences out of the box. However, some fine tuning always help, specially if you use anything other than default Computer Modern font. 
The situation is the same with hyphenation. You may need to fine tune it to get perfect results. Hyphenation works delicately by keeping the balance between line justification, regularity of spacing, and word fragmentation.
I prefer to have following commands in the preamble (before `\begin{document}` where you load all other packages) to adjust sentence spacing and hyphenation.

    {% highlight tex %}
    {% raw %}
    \frenchspacing
    \usepackage{impnattypo}
    \setlength{\emergencystretch}{1em}
    {% endraw %}
    {% endhighlight %}

If you need some ragged text in your document, for example in certain environments, then load [ragged2e](https://ctan.org/pkg/ragged2e?lang=en) package. It gives you some flexible and tunable ragged text environments.

We do not discuss letter spacing and [kerning](https://en.wikipedia.org/wiki/Kerning) here for two reasons. First, if you already know what is kerning then you may not need this guide at all :), and second, such microtypographic details should be automatically handled by proper packages that you load, such as `microtype` and `newtx`.

### Math Spacing
Perfect spacing in math equations is way more complex than text. No matter, how good LaTeX math packages are, there might be still room to apply your own modifications. You can adjust almost any spacing that does not look good. Here I  give few examples.

You may use `array` environment for multiline math equations and matrices. Often with large symbols, array environment looks crammed. The following command increases line spacing for arrays.

    {% highlight tex %}
    {% raw %}
    \renewcommand*{\arraystretch}{1.1} % for array/matrix environments
    {% endraw %}
	{% endhighlight %}

Similarly, the next command doubles the line spacing in `split` and `align` environments of `amsmath`.

    {% highlight tex %}
    {% raw %}	
    \setlength{\jot}{8pt} % for split environment	
    {% endraw %}
	{% endhighlight %}

The next example is for reducing the horizontal spacing in inline math without affecting display math mode. 

    {% highlight tex %}
    {% raw %}
    \everymath{
        \thinmuskip=0.5\medmuskip
        \medmuskip=0.5\medmuskip
        \thickmuskip=0.5\thickmuskip
    }
    {% endraw %}
	{% endhighlight %}

## Floats
Floats include figures, tables, and other blocks such as code listings that are floating in the document. That is, the exact location of them are determined by TeX. The floats will typically have references in the text either as figure or table.


### Figures
We typically use `graphicx` to include figures in the document. In addition to `graphicx`, the following packages are also very helpful in typesetting figures. You may check `subcaption` package documentations for more details.

    {% highlight tex %}
    {% raw %}
    \usepackage{float}
    \usepackage{dblfloatfix}
    \usepackage{wrapfig}
    \usepackage[format=plain]{caption}
    \usepackage{subcaption}
    \captionsetup[subfigure]{justification=centering}
    {% endraw %}
    {% endhighlight %}

If you have an old template that is not compatible with `subcaption` you may use `subfig` package instead.

    {% highlight tex %}
    {% raw %}
    \usepackage[caption=false,font=footnotesize]{subfig}
    {% endraw %}
    {% endhighlight %}

### Tables
The most advanced and flexible tool for typesetting tables is the `tabu` package. It has an extensive documentation. In addition you may need `multirow` and `multicol` for more complex table structures.

	{% highlight tex %}
	{% raw %}
    \usepackage{tabu}
    \usepackage{multirow, multicol, makecell}
    \usepackage{rotating}
    \renewcommand\theadfont{\bfseries}
    {% endraw %}
	{% endhighlight %}

I recommend defining one table style and sticking to it for consistency. We will define some table styles in the next post of this series.

### Other Environments

For verbatim listings, e.g. code snippets, you can use the `listings` package. It provides code highlighting as well. 
For typesetting pseudocode, you can load `algorithmicx` with `algpseudocode` as follows. It provides the `algorithm` environment for pseudocode. The label of the environment is changed to 'Table', as we would like to refer to such blocks as tables. You may check the syntax in the documentation of `algorithmicx` package.

    {% highlight tex %}
    {% raw %}
    \usepackage{algorithm}
    \usepackage[noend]{algpseudocode}
    \floatname{algorithm}{Table}
    {% endraw %}
    {% endhighlight %}  

In the following, we load `algorithm2e` package for fancy typesetting of `algorithm` environment. There are also color setting with `xcolor` package, font setting, and more styling details that you may adjust to your needs.

    {% highlight tex %}
    {% raw %}
    \colorlet{commentColor}{Gray!60!black}%
    \usepackage[algoruled,linesnumbered,algochapter,noline,displayblockmarkers]{algorithm2e}%
    \newcommand\mycommfont[1]{\ttfamily\bfseries\textcolor{commentColor}{#1}}%
    \SetCommentSty{mycommfont}%
    \renewcommand{\algorithmcfname}{Table}%
    \SetAlgoBlockMarkers{}{}%
    \SetKwProg{Fn}{}{\{}{}%
    \SetEndCharOfAlgoLine{}%
    \DontPrintSemicolon%
    \SetNlSty{}{}{:}%
    {% endraw %}
    {% endhighlight %}


## References
We need to refer to figures, tables, sections, equations, etc. in the text. All instances of such objects need to be labeled for consistent referrences. Use prefix in your labels, e.g. `\label{sec:introduction}`. 
This will greatly help if you decide to create lists of different objects, e.g. list of images. 
The next level of consistency can be achieved by creating macros for referring to different objects, for example, `\Fig{myfig}` may print `Fig. 10`.
In the following, we discuss bibliography and acronyms. These are also labeled items that we refer to them in the text. We also create lists of bibliography and acronyms. 
However, instead of using `\label` command, we use specific packages to manage these. 

### Bibliography
Use BibTeX or Biber for your bibliography along with the `cite` package. You need to have a separate style for your reference list. The following example is for BibTeX with `IEEEtran` style. This needs a copy of `IEEEtran.bst` file in your working directory.

    {% highlight tex %}
    {% raw %}
    \usepackage{cite}
    \let\labelindent\relax % needed for compatibility with IEEtran
    \renewcommand\citeleft{{\small[}}
    \renewcommand\citeright{{\small]}} 
    \bibliographystyle{IEEEtran}
    \usepackage{url}
    {% endraw %}
    {% endhighlight %}

You need to call `\bibliography{}` command with the name of your BibTex file where you want to place your bibliography list (typically at the end of the document).

    {% highlight tex %}
    {% raw %}
    \renewcommand{\bibname}{References}
    \bibliography{my_biblio_db}
    {% endraw %}
    {% endhighlight %}


### Acronyms and Glossaries
Use `glossaries` package for list of symbols and acronyms.

    {% highlight tex %}
    {% raw %}
    \usepackage[xindy,acronym,shortcuts,nowarn,nosuper,nonumberlist,smallcaps]{glossaries}
    \usepackage{glossary-longragged}
    \usepackage{glossary-tree}
    \setacronymstyle{long-short}
    \glsdisablehyper
    \makeglossaries
    \immediate\write18{makeglossaries \jobname} % runs (pdf)latex twice with --shell-escape
    \makeglossaries
    {% endraw %}
    {% endhighlight %}

This uses small caps for glossaries, if you want normal capital letters for the glossaries list and still small caps for acronyms in the body text, then use this command after loading glossaries package.

    {% highlight tex %}
    {% raw %}
    \renewcommand{\glsnamefont}[1]{\MakeUppercase{#1}}
    {% endraw %}
    {% endhighlight %}

## Lists
The last part of this post is about typesetting lists, i.e. bulleted, ordered or just simple lists. As long as possible, a list must be part of a paragraph, and belong to or contain full sentences. Proper styling of lists is in itself a complicated matter, and you may refer to a style manual for details. Here, we just consider typesetting options in tex, and recommend the use of `enumitem` package. With `enumitem` you can adjust both inline and block lists with a great degree of freedom. For example, I prefer to reduce the spacing on top of the block list compared to defaults. Defining custom lists, especially inline ones, can greatly help with the consistency of the style. 

As an example, the following code creates the list style `hang` for block lists that are hanging from a paragraph with small separation, the style `alph` for lists with alphabetical labels, and a new environment `Ienum` for inline lists with short phrase. If long phrase or sentences are used in inline list, the punctuation would be different. 

    {% highlight tex %}
    {% raw %}
    \usepackage[shortlabels, inline]{enumitem}
    \setlist{nolistsep}
    \SetEnumitemKey{hang}{topsep=3pt, partopsep=1pt, parsep=0pt, itemsep=2pt, 
        leftmargin=!, labelindent=\parindent+1em, labelsep=0.5em, labelwidth=1em}
    \SetEnumitemKey{alph}{label=\emph{\alph*}\textbf{.}}
    \newenvironment{Ienum}{\begin{enumerate*}[label=(\roman*), itemjoin={{, }}, itemjoin*={{, and }}]}%
    {\end{enumerate*}}
    {% endraw %}
    {% endhighlight %}


## To be Continued
This post covered some essential typesetting subjects in LaTeX. There will be a next part from this series covering XeTeX and providing a long list of custom settings and definitions. Stay tuned :)


	



