---
published: false
---
## Tex-Typography-II

### XeTeX

	
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

Multiligual support
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
    
## Consistency By Definition
Use macros, pre-defined styles and colors. It makes your life easier.

\definecolor{Fuchsia}{cmyk}{0.27,0.9,0,0}%
\colorlet{rowcolor1}{Fuchsia!50!white}

	\newcommand{\TR}{\ensuremath{^{\raisemath{0pt}{\mathrm{\mathsmaller{T}}}}}}% Transpose symbol


	% Definintion Equality, substitudes \triangleq
	\newcommand{\defeq}{%
  	\mathrel{\vbox{\offinterlineskip\ialign{%
    	\hfil##\hfil\cr
    	$\scriptscriptstyle\triangle$\cr
    	\noalign{\kern.25ex}
    	$=$\cr
	}}}}


	% Define a better setminus
	\newcommand{\mysetminusD}{\hbox{\tikz{\draw[line width=0.6pt,line cap=round] (3pt,0) -- (0,6pt);}}}
	\newcommand{\mysetminusT}{\mysetminusD}
	\newcommand{\mysetminusS}{\hbox{\tikz{\draw[line width=0.45pt,line cap=round] (2pt,0) -- (0,4pt);}}}
	\newcommand{\mysetminusSS}{\hbox{\tikz{\draw[line width=0.4pt,line cap=round] (1.5pt,0) -- (0,3pt);}}}
	\DeclareRobustCommand{\mysetminus}{\mathbin{\mathchoice{\mysetminusD}{\mysetminusT}	{\mysetminusS}{\mysetminusSS}}}


% Use wide accents from Math Time Pro font
\DeclareFontEncoding{LMP2}{}{}
\DeclareFontSubstitution{LMP2}{mtt}{m}{n}
\DeclareFontFamily{LMP2}{mtt}{\skewchar\font48}
\DeclareFontShape{LMP2}{mtt}{m}{n}{<-7> mt2syf <7-9> mt2sys <9-> mt2syt}{\skewchar\font32}

\DeclareSymbolFont{mtsymbols}{LMP2}{mtt}{m}{n}

