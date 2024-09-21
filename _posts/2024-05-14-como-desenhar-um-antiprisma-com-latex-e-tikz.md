---
layout: post
title: "Como desenhar um antiprisma com LaTeX e TikZ?"
categories: matemática computação latex tikz
publicado: false
---

<link rel="stylesheet" href="/blog/assets/js/highlight-code/theme.css">
<script src="/blog/assets/js/highlight-code/index.js"></script>
<script src="/blog/assets/js/highlight-code/latex.js"></script>
<script>hljs.highlightAll();</script>

<p>$\DeclareMathOperator{\sen}{sen}\newcommand{\vtu}[1]{\hat{\textbf{#1}}}$Estou escrevendo este post para aumentar a quantidade de imagens disponívels online de um poliedro não muito conhecido: o <b>antiprisma</b>. Talvez você conheça o <b>prisma</b> e tenha intuído que o antiprisma seja, de alguma forma, similar. E você está certo(a).</p>

<p>Os antiprismas são poliedros convexos muito parecidos com prismas. Para começar, a ideia de base do prisma é a mesma para o antiprisma. Eles são formados por duas cópias paralelas de um <b>mesmo</b> polígono convexo, também chamadas de diretrizes. No prisma, as bases são conectadas por uma faixa lateral formada por quadriláteros, e no antiprisma a faixa é composta por triângulos. Os vértices do antiprisma também são dados pelos vértices de suas bases e uma das bases sempre está a uma diferença de $\pi/n$ da outra (metade do ângulo central), onde $n$ é o número de lados da diretriz.</p>

<p>Veja uma comparação entre prismas e antiprismas, na primeira e segunda linha, respectivamente:</p>

<img src="/blog/assets/img/2024/05/14/prismas_e_antiprismas_regulares.png" alt="Comparação entre prismas e antiprismas" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">

> Agora fica a pergunta: como criar esse tipo de desenho com $\LaTeX$ e TikZ?

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
\end{document}</code></pre>

<p>Vamos criar um comando/macro para desenhar um antiprisma regular a partir de alguns parâmetros. Olhando para a forma do antiprisma, seria interessante parametrizar sua construção a partir de, inicialmente, dois parâmetros: o <b>número de lados</b> $n$ da base e a <b>altura</b> $h$.</p>

<p>Como a base do antiprisma é um polígono regular, precisamos de uma outra informação: todo polígono regular está inscrito (dentro) em uma circunferência. Isto é, todos os seus vértices estão na circunferência e sempre a uma distância $r$. Veja alguns casos:</p>

<img src="/blog/assets/img/2024/05/14/polígonos-regulares-n3-n4.png" alt="Polígonos regulares" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">
<img src="/blog/assets/img/2024/05/14/polígonos-regulares-n5-n6.png" alt="Polígonos regulares" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-bottom: 20px;">

<p>Considerando dois eixos $x$ e $y$ com intersecção no centro da circunferência que o polígono regular está inscrito, as coordenadas de qualquer ponto dessa circunferência são:</p>

$$P=(r\cos(\alpha),\,r\sen(\alpha))$$

<p>As coordenadas de $P$ advém da conversão de coordenadas polares para coordenadas cartesianas.</p>

<p>Agora, se queremos uma base sendo um polígono regular de $n$ lados, precisamos saber qual é o ângulo central a partir de $n$. É direto que o ângulo central vale $\alpha=\frac{360^\circ}{n}$. Note que múltiplos de $\alpha$ estão igualmente espaçados ao longo de toda a circunferência.</p>

<p>Por exemplo, a partir da forma de $P$ e de $\alpha$, as coordenadas do triângulo equilátero são, para $\alpha=\frac{360^\circ}{3}=120^\circ$:</p>

$$
\begin{align*}
    P_1&=(r\cos(1\cdot\alpha),\,r\sen(1\cdot\alpha))\\
    &=(r\cos(1\cdot 120^\circ),\,r\sen(1\cdot 120^\circ))
\end{align*}
$$

$$
\begin{align*}
    P_2&=(r\cos(2\cdot\alpha),\,r\sen(2\cdot\alpha))\\
    &=(r\cos(2\cdot 120^\circ),\,r\sen(2\cdot 120^\circ))
\end{align*}
$$

$$
\begin{align*}
    P_3&=(r\cos(3\cdot\alpha),\,r\sen(3\cdot\alpha))\\
    &=(r\cos(3\cdot 120^\circ),\,r\sen(3\cdot 120^\circ))
\end{align*}
$$

<p>Os três pontos diferem-se apenas no valor do arco, que são múltiplos de $\alpha$. Note que a forma geral para $P$ é:</p>

$$P_i=(r\cos(i\cdot\alpha),\,r\sen(i\cdot\alpha))$$

<p>Além disso, surgiu um novo parâmetro para ser adicionado ao processo construtivo: o raio da circunferência circunscrita à base.</p>

<p>Logo, construiremos o antiprisma a partir de três parâmetros: o número de lados $n$ do polígono regular da base, a altura $h$ e o raio $r$ da circunferência circunscrita à base.</p>

<p>Assim, para desenhar o polígono da base precisamos apenas conectar o ponto $P_i$ com o seu próximo $P_{i+1}$ com um segmento de reta através de alguma estrutura iterativa. A estrutura iterativa que vamos utilizar é uma bem conhecida em qualquer linguagem de programação: o <b><a href="https://tikz.dev/pgffor" target="_blank">foreach</a></b> (para cada). Mas antes de montá-lo, é interessante sabermos como criar variáveis dentro do ambiente <b>tikzpicture</b>:</p>

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita à base
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

    \end{tikzpicture}
\end{document}</code></pre>

Conseguimos criar uma variável com o macro <b>\pgfmathsetmacro{identificador}{valor}</b>. Criamos três variáveis que precisaremos para desenhar o antiprisma, mas com valores chumbados que vamos parametrizar depois.

Com isso, ao utilizar o foreach já conseguimos desenhar um polígono regular. Fique à vontade para mudar o valor de $n$ e ver como ele impacta na construção da figura.

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita à base
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

        \foreach \i in {1,...,\n}
        {
            \draw ({\i*\a}:\r) -- ({(\i+1)*\a}:\r);
        }
    \end{tikzpicture}
\end{document}</code></pre>

Utilizamos o comando <b>\draw</b> para desenhar os segmentos de reta para conectar $P_i$ com $P_{i+1}$. Veja que as coordenadas foram escritas no formato polar $(\alpha:r)$, que produz a seguinte figura:

<img src="/blog/assets/img/2024/05/14/polígonos-regulares-n3.png" alt="Polígono regular com 3 lados" style="width: 100%; max-width: 150px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 30px;">

Entretanto, o formato polar $(\alpha:r)$ serve para pontos no plano, mas nosso antiprisma vive em três dimensões. Por isso, é mais conveniente utilizarmos o formato cartesiano de especificação de coordenada, isto é, através de $(x,\,y,\,z)$. Além disso, precisamos que as bases do antiprisma estejam paralelas ao plano $xz$, ou seja, "paralelas ao chão". Basta trocar o cálculo realizado para a coordenada $y$ do ponto para a coordenada $z$, deixando $y$ com um valor constante qualquer:

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita à base
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

        \foreach \i in {1,...,\n}
        {
            % formato (x,0,z)
            \draw ({\r*cos(\i*\a)},0,{\r*sin(\i*\a)}) -- ({\r*cos((\i+1)*\a)},0,{\r*sin((\i+1)*\a)});
        }
    \end{tikzpicture}
\end{document}</code></pre>

Que produz a seguinte figura:

<img src="/blog/assets/img/2024/05/14/triangulo-equilatero-espaco.png" alt="Triângulo equilátero no plano xz" style="width: 100%; max-width: 230px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 30px;">

Em um primeiro momento pode parecer estranho o resultado acima. Por incrível que pareça, ele está correto. Veja o mesmo triângulo em comparação com a base cartesiana $\\{\vtu{x},\,\vtu{y},\,\vtu{z}\\}$:

<img src="/blog/assets/img/2024/05/14/triangulo-equilatero-espaco-base.png" alt="Triângulo equilátero no plano xz em uma base padrão do espaço euclidiano" style="width: 100%; max-width: 230px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 30px;">

Podemos deixar a primeira base do antiprisma como sendo o polígono acima e desenhar uma segunda base da mesma forma, mas alterando a coordenada $y$ com uma nova variável $h$ que representará a altura do nosso sólido, bem como adicionar metade do ângulo central em cada ângulo de seus pontos:

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita à base
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'
        \pgfmathsetmacro{\h}{3} % altura do antiprisma

        \foreach \i in {1,...,\n}
        {
            % formato (x,0,z)
            \draw ({\r*cos(\i*\a)},0,{\r*sin(\i*\a)}) -- ({\r*cos((\i+1)*\a)},0,{\r*sin((\i+1)*\a)});
            % formato (x,h,z)
            \draw ({\r*cos(\i*\a+\a/2)},\h,{\r*sin(\i*\a+\a/2)}) -- ({\r*cos((\i+1)*\a+\a/2)},\h,{\r*sin((\i+1)*\a+\a/2)});
        }
    \end{tikzpicture}
\end{document}</code></pre>

Algumas figuras produzidas variando o valor de $n$:

<img src="/blog/assets/img/2024/05/14/bases-antiprisma-n3-n4.png" alt="Bases de antiprismas com 3 e 4 lados" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 40px;">
<img src="/blog/assets/img/2024/05/14/bases-antiprisma-n5-n6.png" alt="Bases de antiprismas com 5 e 6 lados" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-bottom: 20px;">

Agora, considerando $B_1$ e $B_2$ como sendo o conjunto de vértices da base inferior e superior do antiprisma, respectivamente, podemos conectar o vértice $P_i\in B_1$ com o vértice $P_j\in B_2$, com $i=j$, e também conectar o mesmo $P_j$ com o $P_{i+1}\in B_1$:

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita à base
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'
        \pgfmathsetmacro{\h}{3} % altura do antiprisma

        \foreach \i in {1,...,\n}
        {
            % formato (x,0,z)
            \draw ({\r*cos(\i*\a)},0,{\r*sin(\i*\a)}) -- ({\r*cos((\i+1)*\a)},0,{\r*sin((\i+1)*\a)});
            % formato (x,h,z)
            \draw ({\r*cos(\i*\a+\a/2)},\h,{\r*sin(\i*\a+\a/2)}) -- ({\r*cos((\i+1)*\a+\a/2)},\h,{\r*sin((\i+1)*\a+\a/2)});

            % conectando os vértices das bases
            % P_i com P_j
            \draw ({\r*cos(\i*\a)},0,{\r*sin(\i*\a)}) -- ({\r*cos(\i*\a+\a/2)},\h,{\r*sin(\i*\a+\a/2)});
            % P_j com P_{i+1}
            \draw ({\r*cos(\i*\a+\a/2)},\h,{\r*sin(\i*\a+\a/2)}) -- ({\r*cos((\i+1)*\a)},0,{\r*sin((\i+1)*\a)});
        }
    \end{tikzpicture}
\end{document}</code></pre>

Desenhamos dois novos segmentos em cada iteração para formar os triângulos da lateral do antiprisma. Veja o resultado para alguns valores de $n$:

<img src="/blog/assets/img/2024/05/14/antiprismas-wireframe-n3-n4.png" alt="Wireframes de antiprismas com 3 e 4 lados" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 40px;">
<img src="/blog/assets/img/2024/05/14/antiprismas-wireframe-n5-n6.png" alt="Wireframes de antiprismas com 5 e 6 lados" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-bottom: 20px;">