# Curso Básico de JavaScript - Trabalhando com `fetch`

## O que é o `fetch`?

`fetch` é uma função do JavaScript que permite fazer requisições para obter ou enviar dados de/para servidores (como APIs). Ela facilita o trabalho com dados e é muito usada em aplicações web modernas.

---

## 1. Fazendo uma requisição GET

### O que é GET?

`GET` é um método HTTP usado para pedir dados de um servidor. Quando usamos o `fetch` com `GET`, estamos requisitando informações de uma API ou de outro servidor.

### Exemplo de código:
```javascript
fetch('https://api.exemplo.com/dados')  // Faz a requisição para o servidor
  .then(response => response.json())   // Quando receber a resposta, converte para JSON
  .then(data => console.log(data))      // Exibe os dados no console
  .catch(error => console.error('Erro:', error));  // Se houver erro, exibe no console

---

## 2. Enviando dados com POST

### O que é POST?
POST é um método HTTP utilizado para enviar dados para o servidor. É comum em ações como o envio de formulários ou o cadastro de novos dados.

### Exemplo de código:
fetch('https://api.exemplo.com/criar', {
  method: 'POST', // Diz que a requisição é POST (enviar dados)
  headers: {
    'Content-Type': 'application/json'  // Diz que estamos enviando dados em formato JSON
  },
  body: JSON.stringify({ nome: 'João', idade: 30 })  // Envia os dados convertidos para JSON
})
.then(response => response.json())
.then(data => console.log(data))  // Exibe a resposta no console
.catch(error => console.error('Erro:', error));  // Exibe erro, se houver
---
body: Onde ficam os dados que estamos enviando para o servidor. O body é a parte da requisição onde incluímos as informações que desejamos enviar.
JSON.stringify(): Converte o objeto JavaScript em formato JSON. O servidor geralmente espera esse formato, então usamos JSON.stringify() para garantir que os dados sejam enviados corretamente.

## 3.Usando async e await 

### O que são async e await?

async e await são palavras-chave do JavaScript que facilitam o trabalho com funções assíncronas, permitindo escrever um código assíncrono de forma mais clara e legível.

async: Marca a função como assíncrona, permitindo usar await dentro dela.
await: Espera que a Promise seja resolvida antes de continuar a execução do código

### Exemplo de código:
async function obterDados() {
  try {
    let response = await fetch('https://api.exemplo.com/dados');
    let data = await response.json();
    console.log(data);  // Exibe os dados no console
  } catch (error) {
    console.error('Erro:', error);  // Captura e exibe erro
  }
}

obterDados();  // Chama a função
---
A palavra-chave async transforma a função em uma função assíncrona, permitindo que você use await para esperar a resposta de requisições.
await espera a resposta do fetch() antes de continuar a execução do código.

---

## 4. Lidando com Erros

### Como tratar erros?

Ao trabalhar com requisições, pode ser que algo dê errado, como problemas de rede ou um erro no servidor. O JavaScript oferece mecanismos para capturar e tratar esses erros.
### Exemplo de código:
fetch('https://api.exemplo.com/erro')
  .then(response => {
    if (!response.ok) {  // Se a resposta não for boa (status 200-299), dá erro
      throw new Error('Erro na requisição');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Erro:', error));

---

response.ok: Verifica se a resposta foi bem-sucedida (status HTTP 200-299). Se não for, podemos lançar um erro.
throw new Error(): Lança um erro que pode ser capturado pelo catch().

---

## 5. Adicionando Cabeçalhos

### O que são cabeçalhos (headers)?

Cabeçalhos são informações adicionais que você pode incluir em suas requisições. Eles podem ser usados para passar dados como tokens de autenticação, tipos de conteúdo, entre outros.

### Exemplo de código:
fetch('https://api.exemplo.com/dados', {
  headers: {
    'Authorization': 'Bearer seu-token-aqui',  // Envia um token de autenticação
    'X-Custom-Header': 'valor'  // Exemplo de cabeçalho personalizado
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Erro:', error));

---

Authorization: Um cabeçalho comum usado para passar tokens de autenticação, como o Bearer token.
X-Custom-Header: Cabeçalhos personalizados podem ser definidos para necessidades específicas da sua aplicação.

---

## 6. Trabalhando com Dados Não-JSON (Texto, por exemplo)

### O que fazer se o servidor não enviar JSON?

Às vezes, o servidor pode responder com texto ou outro formato, como arquivos binários. Nesse caso, usamos o método text() para lidar com esse tipo de resposta.

### Exemplo de código:
fetch('https://api.exemplo.com/arquivo')
  .then(response => response.text())  // Converte a resposta para texto
  .then(data => console.log(data))  // Exibe o texto
  .catch(error => console.error('Erro:', error));

---

response.text(): Converte a resposta para texto simples. Use-o quando o servidor retornar dados em formato de texto.

---

### Conclusãp

Agora você tem uma ideia básica de como fazer requisições HTTP usando fetch:

GET para obter dados.
POST para enviar dados.
Lidar com erros usando .catch().
Usar async/await para um código mais limpo e legível.
Você pode começar a usar fetch em suas próprias aplicações para interagir com APIs e buscar ou enviar dados.
