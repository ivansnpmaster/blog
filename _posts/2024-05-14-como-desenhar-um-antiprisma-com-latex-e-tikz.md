---
layout: post
title: "Como desenhar um antiprisma regular com LaTeX e TikZ?"
categories: matemática computação latex tikz
publicado: false
---

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/monokai-sublime.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/highlight.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/languages/latex.min.js"></script>
<script>hljs.highlightAll();</script>

$
    \DeclareMathOperator{\sen}{sen}
$

<p>Estou escrevendo este post para aumentar a quantidade de imagens disponívels online de um poliedro não muito conhecido: o <b>antiprisma</b> regular.</p> Talvez você conheça o <b>prisma</b> regular e tenha intuído que o antiprisma seja, de alguma forma, similar. E você está certo(a).

<p>Os antiprismas regulares são poliedros convexos muito parecidos com prismas regulares. Para começar, a ideia de base do prisma é a mesma para o antiprisma. Eles são formados por duas cópias paralelas de um <b>mesmo</b> polígono convexo, também chamados de diretrizes. No prisma, as bases são conectadas por uma faixa lateral formada por retângulos, e no antiprisma a faixa é composta por triângulos. Os vértices do antiprisma também são dados pelos vértices de suas bases e uma das bases sempre está a uma diferença de $\pi/n$ da outra, onde $n$ é o número de lados da diretriz.</p>

<p>Veja uma comparação entre prismas regulares e antiprismas regulares, na primeira e segunda linha, respectivamente:</p>

<img src="/blog/assets/img/2024/05/14/prismas_e_antiprismas_regulares.png" alt="Comparação entre prismas e antiprismas" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">

> Agora fica a pergunta: como criar esse tipo de desenho com $\LaTeX$ e Tikz?

<p>Eu costumo utilizar o <a href="https://pt.overleaf.com/" target="_blank">Overleaf</a> para escrever documentos com $\LaTeX$, mas você pode utilizar outro de sua preferência.</p>

<p>Após criar o projeto, podemos estruturar um documento mínimo para criação da nossa figura de interesse:</p>

<pre>
<code class="language-latex">\documentclass{standalone}

% pacote 'tikz' para criar desenhos
\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}
        % conteúdo
    \end{tikzpicture}
\end{document}
</code>
</pre>

<p>Vamos criar um comando/macro para desenhar um antiprisma regular a partir de alguns parâmetros. Olhando para a forma do antiprisma, seria interessante parametrizar sua construção a partir de, inicialmente, dois parâmetros: o <b>número de lados</b> $n$ da base e a <b>altura</b> $h$.</p>

<p>Como a base do antiprisma é um polígono regular, precisamos de uma outra informação: todo polígono regular está inscrito (dentro) em uma circunferência. Isto é, todos os seus vértices estão na circunferência e sempre a uma distância $r$. Veja alguns casos:</p>

// Mostrar casos

<b>Considerando dois eixos $x$ e $y$ com intersecção no centro da circunferência que o polígono regular está inscrito, a coordenada de qualquer ponto dessa circunferência pode ser dada por:</b>

$$P=(r\cos(\alpha),\,r\sen(\alpha))$$

<p>As coordenadas de $P$ advém da aplicação das definições de seno e cosseno de um arco no triângulo retângulo.</p>

<p>Agora, se queremos uma base sendo um polígono regular de $n$ lados, precisamos saber qual é o ângulo central a partir de $n$. É direto que o ângulo central vale $\alpha=\frac{360^\circ}{n}$. Note que múltiplos de $\alpha$ estão igualmente espaçados ao longo de toda a circunferência.</p>

<p>Por exemplo, a partir da forma de $P$ e de $\alpha$, as coordenadas do triângulo equilátero são, para $\alpha=\frac{360^\circ}{3}=120^\circ$:</p>

$$P_1=(r\cos(1\cdot\alpha),\,r\sen(1\cdot\alpha))=(r\cos(1\cdot 120^\circ),\,r\sen(1\cdot 120^\circ))$$
$$P_2=(r\cos(2\cdot\alpha),\,r\sen(2\cdot\alpha))=(r\cos(2\cdot 120^\circ),\,r\sen(2\cdot 120^\circ))$$
$$P_3=(r\cos(3\cdot\alpha),\,r\sen(3\cdot\alpha))=(r\cos(3\cdot 120^\circ),\,r\sen(3\cdot 120^\circ))$$

<p>Os três pontos diferem-se apenas no valor do arco, que são múltiplos de $\alpha$. Além disso, surgiu um novo parâmetro para ser adicionado ao processo construtivo: o raio da circunferência circunscrita à base.</p>

<p>Logo, construiremos o antiprisma a partir de três parâmetros: o número de lados $n$ do polígono regular da base, a altura $h$ e o raio $r$ da circunferência circunscrita à base.</p>

<p>Assim, para desenhar o polígono da base precisamos apenas conectar o ponto $P_i$ com o seu próximo $P_{i+1}$ com um segmento de reta através de alguma estrutura iterativa. A estrutura iterativa que vamos utilizar é uma bem conhecida em qualquer linguagem de programação: o <b><a href="https://tikz.dev/pgffor" target="_blank">foreach</a></b> (para cada), que possui o seguinte formato:</p>