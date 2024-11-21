---
layout: post
title: "Como desenhar um polígono regular com LaTeX e TikZ?"
categories: matemática computação latex tikz
publicado: false
---

<link rel="stylesheet" href="/blog/assets/js/highlight-code/theme.css">
<script src="/blog/assets/js/highlight-code/index.js"></script>
<script src="/blog/assets/js/highlight-code/latex.js"></script>
<script>hljs.highlightAll();</script>

<p>Um polígono regular é um polígono que possui $n$ (com $n\geq3$) lados com mesmo comprimento e também ângulos internos iguais (congruentes). Para conseguirmos desenhar um polígono regular, precisamos lembrar de uma informação importante:</p>

> Todo polígono regular está inscrito (dentro) em uma circunferência.

<p>Isto é, todos os seus vértices estão na circunferência e sempre a uma distância $r$, que é o próprio raio da circunferência. Veja alguns casos:</p>

<img src="/blog/assets/img/2024/09/23/polígonos-regulares-n3-n4.png" alt="Polígonos regulares - triângulo e quadrado" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">
<img src="/blog/assets/img/2024/09/23/polígonos-regulares-n5-n6.png" alt="Polígonos regulares - pentágono e hexágono" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-bottom: 20px;">

<p>A ideia deste post é: vamos criar um comando/macro em $\LaTeX$ com TikZ para desenhar um polígono regular. Vamos fazer isso de forma parametrizada a partir do número de lados $n$, inicialmente.</p>

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

<p>Ao utilizar o tipo de documento <b>standalone</b>, vamos obter um PDF que conterá somente a imagem, sem bordas desnecessárias. Importando o pacote <b>tikz</b>, conseguimos utilizar o ambiente <b>tikzpicture</b> para colocar nossos comandos de desenho.</p>

<p>Pensando nas formas de escrita de um ponto disponíveis no pacote <b>tikz</b>, vale mais a pena trabalharmos na representação polar. Na representação polar de um ponto, precisamos de apenas duas informações: o raio $r$ da circunferência e do ângulo $\beta$ em relação ao eixo $x$. Veja a ilustração de um ponto $P=(r,\,\beta)$ qualquer:</p>

\\ inserir imagem

<p>Como todos os vértices do polígono regular sempre estão $r$ unidades da origem, basta encontrarmos o valor do ângulo de cada vértice. Para sabermos o valor do ângulo de cada vértice do polígono regular, precisamos calcular o valor do ângulo central $\alpha$ da circunferência em função do número de lados $n$ do polígono. Isto é, é direto que $\alpha=\frac{360^\circ}{n}$. Note que múltiplos de $\alpha$ estão igualmente espaçados ao longo de toda a circunferência.</p>

<p>Por exemplo, a partir $r$ e de $\alpha$, os três pontos que formam o triângulo equilátero são, para $\alpha=\frac{360^\circ}{3}=120^\circ$:</p>

$$
\begin{align*}
    P_1&=(r,\,1\cdot\alpha)\\
    &=(r,\,1\cdot120^\circ)
\end{align*}
$$

$$
\begin{align*}
    P_2&=(r,\,2\cdot\alpha)\\
    &=(r,\,2\cdot120^\circ)\\
    &=(r,\,240^\circ)
\end{align*}
$$

$$
\begin{align*}
    P_3&=(r,\,3\cdot\alpha)\\
    &=(r,\,3\cdot120^\circ)\\
    &=(r,\,360^\circ)
\end{align*}
$$

<p>Da mesma maneira, os quatro pontos que formam o quadrado são, para $\alpha=\frac{360^\circ}{4}=90^\circ$:</p>

$$
\begin{align*}
    P_1&=(r,\,1\cdot\alpha)\\
    &=(r,\,1\cdot90^\circ)
\end{align*}
$$

$$
\begin{align*}
    P_2&=(r,\,2\cdot\alpha)\\
    &=(r,\,2\cdot90^\circ)\\
    &=(r,\,180^\circ)
\end{align*}
$$

$$
\begin{align*}
    P_3&=(r,\,3\cdot\alpha)\\
    &=(r,\,3\cdot90^\circ)\\
    &=(r,\,270^\circ)
\end{align*}
$$

$$
\begin{align*}
    P_4&=(r,\,4\cdot\alpha)\\
    &=(r,\,4\cdot90^\circ)\\
    &=(r,\,360^\circ)
\end{align*}
$$

> Note que essa atribuição de pontos faz sempre o $n$-ésimo ponto ficar sempre com ângulo de {$360^\circ$}, independentemente do valor escolhido para $n$.

<p>Assim, para desenhar o polígono precisamos apenas conectar o ponto $P_i$ com o seu próximo $P_{i+1}$. Conectar o $i$-ésimo com o $(i+1)$-ésimo ponto funciona mesmo quando $i=n$, pois o ângulo do ponto $(n+1)$ é igual ao ângulo do primeiro ponto, pela estrutura cíclica dos ângulos na circunferência.</p>

<p>Vamos realizar a conexão dos pontos com um segmento de reta através de alguma estrutura iterativa. A estrutura iterativa que vamos utilizar é uma bem conhecida em qualquer linguagem de programação: o <b><a href="https://tikz.dev/pgffor" target="_blank">foreach</a></b> (para cada). Mas antes de montá-lo, é interessante sabermos como criar variáveis dentro do ambiente <b>tikzpicture</b>:</p>

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

    \end{tikzpicture}
