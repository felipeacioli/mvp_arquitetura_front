# Controle de Estoque

Front-End do projeto MVP da Disciplina - Arquitetura de Software da PUC-RIO. 

Single page application (SPA) que tem por objetivo gerenciar o estoque de um almoxarifado. 


## Arquitetura da Aplicação     

1. Tecnológias da Aplicação Front-End

HTML (HyperText Markup Language): Estrutura e conteúdo da aplicação web. Define a estrutura das páginas e elementos, como cabeçalhos, parágrafos, formulários, etc.
CSS (Cascading Style Sheets): Estilos e design da aplicação web. Controla a aparência dos elementos HTML, incluindo layout, cores, fontes, e responsividade.
JavaScript: Interatividade e lógica de negócios do lado do cliente. Responde a eventos do usuário e faz chamadas assíncronas às APIs REST.

2. Comunicação com APIs
 
Realiza fetches JavaScript para fazer solicitações HTTP (GET, POST, PUT, DELETE) para APIs REST externas e locais.

API REST Externa: é implementada uma rota que faz um GET para buscar a cotação do dólar comercial através de uma API externa. Foi utilizada a seguinte API: https://v6.exchangerate-api.com. Chamada externa:

```
const getUSDExchangeRate = async () => {
  let apiKey = "ec91dba71503e226d37905fc";
  let url = `https://v6.exchangerate-api.com/v6/${apiKey}/latest/USD`;
  try {
    const response = await fetch(url, {
      method: "GET",
    });
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    const usdRate = data.conversion_rates.BRL;
    return usdRate;
  } catch (error) {
    console.error("Error:", error);
    return null;
  }
};
```

API REST Local: serviço executado na mesma máquina, porém em containers separados via Docker. Foi utilizado operações CRUD (Create, Read, Update, Delete) em um banco de dados local em SQLite.


### Work Flow:

Carregamento da Página:
O navegador carrega os arquivos HTML, CSS e JavaScript. Além disso, a página faz um GET para buscar a cotação do dólar comercial através de uma API externa e mostra o valor na página principal.

Interação do Usuário:
O usuário interage com a interface da aplicação (clicando em botões, preenchendo formulários, etc.).

Solicitações de API:

Com base nas interações do usuário, o JavaScript faz chamadas assíncronas às APIs REST externas e locais usando fetch.

Processamento de Respostas:

As respostas das APIs são processadas pelo JavaScrip.

### Arquitetura do sistema: 

![image](https://github.com/user-attachments/assets/b407d9df-9708-47fb-9b74-83800db91d62)

---
## Como executar via Docker:

Basta fazer o download do projeto e abrir o arquivo index.html no seu browser.
