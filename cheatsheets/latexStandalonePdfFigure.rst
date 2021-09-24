###############################
Stand-alone PDF Figure in LaTeX
###############################

Easiest thing is to use pdfcrop.  ::

  \documentclass{article}
  \usepackage{graphicx}
  \usepackage{caption}
  \usepackage{subcaption}
  \pagestyle{empty}
  \begin{document}
  \begin{figure}[!ht]
    \centering
    \begin{subfigure}{1\textwidth}
    \begin{Large}A)\end{Large}
    \end{subfigure}
    \begin{subfigure}{1\textwidth}
    \includegraphics[width=1\textwidth]{../img/rf/m5_2010_allyears_allphases.pdf} 
    \end{subfigure}
    \begin{subfigure}{1\textwidth}
    \begin{Large}B)\end{Large}
    \end{subfigure}
    \begin{subfigure}{1\textwidth}
    \includegraphics[width=1\textwidth]{../img/rf/m5_2010_by_two_allphases.pdf} 
    \end{subfigure}
    \end{figure}
  \end{document}
  
  
and then  ::
 
  files=`ls Figure?.tex`
  for f in $files
  do
    pdflatex $f
    f2="${f/.tex/.pdf}"
    f3="${f2/.pdf/-crop.pdf}"
    pdfcrop $f2
    rm $f2
    mv $f3 $f2
  done
