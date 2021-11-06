//HTML
# Teste-Conversor-Moedas
Projeto de Conversor de Moedas
<!DOCTYPE html>
<html lang="pt-BR">
<head>
   <meta charset="UTF-8">
   <title>Conversor Monetário</title> 
   <meta name="viewport" content="width=device-width,initial-scale=1">
   <link rel="stylesheet" media="(min-width: 599px)" href="Estilo/principal.css">
   <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
   <script src="conversor.js"></script>
</head>
<body>

  <div id="interface"> 
      <h1 id="titulo">CAIXA Conversor de Moedas</h1> 
      <label>Câmbio</label> </span>  
      <input id="entrada" type="number">   
         
        <select id="moedas">
              <option value='NULL'>Selecionar Moeda</option>
              <option value='EUR'>Euro</option>
              <option value='USD'>Dólar Comercial</option>
              <option value='USDT'>Dólar Turismo</option>
              <option value='CAD'>Dólar Canadense</option>
              <option value='AUD'>Dólar Australiano</option>
              <option value='GBP'>Libra Esterlina</option>
              <option value='ARS'>Peso Argentino</option>
              <option value='JPY'>Yen Japonês</option>
              <option value='CNY'>Yuan Chinês</option>
              <option value='CHF'>Franco Suíço</option>
              <option value='ILS'>Shekel Israelense</option>
              <option value='BTC'>Bitcoins</option>
              <option value='ETH'>Ethereum</option>
              <option value='LTC'>Litecoin</option>
              <option value='DOGE'>Dogecoin</option>
              <option value='XRP'>XRP</option>
        </select>  

      <button onclick="converter()">Fazer Conversão</button>
      <h3 id="saida"></h3> 
      <span id="atualizacao"></span>
  </div>  

</body>
</html>

//CSS
body {
  max-width: 500px;
  margin: auto;
  background-image: url(mercado-financeiro.jpg);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

#interface {
  background-image: url(azul.jpg);
  padding: 40px;
  margin: 25% auto;
  border: 2px solid rgba(136, 136, 136, 0.7);
  border-radius: 5px;
  min-height: 260px;
}

div button {
  padding: 7px;
  border: 1px solid #eee;
  border-radius: 6px;
  background-color: rgb(47, 224, 255);
  font-size: 18px;
  width: 100%;
  margin: 30px 0px 0px 0px;
}

button:hover {
  color: white;
  border: 1px solid black;
  transition: 350ms;
  background-color: rgb(5, 255, 201);
}

button:active {
  background-color: rgb(0, 255, 42);
}

#titulo {
  text-align: center;
  margin: 0px 0px 30px 0px;
  color:#eee;
}

#atualizacao {
  margin-top: 5px;
  color: gray;
}

.alerta {
  position: relative;
  padding: 1rem 1rem;
  margin-bottom: 1rem;
  border: 1px solid transparent;
  border-radius: .25rem;
  display: none;
}

#falha {
  color: #842029;
  background-color: #f8d7da;
  border-color: #f5c2c7;
}

#sucesso {
  color: #0f5132;
  background-color: #d1e7dd;
  border-color: #badbcc;
}

//JS
var resultado;

$.ajax({
  type: "GET",
  dataType: "JSON",
  url: "https://economia.awesomeapi.com.br/json/all",
  success: function (data) {
    resultado = data
  },
  error: function (data) {
    alert('Erro! Falha de carregamento da cotação. Tente novamente mais tarde!!!');
  }
});

