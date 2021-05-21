# Desafio javascript

## Introdução

Esse desafio foi solicitado para mostrar os conhecimentos adquiridos sobre javascript, foi desenvolvido um script que crie uma tabela com o Nome e CPF de uma pessoa, essas informações são adquiridas através do HTML e são processadas nele mesmo. Algumas restrições foram adicionadas: caso o CPF ou Nome da pessoa já estivem registradas na tabela será exibida uma mensagem dizendo que o nome ou CPF já estão registrados na tabela. Também há uma validação para que se houver algum campo vazio as informações não são adicionadas a tabela.

## Comentários sobre o código

Esse trecho do código é o HMTL da página. Nele temos a construção das caixas para receber os valores e do botão "adicionar".

```
<head>
<title>Desafio</title>
</head>

<body>
<h2>Desafio Javascript</h2>
<p>
CPF: <input type="number" id="txtCPF" name="txtName" maxlength="11" />
NOME: <input type="text" id="txtNome" name="txtNome" />
<input type="button" id="buttonAdicionar" value="Adicionar" onclick="AdicionarLinha()" />
</p>

<table id="tabelaClientes" name="tabelaClientes" border="1">
<tr>
<td><strong>CPF</strong></td>
<td><strong>NOME</strong></td>
<td><strong>REMOVER</strong></td>
</tr>
</table>
</body>
```

Esse array foi criado para guarda os objetos que serão criados com as informações das caixas.

```
var arrayTabela = [];
```

A função AdicionarLinha() vai validar se os dados passados estão de acordo com as regras e depois disso vai os adicionar a tabela.

```
function AdicionarLinha() { 
```

A variavel cpf vai receber o CPF digitado e a variavel nome vai receber o nome.

```  
var cpf = document.getElementById("txtCPF").value;
var nome = document.getElementById("txtNome").value;
```

Esse código vai validar de algum dos valores recebidos é vazio.

```		  	
if (nome.trim() == "" || cpf == "") {
window.alert("Insira um valor possivel!");
}
```

Se os valores forem validos é criado um objeto com os dados recebidos e é criada a variável jaValidou para apagar os dados escritos se o valor for false.

```
else {

var tabela =
{
"id": arrayTabela.length,
"nome": nome,
"cpf": cpf
}

arrayTabela.push(tabela);

var jaValidou = false;
```

O código seguinte serve para validar se não há na tabela nenhum valor igual aos valores que serão inseridos.

```
for (let i = 0; i < (arrayTabela.length - 1); i++) {
var cpfTabela = tabela.cpf;
var cpfArray = arrayTabela[i].cpf;
var nomeTabela = tabela.nome;
var nomeArray = arrayTabela[i].nome;

if (cpfTabela == cpfArray) {
jaValidou = true;
window.alert("Ja existe um nome com esse CPF cadastrado!");
arrayTabela.pop();
break;
}

if (nomeTabela == nomeArray) {
jaValidou = true;
window.alert("Ja existe um nome como esse cadastrado!");
arrayTabela.pop();
}
```

Se houver os valores inseridos passarem na validação muda os valores dos campos para vazio.

```
if (!jaValidou) {
document.getElementById("txtNome").value = "";
document.getElementById("txtCPF").value = "";
}
```

Apos as validações serem feitas a tabela é construida e a função AdicionarLinha acaba.

```
document.getElementById("tabelaClientes").innerHTML = constroiTabela();
}
}
```

A proxima função é acionada quando o botão "remover" é acionado, ela remove a linha do botão acionado.

```
function RemoverLinha(idLinha) {
arrayTabela.splice(idLinha, 1);
document.getElementById("linhaRemover" + idLinha).remove();
document.getElementById("tabelaClientes").innerHTML = constroiTabela();
}
```

E por ultimo temos a função constroiTabela() que serve para criar e mostrar a tabela atraves do vetor arrayTabela.

```
function constroiTabela() {
var tabelaScript =  "<tr>" +
"<td>" +
"<strong>" +
"CPF" +
"</strong>" +
"</td>" +
"<td>" +
"<strong>" +
"NOME" +
"</strong>" +
"</td>" +
"<td>" +
"<strong>" +
"REMOVER" +
"<strong>" +
"</td>" +
"</tr>";

for (let i = 0; i < arrayTabela.length; i++) {
tabelaScript += "<tr id='linhaRemover" + i + "'>" +
"<td>" +
arrayTabela[i].cpf +
"</td>" +
"<td>" +
arrayTabela[i].nome +
"</td>" +
"<td>" +
"<input type='button' id='buttonRemover" + i + "' value='Remover' onclick='RemoverLinha(" + i + ")' />" +
"</td>"
"</tr>";
}

return tabelaScript;
}
```
