<h1> SASS - Compilador CSS</h1>

<h2>Introdução</h2>

<p>Vamos imaginar uma situação hipotética, você vai fazer um site para uma empresa grande, e vai existir várias linhas em css de estilização, então você vai ter que escrever muitas coisas repetitivamente e isso é muito cansativo. Bem, o SASS ajuda nisso, o SASS serve para ajudar na hora de estilizar uma página web. O SASS consegue aninhar classes, criar variáveis, realizar contas matemáticas, quebrar arquivos de estilos em diversos arquivos, importar estilos e arquivos e reaproveitar os estilos.</p>

<p>Então para começar vamos criar um arquivo com o nome "style.scss" que nada mais é que o SASS, após isso aperte o (ctrl+shift+P) e procure por "Live Sass: Watch Sass".</p>

<h2>Aninhamento</h2>

<p>No css é muito comum fazermos linhas com várias classes e isso se torna repetitivo. Por exemplo, quando pensamos em um container que dentro dele tem uma classe (vamos dar o nome de texto), para que haja a estilização do container, usamos em css o ".container .texto", porém agora em Sass não precisamos mais fazer isso, pois o Sass trabalha com aninhamento. Para entendermos melhor vamos ver o exemplo:</p>

```
.container{
    height: 100vh;
    display: flex; 
    .esquerdo{
        width: 50%;
        background-color: blueviolet;
        .texto{
            margin-top: 40%;
            text-align: center;
            font-size: 150px;
            color:aquamarine;
        }
    }
```

<p>Dessa forma não temos que repetir nomes de classes, e com isso, o código fica mais limpo e melhor para entendermos.</p>
<i>"Mas...e o style.css, como fica? Ja que não existe essa de aninhamento no css."</i>
<p>O Sass e o CSS trabalha igual no typescript com o javascript, ele basicamente reescreve o código só que nos padrões estipulados na linguagem em questão. Por exemplo, esta linha de código que foi passado anteriormente, em CSS vai ficar assim:</p>

```
.container {
  height: 100vh;
  display: flex;
}
.container .esquerdo {
  width: 50%;
  background-color: blueviolet;
}
.container .esquerdo .texto {
  margin-top: 40%;
  text-align: center;
  font-size: 150px;
  color: aquamarine;
}
```

<p>O que o css fez foi traduzir o que tem no Sass.</p>

<h2>Variáveis</h2>

<p>Para criarmos variáveis no sass, usamos o cifrão.</p>

```
$cor-principal:blueviolet ;
$cor-secundaria: aquamarine;
```

<i>"Mas qual a necessidade disso?"</i>
<p>Pense em um projeto gigantesco, com mais de 10 mil linhas, o cliente pediu para trocar as cores, porém tem muito lugar para trocar. Em uma situação em que a pessoa não utilizou uma variável e só foi repetindo o famoso "color:...", basicamente vai demorar uma eternidade para mudar todas as cores. Porém, em uma situação que existe variáveis, você pode só mudar a cor na variável e pronto, tudo que tiver a variável, vai mudar para a nova cor.</p>
<p>Para chamar é bem simples, só precisamos colocar o $ + nome da variável.</p>

```
background-color: $cor-secundaria;
```

<h2>Mixin</h2>

<p>Nosso código ta bem repetitivo novamente, se olharmos para a classe "esquerdo" e "direito" vemos que existe coisas que se repetem entre elas, então para resolver isso temos o mixin. Basicamente vai server para guardar um código que poderá ser utilizado posteriormente.</p>

```
@mixin cor-e-texto($cor-de-fundo, $cor-do-texto) {
    width: 50%;
    background-color: $cor-de-fundo;
        .texto{
            margin-top: 40%;
            text-align: center;
            font-size: 150px;
            color:$cor-do-texto;
        }
}
```

<p>Nesse caso a variável teve que ser definida antes. Quando chamarmos o mixin, vamos ter que passar as variáveis como parametro.</p>

```
    .esquerdo{
        @include cor-e-texto($cor-principal, $cor-secundaria);
    }
    .direito{
        @include cor-e-texto($cor-secundaria, $cor-principal)
    }
```