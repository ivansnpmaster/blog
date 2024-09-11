---
layout: post
title: "Como desenhar um antiprisma regular com LaTeX e TikZ?"
categories: matemática computação latex tikz
publicado: false
---

<!-- Adicionando CSS do Highlight.js -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/monokai-sublime.min.css">
<!-- Adicionando JS do Highlight.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/highlight.min.js"></script>
<!-- Adicionando suporte a LaTeX -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/languages/latex.min.js"></script>

<!-- Inicializando o Highlight.js -->
<script>hljs.highlightAll();</script>

<p>Estou escrevendo este post para aumentar a quantidade de imagens disponívels online de um poliedro não muito conhecido: o <b>antiprisma</b> regular.</p> Talvez você conheça o <b>prisma</b> regular e tenha intuído que o antiprisma seja, de alguma forma, similar. E você está certo(a).

<p>Os antiprismas regulares são poliedros convexos muito parecidos com prismas regulares. Para começar, a ideia de base do prisma é a mesma para o antiprisma. Eles são formados por duas cópias paralelas de um <b>mesmo</b> polígono convexo, também chamados de diretrizes. No prisma, as bases são conectadas por uma faixa lateral formada por retângulos, e no antiprisma a faixa é composta por triângulos. Os vértices do antiprisma também são dados pelos vértices de suas bases e uma das bases sempre está a uma diferença de $\pi/n$ da outra, onde $n$ é o número de lados da diretriz.</p>

<p>Veja uma comparação entre prismas regulares e antiprismas regulares, na primeira e segunda linha, respectivamente:</p>

<img src="/blog/assets/img/2024/05/14/prismas_e_antiprismas_regulares.png" alt="Comparação entre prismas e antiprismas" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">

<p>Agora fica a pergunta: como criar esse tipo de desenho com $\LaTeX$ e Tikz?</p>

<p>Eu costumo utilizar o <a href="https://pt.overleaf.com/" target="_blank">Overleaf</a> para escrever documentos com $\LaTeX$, mas você pode utilizar outro de sua preferência.</p>

<p>Após criar o projeto, podemos estruturar um documento mínimo para criação da nossa figura de interesse:</p>

<!-- Exemplo de código LaTeX -->
<pre><code class="language-latex">\documentclass{standalone}

% carregando o pacote 'tikz' para criar desenhos
\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}
        % digitaremos macros da biblioteca 'tikz' para criar a figura dentro do ambiente 'tikzpicture'
    \end{tikzpicture}
\end{document}
</code></pre>