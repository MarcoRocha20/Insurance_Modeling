# Insurance_Modeling
Base de dados da Susep (Autoseg), para incidência de sinistros para seguros de automóveis. Análise exploratória dos dados e ajuste um modelo para a frequência e severidade de sinistros em função das variáveis: sexo, idade do condutor e estado.
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en"><head>

<meta charset="utf-8">
<meta name="generator" content="quarto-1.2.247">

<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">

<meta name="author" content="Marco Rocha - Debora Rocha">

<title>Trabalho Final - Tarifação</title>
<style>
code{white-space: pre-wrap;}
span.smallcaps{font-variant: small-caps;}
div.columns{display: flex; gap: min(4vw, 1.5em);}
div.column{flex: auto; overflow-x: auto;}
div.hanging-indent{margin-left: 1.5em; text-indent: -1.5em;}
ul.task-list{list-style: none;}
ul.task-list li input[type="checkbox"] {
  width: 0.8em;
  margin: 0 0.8em 0.2em -1.6em;
  vertical-align: middle;
}
pre > code.sourceCode { white-space: pre; position: relative; }
pre > code.sourceCode > span { display: inline-block; line-height: 1.25; }
pre > code.sourceCode > span:empty { height: 1.2em; }
.sourceCode { overflow: visible; }
code.sourceCode > span { color: inherit; text-decoration: inherit; }
div.sourceCode { margin: 1em 0; }
pre.sourceCode { margin: 0; }
@media screen {
div.sourceCode { overflow: auto; }
}
@media print {
pre > code.sourceCode { white-space: pre-wrap; }
pre > code.sourceCode > span { text-indent: -5em; padding-left: 5em; }
}
pre.numberSource code
  { counter-reset: source-line 0; }
pre.numberSource code > span
  { position: relative; left: -4em; counter-increment: source-line; }
pre.numberSource code > span > a:first-child::before
  { content: counter(source-line);
    position: relative; left: -1em; text-align: right; vertical-align: baseline;
    border: none; display: inline-block;
    -webkit-touch-callout: none; -webkit-user-select: none;
    -khtml-user-select: none; -moz-user-select: none;
    -ms-user-select: none; user-select: none;
    padding: 0 4px; width: 4em;
    color: #aaaaaa;
  }
