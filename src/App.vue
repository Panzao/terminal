<template>
  <!-- Corpo -->
    <div class="container">
      <div class="janela">
        <div class="barra_menu">
          <!-- Botão -->
          <div class="botoes">
            <button class="btn_sair"></button>
            <button class="btn_minimizar"></button>
            <button class="btn_maximizar"></button>
          </div>
          <!-- Titulo -->
          <span>1. dalmo@313x.com.br ~ (Cybersecurity)</span>
        </div>
        <!-- Terinal -->
        
        <div class="terminal" id="terminal">{{ titulo }}
          <br>
          <span id="pula_linha"></span>
          <span class="prompt">➜ </span>
          <span class="path">~ </span>
          <span id="historia"></span>
        </div>
      </div>
    </div>
</template>


<script>
  // VueJs Página Atual //
  
  // Import // 
  // import Vue from 'vue';
  import axios from 'axios';

  // Pega o ip e a data para gerar o titulo //
  export default{
    name: 'App',
    data() {
      return {
        ip:'',
        titulo:''
      }
    },
    created: function(){
      axios.get('https://api.ipify.org?format=json&callback=?').then(res => {
        const today = new Date();
        const date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
        const time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
        const dateTime = date + ' ' + time;

        this.ip = res.data.ip;
        this.titulo = 'Last login: ' + dateTime + ' on ttys000 / ip: ' + this.ip;
      })
    }
  }

  // Ascii //
  document.addEventListener('keypress', (event) => {
    // console.log(event);
    
    var historia = document.getElementById("historia");
    var pula_linha = document.getElementById("pula_linha");

    // Apagar //
    if (event.charCode == 61) {
      historia.innerHTML = historia.innerHTML.substring(0, historia.innerHTML.length - 1);
      return;
    }

      // Executar no enter //
    if (event.key == "Enter") {
      var msg = ' <span class="prompt">➜</span> <span class="path">~</span> '+historia.innerHTML+' <br> Cybersecurity: ';
      
      if (historia.innerHTML == "clear") {
        pula_linha.innerHTML = '';
        historia.innerHTML = '';
      } else if (historia.innerHTML == "help") {
        pula_linha.innerHTML += msg + 'Comandos aceitáveis: help, clear, historia <br>';
        pula_linha.innerHTML += ' Cybersecurity: Apagar caracteres "=" <br>';
      } else if (historia.innerHTML == "historia") {
        pula_linha.innerHTML += msg + ' A melhoria da segurança de rede é a prioridade máxima de todas as empresas e organizações de hoje. A história da segurança de rede teve início por volta de 1950, quando as pessoas começaram a perceber que havia valor intrínseco nos dados. Isso aconteceu em uma série de eventos, na medida em que a era da informação digital foi se desenrolando na segunda metade do século 20.<br><br>';
        pula_linha.innerHTML += ' No fim da década de 1960 e início de 1970, o armazenamento digital começou a se tornar realidade. Mainframes que ocupavam salas inteiras eram responsáveis pelo armazenamento dessa informação e o acesso a esses repositórios era feito por meio de uma conexão direta ou acesso por um dos inúmeros terminais dentro das instalações. As primeiras empresas a adotarem a tecnologia de armazenamento digital não enfrentaram nenhum problema relativo à proteção de informações sigilosas, já que era necessário estar dentro do prédio em que o equipamento estava para acessar a informação.<br><br>';
        pula_linha.innerHTML += ' Menos de uma década depois, com um número crescente de dados armazenados, houve uma mudança de pensamento. Dados tinham valor e incluíam grandes volumes de informações pessoais identificáveis, como dados de cartões de crédito, número de contas bancárias, declarações de renda, detalhes pessoais, informações demográficas sobre grandes grupos populacionais. Durante essa mudança, a informação começou a se tornar uma commodity.<br><br>';
        pula_linha.innerHTML += ' Isso foi apenas o começo do futuro da segurança de rede, já que a revolução de dados teria continuidade, provocando mudanças nas estratégias de segurança. Pense que em apenas cinco anos a partir de agora, os dados somados do mundo todo devem alcançar 175 zettabytes. É até difícil imaginar o tamanho de um zettabyte, mas só para você ter uma ideia do que isso representa, pense no número 175 seguido de 21 zeros. Esse volume de dados gigantesco incluirá banco de dados, vídeos, fotos, todos os tipos de aplicativos e muito mais.<br><br>';
        pula_linha.innerHTML += ' A proliferação rápida dos dados digitais trouxe um risco sem precedentes de que informações super sigilosas acabem caindo nas mãos das pessoas erradas.<br><br>';
        pula_linha.innerHTML += ' A introdução do acesso online e a internet aumentaram enormemente esse risco. As empresas não tinham apenas grandes volumes de informações pessoais de funcionários e clientes, mas também começaram a compartilhar, vender e reempacotar esses dados. Isso trouxe preocupações e riscos ainda maiores.<br><br>';
        pula_linha.innerHTML += ' Na medida em que dados se tornaram commodities de alto valor, foi inevitável o surgimento dos crimes cibernéticos e a abordagem moderna de segurança contra essa prática. Qualquer coisa com valor pode ser comprada, vendida e, mais importante, roubada. As empresas tiveram que enfrentar a nova realidade: é preciso proteger as informações sigilosas contra cibercriminosos.<br><br>';
        pula_linha.innerHTML += ' De fato, estudos recentes mostram que, até 2023, mais de 33 bilhões de registros de dados serão roubados por cibercriminosos, representando um aumento de 175% em relação a 2018.<br><br>';
      } else {
        pula_linha.innerHTML += msg + 'Comando "'+historia.innerHTML+'" não encontrado! para mais informações utilize o comando "help"<br>';
      }
      historia.innerHTML = '';
    }

    // Escrever //
    if (event.charCode >= 32 && event.charCode <= 126) {
      historia.innerHTML += event.key;
    }
  });

