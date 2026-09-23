# 🌊 Project Atlântida

> Um projeto pessoal para automatizar, organizar e centralizar informações da plataforma FIAP EAD.

O **Project Atlântida** é um sistema em desenvolvimento que utiliza automação, web scraping e, futuramente, inteligência artificial para interagir com a plataforma da FIAP, coletar informações acadêmicas e disponibilizá-las de forma prática.

O projeto nasceu da vontade de transformar tarefas repetitivas da plataforma em processos automatizados e, ao mesmo tempo, estudar na prática conceitos de programação, automação, sistemas web e inteligência artificial.

---

## 🚀 Objetivo

O objetivo principal do Atlântida é criar um sistema capaz de:

- Fazer login automaticamente na plataforma FIAP EAD;
- Acessar páginas específicas da plataforma;
- Coletar materiais e informações acadêmicas;
- Identificar o progresso de leitura dos materiais;
- Armazenar nomes, status e links dos conteúdos;
- Coletar tarefas, quizzes, reuniões e provas;
- Organizar as informações em um arquivo `data.json`;
- Manter um histórico mensal dos dados coletados;
- Disponibilizar essas informações futuramente através de um bot do Discord;
- Evoluir para um sistema com inteligência artificial capaz de interpretar a plataforma de forma mais autônoma.

---

## 🧠 Arquitetura

O Atlântida está sendo desenvolvido de forma modular.

A ideia é separar as responsabilidades do projeto em diferentes componentes:

```text
Project Atlântida
│
├── Scraper
│   ├── Login
│   ├── Materiais
│   ├── Tarefas
│   ├── Reuniões
│   └── Provas
│
├── Data
│   ├── data.json
│   └── Histórico mensal
│
├── Discord Bot
│   └── Comandos para consultar as informações
│
└── Inteligência Artificial
    └── Futuro módulo de interpretação e tomada de decisões
```

O scraper é responsável por acessar a FIAP e coletar os dados.

O `data.json` funciona como o armazenamento das informações do mês atual.

O bot do Discord será responsável por apresentar essas informações ao usuário.

---

## 🕷️ Web Scraper

O scraper utiliza **Node.js** e **Puppeteer** para controlar um navegador e interagir com a plataforma.

Entre as tarefas do scraper estão:

1. Acessar a FIAP;
2. Realizar login;
3. Verificar se o login foi realizado corretamente;
4. Acessar as páginas necessárias;
5. Encontrar elementos HTML através de seletores;
6. Extrair informações;
7. Filtrar elementos duplicados;
8. Organizar os dados;
9. Salvar as informações no `data.json`.

A estrutura está sendo dividida em funções para evitar que o `index.js` se transforme em um arquivo gigante.

Exemplo:

```text
Functions/
├── login.js
├── materiais.js
├── json.js
└── ...
```

Novas funções serão adicionadas conforme novos módulos do Atlântida forem desenvolvidos.

---

## 📚 Materiais

Um dos primeiros módulos do projeto é a coleta dos materiais das fases da FIAP.

Cada material deverá possuir:

```json
{
    "nome": "Nome do material",
    "status": "100%",
    "link": "https://..."
}
```

No `data.json`, os materiais serão organizados desta forma:

```json
{
    "materiais": {
        "material1": {
            "nome": "Cap 1 - INTELIGÊNCIA ARTIFICIAL NO COMANDO",
            "status": "100%",
            "link": "https://..."
        },
        "material2": {
            "nome": "Cap 2 - A Arquitetura Modular que Sustenta o Cérebro Lógico da IA",
            "status": "0%",
            "link": "https://..."
        }
    }
}
```

O scraper também precisa lidar com a estrutura responsiva da plataforma, que pode apresentar elementos duplicados entre os layouts desktop e mobile.

Por isso, existe uma etapa de filtragem e comparação para evitar que o mesmo material seja processado duas vezes.

---

## 💾 Armazenamento

O arquivo `data.json` representa o estado atual do projeto.

A ideia é que ele seja utilizado durante o mês para armazenar:

```text
data.json
├── materiais
├── tarefas
├── reuniões
├── provas
└── outras informações
```

No final de cada mês, os dados serão arquivados em um arquivo histórico, seguindo o padrão:

```text
08-2026.txt
09-2026.txt
10-2026.txt
...
```

Depois do arquivamento, o `data.json` será limpo e preparado para receber os dados do próximo mês.

Dessa forma:

```text
Mês atual
    ↓
data.json
    ↓
arquivamento
    ↓
08-2026.txt
    ↓
limpeza
    ↓
novo mês
```

---

## 🤖 Discord Bot

O bot do Discord será a interface de consulta do Atlântida.

A ideia é permitir comandos como:

