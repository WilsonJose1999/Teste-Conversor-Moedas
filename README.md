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