pre.numberSource { margin-left: 3em; border-left: 1px solid #aaaaaa;  padding-left: 4px; }
div.sourceCode
  {   }
@media screen {
pre > code.sourceCode > span > a:first-child::before { text-decoration: underline; }
}
code span.al { color: #ff0000; font-weight: bold; } /* Alert */
code span.an { color: #60a0b0; font-weight: bold; font-style: italic; } /* Annotation */
code span.at { color: #7d9029; } /* Attribute */
code span.bn { color: #40a070; } /* BaseN */
code span.bu { color: #008000; } /* BuiltIn */
code span.cf { color: #007020; font-weight: bold; } /* ControlFlow */
code span.ch { color: #4070a0; } /* Char */
code span.cn { color: #880000; } /* Constant */
code span.co { color: #60a0b0; font-style: italic; } /* Comment */
code span.cv { color: #60a0b0; font-weight: bold; font-style: italic; } /* CommentVar */
code span.do { color: #ba2121; font-style: italic; } /* Documentation */
code span.dt { color: #902000; } /* DataType */
code span.dv { color: #40a070; } /* DecVal */
code span.er { color: #ff0000; font-weight: bold; } /* Error */
code span.ex { } /* Extension */
code span.fl { color: #40a070; } /* Float */
code span.fu { color: #06287e; } /* Function */
code span.im { color: #008000; font-weight: bold; } /* Import */
code span.in { color: #60a0b0; font-weight: bold; font-style: italic; } /* Information */
code span.kw { color: #007020; font-weight: bold; } /* Keyword */
code span.op { color: #666666; } /* Operator */
code span.ot { color: #007020; } /* Other */
code span.pp { color: #bc7a00; } /* Preprocessor */
code span.sc { color: #4070a0; } /* SpecialChar */
code span.ss { color: #bb6688; } /* SpecialString */
code span.st { color: #4070a0; } /* String */
code span.va { color: #19177c; } /* Variable */
code span.vs { color: #4070a0; } /* VerbatimString */
code span.wa { color: #60a0b0; font-weight: bold; font-style: italic; } /* Warning */
</style>


<script src="Sandero_files/libs/clipboard/clipboard.min.js"></script>
<script src="Sandero_files/libs/quarto-html/quarto.js"></script>
<script src="Sandero_files/libs/quarto-html/popper.min.js"></script>
<script src="Sandero_files/libs/quarto-html/tippy.umd.min.js"></script>
<script src="Sandero_files/libs/quarto-html/anchor.min.js"></script>
<link href="Sandero_files/libs/quarto-html/tippy.css" rel="stylesheet">
<link href="Sandero_files/libs/quarto-html/quarto-syntax-highlighting.css" rel="stylesheet" id="quarto-text-highlighting-styles">
<script src="Sandero_files/libs/bootstrap/bootstrap.min.js"></script>
<link href="Sandero_files/libs/bootstrap/bootstrap-icons.css" rel="stylesheet">
<link href="Sandero_files/libs/bootstrap/bootstrap.min.css" rel="stylesheet" id="quarto-bootstrap" data-mode="light">


</head>

<body class="fullcontent">

<div id="quarto-content" class="page-columns page-rows-contents page-layout-article">

<main class="content" id="quarto-document-content">

<header id="title-block-header" class="quarto-title-block default">
<div class="quarto-title">
<h1 class="title">Trabalho Final - Tarifação</h1>
</div>



<div class="quarto-title-meta">

    <div>
    <div class="quarto-title-meta-heading">Author</div>
    <div class="quarto-title-meta-contents">
             <p>Marco Rocha - Debora Rocha </p>
          </div>
  </div>
    
  
    
  </div>
  

</header>

<section id="sandero" class="level2">
<h2 class="anchored" data-anchor-id="sandero">Sandero</h2>
<p>• Análise exploratória dos dados. • Ajuste um modelo para a frequência e severidade de sinistros em função das variáveis: sexo, idade do condutor e estado</p>
<div class="cell">
<div class="sourceCode cell-code" id="cb1"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="co"># Autores: Debora Rocha e Marco Rocha </span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a><span class="co"># Carregando Pacotes ------------------------------------------------------</span></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="fu">library</span>(tidyverse)</span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a><span class="fu">library</span>(readxl)</span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a><span class="fu">library</span>(fitdistrplus)</span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a><span class="fu">library</span>(MASS)</span>
<span id="cb1-7"><a href="#cb1-7" aria-hidden="true" tabindex="-1"></a><span class="fu">require</span>(pscl)</span>
<span id="cb1-8"><a href="#cb1-8" aria-hidden="true" tabindex="-1"></a><span class="fu">require</span> (hnp)</span>
<span id="cb1-9"><a href="#cb1-9" aria-hidden="true" tabindex="-1"></a><span class="fu">require</span>(boot)</span>
<span id="cb1-10"><a href="#cb1-10" aria-hidden="true" tabindex="-1"></a><span class="co"># Lendo os dados</span></span>
<span id="cb1-11"><a href="#cb1-11" aria-hidden="true" tabindex="-1"></a>dados <span class="ot">&lt;-</span> <span class="fu">read_excel</span>(<span class="st">"E:/7° Semestre 2023-01/Tarifação Seguros/Trabalho Final/Insurance_Modeling/Dados R.xlsx"</span>)</span>
<span id="cb1-12"><a href="#cb1-12" aria-hidden="true" tabindex="-1"></a><span class="co"># 121 observações, 15 variáveis</span></span>
<span id="cb1-13"><a href="#cb1-13" aria-hidden="true" tabindex="-1"></a>dados <span class="ot">&lt;-</span> dados[<span class="sc">-</span><span class="dv">121</span>,]</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
</div>
<p>Agora é preciso agrupar os dados por Região e por tipos de sinistro.</p>
<div class="cell">
<div class="sourceCode cell-code" id="cb2"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb2-1"><a href="#cb2-1" aria-hidden="true" tabindex="-1"></a><span class="co"># Agrupando os dados por sub_regiões e por tipo de sinistro ---------------</span></span>
<span id="cb2-2"><a href="#cb2-2" aria-hidden="true" tabindex="-1"></a>dados<span class="sc">$</span>Freq_Total <span class="ot">&lt;-</span> dados<span class="sc">$</span>Freq_Incencio_Roubo <span class="sc">+</span> dados<span class="sc">$</span>Freq_Colisao <span class="sc">+</span> dados<span class="sc">$</span>Freq_Outras</span>
<span id="cb2-3"><a href="#cb2-3" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-4"><a href="#cb2-4" aria-hidden="true" tabindex="-1"></a>dados<span class="sc">$</span>Indeni_Total <span class="ot">&lt;-</span> dados<span class="sc">$</span>Indeni_Colisao <span class="sc">+</span> dados<span class="sc">$</span>Indeni_Incencio_Roubo <span class="sc">+</span> dados<span class="sc">$</span>Indeni_Outras</span>
<span id="cb2-5"><a href="#cb2-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-6"><a href="#cb2-6" aria-hidden="true" tabindex="-1"></a>dados<span class="sc">$</span>Regiao <span class="ot">=</span> <span class="fu">substr</span>(dados<span class="sc">$</span>Regiao, <span class="at">start=</span><span class="dv">1</span>, <span class="at">stop=</span><span class="dv">2</span>)</span>
<span id="cb2-7"><a href="#cb2-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb2-8"><a href="#cb2-8" aria-hidden="true" tabindex="-1"></a>dados<span class="sc">$</span>Freq_Media <span class="ot">&lt;-</span> dados<span class="sc">$</span>Freq_Total <span class="sc">/</span> dados<span class="sc">$</span>Expostos</span>
<span id="cb2-9"><a href="#cb2-9" aria-hidden="true" tabindex="-1"></a>dados<span class="sc">$</span>Indeni_Media <span class="ot">&lt;-</span> dados<span class="sc">$</span>Indeni_Total <span class="sc">/</span> dados<span class="sc">$</span>Expostos</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
</div>
</section>
<section id="análise-exploratória" class="level2">
<h2 class="anchored" data-anchor-id="análise-exploratória">Análise Exploratória</h2>
<section id="sexo" class="level3">
<h3 class="anchored" data-anchor-id="sexo">Sexo</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb3"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb3-1"><a href="#cb3-1" aria-hidden="true" tabindex="-1"></a><span class="co"># Análise Explortória -----------------------------------------------------</span></span>
<span id="cb3-2"><a href="#cb3-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-3"><a href="#cb3-3" aria-hidden="true" tabindex="-1"></a><span class="fu">attach</span>(dados)</span>
<span id="cb3-4"><a href="#cb3-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb3-5"><a href="#cb3-5" aria-hidden="true" tabindex="-1"></a><span class="co"># Distribuição das variavies de interrese </span></span>
<span id="cb3-6"><a href="#cb3-6" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Freq_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">bins =</span> <span class="dv">25</span>, <span class="at">col=</span><span class="st">'blue'</span>)<span class="sc">+</span></span>
<span id="cb3-7"><a href="#cb3-7" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Distribuição da Frequência média de sinistros"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-3-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb4"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb4-1"><a href="#cb4-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Indeni_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">bins =</span> <span class="dv">50</span>, <span class="at">col=</span><span class="st">'blue'</span>)<span class="sc">+</span></span>
<span id="cb4-2"><a href="#cb4-2" aria-hidden="true" tabindex="-1"></a>   <span class="fu">ggtitle</span>(<span class="st">"Distribuição da Indenização média por sinistro"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-3-2.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb5"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb5-1"><a href="#cb5-1" aria-hidden="true" tabindex="-1"></a><span class="co"># Distribuição das variavies de interrese por sexo </span></span>
<span id="cb5-2"><a href="#cb5-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb5-3"><a href="#cb5-3" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Freq_Media, <span class="at">color=</span>Sexo)) <span class="sc">+</span> <span class="fu">geom_histogram</span>()<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Sexo)<span class="sc">+</span></span>
<span id="cb5-4"><a href="#cb5-4" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência média de sinistros por Sexo"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-3-3.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb7"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb7-1"><a href="#cb7-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Indeni_Media, <span class="at">color=</span>Sexo)) <span class="sc">+</span> <span class="fu">geom_histogram</span>()<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Sexo)<span class="sc">+</span></span>
<span id="cb7-2"><a href="#cb7-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização média de sinistros por Sexo"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-3-4.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb9"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb9-1"><a href="#cb9-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span>Freq_Media, <span class="at">color=</span>Sexo)) <span class="sc">+</span> <span class="fu">geom_boxplot</span>()<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Sexo)<span class="sc">+</span></span>
<span id="cb9-2"><a href="#cb9-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência média de sinistros por Sexo"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-3-5.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb10"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb10-1"><a href="#cb10-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span>Indeni_Media, <span class="at">color=</span>Sexo)) <span class="sc">+</span> <span class="fu">geom_boxplot</span>()<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Sexo)<span class="sc">+</span></span>
<span id="cb10-2"><a href="#cb10-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização média de sinistros por Sexo"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-3-6.png" class="img-fluid" width="672"></p>
</div>
</div>
</section>
<section id="idade" class="level3">
<h3 class="anchored" data-anchor-id="idade">Idade</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb11"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb11-1"><a href="#cb11-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Freq_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">color=</span><span class="st">'blue'</span>)<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Idade)<span class="sc">+</span></span>
<span id="cb11-2"><a href="#cb11-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência média de sinistros por Idade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-4-1.png" class="img-fluid" width="672"></p>
</div>
</div>
<div class="cell">
<div class="sourceCode cell-code" id="cb13"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb13-1"><a href="#cb13-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Indeni_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">color=</span><span class="st">'blue'</span>)<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Idade)<span class="sc">+</span></span>
<span id="cb13-2"><a href="#cb13-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização média de sinistros por Idade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-5-1.png" class="img-fluid" width="672"></p>
</div>
</div>
<div class="cell">
<div class="sourceCode cell-code" id="cb15"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb15-1"><a href="#cb15-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span>Freq_Media, <span class="at">color=</span>Idade)) <span class="sc">+</span> <span class="fu">geom_boxplot</span>()<span class="sc">+</span> </span>
<span id="cb15-2"><a href="#cb15-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência média de sinistros por Idade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-6-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb16"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb16-1"><a href="#cb16-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span>Indeni_Media, <span class="at">color=</span>Idade)) <span class="sc">+</span> <span class="fu">geom_boxplot</span>()<span class="sc">+</span> </span>
<span id="cb16-2"><a href="#cb16-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização média de sinistros por Idade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-6-2.png" class="img-fluid" width="672"></p>
</div>
</div>
<div class="cell">
<div class="sourceCode cell-code" id="cb17"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb17-1"><a href="#cb17-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span>Freq_Total, <span class="at">color=</span>Idade)) <span class="sc">+</span> <span class="fu">geom_boxplot</span>()<span class="sc">+</span> </span>
<span id="cb17-2"><a href="#cb17-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência total de sinistros por Idade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-7-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb18"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb18-1"><a href="#cb18-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span>Indeni_Total, <span class="at">color=</span>Idade)) <span class="sc">+</span> <span class="fu">geom_boxplot</span>()<span class="sc">+</span> </span>
<span id="cb18-2"><a href="#cb18-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização total de sinistros por Idade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-7-2.png" class="img-fluid" width="672"></p>
</div>
</div>
</section>
<section id="estado" class="level3">
<h3 class="anchored" data-anchor-id="estado">Estado</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb19"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb19-1"><a href="#cb19-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Freq_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">color=</span><span class="st">'blue'</span>)<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Regiao)<span class="sc">+</span></span>
<span id="cb19-2"><a href="#cb19-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência média de sinistros por Região"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-8-1.png" class="img-fluid" width="672"></p>
</div>
</div>
<div class="cell">
<div class="sourceCode cell-code" id="cb21"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb21-1"><a href="#cb21-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x=</span>Indeni_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">color=</span><span class="st">'blue'</span>)<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Regiao)<span class="sc">+</span></span>
<span id="cb21-2"><a href="#cb21-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização média de sinistros por Região"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-9-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb23"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb23-1"><a href="#cb23-1" aria-hidden="true" tabindex="-1"></a>dados2 <span class="ot">&lt;-</span> dados[dados<span class="sc">$</span>Indeni_Media<span class="sc">&lt;</span><span class="dv">3000</span>,]</span>
<span id="cb23-2"><a href="#cb23-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb23-3"><a href="#cb23-3" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados2, <span class="fu">aes</span>(<span class="at">x=</span>Indeni_Media)) <span class="sc">+</span> <span class="fu">geom_histogram</span>(<span class="at">color=</span><span class="st">'blue'</span>)<span class="sc">+</span> <span class="fu">facet_wrap</span>(<span class="sc">~</span>Regiao)<span class="sc">+</span></span>
<span id="cb23-4"><a href="#cb23-4" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Indenização média de sinistros por Região"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-9-2.png" class="img-fluid" width="672"></p>
</div>
</div>
</section>
<section id="relação-número-de-sinistro-e-valor-de-indenizações" class="level3">
<h3 class="anchored" data-anchor-id="relação-número-de-sinistro-e-valor-de-indenizações">Relação número de sinistro e valor de indenizações</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb25"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb25-1"><a href="#cb25-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span> Indeni_Total, <span class="at">x =</span> Freq_Total)) <span class="sc">+</span> <span class="fu">geom_point</span>()<span class="sc">+</span> </span>
<span id="cb25-2"><a href="#cb25-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência total e indenização total"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-10-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb26"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb26-1"><a href="#cb26-1" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">y=</span> Indeni_Total, <span class="at">x =</span> Freq_Total)) <span class="sc">+</span> <span class="fu">geom_smooth</span>()<span class="sc">+</span> <span class="fu">geom_point</span>()<span class="sc">+</span></span>
<span id="cb26-2"><a href="#cb26-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência total e indenização total"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`geom_smooth()` using method = 'loess' and formula = 'y ~ x'</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-10-2.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb28"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb28-1"><a href="#cb28-1" aria-hidden="true" tabindex="-1"></a>dados1 <span class="ot">&lt;-</span> dados[dados<span class="sc">$</span>Freq_Total<span class="sc">&lt;</span><span class="dv">4500</span>,]</span>
<span id="cb28-2"><a href="#cb28-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb28-3"><a href="#cb28-3" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados1, <span class="fu">aes</span>(<span class="at">y=</span> Indeni_Total, <span class="at">x =</span> Freq_Total)) <span class="sc">+</span> <span class="fu">geom_smooth</span>()<span class="sc">+</span> <span class="fu">geom_point</span>()<span class="sc">+</span></span>
<span id="cb28-4"><a href="#cb28-4" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Frequência total e indenização total"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stderr">
<pre><code>`geom_smooth()` using method = 'loess' and formula = 'y ~ x'</code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-10-3.png" class="img-fluid" width="672"></p>
</div>
</div>
</section>
<section id="total-de-expostos" class="level3">
<h3 class="anchored" data-anchor-id="total-de-expostos">Total de expostos</h3>
<div class="cell">
<div class="sourceCode cell-code" id="cb30"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb30-1"><a href="#cb30-1" aria-hidden="true" tabindex="-1"></a><span class="co"># total de expostos homens </span></span>
<span id="cb30-2"><a href="#cb30-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb30-3"><a href="#cb30-3" aria-hidden="true" tabindex="-1"></a><span class="fu">ggplot</span>(dados, <span class="fu">aes</span>(<span class="at">x =</span> Sexo)) <span class="sc">+</span> <span class="fu">geom_bar</span>()<span class="sc">+</span> </span>
<span id="cb30-4"><a href="#cb30-4" aria-hidden="true" tabindex="-1"></a>  <span class="fu">ggtitle</span>(<span class="st">"Expostos por sexo"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-11-1.png" class="img-fluid" width="672"></p>
</div>
</div>
<p>Fazer uma tabela de expostos por faixa etária por estado e por sexo</p>
<div class="cell">
<div class="sourceCode cell-code" id="cb31"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb31-1"><a href="#cb31-1" aria-hidden="true" tabindex="-1"></a>soma_sexo_F <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb31-2"><a href="#cb31-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Sexo <span class="sc">==</span> <span class="st">"Feminino"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb31-3"><a href="#cb31-3" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb31-4"><a href="#cb31-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb31-5"><a href="#cb31-5" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb31-6"><a href="#cb31-6" aria-hidden="true" tabindex="-1"></a>soma_sexo_M <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb31-7"><a href="#cb31-7" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Sexo <span class="sc">==</span> <span class="st">"Masculino"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb31-8"><a href="#cb31-8" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb31-9"><a href="#cb31-9" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb31-10"><a href="#cb31-10" aria-hidden="true" tabindex="-1"></a>valores <span class="ot">&lt;-</span> <span class="fu">c</span>(<span class="fu">as.numeric</span>(soma_sexo_F),<span class="fu">as.numeric</span>(soma_sexo_M))</span>
<span id="cb31-11"><a href="#cb31-11" aria-hidden="true" tabindex="-1"></a><span class="fu">barplot</span>(valores)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-12-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb32"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb32-1"><a href="#cb32-1" aria-hidden="true" tabindex="-1"></a>soma_MG <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-2"><a href="#cb32-2" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Regiao <span class="sc">==</span> <span class="st">"MG"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-3"><a href="#cb32-3" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-4"><a href="#cb32-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-5"><a href="#cb32-5" aria-hidden="true" tabindex="-1"></a>soma_ES <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-6"><a href="#cb32-6" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Regiao <span class="sc">==</span> <span class="st">"ES"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-7"><a href="#cb32-7" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-8"><a href="#cb32-8" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-9"><a href="#cb32-9" aria-hidden="true" tabindex="-1"></a>soma_RJ <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-10"><a href="#cb32-10" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Regiao <span class="sc">==</span> <span class="st">"RJ"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-11"><a href="#cb32-11" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-12"><a href="#cb32-12" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-13"><a href="#cb32-13" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-14"><a href="#cb32-14" aria-hidden="true" tabindex="-1"></a>soma_SP <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-15"><a href="#cb32-15" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Regiao <span class="sc">==</span> <span class="st">"SP"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-16"><a href="#cb32-16" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-17"><a href="#cb32-17" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-18"><a href="#cb32-18" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-19"><a href="#cb32-19" aria-hidden="true" tabindex="-1"></a>soma_18_25 <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-20"><a href="#cb32-20" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Idade <span class="sc">==</span> <span class="st">"Entre 18 e 25 anos"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-21"><a href="#cb32-21" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-22"><a href="#cb32-22" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-23"><a href="#cb32-23" aria-hidden="true" tabindex="-1"></a>soma_26_35 <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-24"><a href="#cb32-24" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Idade <span class="sc">==</span> <span class="st">"Entre 26 e 35 anos"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-25"><a href="#cb32-25" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-26"><a href="#cb32-26" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-27"><a href="#cb32-27" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-28"><a href="#cb32-28" aria-hidden="true" tabindex="-1"></a>soma_36_45 <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-29"><a href="#cb32-29" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Idade <span class="sc">==</span> <span class="st">"Entre 36 e 45 anos"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-30"><a href="#cb32-30" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-31"><a href="#cb32-31" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-32"><a href="#cb32-32" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-33"><a href="#cb32-33" aria-hidden="true" tabindex="-1"></a>soma_46_55 <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-34"><a href="#cb32-34" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Idade <span class="sc">==</span> <span class="st">"Entre 46 e 55 anos"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-35"><a href="#cb32-35" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-36"><a href="#cb32-36" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-37"><a href="#cb32-37" aria-hidden="true" tabindex="-1"></a>soma_55_mais <span class="ot">&lt;-</span> dados <span class="sc">%&gt;%</span></span>
<span id="cb32-38"><a href="#cb32-38" aria-hidden="true" tabindex="-1"></a>  <span class="fu">filter</span>(Idade <span class="sc">==</span> <span class="st">"Maior que 55 anos"</span>) <span class="sc">%&gt;%</span></span>
<span id="cb32-39"><a href="#cb32-39" aria-hidden="true" tabindex="-1"></a>  <span class="fu">summarize</span>(<span class="at">soma =</span> <span class="fu">sum</span>(Expostos))</span>
<span id="cb32-40"><a href="#cb32-40" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb32-41"><a href="#cb32-41" aria-hidden="true" tabindex="-1"></a>expostos_idade <span class="ot">&lt;-</span> <span class="fu">cbind</span>(<span class="st">"Entre 18 e 25 anos"</span> <span class="ot">=</span> soma_18_25,</span>
<span id="cb32-42"><a href="#cb32-42" aria-hidden="true" tabindex="-1"></a>                        <span class="st">"Entre 26 e 35 anos"</span> <span class="ot">=</span> soma_26_35,</span>
<span id="cb32-43"><a href="#cb32-43" aria-hidden="true" tabindex="-1"></a>                        <span class="st">"Entre 36 e 45 anos"</span> <span class="ot">=</span> soma_36_45,</span>
<span id="cb32-44"><a href="#cb32-44" aria-hidden="true" tabindex="-1"></a>                        <span class="st">"Entre 46 e 55 anos"</span> <span class="ot">=</span> soma_46_55,</span>
<span id="cb32-45"><a href="#cb32-45" aria-hidden="true" tabindex="-1"></a>                        <span class="st">"Maior que 55 anos"</span> <span class="ot">=</span> soma_55_mais)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
</div>
</section>
</section>
<section id="modelando-a-distribuição-da-indenização" class="level2">
<h2 class="anchored" data-anchor-id="modelando-a-distribuição-da-indenização">Modelando a Distribuição da Indenização</h2>
<div class="cell">
<div class="sourceCode cell-code" id="cb33"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb33-1"><a href="#cb33-1" aria-hidden="true" tabindex="-1"></a><span class="do">## estimador máxima verossimilhança</span></span>
<span id="cb33-2"><a href="#cb33-2" aria-hidden="true" tabindex="-1"></a>fgamEMV <span class="ot">=</span> <span class="fu">fitdist</span>(dados<span class="sc">$</span>Indeni_Media, <span class="st">"gamma"</span>, <span class="at">method=</span><span class="st">"mle"</span>)</span>
<span id="cb33-3"><a href="#cb33-3" aria-hidden="true" tabindex="-1"></a>fgamEMV</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Fitting of the distribution ' gamma ' by maximum likelihood 
Parameters:
         estimate   Std. Error
shape 3.961055213 0.4122702683
rate  0.004983358 0.0005295789</code></pre>
</div>
<div class="sourceCode cell-code" id="cb35"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb35-1"><a href="#cb35-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(fgamEMV)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-13-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb36"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb36-1"><a href="#cb36-1" aria-hidden="true" tabindex="-1"></a>fpoisEMV <span class="ot">=</span> <span class="fu">fitdist</span>(<span class="fu">round</span>(dados<span class="sc">$</span>Indeni_Media), <span class="st">"pois"</span>, <span class="at">method=</span><span class="st">"mle"</span>)</span>
<span id="cb36-2"><a href="#cb36-2" aria-hidden="true" tabindex="-1"></a>fpoisEMV</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Fitting of the distribution ' pois ' by maximum likelihood 
Parameters:
       estimate Std. Error
lambda    794.9   2.573745</code></pre>
</div>
<div class="sourceCode cell-code" id="cb38"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb38-1"><a href="#cb38-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(fpoisEMV)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-13-2.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb39"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb39-1"><a href="#cb39-1" aria-hidden="true" tabindex="-1"></a>fnbinomEMV<span class="ot">=</span> <span class="fu">fitdist</span>(<span class="fu">round</span>(dados<span class="sc">$</span>Indeni_Media), <span class="st">"nbinom"</span>, <span class="at">method=</span><span class="st">"mle"</span>)</span>
<span id="cb39-2"><a href="#cb39-2" aria-hidden="true" tabindex="-1"></a>fnbinomEMV</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Fitting of the distribution ' nbinom ' by maximum likelihood 
Parameters:
       estimate Std. Error
size   3.985998    0.49730
mu   794.974610   36.44329</code></pre>
</div>
<div class="sourceCode cell-code" id="cb41"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb41-1"><a href="#cb41-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(fnbinomEMV)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-13-3.png" class="img-fluid" width="672"></p>
</div>
</div>
</section>
<section id="modelando-a-distribuição-da-frequência" class="level2">
<h2 class="anchored" data-anchor-id="modelando-a-distribuição-da-frequência">Modelando a distribuição da Frequência</h2>
<div class="cell">
<div class="sourceCode cell-code" id="cb42"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb42-1"><a href="#cb42-1" aria-hidden="true" tabindex="-1"></a><span class="do">## estimador máxima verossimilhança</span></span>
<span id="cb42-2"><a href="#cb42-2" aria-hidden="true" tabindex="-1"></a>fgamEMV <span class="ot">=</span> <span class="fu">fitdist</span>(dados<span class="sc">$</span>Freq_Media, <span class="st">"gamma"</span>, <span class="at">method=</span><span class="st">"mle"</span>)</span>
<span id="cb42-3"><a href="#cb42-3" aria-hidden="true" tabindex="-1"></a>fgamEMV</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Fitting of the distribution ' gamma ' by maximum likelihood 
Parameters:
       estimate Std. Error
shape  8.202499   1.038115
rate  21.539838   2.811225</code></pre>
</div>
<div class="sourceCode cell-code" id="cb44"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb44-1"><a href="#cb44-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(fgamEMV)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-14-1.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb45"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb45-1"><a href="#cb45-1" aria-hidden="true" tabindex="-1"></a>fpoisEMV <span class="ot">=</span> <span class="fu">fitdist</span>((dados<span class="sc">$</span>Freq_Total), <span class="st">"pois"</span>, <span class="at">method=</span><span class="st">"mle"</span>)</span>
<span id="cb45-2"><a href="#cb45-2" aria-hidden="true" tabindex="-1"></a>fpoisEMV</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Fitting of the distribution ' pois ' by maximum likelihood 
Parameters:
       estimate Std. Error
lambda 511.4583   2.064502</code></pre>
</div>
<div class="sourceCode cell-code" id="cb47"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb47-1"><a href="#cb47-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(fpoisEMV)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-14-2.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb48"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb48-1"><a href="#cb48-1" aria-hidden="true" tabindex="-1"></a>fnbinomEMV<span class="ot">=</span> <span class="fu">fitdist</span>((dados<span class="sc">$</span>Freq_Total), <span class="st">"nbinom"</span>, <span class="at">method=</span><span class="st">"mle"</span>)</span>
<span id="cb48-2"><a href="#cb48-2" aria-hidden="true" tabindex="-1"></a>fnbinomEMV</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Fitting of the distribution ' nbinom ' by maximum likelihood 
Parameters:
        estimate  Std. Error
size   0.5634169  0.06110501
mu   511.3822643 62.21811575</code></pre>
</div>
<div class="sourceCode cell-code" id="cb50"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb50-1"><a href="#cb50-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(fnbinomEMV)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-14-3.png" class="img-fluid" width="672"></p>
</div>
</div>
</section>
<section id="modelos-mlg" class="level2">
<h2 class="anchored" data-anchor-id="modelos-mlg">Modelos MLG</h2>
<div class="cell">
<div class="sourceCode cell-code" id="cb51"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb51-1"><a href="#cb51-1" aria-hidden="true" tabindex="-1"></a>modelSg <span class="ot">=</span> <span class="fu">glm</span>(dados<span class="sc">$</span>Indeni_Media <span class="sc">~</span> dados<span class="sc">$</span>Regiao <span class="sc">+</span> dados<span class="sc">$</span>Sexo <span class="sc">+</span> dados<span class="sc">$</span>Idade, <span class="at">family=</span> Gamma)</span>
<span id="cb51-2"><a href="#cb51-2" aria-hidden="true" tabindex="-1"></a><span class="fu">summary</span>(modelSg)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>
Call:
glm(formula = dados$Indeni_Media ~ dados$Regiao + dados$Sexo + 
    dados$Idade, family = Gamma)

Coefficients:
                                Estimate Std. Error t value Pr(&gt;|t|)    
(Intercept)                    9.290e-04  1.663e-04   5.588 1.66e-07 ***
dados$RegiaoMG                 9.366e-05  1.600e-04   0.585  0.55943    
dados$RegiaoRJ                 3.853e-05  1.740e-04   0.221  0.82515    
dados$RegiaoSP                 3.360e-04  1.644e-04   2.044  0.04332 *  
dados$SexoMasculino           -3.274e-04  9.898e-05  -3.308  0.00127 ** 
dados$IdadeEntre 26 e 35 anos  2.238e-04  1.242e-04   1.802  0.07428 .  
dados$IdadeEntre 36 e 45 anos  3.963e-04  1.372e-04   2.889  0.00465 ** 
dados$IdadeEntre 46 e 55 anos  6.285e-04  1.553e-04   4.046 9.64e-05 ***
dados$IdadeMaior que 55 anos   8.938e-04  1.766e-04   5.060 1.67e-06 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for Gamma family taken to be 0.1868491)

    Null deviance: 31.532  on 119  degrees of freedom
Residual deviance: 20.657  on 111  degrees of freedom
AIC: 1724.1

Number of Fisher Scoring iterations: 6</code></pre>
</div>
<div class="sourceCode cell-code" id="cb53"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb53-1"><a href="#cb53-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(<span class="fu">hnp</span>(modelSg, <span class="at">sim=</span><span class="dv">100</span>, <span class="at">type.resid=</span><span class="st">"deviance"</span>, <span class="at">how.many.out=</span><span class="cn">TRUE</span>, <span class="at">paint.out=</span><span class="cn">TRUE</span>),<span class="at">main=</span><span class="st">"Resíduos Severidade de Sinistros Observados </span><span class="sc">\n</span><span class="st"> vs. </span><span class="sc">\n</span><span class="st"> Distribuição Gama com Função Log"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Gamma model </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-1.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 80 ( 66.67 %) </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-2.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 80 ( 66.67 %) </code></pre>
</div>
<div class="sourceCode cell-code" id="cb57"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb57-1"><a href="#cb57-1" aria-hidden="true" tabindex="-1"></a>modelSgi <span class="ot">=</span> <span class="fu">glm</span>(dados<span class="sc">$</span>Indeni_Media <span class="sc">~</span> dados<span class="sc">$</span>Regiao <span class="sc">+</span> dados<span class="sc">$</span>Sexo <span class="sc">+</span> dados<span class="sc">$</span>Idade, <span class="at">family=</span> <span class="fu">Gamma</span>(<span class="at">link =</span> identity))</span>
<span id="cb57-2"><a href="#cb57-2" aria-hidden="true" tabindex="-1"></a><span class="fu">summary</span>(modelSgi)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>
Call:
glm(formula = dados$Indeni_Media ~ dados$Regiao + dados$Sexo + 
    dados$Idade, family = Gamma(link = identity))

Coefficients:
                              Estimate Std. Error t value Pr(&gt;|t|)    
(Intercept)                    1030.27     145.05   7.103 1.24e-10 ***
dados$RegiaoMG                   38.40     119.37   0.322 0.748282    
dados$RegiaoRJ                   85.36     134.95   0.633 0.528348    
dados$RegiaoSP                 -102.21     112.80  -0.906 0.366864    
dados$SexoMasculino             169.04      60.25   2.805 0.005935 ** 
dados$IdadeEntre 26 e 35 anos  -220.51     128.57  -1.715 0.089132 .  
dados$IdadeEntre 36 e 45 anos  -324.26     122.65  -2.644 0.009387 ** 
dados$IdadeEntre 46 e 55 anos  -450.88     116.14  -3.882 0.000176 ***
dados$IdadeMaior que 55 anos   -539.66     112.14  -4.812 4.74e-06 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for Gamma family taken to be 0.2085772)

    Null deviance: 31.532  on 119  degrees of freedom
Residual deviance: 21.053  on 111  degrees of freedom
AIC: 1726.4

Number of Fisher Scoring iterations: 11</code></pre>
</div>
<div class="sourceCode cell-code" id="cb59"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb59-1"><a href="#cb59-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(<span class="fu">hnp</span>(modelSgi, <span class="at">sim=</span><span class="dv">100</span>, <span class="at">type.resid=</span><span class="st">"deviance"</span>, <span class="at">how.many.out=</span><span class="cn">TRUE</span>, <span class="at">paint.out=</span><span class="cn">TRUE</span>),<span class="at">main=</span><span class="st">"Resíduos Severidade de Sinistros Observados </span><span class="sc">\n</span><span class="st"> vs. </span><span class="sc">\n</span><span class="st"> Distribuição Gama com Função Identidade"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Gamma model </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-3.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 77 ( 64.17 %) </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-4.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 77 ( 64.17 %) </code></pre>
</div>
<div class="sourceCode cell-code" id="cb63"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb63-1"><a href="#cb63-1" aria-hidden="true" tabindex="-1"></a>modelLN <span class="ot">=</span> <span class="fu">glm</span>(<span class="fu">log</span>(dados<span class="sc">$</span>Indeni_Media) <span class="sc">~</span> dados<span class="sc">$</span>Regiao <span class="sc">+</span> dados<span class="sc">$</span>Sexo <span class="sc">+</span> dados<span class="sc">$</span>Idade, <span class="at">family=</span> <span class="fu">gaussian</span>(<span class="at">link=</span>log))</span>
<span id="cb63-2"><a href="#cb63-2" aria-hidden="true" tabindex="-1"></a><span class="fu">summary</span>(modelLN)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>
Call:
glm(formula = log(dados$Indeni_Media) ~ dados$Regiao + dados$Sexo + 
    dados$Idade, family = gaussian(link = log))

Coefficients:
                               Estimate Std. Error t value Pr(&gt;|t|)    
(Intercept)                    1.888511   0.025612  73.735  &lt; 2e-16 ***
dados$RegiaoMG                -0.009231   0.024173  -0.382 0.703297    
dados$RegiaoRJ                 0.024207   0.026222   0.923 0.357924    
dados$RegiaoSP                -0.016688   0.023707  -0.704 0.482950    
dados$SexoMasculino            0.042965   0.012543   3.425 0.000862 ***
dados$IdadeEntre 26 e 35 anos  0.003221   0.019295   0.167 0.867708    
dados$IdadeEntre 36 e 45 anos -0.014881   0.019471  -0.764 0.446354    
dados$IdadeEntre 46 e 55 anos -0.048153   0.019808  -2.431 0.016661 *  
dados$IdadeMaior que 55 anos  -0.068974   0.020028  -3.444 0.000810 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for gaussian family taken to be 0.2022275)

    Null deviance: 29.955  on 119  degrees of freedom
Residual deviance: 22.447  on 111  degrees of freedom
AIC: 159.39

Number of Fisher Scoring iterations: 5</code></pre>
</div>
<div class="sourceCode cell-code" id="cb65"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb65-1"><a href="#cb65-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(<span class="fu">hnp</span>(modelLN, <span class="at">sim=</span><span class="dv">100</span>, <span class="at">type.resid=</span><span class="st">"deviance"</span>, <span class="at">how.many.out=</span><span class="cn">TRUE</span>, <span class="at">paint.out=</span><span class="cn">TRUE</span>),<span class="at">main=</span><span class="st">"Resíduos Severidade de Sinistros Observados </span><span class="sc">\n</span><span class="st"> vs. </span><span class="sc">\n</span><span class="st"> Distribuição LogNormal"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Gaussian model (glm object) </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-5.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 96 ( 80 %) </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-6.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 96 ( 80 %) </code></pre>
</div>
<div class="sourceCode cell-code" id="cb69"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb69-1"><a href="#cb69-1" aria-hidden="true" tabindex="-1"></a><span class="co"># Gráficos de Diagnósticos para GLM, do pacote "boot"</span></span>
<span id="cb69-2"><a href="#cb69-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb69-3"><a href="#cb69-3" aria-hidden="true" tabindex="-1"></a><span class="fu">glm.diag.plots</span>(modelSg, <span class="at">glmdiag =</span> <span class="fu">glm.diag</span>(modelSg), <span class="at">subset =</span> <span class="cn">NULL</span>,<span class="at">iden =</span> <span class="cn">FALSE</span>, <span class="at">labels =</span> <span class="cn">NULL</span>, <span class="at">ret =</span> <span class="cn">FALSE</span>) <span class="co">#"Diagnósticos para o Modelo de Severidade de Sinistros \n utilizando a Distribuição Gama"</span></span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-7.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb70"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb70-1"><a href="#cb70-1" aria-hidden="true" tabindex="-1"></a><span class="fu">glm.diag.plots</span>(modelSgi, <span class="at">glmdiag =</span> <span class="fu">glm.diag</span>(modelSgi), <span class="at">subset =</span> <span class="cn">NULL</span>,<span class="at">iden =</span> <span class="cn">FALSE</span>, <span class="at">labels =</span> <span class="cn">NULL</span>, <span class="at">ret =</span> <span class="cn">FALSE</span>) <span class="co">#"Diagnósticos para o Modelo de Severidade de Sinistros \n utilizando a Distribuição Gama"</span></span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-8.png" class="img-fluid" width="672"></p>
</div>
<div class="sourceCode cell-code" id="cb71"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb71-1"><a href="#cb71-1" aria-hidden="true" tabindex="-1"></a><span class="fu">glm.diag.plots</span>(modelLN, <span class="at">glmdiag =</span> <span class="fu">glm.diag</span>(modelLN), <span class="at">subset =</span> <span class="cn">NULL</span>,<span class="at">iden =</span> <span class="cn">FALSE</span>, <span class="at">labels =</span> <span class="cn">NULL</span>, <span class="at">ret =</span> <span class="cn">FALSE</span>) <span class="co">#"Diagnósticos para o Modelo de Severidade de Sinistros \n utilizando a Distribuição Gama"</span></span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-15-9.png" class="img-fluid" width="672"></p>
</div>
</div>
<div class="cell">
<div class="sourceCode cell-code" id="cb72"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb72-1"><a href="#cb72-1" aria-hidden="true" tabindex="-1"></a>modelbinneg <span class="ot">=</span> <span class="fu">glm.nb</span>(dados<span class="sc">$</span>Indeni_Media <span class="sc">~</span> dados<span class="sc">$</span>Regiao <span class="sc">+</span> dados<span class="sc">$</span>Sexo <span class="sc">+</span> dados<span class="sc">$</span>Idade)</span>
<span id="cb72-2"><a href="#cb72-2" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb72-3"><a href="#cb72-3" aria-hidden="true" tabindex="-1"></a>dados<span class="sc">$</span>Severidade <span class="ot">&lt;-</span> dados<span class="sc">$</span>Indeni_Total <span class="sc">/</span> dados<span class="sc">$</span>Freq_Total</span>
<span id="cb72-4"><a href="#cb72-4" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb72-5"><a href="#cb72-5" aria-hidden="true" tabindex="-1"></a>modelbinneg <span class="ot">=</span> <span class="fu">glm.nb</span>(dados<span class="sc">$</span>Severidade <span class="sc">~</span> dados<span class="sc">$</span>Regiao <span class="sc">+</span> dados<span class="sc">$</span>Sexo <span class="sc">+</span> dados<span class="sc">$</span>Idade)</span>
<span id="cb72-6"><a href="#cb72-6" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb72-7"><a href="#cb72-7" aria-hidden="true" tabindex="-1"></a></span>
<span id="cb72-8"><a href="#cb72-8" aria-hidden="true" tabindex="-1"></a><span class="fu">summary</span>(modelbinneg)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>
Call:
glm.nb(formula = dados$Severidade ~ dados$Regiao + dados$Sexo + 
    dados$Idade, init.theta = 5.075790123, link = log)

Coefficients:
                               Estimate Std. Error z value Pr(&gt;|z|)    
(Intercept)                    8.234665   0.167230  49.241  &lt; 2e-16 ***
dados$RegiaoMG                 0.198364   0.157094   1.263 0.206695    
dados$RegiaoRJ                -0.003475   0.172095  -0.020 0.983889    
dados$RegiaoSP                -0.471975   0.153943  -3.066 0.002170 ** 
dados$SexoMasculino            0.301962   0.081143   3.721 0.000198 ***
dados$IdadeEntre 26 e 35 anos -0.516153   0.128252  -4.025 5.71e-05 ***
dados$IdadeEntre 36 e 45 anos -0.669781   0.128264  -5.222 1.77e-07 ***
dados$IdadeEntre 46 e 55 anos -0.743495   0.128271  -5.796 6.78e-09 ***
dados$IdadeMaior que 55 anos  -0.961627   0.128294  -7.496 6.60e-14 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for Negative Binomial(5.0758) family taken to be 1)

    Null deviance: 256.16  on 119  degrees of freedom
Residual deviance: 123.83  on 111  degrees of freedom
AIC: 1991.6

Number of Fisher Scoring iterations: 1

              Theta:  5.076 
          Std. Err.:  0.636 

 2 x log-likelihood:  -1971.608 </code></pre>
</div>
<div class="sourceCode cell-code" id="cb74"><pre class="sourceCode r code-with-copy"><code class="sourceCode r"><span id="cb74-1"><a href="#cb74-1" aria-hidden="true" tabindex="-1"></a><span class="fu">plot</span>(<span class="fu">hnp</span>(modelbinneg, <span class="at">sim=</span><span class="dv">100</span>, <span class="at">type.resid=</span><span class="st">"deviance"</span>, <span class="at">how.many.out=</span><span class="cn">TRUE</span>, <span class="at">paint.out=</span><span class="cn">TRUE</span>),<span class="at">main=</span><span class="st">"Resíduos Severidade de Sinistros Observados </span><span class="sc">\n</span><span class="st"> vs. </span><span class="sc">\n</span><span class="st"> Distribuição Binomial Negativa"</span>)</span></code><button title="Copy to Clipboard" class="code-copy-button"><i class="bi"></i></button></pre></div>
<div class="cell-output cell-output-stdout">
<pre><code>Negative binomial model (using MASS package) </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-16-1.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 88 ( 73.33 %) </code></pre>
</div>
<div class="cell-output-display">
<p><img src="Sandero_files/figure-html/unnamed-chunk-16-2.png" class="img-fluid" width="672"></p>
</div>
<div class="cell-output cell-output-stdout">
<pre><code>Total points: 120 
Points out of envelope: 88 ( 73.33 %) </code></pre>
</div>
</div>
</section>

</main>
<!-- /main column -->
<script id="quarto-html-after-body" type="application/javascript">
window.document.addEventListener("DOMContentLoaded", function (event) {
  const toggleBodyColorMode = (bsSheetEl) => {
    const mode = bsSheetEl.getAttribute("data-mode");
    const bodyEl = window.document.querySelector("body");
    if (mode === "dark") {
      bodyEl.classList.add("quarto-dark");
      bodyEl.classList.remove("quarto-light");
    } else {
      bodyEl.classList.add("quarto-light");
      bodyEl.classList.remove("quarto-dark");
    }
  }
  const toggleBodyColorPrimary = () => {
    const bsSheetEl = window.document.querySelector("link#quarto-bootstrap");
    if (bsSheetEl) {
      toggleBodyColorMode(bsSheetEl);
    }
  }
  toggleBodyColorPrimary();  
  const icon = "";
  const anchorJS = new window.AnchorJS();
  anchorJS.options = {
    placement: 'right',
    icon: icon
  };
  anchorJS.add('.anchored');
  const clipboard = new window.ClipboardJS('.code-copy-button', {
    target: function(trigger) {
      return trigger.previousElementSibling;
    }
  });
  clipboard.on('success', function(e) {
    // button target
    const button = e.trigger;
    // don't keep focus
    button.blur();
    // flash "checked"
    button.classList.add('code-copy-button-checked');
    var currentTitle = button.getAttribute("title");
    button.setAttribute("title", "Copied!");
    let tooltip;
    if (window.bootstrap) {
      button.setAttribute("data-bs-toggle", "tooltip");
      button.setAttribute("data-bs-placement", "left");
      button.setAttribute("data-bs-title", "Copied!");
      tooltip = new bootstrap.Tooltip(button, 
        { trigger: "manual", 
          customClass: "code-copy-button-tooltip",
          offset: [0, -8]});
      tooltip.show();    
    }
    setTimeout(function() {
      if (tooltip) {
        tooltip.hide();
        button.removeAttribute("data-bs-title");
        button.removeAttribute("data-bs-toggle");
        button.removeAttribute("data-bs-placement");
      }
      button.setAttribute("title", currentTitle);
      button.classList.remove('code-copy-button-checked');
    }, 1000);
    // clear code selection
    e.clearSelection();
  });
  function tippyHover(el, contentFn) {
    const config = {
      allowHTML: true,
      content: contentFn,
      maxWidth: 500,
      delay: 100,
      arrow: false,
      appendTo: function(el) {
          return el.parentElement;
      },
      interactive: true,
      interactiveBorder: 10,
      theme: 'quarto',
      placement: 'bottom-start'
    };
    window.tippy(el, config); 
  }
  const noterefs = window.document.querySelectorAll('a[role="doc-noteref"]');
  for (var i=0; i<noterefs.length; i++) {
    const ref = noterefs[i];
    tippyHover(ref, function() {
      // use id or data attribute instead here
      let href = ref.getAttribute('data-footnote-href') || ref.getAttribute('href');
      try { href = new URL(href).hash; } catch {}
      const id = href.replace(/^#\/?/, "");
      const note = window.document.getElementById(id);
      return note.innerHTML;
    });
  }
  const findCites = (el) => {
    const parentEl = el.parentElement;
    if (parentEl) {
      const cites = parentEl.dataset.cites;
      if (cites) {
        return {
          el,
          cites: cites.split(' ')
        };
      } else {
        return findCites(el.parentElement)
      }
    } else {
      return undefined;
    }
  };
  var bibliorefs = window.document.querySelectorAll('a[role="doc-biblioref"]');
  for (var i=0; i<bibliorefs.length; i++) {
    const ref = bibliorefs[i];
    const citeInfo = findCites(ref);
    if (citeInfo) {
      tippyHover(citeInfo.el, function() {
        var popup = window.document.createElement('div');
        citeInfo.cites.forEach(function(cite) {
          var citeDiv = window.document.createElement('div');
          citeDiv.classList.add('hanging-indent');
          citeDiv.classList.add('csl-entry');
          var biblioDiv = window.document.getElementById('ref-' + cite);
          if (biblioDiv) {
            citeDiv.innerHTML = biblioDiv.innerHTML;
          }
          popup.appendChild(citeDiv);
        });
        return popup.innerHTML;
      });
    }
  }
});
</script>
</div> <!-- /content -->



</body></html>