</script>


<style>
/* CSS Página atual */

  /* Tela cheia */
  html, body {
    height: 100%;
    overflow: hidden;
  }

  /* Fundo */
  body {
    background: #3a7bd5;
    background-image: -webkit-radial-gradient(top, circle cover, #00d2ff 0%, #3a7bd5 80%);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  /* Borda */
  * {
    box-sizing: border-box;
  }

  /* Scrollbar customizada */
  textarea, input, button {
    outline: none;
  }

  ::-webkit-scrollbar {
    width: 5px;
  }

  ::-webkit-scrollbar-track {
    background: #f1f1f1; 
  }
  
  ::-webkit-scrollbar-thumb {
    background: #888; 
  }

  ::-webkit-scrollbar-thumb:hover {
    background: #555; 
  }

  /* Css padrão botões */
  .janela-button, .janela .botoes .btn_maximizar, .janela .botoes .btn_minimizar, .janela .botoes .btn_sair {
    padding: 0;
    margin: 0;
    margin-right: 4px;
    width: 12px;
    height: 12px;
    cursor: default;
    background-color: gainsboro;
    border: 1px solid rgba(0, 0, 0, 0.2);
    border-radius: 6px;
    color: rgba(0, 0, 0, 0.5);
  }

  /* Barra do botões */
  .janela .barra_menu {
    height: 22px;
    background: linear-gradient(0deg, #d8d8d8, #ececec);
    border-top: 1px solid white;
    border-bottom: 1px solid #b3b3b3;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    color: rgba(0, 0, 0, 0.7);
    font-family: Helvetica, sans-serif;
    font-size: 13px;
    line-height: 22px;
    text-align: center;
  }

  /* Botões  btn_Minimizar / btn_Maximizar / btn_Sair */
  .janela .botoes {
    position: absolute;
    float: left;
    margin: 0 8px;
  }

  .janela .botoes .btn_sair {
    background-color: #ff6159;
  }

  .janela .botoes .btn_minimizar {
    background-color: #ffbf2f;
  }

  .janela .botoes .btn_maximizar {
    background-color: #25cc3e;
  }

  /* Css terminal */
  .janela .terminal {
    padding: 4px;
    background-color: black;
    opacity: 0.7;
    height: 218px;
    color: white;
    font-family: "Source Code Pro", monospace;
    font-weight: 200;
    font-size: 14px;
    white-space: pre-wrap;
    white-space: -moz-pre-wrap;
    white-space: -pre-wrap;
    white-space: -o-pre-wrap;
    word-wrap: break-word;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    overflow-y: auto;
  }

  /* Barra de digitar piscando | */
  .janela .terminal::after {
    content: "|";
    animation: blink 2s steps(1) infinite;
  }

  /* Cor do ➜ */
  .prompt {
    color: #bde371;
  }

  /* Cor do ~ */
  .path {
    color: #5ed7ff;
  }
  
  /* Animação Inicia */
  .janela {
    animation: bounceIn 1s ease-in-out;
    width: 640px;
  }
  
  /* Animação */
  /* Animação barra de digitar piscando | */
  @keyframes blink {
    50% {
      color: transparent;
    }
  }
  
  /* Animação Inicial */
  @keyframes bounceIn {
    0% {
      transform: translateY(-1000px);
    }

    60% {
      transform: translateY(200px);
    }

    100% {
      transform: translateY(0px);
    }
  }
</style>