function converter() {
  var euro = resultado["EUR"]["bid"] //Moeda da Europa
  var dolar = resultado["USD"]["bid"] //Moeda Comercial dos Estados Unidos 
  var dolarTurismo = resultado["USDT"]["bid"] //Moeda Conversão/Turismo nos Estados Unidos
  var dolarCanadense = resultado["CAD"]["bid"] //Moeda do Canadá
  var dolarAustraliano = resultado["AUD"]["bid"] //Moeda da Austrália
  var libra = resultado["GBP"]["bid"] //Moeda do Reino Unido (UK)
  var peso = resultado["ARS"]["bid"] //Moeda da Argentina
  var iene = resultado["JPY"]["bid"] //Moeda do Japão
  var yuan = resultado["CNY"]["bid"] //Moeda da China
  var franco = resultado["CHF"]["bid"] //Moeda da Suíça
  var shekel = resultado["ILS"]["bid"] //Moeda de Israel
  var btcoin = resultado["BTC"]["bid"] //Criptoeda Mundial
  var ethereum = resultado["ETH"]["bid"] //Moeda Digital Cripto ETHER
  var ltcoin = resultado["LTC"]["bid"] //LITECOIN: Criptomoeda
  var dogecoin = resultado["DOGE"]["bid"] //DOGECOIN: Criptomoeda
  var xrp = resultado["XRP"]["bid"] //Moeda Ripple XRP

function getHorarioAtualizacao(codigoMoeda) {
      var data = (resultado[codigoMoeda]["create_date"])
//Mudando a formatação da data para DD/MM/AA 
    var dia = data.substring(8, 10)
    var mes = data.substring(5, 7)
    var ano = data.substring(0, 4)
    var hora = data.substring(11, 16)
    var dataFormatada = `${dia}/${mes}/${ano} às ${hora}`
    atualizacao = document.querySelector("#atualizacao");
    atualizacao.innerHTML = 'Cotação atualizada em ' + dataFormatada; //Data da Operação
  }

  var numeroDigitado = document.querySelector("#entrada").value;
  numeroDigitado = parseFloat(numeroDigitado);

  var calculo;

  var saida = document.querySelector("#saida");
  var selecionado = document.querySelector("#moedas").value;

  function calcular(valorMoeda, codigoMoeda){
    calculo = numeroDigitado * valorMoeda
    numeroDigitado = numeroDigitado.toLocaleString('en-us', { style: 'currency', currency: codigoMoeda });
    calculo = calculo.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' });
    saida.innerHTML = `Resultado: ${numeroDigitado} = ${calculo}`
    getHorarioAtualizacao(codigoMoeda)
  }

  if (isNaN(numeroDigitado) == true && selecionado == "NULL") {
    alert("ENTRE COM UM VALOR E OPTE POR UMA MOEDA ESPECÍFICA!!!")
  } else {
    if (isNaN(numeroDigitado) == true) {
      alert("ESCREVA UM VALOR!!!")
    }
    if (selecionado == "NULL") {
      alert("ELEJA UMA MOEDA ESPECÍFICA!")
    }
  }

  if (numeroDigitado <= 0) {
    alert("OPERAÇÃO NEGADA! DIGITE UM VALOR POSITIVO E DIFERENTE DE ZERO!!!")
  }

  if (selecionado == "EUR" && !isNaN(numeroDigitado) && !isNaN(euro)) {
      calcular(euro, "EUR")
  }

  if (selecionado == "USD" && !isNaN(numeroDigitado) && !isNaN(dolar)) {
      calcular(dolar, "USD")
  }

  if (selecionado == "USDT" && !isNaN(numeroDigitado) && !isNaN(dolarTurismo)) {
    calcular(euro, "USDT")
  }

  if (selecionado == "CAD" && !isNaN(numeroDigitado) && !isNaN(dolarCanadense)) {
      calcular(dolarCanadense, "CAD")        
  }

  if (selecionado == "AUD" && !isNaN(numeroDigitado) && !isNaN(dolarAustraliano)) {
      calcular(dolarAustraliano, "AUD")
  }

  if (selecionado == "GBP" && !isNaN(numeroDigitado) && !isNaN(libra)) {
      calcular(libra, "GBP")
  }

  if (selecionado == "ARS" && !isNaN(numeroDigitado) && !isNaN(peso)) {
      calcular(peso, "ARS")
  }

  if (selecionado == "JPY" && !isNaN(numeroDigitado) && !isNaN(iene)) {
      calcular(iene, "JPY")
  }

  if (selecionado == "CNY" && !isNaN(numeroDigitado) && !isNaN(yuan)) {
      calcular(yuan, "CNY")
  }

  if (selecionado == "CHF" && !isNaN(numeroDigitado) && !isNaN(franco)) {
      calcular(franco, "CHF")
  }

  if (selecionado == "ILS" && !isNaN(numeroDigitado) && !isNaN(shekel)) {
      calcular(shekel, "ILS")
  }

  if (selecionado == "BTC" && !isNaN(numeroDigitado) && !isNaN(btcoin)) {
      btcoin = btcoin * 1000
      calcular(btcoin, "BTC")
  }

  if (selecionado == "ETH" && !isNaN(numeroDigitado) && !isNaN(ethereum)) {
      calcular(ethereum, "ETH")
  }

  if (selecionado == "LTC" && !isNaN(numeroDigitado) && !isNaN(ltcoin)) {
      calcular(ltcoin, "LTC")
  }

  if (selecionado == "DOGE" && !isNaN(numeroDigitado) && !isNaN(dogecoin)) {
      calcular(dogecoin, "XDG")
  }

  if (selecionado == "XRP" && !isNaN(numeroDigitado) && !isNaN(xrp)) {
      calcular(xrp, "XRP")
  }
}
