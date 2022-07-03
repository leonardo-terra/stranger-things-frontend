
# Stranger Things

Essa é uma simples aplicação front-end que busca os dados de uma API REST desenvolvida utilizando Node.js e deploy feito no heroku.

A magica do projeto está em:
https://github.com/leonardo-terra/stranger-things-backend

## Retornos
A lista de personagem possui os seguintes campos:


name: Nome da personagem;

status: se a personagem está viva ou não na série. Os valores possíveis são alive, deceased ou unknown;

origin: o local de origem da personagem.

A resposta é em formato JSON, e o retorno é sempre um array de objetos. Abaixo, um exemplo:
```
[
  {
    "name": "Will",
    "status": "Alive",
    "origin": "Byers Family"
  }
]
```

Modo upside down (dw) 
Na API, no arquivo index.js, há a seguinte variável de controle:

const hereIsTheUpsideDown = true;
Caso ela seja true, a API ativará o modo "Mundo Invertido", conforme a série, e começará a responder desta forma:
```
[
  {
    "name":"llǝssnᴚ",
    "origin":"looɥɔS ǝlppᴉW sƃuᴉʞʍɐH",
    "status":"ǝʌᴉl∀"
  },
  {
    "name":"uǝʌǝlƎ",
    "origin":"ʎlᴉɯɐℲ ɹǝddoH",
    "status":"ǝʌᴉl∀"
  }
]
```
## Filtros
Todos os campos da estrutura de retorno da resposta podem ser utilizados como filtros. Para isso, basta passar na query string o filtro desejado. No exemplo abaixo, estamos filtrando pelo nome do personagem:

localhost:3000?name=el

Os filtros são feitos utilizando uma regex, buscando pelo texto passado na query string em qualquer parte do campo, sem diferenciar maiúsculas de minúsculas.

Nesse caso o retorno seria:
```
[
  {
    "name":"Russell",
    "status":"Alive",
    "origin":"Hawkings Middle School"
  },
  {
    "name":"Eleven",
    "status":"Alive",
    "origin":"Hopper Family"
  }
]
```

## Instalação

Faça o download do repositório:

```bash
git clone git@github.com:leonardo-terra/stranger-things-frontend.git
```
Entre na pasta criada e instale o projeto:

```bash
  npm install
```
Assim que finalizada a instalação, será necessário configurar as variáveis de ambiente no arquivo .env, na raiz do projeto.

Quando configurado, rodar o comando para inicializar o projeto:
```bash
npm start
```

## Funcionalidades

* Uma tabela para exibição da resposta da nossa API;

* Um campo de pesquisa para filtro de nome;

* Botões de navegação para paginação;

* Um botão para ativar o modo Mundo Invertido no front-end.

* Todas essas funcionalidades estão implementadas no componente StrangerThings.




## Comunicação com o backend

Comunicação com o back-end
Na estrutura do projeto, temos um diretório services. Nesse diretório, há um arquivo charactersAPI.js, onde são feitas as chamadas HTTP para a nossa API, utilizando o axios.

O service é uma classe que espera receber a URL da nossa API e um timeout para a requisição:
```
{
  url: 'localhost:3003',
  timeout: 30000
}
Esses parâmetros estão pré-programados de maneira fixa no componente (alteraremos esse comportamento durante o projeto):

const strangerThingsConfig = {
  url: 'localhost:3002',
  timeout: 30000,
};

const upsideDownConfig = {
  url: 'localhost:3003',
  timeout: 30000,
};

const charactersService = new CharactersService(strangerThingsConfig);
const charactersUpsideDownService = new CharactersService(upsideDownConfig);
```
Modo upside down (dw) - Front-end
Assim como no back-end, o front-end também possui um modo "Mundo Invertido". Esse modo é ativado e desativado com o botão "Mudar de Realidade".

A ideia é a seguinte: inicialmente, o front-end possui uma imagem de background e utiliza o service instanciado com a configuração contida na variável strangerThingsConfig. Ao ativar o Mundo Invertido, a imagem de background é alterada e passamos a utilizar o serviço instanciado com a configuração upsideDownConfig.

Desse modo, ao "alternar entre os universos", vamos realizar chamadas a API's diferentes.

No exemplo pré-programado, em um dos "universos", chamamos um serviço na porta 3002 e o outro serviço na porta 3003. Exploraremos esse comportamento durante o projeto.

## Stack utilizada

**Front-end:** React

**Back-end:** Node, Express, Heroku, 

