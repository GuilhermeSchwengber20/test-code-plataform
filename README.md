# The Test Code Generator

## Visão Geral

Esta aplicação foi construída usando Vite e Vue.js para interagir com a API ChatGPT. Permite aos usuários gerar testes em sua linguagem de programação preferida (atualmente suportando JavaScript e Python) e escolher entre bibliotecas de teste como Jest, Cypress, PyTest e Unittest. A aplicação envia uma solicitação HTTP para a API ChatGPT, que retorna um script de teste na linguagem e biblioteca de teste selecionadas.

## Tecnologias Utilizadas

- Vue.js
- JavaScript
- API ChatGPT
- CodeMirror
- Vite
- TailwindCSS

## Como Começar

Siga as etapas abaixo para configurar e executar a aplicação localmente.

### Pré-requisitos

- Node.js (v14.0.0 ou superior)
- npm (v6.0.0 ou superior)

### Instalação

1. Clone o repositório:

```bash
git clone https://github.com/seu-nome/test-code-plataform.git
cd test-code-plataform
```

2. Instale as dependências:

```bash
npm install
```
3. Configure 2 variaveis de ambiente em .env
```
  VITE_SECRET_API_KEY=<chave-api-chatgpt>
  VITE_BASE_URL=<url-api-chatgpt>
```
### Uso

1. Inicie o servidor de desenvolvimento:

```bash
npm run dev
```

2. Abra seu navegador e vá para [http://localhost:5173](http://localhost:5173).

3. Escolha sua linguagem e biblioteca de teste preferidas, em seguida, insira seu trecho de código.

4. Clique no botão "Gerar Teste" e a aplicação fará uma solicitação à API do ChatGPT para gerar um script de teste.

## Trechos de Código

### JavaScript (Jest)

```javascript
// Exemplo de Teste em JavaScript (Jest)
test('Exemplo de teste', () => {
  // Seu código de teste gerado aqui
});
```

### Python (PyTest)

```python
# Exemplo de Teste em Python (PyTest)
def test_exemplo():
    # Seu código de teste gerado aqui
```

## Contribuições

Sinta-se à vontade para contribuir para este projeto enviando problemas (issues) ou pull requests. Certifique-se de seguir o [código de conduta](CODE_OF_CONDUCT.md).

## Licença

Este projeto é licenciado sob a Licença MIT - consulte o arquivo [LICENSE](LICENSE) para obter detalhes.

---