```text
!tarefas
!materiais
!agenda
!reunioes
!provas
!status
!ping
!atualizar
!login
!reset
```

O bot não precisa acessar diretamente a plataforma.

A arquitetura planejada separa o scraper do bot:

```text
              ┌───────────────┐
              │  FIAP EAD     │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │    Scraper    │
              └───────┬───────┘
                      │
                      ▼
                data.json
                      │
                      ▼
              ┌───────────────┐
              │ Discord Bot   │
              └───────┬───────┘
                      │
                      ▼
                   Usuário
```

Essa separação permite que o scraper e o bot sejam executados como processos independentes.

---

## 🖥️ Servidores

O projeto também possui uma arquitetura planejada para execução em máquinas separadas.

Um servidor será responsável principalmente por:

- manter o bot online;
- executar o scraper;
- executar processos automatizados;
- realizar tarefas de manutenção.

Outro computador poderá funcionar como servidor de armazenamento, mantendo as informações coletadas e o histórico.

A ideia é transformar máquinas antigas em infraestrutura útil para o próprio projeto.

---

## 🧹 Automação e manutenção

Além do scraper, o projeto pretende possuir scripts próprios para administração do servidor, incluindo futuramente:

- atualização do sistema;
- manutenção de disco;
- limpeza de arquivos;
- monitoramento;
- execução automática de processos;
- gerenciamento dos serviços do Atlântida;
- comandos personalizados para administração.

---

## 🧠 Inteligência Artificial

A inteligência artificial é uma das etapas futuras mais ambiciosas do projeto.

A ideia é que a IA não dependa exclusivamente de seletores previamente definidos.

Um possível módulo futuro poderá analisar a própria página e identificar:

- textos;
- botões;
- links;
- menus;
- pop-ups;
- caminhos de navegação;
- informações importantes.

Por exemplo, caso a FIAP apresente um novo pop-up, o scraper atualmente poderá possuir uma função específica para identificá-lo e fechá-lo.

No futuro, a IA poderá interpretar visualmente ou estruturalmente a página e descobrir por conta própria como continuar a navegação.

Isso poderá permitir que o Atlântida:

```text
visualize a página
      ↓
interprete os elementos
      ↓
identifique o objetivo
      ↓
escolha uma ação
      ↓
execute a ação
      ↓
interprete o resultado
```

Essa parte ainda está em planejamento e será desenvolvida posteriormente.

---

## 🛠️ Tecnologias

Atualmente, o projeto utiliza principalmente:

- **Node.js**
- **JavaScript**
- **Puppeteer**
- **JSON**
- **Discord**
- **Git / GitHub**

Tecnologias adicionais poderão ser incorporadas conforme o projeto evoluir.

---

## 📌 Status do projeto

**Em desenvolvimento.**

### Atualmente

- [x] Login automatizado na FIAP
- [x] Separação das funções em arquivos
- [x] Leitura e escrita do JSON
- [x] Acesso direto à página de materiais
- [x] Coleta dos nomes dos materiais
- [x] Identificação de duplicatas
- [x] Coleta dos percentuais de progresso
- [ ] Associação definitiva entre material, progresso e link
- [ ] Estrutura completa do `data.json`
- [ ] Coleta de tarefas
- [ ] Coleta de reuniões
- [ ] Coleta de provas
- [ ] Arquivamento mensal automático
- [ ] Integração completa com Discord
- [ ] Sistema de manutenção dos servidores
- [ ] Módulo de inteligência artificial

---

## 🌊 Por que "Atlântida"?

O nome **Atlântida** nasceu de uma conversa familiar que marcou a história do projeto.

A inspiração veio de uma pessoa que, anos atrás, despertou o interesse do desenvolvedor por tecnologia ao explicar que os programas e jogos eram construídos a partir de linhas de código e que profissionais de engenharia de software eram responsáveis por criá-los.

Anos depois, durante uma conversa sobre o projeto, surgiu o nome **Atlântida**.

A ideia acabou se tornando mais do que apenas um nome: representa a origem e a evolução do projeto.

---

## ⚠️ Segurança

Credenciais da FIAP, tokens de bots, chaves de API e outras informações sensíveis **não devem ser armazenadas diretamente no código-fonte ou commitadas no GitHub**.

Utilize variáveis de ambiente, arquivos locais ignorados pelo Git ou outro mecanismo seguro de configuração.

Exemplo:

```text
.env
```

E mantenha esse arquivo fora do repositório através do `.gitignore`.

---

## 📜 Licença

Projeto pessoal em desenvolvimento.

A licença poderá ser definida futuramente.

---

## 👨‍💻 Desenvolvedor

**Project Atlântida** — desenvolvido como projeto pessoal de estudo, automação e experimentação em tecnologia.

> "Tudo começa com algumas linhas de código."
