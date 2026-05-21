# 🚀 Automação de API E2E - ServeRest

Este projeto contém uma suíte completa de testes automatizados End-to-End (E2E) para a API [ServeRest](https://serverest.dev/). O foco desta arquitetura é validar o ciclo de vida completo de dados, regras de negócio, segurança de endpoints e garantir a independência do ambiente de testes (Teardown).

## 🎯 Objetivos do Projeto
Demonstrar domínio sobre o ciclo de desenvolvimento de testes de API, incluindo:
- Validação de rotas CRUD (POST, GET, PUT, DELETE).
- Design de Testes Negativos (Validação de status 400 e 401).
- Validação de cabeçalhos de segurança e métodos permitidos (CORS/OPTIONS).
- Configuração de Herança de Autorização (Bearer Token).
- Execução via linha de comando (CLI) com relatórios visuais profissionais.

---

## 🏗️ Arquitetura da Collection

A automação foi dividida em três domínios principais para facilitar a manutenção e escalar os testes:

### 📁 1. Autenticação e Segurança
Responsável por garantir o controle de acesso à API.
- Criação de usuário dinâmico administrador.
- Geração e extração de token de acesso.
- **Teste Negativo:** Validação de bloqueio (401 Unauthorized) com credenciais inválidas.
- **Teste de Segurança:** Requisição `OPTIONS` para validar métodos permitidos no cabeçalho do servidor (`Access-Control-Allow-Methods`).

### 📁 2. Ciclo de Vida do Produto
Valida a persistência e a integridade dos dados no banco.
- Cadastros com massa de dados dinâmica.
- Consultas (`GET`) para garantir a integridade dos dados salvos.
- Atualizações completas de recursos (`PUT`).
- **Teste Negativo:** Prevenção de duplicidade de registros (400 Bad Request).
- *Nota: Utiliza herança de autorização no nível da pasta.*

### 📁 3. Fluxos de Negócio
Simula o comportamento real do usuário final.
- Criação de carrinhos de compra.
- Consultas avançadas utilizando *Query Parameters*.
- **Teardown (Limpeza de Dados):** Exclusão do carrinho e do usuário ao final do ciclo para garantir a independência do ambiente e evitar lixo no banco de dados para execuções futuras.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
- **Postman:** Modelagem da arquitetura, chamadas e validação inicial de scripts (JavaScript/Chai).
- **Node.js:** Ambiente de execução base.
- **Newman:** Ferramenta CLI oficial do Postman para execução da automação no terminal.
- **Newman HTML Extra:** Gerador de relatórios visuais (Dashboard).

---

## 🚀 Como Executar o Projeto Localmente

### Pré-requisitos
Certifique-se de ter o [Node.js](https://nodejs.org/) instalado na sua máquina.

1. Clone este repositório:
   ```bash
   git clone [URL_DO_SEU_REPOSITORIO]
   cd [NOME_DA_PASTA_DO_REPOSITORIO]

```

2. Instale o Newman e o repórter HTML globalmente:
```bash
npm install -g newman newman-reporter-htmlextra

```


3. Execute a suíte de testes injetando as variáveis dinamicamente:
```bash
newman run "ServeRest - Automacao E2E.postman_collection.json" -e "ServeRest - QA.postman_environment.json" --env-var "base_url=[https://serverest.dev](https://serverest.dev)" --env-var "email_invalido=naocadastrado@qa.com.br" --env-var "timeout_esperado=500" -r cli,htmlextra

```



### 📊 Relatório de Testes

Após a execução do comando acima, uma pasta chamada `newman` será gerada automaticamente na raiz do projeto. Abra o arquivo `.html` no seu navegador para visualizar um dashboard interativo contendo os gráficos de sucesso, falhas e tempo de requisição de todos os endpoints testados.

---

