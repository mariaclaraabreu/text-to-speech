# text to speech
Este é um simples transformador de texto em voz, desenvolvido em JavaScript, feito com a SpeechSynthesis da Web Speech API

<h3>1º passo: </h3>

<p>Coloque o código abaixo no seu arquivo html:</p>

```
<input type="text" id="txtInput">
<button id="btnSpeak">Falar</button>

```

<h3>2º passo: </h3>
<p>No mesmo arquivo, antes de fechar a tag </body>, insira a chamada do script em que o código JavaScript estará:</p>

```
<script src="tts.js"></script>
```

<h3>3º passo:</h3>
<p>Crie um arquivo de extensão .js, no meu caso, chamei de <b>tts</b> .</p>

<h3>4º passo:</h3>
<p>Para termos acesso aos elementos que colocamos no nosso html (input e button), inseriremos o código abaixo no nosso tts:</p>

```
var btnSpeak = document.querySelector('#btnSpeak');
var txtInput = document.querySelector('#txtInput');

```

<p> o <b>querySelector</b> permitirá que manipulemos em nosso arquivo js os elementos do frontend (do html).</p>

<h3>5º passo:</h3>
<p> Criaremos um array de objetos. Esses objetos são referentes ao idioma que queremos utilizar. Nesse caso, criei apenas um, o chamei de Clarinha e disse que ela falaria em português do Brasil.</p>
<p> Caso queiramos inserir o inglês também, basta criar um novo objeto, ou mesmo alterar a linguagem do objeto que já existe (A Clarinha do pt-BR se transformaria em Clarinha do en-US).</P>

```
speaks = [
  {
    "name": "Clarinha",
    "lang":"pt-BR"
  }
]

```
<h3>6º passo:</h3>
<p>Atribuiremos ao nosso botão uma função que será ativada pelo clique:</p>

```
btnSpeak.addEventListener('click', () => {

});

```

<h3>7º passo: </h3>
<p>Dentro da função colocaremos o que desejamos que ocorra após o clique no botão. No caso, queremos que o conteúdo que digitamos no input seja falado pela Clarinha na linguagem pt-BR.</p>
<p>Primeiro criaremos um objeto sintetizador da fala: </p>

```
const msg = new SpeechSynthesisUtterance();

```
<p>Agora, inseriremos os atributos desse objeto sintetizador:</p>

```
  msg.volume = 1; //define o volume do áudio (de 0 a 1)
  msg.rate = 1; // define a velocidade do áudio (0.1 a 1)
  msg.pitch = 1; // define o tom em que o áudio é falado (de 0 a 2)
  msg.text = txtInput.value; //Pega o valor do input e passa para o objeto sintetizar

```

<p>Depois disso, nos comunicamos com o servidor e pedimos o serviço que queremos, no caso, que o texto seja falado:</p>

```

  const voice = speaks[0]; //pegamos o objeto que queremos que seja a nossa fala. [0], pois nosso array speaks só possui uma posição, que é a que queremos (Clarinha pt-BR)
  voice.voiceURI = voice.name; //voiceURI busca o servidor da voz escolhida, no caso, pt-BR defnido em voice.name
  msg.lang = voice.lang; // Define o idioma a ser utilizado para a fala, no caso, o que foi definido para voice.lang

```

<p>Por último, pedimos que o serviço fale o que desejamos passando o msg, cujos atributos definimos anteriormente: </p>

```
 speechSynthesis.speak(msg); //executa a voz

```

<h3>Código final de tts </h3>

```
var btnSpeak = document.querySelector('#btnSpeak');
var txtInput = document.querySelector('#txtInput');

speaks = [
  {
    "name": "Clarinha",
    "lang":"pt-BR"
  }
]

btnSpeak.addEventListener('click', () => {

  const msg = new SpeechSynthesisUtterance();
  msg.volume = 1; //define o volume do áudio (de 0 a 1)
  msg.rate = 1; // define a velocidade do áudio (0.1 a 1)
  msg.pitch = 1; // define o tom em que o áudio é falado ( de 0 a 2)
  msg.text = txtInput.value;
  
  
  const voice = speaks[0];
  // console.log(`Voice: ${voice.name} and Lang: ${voice.lang}`);
  voice.voiceURI = voice.name; //voiceURI busca o servidor da voz escolhida, no caso, pt-BR defnido em voice.name
  msg.lang = voice.lang; // Define o idioma a ser utilizado para a fala, no caso, o que foi definido para voice.lang
  
  speechSynthesis.speak(msg); //executa a voz
  

});

```
![](exemplo.gif)
