# 📊 Power BI Dashboard – Integração com API do ERP Bling

Este projeto apresenta um dashboard desenvolvido no Power BI com integração à API REST do ERP Bling. A proposta é visualizar dados estratégicos do sistema Bling em um relatório dinâmico e automatizado.

---

## 🚀 Funcionalidades

- Conexão com a API REST do Bling (v3)
- Coleta e autenticação de dados por scripts via Google Apps Script
- Visualização dos dados de vendas, pedidos, produtos e mais
- Dashboard interativo no Power BI com filtros e KPIs
- Atualização automatizada de tokens para manter o fluxo de dados funcionando

---

## 🧰 Tecnologias Utilizadas

- Power BI Desktop
- Google Sheets + Google Apps Script
- API REST do ERP Bling (v3)
- Scripts para atualização de token OAuth2
- Power Query (M)

---

## 🔗 Link da documentação oficial da API Bling

[🔗 Acessar documentação oficial da API Bling](https://developer.bling.com.br/bling-api#introdu%C3%A7%C3%A3o)

---

## 🛠️ Etapas de Configuração

### 1. Criando o Aplicativo no Bling

Acesse o painel do Bling e crie um novo aplicativo:

- **Nome:** api-powerbi (ou outro nome personalizado)
- **Categoria:** Automação
- **Descrição:** Coleta de dados via API para uso em relatórios Power BI
- **URL de redirecionamento:** Use um domínio válido (ex: `https://www.meusite.com.br`)
- **Escopos:** Libere todos os acessos necessários (consultas, inclusões, exclusões)

Após salvar, serão gerados:

- `Client ID`
- `Client Secret`
- Link de convite (usado para obter o `Code`)

📷 *Exemplo de configuração no Bling:*

![Configuração API Bling](imgs/img01.png)

---

### 2. Configurando Google Sheets + Scripts

#### 2.1 Criando a planilha de autenticação

Crie uma planilha chamada **Autenticação Bling** no Google Drive com a estrutura das abas:

- `PrimeiraAuth`
- `AuthBling`

> ⚠️ Mantenha os nomes exatamente iguais aos usados no projeto para evitar erros.

#### 2.2 Criando os scripts de autenticação

1. Acesse `Extensões > Apps Script` dentro da planilha.
2. Crie dois scripts com os mesmos nomes que estão na pasta `/scripts` do repositório:
   - `PrimeiraAutenticacao`
   - `RenovaToken`
3. Renomeie o projeto do script para `AutomacaoBling`.

📷 *Exemplo de estrutura no Google Apps Script:*

![Scripts no Apps Script](imgs/img02.png)

---

### 3. Processo de Autenticação

#### 3.1 Gerar o primeiro token (Code)

1. Cole o `Client ID` e `Client Secret` na aba `PrimeiraAuth`.
2. Acesse o link de convite (em aba anônima) e clique em **Autorizar**.
3. Copie o código da URL após `code=` e cole na coluna `Code` da aba `PrimeiraAuth`.
4. Execute o script `PrimeiraAutenticacao` para gerar o `RefreshToken` e o `Token`.

> ❗ Caso não funcione, repita o processo rapidamente para evitar expiração.

#### 3.2 Gerar novos tokens automaticamente

1. Copie os dados da aba `PrimeiraAuth` para a aba `AuthBling`.
2. Execute o script `RenovaToken` para atualizar os tokens.

#### 3.3 Agendar renovação automática dos tokens

1. No menu lateral do Google Apps Script, vá em **Acionadores**.
2. Adicione um acionador com as opções:
   - Função: `atualizaTokens`
   - Evento: Baseado no tempo
   - Intervalo: A cada 4 horas

---

### 4. Configurando o Power BI

Para melhorar o desempenho no carregamento dos dados da planilha:

1. Acesse:  
   `Arquivo > Opções e configurações > Opções > Arquivo atual > Carregamento de Dados`
2. Marque a opção:  
   `Um (desabilitar o carregamento paralelo de tabelas)`

---

## 📁 Estrutura do Projeto

