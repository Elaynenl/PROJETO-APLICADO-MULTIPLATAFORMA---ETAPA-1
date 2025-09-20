## ConectaBairro
ConectaBairro é uma proposta de plataforma digital voltada para conectar moradores de bairros urbanos com empreendimentos locais. A aplicação permitirá que empreendedores, micro e pequenos empresários divulguem seus serviços e produtos, enquanto moradores poderão buscar opções próximas de forma rápida, centralizada e acessível.

---

## Sumário

- [ConectaBairro](#conectabairro)
- [Descrição](#descrição)
- [Problema Abordado e Justificativa](#problema-abordado-e-justificativa)
- [Conexão com o ODS 11](#conexão-com-o-ods-11)
- [Objetivos do Sistema](#objetivos-do-sistema)
- [Visão Geral da Arquitetura (com diagrama)](#visão-geral-da-arquitetura-com-diagrama)
- [Tecnologias Propostas](#tecnologias-propostas)
- [Cronograma para Etapa 2 (Implementação do Projeto)](#cronograma-para-etapa-2-implementação-do-projeto)
- [Integrantes da Equipe e Seus Papéis](#integrantes-da-equipe-e-seus-papéis)
- [Documentos Complementares](#documentos-complementares)

  ---

## Descrição

Muitas vezes, moradores percorrem grandes distâncias em busca de serviços que já existem dentro do próprio bairro. A ideia é transformar essa realidade por meio de uma solução digital que valorize o comércio local e incentive a economia colaborativa.

Inspirado nos antigos “jornalzinhos de bairro”, o projeto pretende criar um ambiente moderno e acessível, onde qualquer pessoa possa encontrar o que precisa — de forma prática, sem depender de grandes plataformas ou redes sociais. O foco está na simplicidade, na proximidade e na valorização da comunidade.

---

## Problema Abordado e Justificativa

Atualmente, pequenos empreendimentos enfrentam baixa visibilidade e dificuldade de se conectar com o público local, especialmente quando não possuem presença digital. Isso limita o alcance desses negócios e reduz o potencial de consumo dentro da própria comunidade.

O ConectaBairro busca resolver esse problema oferecendo uma plataforma acessível, que centralize informações relevantes sobre serviços e produtos disponíveis nos bairros. Ao facilitar essa conexão, o sistema contribui para o fortalecimento da economia local, reduz deslocamentos desnecessários e promove inclusão digital.

---

## Conexão com o ODS 11
O projeto ConectaBairro contribui diretamente para o Objetivo de Desenvolvimento Sustentável 11 — Cidades e Comunidades Sustentáveis — ao promover a valorização da economia local, facilitar o acesso a serviços e produtos no próprio bairro e incentivar a interação entre moradores e empreendedores. A plataforma fortalece a resiliência econômica das comunidades e estimula práticas de consumo mais conscientes e sustentáveis.

---

## Objetivos do Sistema

Objetivo Geral: Desenvolver uma aplicação multiplataforma que permita o cadastro, consulta e divulgação de empreendimentos e iniciativas locais por região.

Objetivos Específicos:

- Criar uma API RESTful para gerenciamento de usuários e empreendimentos

- Implementar autenticação segura via JWT

- Integrar com serviços externos: ViaCEP e OpenWeather

- Disponibilizar filtros de busca por localização e palavras-chave

- Planejar interfaces para web e dispositivos móveis

- Garantir estrutura de testes automatizados desde o início

---

## Escopo do Projeto

O escopo do ConectaBairro abrange o desenvolvimento de uma aplicação multiplataforma composta por backend (API RESTful em Node.js/Express), banco de dados NoSQL (MongoDB), integração com serviços externos (ViaCEP e OpenWeather), e frontend web/mobile responsivo.  
O sistema permitirá o cadastro, consulta, edição e exclusão de empreendimentos locais, autenticação de usuários via JWT, listagem e busca com filtros, além da exibição de informações climáticas por cidade.  
Estão fora do escopo, nesta etapa, funcionalidades de marketplace, pagamentos online ou gestão financeira dos empreendimentos.

---

## Visão Geral da Arquitetura (com diagrama)

Arquitetura prevista:

- Comunicação via protocolo HTTP

- Autenticação baseada em JWT

- Banco de dados NoSQL com Mongoose

- Integrações externas para enriquecimento de dados

---

## Tecnologias Propostas

- Node.js — ambiente de execução backend

- Express.js — framework para rotas e middlewares

- MongoDB + Mongoose — banco de dados NoSQL

- JWT — autenticação segura

- Jest + Supertest — testes automatizados

- Dotenv — gerenciamento de variáveis de ambiente

- ViaCEP API — consulta de endereço por CEP

- OpenWeather API — consulta de clima por cidade

---

## Cronograma para Etapa 2 (Implementação do Projeto)

A Etapa 2 será dedicada à implementação prática do projeto ConectaBairro, contemplando o desenvolvimento do backend e frontend da aplicação. O cronograma abaixo distribui as atividades por semana, considerando a complexidade técnica e a colaboração entre os integrantes da equipe:

| Semana | Atividades                                                                 |
|--------|-----------------------------------------------------------------------------|
| 1      | Configuração inicial do repositório, estrutura de pastas e variáveis de ambiente |
| 2      | Desenvolvimento do backend: rotas, controllers, models, serviços e autenticação |
| 3      | Implementação dos testes automatizados e integração com APIs externas (ViaCEP e OpenWeather) |
| 4      | Início do frontend: estruturação das páginas com HTML e CSS responsivo     |
| 5      | Adição de interatividade com JavaScript e integração com a API             |
| 6      | Validação técnica, ajustes finais, documentação complementar e entrega do projeto |

## Integrantes da Equipe e Seus Papéis
O projeto será desenvolvido por uma equipe de seis integrantes, com divisão clara de responsabilidades desde o planejamento. Cada membro atuará em áreas específicas do backend e frontend, garantindo organização, rastreabilidade e colaboração eficiente.

### Elayne Nascimento Lima

**Função:** Líder Técnica e Desenvolvedora Principal 

**Responsabilidades Planejadas:**

- Definição da arquitetura da API e estrutura de pastas

- Implementação das rotas de empreendimentos (controller, model, validações)

- Criação do middleware de autenticação com JWT

- Desenvolvimento do serviço de integração com a API ViaCEP

- Estruturação dos arquivos principais do servidor (server.js, app.js, utils.js)

- Organização da documentação técnica e do README

- Apoio na estruturação do frontend (HTML base e organização das seções)

### Gilssilany Valentino Chaves
**Função:** Autenticação e Segurança

**Responsabilidades Planejadas:**

- Implementação do controller de usuários (cadastro e login)

- Configuração da conexão com o banco de dados MongoDB

- Validação de tokens JWT e proteção de rotas

- Apoio na criação da página de login no frontend

### Igor Marcelo de Sousa Freire

**Função:** Integração com Serviços Externos

**Responsabilidades Planejadas:**

- Desenvolvimento dos serviços de clima e CEP (OpenWeather e ViaCEP)

- Implementação dos controllers e rotas externas

- Apoio na exibição de dados climáticos no frontend

### Francisco Eudes Rodrigues da Silva

**Função:** Documentação Técnica e Estrutura de Rotas 

**Responsabilidades Planejadas:**

- Redação da documentação técnica da arquitetura da API

- Organização das rotas de usuários e autenticação

- Apoio na estruturação das páginas de cadastro e navegação no frontend

### Marcus Vinicius Monteiro da Silva Costa

**Função:** Modelagem de Dados e Validações

**Responsabilidades Planejadas:**

- Definição dos schemas de usuário e empreendimento

- Implementação das regras de validação e criptografia de senha

- Sugestões de tratamento de erros e mensagens no backend

- Apoio na validação de formulários no frontend (JavaScript)

### Aluísio Rodrigues Júnior

**Função:** Testes e Validação Técnica

**Responsabilidades Planejadas:**

- Estruturação dos testes automatizados com Jest e Supertest

- Testes manuais das rotas públicas e protegidas

- Validação das respostas da API e integração com o frontend

- Apoio na criação de scripts de teste e simulação de uso.

---

## Documentos Complementares

- [Requisitos do Sistema](./docs/requirements/requirements.md)
- [Arquitetura do Sistema](./docs/architecture/architecture.md)
- [Modelo de Dados](./docs/database/database_model.md)
- [Especificação da API](./docs/api/api_specification.md)
- [Protótipos Web](./prototypes/web)
- [Protótipos Mobile](./prototypes/mobile)
