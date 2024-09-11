---
layout: post
title: "Como desenhar um antiprisma regular com LaTeX e TikZ?"
categories: matemática computação latex tikz
publicado: true
---

<p>Estou escrevendo este post para aumentar a quantidade de imagens disponívels online de um poliedro não muito conhecido: o <b>antiprisma</b> regular.</p> Talvez você conheça o <b>prisma</b> regular e tenha intuído que o antiprisma seja, de alguma forma, similar. E você está certo(a).

<p>Os antiprismas regulares são poliedros convexos muito parecidos com prismas regulares. Para começar, a ideia de base do prisma é a mesma para o antiprisma. Eles são formados por duas cópias paralelas de um <b>mesmo</b> polígono convexo, também chamadas de diretrizes. No prisma, as bases são conectadas por uma faixa lateral formada por retângulos, e no antiprisma a faixa é composta por triângulos. Os vértices do antiprisma também são dados pelos vértices de suas bases e uma das bases sempre está a uma diferença de $\pi/n$ da outra, onde $n$ é o número de lados da diretriz. Veja uma comparação entre prismas regulares e antiprismas regulares, na primeira e segunda linha, respectivamente:</p>

<img src="/blog/assets/img/2024/05/14/prismas_e_antiprismas_regulares.png" alt="Comparação entre prismas e antiprismas" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">

<p>Agora fica a pergunta: como criar esse tipo de desenho com $\LaTeX$ e Tikz?</p>

<p>Eu costumo utilizar o <a href="https://pt.overleaf.com/">Overleaf</a> para escrever documentos com $\LaTeX$, mas você pode utilizar outro de sua preferência.</p>

<p>Após criar o projeto, podemos estruturar um documento mínimo para criação da nossa figura de interesse:</p>

<form action="https://www.overleaf.com/docs" method="post" target="_blank">
    <textarea rows="8" cols="60" name="snip">
    \usepackage[T1]{fontenc}
    \usepackage{amsmath}

    \begin{document}
    \noindent
    Bla bla bla bla :
    \begin{align*}
    A &amp;= B + C - D \\ \\
    %phantom
    &amp;\phantom{= B + C \;}
    %phantom
    + D - E \\ \\
    &amp;= F + G - H.
    \end{align*}
    \end{document}
    </textarea>
    <input type="submit" value="Open in Overleaf">
</form>