\end{document}</code></pre>

Conseguimos criar uma variável com o macro <b>\pgfmathsetmacro{identificador}{valor}</b>. Criamos duas variáveis que precisaremos para desenhar o antiprisma: $n$ e $r$, mas com valores chumbados que vamos parametrizar depois. Foi criada também uma terceira variável $a$ para guardar o valor do ângulo central, a partir de $n$.

Com isso, ao utilizar o foreach já conseguimos desenhar um polígono regular. Fique à vontade para mudar o valor de $n$ e ver como ele impacta na construção da figura.

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

        \foreach \i in {1,...,\n} % lista que vai de 1 até '\n'
        {
            % conectando P_i com P_{i+1}
            \draw ({\i*\a}:\r) -- ({(\i+1)*\a}:\r);
        }
    \end{tikzpicture}
\end{document}</code></pre>

Utilizamos o comando <b>\draw</b> para desenhar os segmentos de reta para conectar $P_i$ com $P_{i+1}$. Veja que as coordenadas foram escritas no formato polar $(\alpha:r)$ do <b>tikz</b>, que produz a seguinte figura:

<img src="/blog/assets/img/2024/09/23/polígonos-regulares-n3.png" alt="Polígono regular com 3 lados" style="width: 100%; max-width: 150px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 30px;">

Podemos numerar cada vértice do polígono gerado. Basta adicionar um <b>node</b> para cada segmento:

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}

\begin{document}
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{3} % lados do polígono
        \pgfmathsetmacro{\r}{2} % raio da circunferência circunscrita
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

        \foreach \i in {1,...,\n} % lista que vai de 1 até '\n'
        {
            % conectando P_i com P_{i+1}
            \draw ({\i*\a}:\r) -- ({(\i+1)*\a}:\r) node at ({\i*\a}:{\r+0.3}) {\i};
        }
    \end{tikzpicture}
\end{document}</code></pre>

Que gera o seguinte resultado:

<img src="/blog/assets/img/2024/09/23/triângulo-equilátero-nodes.png" alt="Triângulo equilátero com nodes nos vértices" style="width: 100%; max-width: 150px; margin-left: auto; margin-right: auto; display: block; margin-top: 30px; margin-bottom: 30px;">

Veja que desenhamos o segmento de reta que conecta $P_i$ com $P_{i+1}$ e posicionamos o número do vértice próximo de $P_i$. Nesse processo adicionamos um pequeno valor ao raio para que o número do vértice não fique no mesmo lugar de $P_i$.

Temos o que é necessário para transformar o código acima em um comando de desenho. A ideia é deixar o valor $n$ e o raio $r$ parametrizados. Vamos criar um comando que aceita dois parâmetros. Para isso, crie um novo arquivo dentro do projeto chamado <b>polígono-regular.tex</b> com a seguinte estrutura base:

<pre>
<code class="language-latex">\newcommand{\desenharPoligonoRegular}[2]{
    % conteúdo do comando
}</code></pre>

Um comando com dois parâmetros em $\LaTeX$ é criado com o macro <b>\newcommand{\nomeComando}[número de parâmetros]{}</b>. Vamos copiar o código feito até aqui que desenha o polígono regular e fazer algumas alterações: vamos substituir onde estava $n$ e $r$ por <b>#1</b> e <b>#2</b>, respectivamente:

<pre>
<code class="language-latex">\newcommand{\desenharPoligonoRegular}[2]{
    \begin{tikzpicture}

        \pgfmathsetmacro{\n}{#1} % lados do polígono
        \pgfmathsetmacro{\r}{#2} % raio da circunferência circunscrita
        \pgfmathsetmacro{\a}{360/\n} % ângulo central a partir de '\n'

        \foreach \i in {1,...,\n} % lista que vai de 1 até '\n'
        {
            % conectando P_i com P_{i+1}
            \draw ({\i*\a}:\r) -- ({(\i+1)*\a}:\r) node at ({\i*\a}:{\r+0.3}) {\i};
        }
    \end{tikzpicture}
}</code></pre>

Com o código acima em um arquivo separado, podemos deixar apenas a invocação do comando no arquivo principal:

<pre>
<code class="language-latex">\documentclass{standalone}

\usepackage{tikz}
\input{polígono-regular}

\begin{document}
    \desenharPoligonoRegular{3}{2}
\end{document}</code></pre>

Perceba que importamos o arquivo contendo o comando criado com <b>\input{polígono-regular}</b> no preâmbulo do documento. Isso avisa o compilador que o comando definido no arquivo está disponível. Ao usar o comando <b>\desenharPoligonoRegular{3}{2}</b> estamos rodando o código para desenhar o polígono regular com $n=3$ e $r=2$. A imagem gerada não sofrerá alterações. Se testarmos alguns valores de $n$, teremos os seguintes resultados:

<img src="/blog/assets/img/2024/09/23/polígonos-regulares-n3-n4-nodes.png" alt="Polígonos regulares - triângulo e quadrado com nodes" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">
<img src="/blog/assets/img/2024/09/23/polígonos-regulares-n5-n6-nodes.png" alt="Polígonos regulares - pentágono e quadrado com nodes" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block; margin-top: 20px; margin-bottom: 20px;">