\DeclareMathAccent{\what}  {\mathord}{mtsymbols}{"79}
\DeclareMathAccent{\wtilde}{\mathord}{mtsymbols}{"7A}
\DeclareMathAccent{\wcheck}{\mathord}{mtsymbols}{"7B}
\DeclareMathAccent{\wbar}  {\mathord}{mtsymbols}{"78}

%bar under the symbol
\newcommand{\ubar}[1]{\underaccent{\bar}{#1}}

%%% Units
\newcommand{\us}{\relax\ifmmode \,\mathrm{\mu s}
\else {\,{\textmu}s\xspace}\expandafter\xspace\fi}% microsecond

\newcommand{\ns}{\relax\ifmmode \,\mathrm{ns}
\else {\,ns\xspace}\expandafter\xspace\fi}% microsecond

\newcommand{\ms}{\relax\ifmmode \,\mathrm{ms}
\else {\,ms\xspace}\expandafter\xspace\fi}% microsecond

\newcommand{\ppm}{\relax\ifmmode \,\mathrm{ppm}
\else {\,ppm\xspace}\expandafter\xspace\fi}% ppm, part/million

\newcommand{\db}{\relax\ifmmode \,\mathrm{dB} 
\else {\,dB\xspace}\expandafter\xspace\fi}% dB, decibel

\newcommand{\dbm}{\relax\ifmmode \,\mathrm{dBm} 
\else {\,dBm\xspace}\expandafter\xspace\fi}% dB, decibel

\newcommand{\mbps}{\relax\ifmmode \,\text{Mbit}{/}\text{s}
\else {\,$\text{Mbit}{/}\text{s}$\xspace}\expandafter\xspace\fi}% 

\newcommand{\msps}{\relax\ifmmode \,\text{MS}{/}\text{s}
\else {\,$\text{MS}{/}\text{s}$\xspace}\expandafter\xspace\fi}% 

\newcommand{\hz}{\relax\ifmmode \,\mathrm{Hz}
\else {\,Hz\xspace}\expandafter\xspace\fi}% 

\newcommand{\khz}{\relax\ifmmode \,\mathrm{KHz}
\else {\,KHz\xspace}\expandafter\xspace\fi}% 

\newcommand{\mhz}{\relax\ifmmode \,\mathrm{MHz}
\else {\,MHz\xspace}\expandafter\xspace\fi}% 

\newcommand{\ghz}{\relax\ifmmode \,\mathrm{GHz}
\else {\,GHz\xspace}\expandafter\xspace\fi}% 

\newcommand{\cm}{\relax\ifmmode \,\mathrm{cm}
\else {\,cm\xspace}\expandafter\xspace\fi}% 

\newcommand{\mm}{\relax\ifmmode \,\mathrm{mm}
\else {\,mm\xspace}\expandafter\xspace\fi}% 

\newcommand{\meter}{\relax\ifmmode \,\mathrm{m}
\else {\,m\xspace}\expandafter\xspace\fi}% 

\newcommand{\degc}{\relax\ifmmode \mathrm{\textcelsius} 
\else {\textcelsius\xspace}\expandafter\xspace\fi}% dB, decibel

\newcommand{\degree}{\relax\ifmmode ^{\circ} 
\else {$^{\circ}$\xspace}\expandafter\xspace\fi}% dB, decibel

\newcommand{\Dollar}{{\fontfamily{cmr}\fontseries{m}\fontsize{10}{10}\selectfont\textdollaroldstyle}}

%\newcommand{\PM}{\protect\raisebox{.25ex}{\scriptstyle{\mathrm{\pm}}$}}  % plus-minus
\newcommand{\PM}{\textpm}  % plus-minus


%\newcommand{\sless}{\raisebox{.2ex}{\begingroup\scriptsize{<\,}\endgroup} }
%\newcommand{\lless}{\raisebox{.2ex}{\begingroup{<<\,}\endgroup}}

\newcommand{\sless}{\raisebox{.1ex}{$\scriptstyle{<}$}\,}
\newcommand{\lless}{\raisebox{.1ex}{$\scriptstyle{\ll}$}\,}


\newcommand{\Node}[1]{node~#1}

%\newcommand{\vect}[1]{\ensuremath{\boldsymbol{\mathbf{#1}}}}
%\newcommand{\mat}[1]{\ensuremath{\boldsymbol{\mathbf{#1}}}}
\newcommand{\vect}[1]{\ensuremath{\mathbfup{#1}}}
\newcommand{\mat}[1]{\ensuremath{\mathbfup{#1}}}
% define \set command
%\makeatletter
%\@ifundefined{mathscr}
%{\newcommand{\set}[1]{\ensuremath{\mathcal{#1}}}}
%{\newcommand{\set}[1]{\ensuremath{\mathscr{#1}}}}
%\makeatother
%\newcommand{\set}[1]{\ensuremath{\mathbb{#1}}}
\newcommand{\set}[1]{\ensuremath{\mathcal{#1}}}
%
\newcommand{\freq}[1]{#1}
%\newcommand{\freq}[1]{\ensuremath{\mathscr{#1}}}



%%%%%%%%%%%%%%%%%%%%%% Some operators %%%%%%%%%%%%%%%%%%%%%%%%%%
\DeclareMathOperator*{\argmin}{arg\,min}
\DeclareMathOperator*{\argmax}{arg\,max}
\DeclareMathOperator*{\minimize}{minimize}
\DeclareMathOperator*{\maximize}{maximize}
\DeclareMathOperator*{\trace}{tr}
%
\DeclareMathOperator*{\sign}{sign}
%\DeclareMathOperator*{\diag}{diag}
\DeclareMathOperator*{\atan2}{atan2}

\DeclareMathOperator*{\cov}{cov}
\DeclareMathOperator*{\Cov}{Cov}
\DeclareMathOperator*{\Var}{Var}

%
\newcommand{\argminu}[1]{\underset{#1}{\argmin}}
\newcommand{\argmaxu}[1]{\underset{#1}{\argmax}}
\newcommand{\minimizeu}[1]{\underset{\raisebox{-0.2em}{\scalebox{0.8}{\ensuremath{#1}}}}{\minimize}}
%\newcommand{\minimizeu}[1]{\underset{\raisebox{-0.2em}{\scalebox{0.2}{\ensuremath{#1}}}}{\minimize}}
\newcommand{\maximizeu}[1]{\underset{#1}{\maximize}}
\newcommand{\minu}[1]{\underset{#1}{\min}}
\newcommand{\maxu}[1]{\underset{#1}{\max}}
% \underset
\newcommand{\modi}{\ensuremath{\operatorname{mod}}}
%\newcommand{\diag}{\ensuremath{\operatorname{diag}}}
\newcommand{\diag}{\ensuremath{\operatorname{\delta}}}
\newcommand{\rank}{\ensuremath{\operatorname{rank}}}
%\newcommand{\det}{\ensuremath{\operatorname{det}}}
\newcommand{\tran}{\ensuremath{\operatorname{tr}}} % transpose
\newcommand{\rel}{\ensuremath{\operatorname{rel}}} % transpose
\newcommand{\toep}{\ensuremath{\operatorname{toep}}}
\newcommand{\conv}{\ensuremath{\operatorname{conv}}}
\newcommand{\Exp}[2][]{\ensuremath{\varmathbb{E}\IfValueT{#1}{_{#1}}\raisemath{1pt}{\left[#2\right]}}} % Expected value



%\renewcommand{\Re}[1]{\ensuremath{\operatorname{Re}\left(#1\right)}}
%\renewcommand{\Im}[1]{\ensuremath{\operatorname{Im}\left(#1\right)}}
%\let\oldRe\Re
%\let\oldIm\Im
%\renewcommand{\Re}[1]{\ensuremath{\oldRe\left(#1\right)}}
%\renewcommand{\Im}[1]{\ensuremath{\oldIm\left(#1\right)}}

%\def\Graph#1{\GraphInner(#1)}
%\def\GraphInner(#1,#2,#3){\ensuremath{{#1}({#2},{#3})}}
\makeatletter   
\def\Graph#1{\expandafter\Graph@i#1,,,\@nil}
\def\Graph@i#1,#2,#3,#4\@nil{%    
	\ifx $#2$ \ensuremath{{#1}} \else   
		%\ifx $#4$ {\ensuremath{{#1}({#2},{#3})}}           
		%\fi  
		\ensuremath{{#1}(\set{#2},\set{#3})}
	\fi  
}   
\makeatother

\newcommand{\node}[1]{\ensuremath{{#1}}}
\newcommand{\edge}[1]{\ensuremath{{#1}}}

\newcommand{\Uni}[2]{\ensuremath{\mathscr{U}\left(}{#1},\,{#2}\ensuremath{\right)}}
%\newcommand{\Normal}[2]{\ensuremath{\mathscr{N}\left(}{#1},\, {#2}\ensuremath{\right)}}
\newcommand{\Normal}[2]{\ensuremath{\mathcal{N}\left(}{#1},\hspace{2pt}{#2}\ensuremath{\right)}}
\newcommand{\CNormal}[2]{\ensuremath{\mathscr{N}_{\mathcal{C}}\left(}{#1},\, {#2}\ensuremath{\right)}}
\newcommand{\Rice}[2]{\ensuremath{\operatorname{Rice}\left(}{#1},\, {#2}\ensuremath{\right)}}

\makeatletter
\@ifundefined{varmathbb}{%
  \newcommand\varmathbb[1]{\mathbb{#1}}
 }{}
\makeatother

% Sets
\newcommand{\realSet}[1]{\ensuremath{\varmathbb{R}^{#1}}}
\newcommand{\realSetP}[1]{\ensuremath{\varmathbb{R}^{#1}_{+}}}
\newcommand{\compSet}[1]{\ensuremath{\varmathbb{C}^{#1}}}
\newcommand{\intSet}[1]{\ensuremath{\varmathbb{Z}^{#1}}}
\newcommand{\natSet}[1]{\ensuremath{\varmathbb{N}^{#1}}}
%
\newcommand{\losSet}{\set{P}_{\textsc{los}}}
\newcommand{\sbrSet}{\set{P}_{\textsc{sbr}}}
%
\newcommand{\EDM}[1]{\ensuremath{\varmathbb{EDM}^{\raisemath{-1pt}{#1}}}}
\newcommand{\PSD}[1]{\ensuremath{\varmathbb{S}_+^{#1}}}
\newcommand{\symSet}[1]{\ensuremath{\varmathbb{S}^{#1}}}
\newcommand{\ortSet}[1]{\ensuremath{\varmathbb{O}({#1})}}

\newcommand{\Deg}{$^{\circ}$}
\newcommand{\TM}{$^{\text{\tiny{TM}}}$}
%\newcommand{\TM}{\copyright}

\newcommand{\Grad}{\ensuremath{\bm{\nabla}}}

% Euclidean spaces, 2D nd 3D
\newcommand{\Etwo}{$\mathbb{E}^2$\xspace}
\newcommand{\Etri}{$\mathbb{E}^3$\xspace}


\newcommand\dash{\nobreakdash-\hspace{0pt}}
\newcommand\nth{$n$\nobreakdash-th\xspace}


\newcommand\NP{$\mathcal{NP}$}

% New sum command 
%\newlength{\depthofsumsign}
%\setlength{\depthofsumsign}{\depthof{$\sum$}}
%\newlength{\extrapushdown}
%\setlength\extrapushdown{5pt}
%\newcommand{\nsum}[1][1.4]{% only for \displaystyle
%	\mathop{%
%		\raisebox
%		{-#1\depthofsumsign-#1\extrapushdown}
%		{\scalebox
%			{#1}
%			{$\displaystyle\sum$}%
%		}
%	}
%}

%%%%%%%%%% Personal variable and matrices

\newcommand{\Imat}{\relax\ifmmode \mat{A}%
\else {\mat{A}\xspace}\expandafter\xspace\fi}%

\newcommand{\RImat}{\relax\ifmmode \mat{\wtilde{A}}%
\else {\mat{\wtilde{A}}\xspace}\expandafter\xspace\fi}%

\newcommand{\Amat}{\relax\ifmmode \mat{M}%
\else {\mat{M}\xspace}\expandafter\xspace\fi}%

\newcommand{\MAmat}{\relax\ifmmode \mat{\wtilde{M}}%
\else {\mat{\wtilde{M}}\xspace}\expandafter\xspace\fi}%

\newcommand{\Cmat}{\relax\ifmmode \mat{B}%
\else {\mat{B}\xspace}\expandafter\xspace\fi}%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Referencing and Citation

\newcounter{rownumbers}
\setcounter{rownumbers}{0}
\newcommand\rowno{\stepcounter{rownumbers}\arabic{rownumbers}{.}} 

%\newcommand\chap[1]{chapter~\ref{chap:#1}}
%\newcommand\sect[1]{section~\ref{sec:#1}}
%\newcommand\ssect[1]{subsection~\ref{sec:#1}}
%\newcommand\appex[1]{appendix~\ref{appex:#1}}
%\newcommand\eq[1]{~(\ref{eq:#1})}
%\newcommand\eeq[1]{eq.~(\ref{eq:#1})}
%\newcommand\fig[1]{figure~\ref{fig:#1}}
%\newcommand\tab[1]{table~\ref{tab:#1}}
%\newcommand\theo[1]{\textit{theorem~\ref{th:#1}}}
%\newcommand\lst[1]{listing~\ref{lst:#1}}
%\newcommand\defi[1]{definition~\ref{def:#1}}
%\newcommand\alg[1]{table~\ref{alg:#1}}
%\newcommand\proc[1]{table~\ref{alg:#1}}
%\newcommand\stage[2]{(\alg{#1}~step~#2)}

\newcommand\chap[1]{Chapter~\ref{chap:#1}}
\newcommand\sect[1]{Section~\ref{sec:#1}}
\newcommand\ssect[1]{Subsection~\ref{sec:#1}}
\newcommand\appex[1]{Appendix~\ref{appex:#1}}
\newcommand\eq[1]{~(\ref{eq:#1})}
\newcommand\eeq[1]{Eq.~(\ref{eq:#1})}
\newcommand\fig[1]{Figure~\ref{fig:#1}}
\newcommand\tab[1]{Table~\ref{tab:#1}}
\newcommand\theo[1]{\textit{Theorem~\ref{th:#1}}}
\newcommand\lst[1]{Listing~\ref{lst:#1}}
\newcommand\defi[1]{Definition~\ref{def:#1}}
\newcommand\alg[1]{Table~\ref{alg:#1}}
\newcommand\proc[1]{Table~\ref{alg:#1}}
\newcommand\stage[2]{(\alg{#1}~Step~#2)}

\newcommand\Chap[1]{Chapter~\ref{chap:#1}}
\newcommand\Sect[1]{Section~\ref{sec:#1}}
\newcommand\Ssect[1]{Subsection~\ref{sec:#1}}
\newcommand\Appex[1]{Appendix~\ref{appex:#1}}
\newcommand\Eq[1]{~(\ref{eq:#1})}
\newcommand\Eeq[1]{eq.~(\ref{eq:#1})}
\newcommand\Fig[1]{Fig.~\ref{fig:#1}}
%\newcommand\Fig[1]{Figure~\ref{fig:#1}}
\newcommand\Tab[1]{Table~\ref{tab:#1}}
\newcommand\Theo[1]{\textit{Theorem~\ref{th:#1}}}
\newcommand\Lst[1]{Listing~\ref{lst:#1}}
\newcommand\Defi[1]{Definition~\ref{def:#1}}
\newcommand\Alg[1]{Table~\ref{alg:#1}}
\newcommand\Proc[1]{Table~\ref{alg:#1}}
\newcommand\Stage[2]{(\Alg{#1}~step~#2)}

\newcommand\colName[1]{\emph{#1}}

% Chapter and section citing
%\newcommand\ccite[2]{\cite[Chapter~{#2}]{{#1}}} % cite a chapter
%\newcommand\scite[2]{\cite[Section~{#2}]{{#1}}} % cite a section


% \cite with non-breaking space
\let\oldcite\cite
\renewcommand{\cite}{ \oldcite}
\newcommand{\bcite}{ (\oldcite)}

\newcommand\pcite[2]{\mbox{\cite[p.\,{#2}]{{#1}}}}% cite a chapter
\newcommand\ccite[2]{\mbox{\cite[chap.\,{#2}]{{#1}}}}% cite a chapter
\newcommand\scite[2]{\mbox{\cite[sec.\,{#2}]{{#1}}}}% cite a section
\newcommand\acite[2]{\mbox{\cite[appx.\,{#2}]{{#1}}}}% cite an appendix

%\newcommand\citep[1]{[P. \cp{#1}]}
\newcommand\citep[1]{[\cpub{#1}]}


\newcommand\ieeecr[1]{Copyright #1 IEEE.}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Lists and presentation styles


\newcommand\bfitem[1]{\item{\bfseries #1}} % Bold face item

\newcommand{\buitem}{\item[$\bullet$]}
\newcommand{\bsitem}{\item[$\bigstar$]}
\newcommand{\sqitem}{\item[\blacksquare]}
\newcommand{\tritem}{\item[$\blacktriangleright$]}
\newcommand{\stitem}{\item[$\scriptstyle\blacktriangleright$]}

\fboxsep 2pt
\newcommand{\hilight}[1]{\colorbox{hilightcolor}{#1}}
\newcommand{\eqlight}[1]{\begin{center} \colorbox{hilightcolor}{\parbox{0.8\textwidth}{#1}} \end{center}}
\newcommand{\boxlight}[2]{\begin{center} \colorbox{hilightcolor}{\parbox{#1\linewidth}{#2}} \end{center}}

\newcommand{\tr}{$\blacktriangleright\,\,$}

\newcommand{\llab}[1]{\emph{\textbf{#1.}}} % List label for inline

%\newenvironment{Ienum}{\begin{enumerate*}[label=\textbf{\emph{\alph*})}]}%
%		{\end{enumerate*}}

%\newenvironment{Ienum}{\begin{enumerate*}[label=(\roman*),before=\unskip{: }, itemjoin={{; }}, itemjoin*={{; and }}]}%
%{\end{enumerate*}}

% Inline (and) list of short phrases
\newenvironment{Ienum}{\begin{enumerate*}[label=(\roman*), itemjoin={{, }}, itemjoin*={{, and }}]}%
{\end{enumerate*}}
% Inline list of complete sentences
\newenvironment{Ienum1}{\begin{enumerate*}[label=(\roman*), itemjoin={{ }}, itemjoin*={{ }}]}%
	{\end{enumerate*}}
% Inline (and) list of long phrases or complete sentences
\newenvironment{Ienum2}{\begin{enumerate*}[label=(\roman*), itemjoin={{; }}, itemjoin*={{; and }}]}%
{\end{enumerate*}}
% Inline (or) list of short phrases
\newenvironment{Ienum3}{\begin{enumerate*}[label=(\roman*), itemjoin={{, }}, itemjoin*={{, or }}]}%
{\end{enumerate*}}
% Inline (or) list of long phrases or complete sentences
\newenvironment{Ienum4}{\begin{enumerate*}[label=(\roman*), itemjoin={{; }}, itemjoin*={{; or }}]}%
{\end{enumerate*}}

\newenvironment{Thenum}{\begin{enumerate}[hang-2, label=\textbf{\emph{\roman*.}}]}%
{\end{enumerate}}
