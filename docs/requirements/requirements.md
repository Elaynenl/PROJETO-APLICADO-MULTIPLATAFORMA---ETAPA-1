# Documento de Requisitos do Sistema ConectaBairro

Este documento apresenta os requisitos planejados para o sistema **ConectaBairro**.  
O objetivo é detalhar os **requisitos funcionais**, **não-funcionais**, **regras de negócio**, além de **histórias de usuário** e **perfis de usuários** que orientarão o desenvolvimento da aplicação.  
A especificação foi elaborada para garantir clareza, rastreabilidade e alinhamento com os objetivos do projeto.

---

## Sumário

- [Requisitos Funcionais](#requisitos-funcionais)
- [Requisitos Não-Funcionais](#requisitos-não-funcionais)
- [Regras de Negócio](#regras-de-negócio)
- [Histórias de usuário ou casos de uso](#histórias-de-usuário-ou-casos-de-uso)
- [Perfis de usuários](#perfis-de-usuários)

---

## Requisitos Funcionais

Os requisitos funcionais descrevem o comportamento esperado do sistema e suas funcionalidades principais.

- **RF01**: O sistema deve permitir o cadastro de usuários com nome, email e senha.  
- **RF02**: O sistema deve validar a unicidade do email no momento do cadastro.  
- **RF03**: O sistema deve permitir o login de usuários e retornar um token JWT.  
- **RF04**: O sistema deve proteger rotas sensíveis, exigindo autenticação via token JWT.  
- **RF05**: O sistema deve verificar se o usuário autenticado é o criador do empreendimento antes de permitir edição ou exclusão.  
- **RF06**: O sistema deve permitir o cadastro de empreendimentos com nome, descrição, endereço, telefone, email e palavras-chave.  
- **RF07**: O sistema deve integrar-se à API ViaCEP para preencher automaticamente os campos de endereço com base no CEP informado.  
- **RF08**: O sistema deve normalizar os campos `cidade`, `bairro` e `palavrasChave` para facilitar buscas.  
- **RF09**: O sistema deve permitir a edição parcial de qualquer campo do empreendimento.  
- **RF10**: Ao editar o CEP, o sistema deve atualizar automaticamente os dados de endereço via API ViaCEP.  
- **RF11**: O sistema deve validar os campos obrigatórios durante a edição.  
- **RF12**: O sistema deve permitir a listagem de todos os empreendimentos cadastrados.  
- **RF13**: O sistema deve permitir a busca por empreendimentos usando filtros como rua, bairro, cidade, estado, CEP ou palavras-chave.  
- **RF14**: O sistema deve agrupar os empreendimentos por cidade e retornar os dados climáticos da cidade via API OpenWeatherMap.  
- **RF15**: O sistema deve permitir que o criador de um empreendimento o exclua permanentemente.
<br>

## Requisitos Não-Funcionais

Os requisitos não funcionais definem critérios de qualidade, desempenho, segurança e arquitetura.

### Segurança

- **RNF01**: As senhas dos usuários devem ser armazenadas de forma criptografada usando bcrypt.  
- **RNF02**: O sistema deve utilizar JWT para autenticação segura e stateless.  
- **RNF03**: O sistema deve validar o token JWT em todas as rotas protegidas.  

### Usabilidade

- **RNF04**: As mensagens de erro devem ser claras e explicativas, especialmente em casos de validação.  
- **RNF05**: As respostas da API devem seguir um padrão consistente, com mensagens e dados agrupados.  

### Manutenibilidade

- **RNF06**: O sistema deve seguir a arquitetura MVC para facilitar manutenção e escalabilidade.  
- **RNF07**: O código deve estar modularizado em controllers, models, routes, services e middlewares.  

### Testabilidade

- **RNF08**: O sistema deve possuir testes automatizados cobrindo o fluxo completo de autenticação e CRUD de empreendimentos.  
- **RNF09**: Os testes devem ser executados em banco de dados em memória (MongoMemoryServer) para garantir isolamento.  

---

## Regras de Negócio

As regras de negócio definem os comportamentos esperados e restrições que garantem a integridade e coerência do sistema.

- Um usuário só pode editar ou excluir empreendimentos que ele mesmo cadastrou.

- O campo de email deve ser único para cada usuário.

- O campo CEP deve ser validado e, quando possível, preenchido automaticamente via API ViaCEP.

- O sistema deve normalizar os campos cidade, bairro e palavrasChave para facilitar buscas.

- A autenticação via JWT é obrigatória para qualquer operação de cadastro, edição ou exclusão.

- Empreendimentos devem conter todos os campos obrigatórios para serem salvos ou atualizados.

- A exclusão de empreendimentos é permanente e só pode ser realizada pelo criador.

- A listagem de empreendimentos deve permitir filtros por localização e palavras-chave.

- O clima exibido deve corresponder à cidade do empreendimento, via integração com OpenWeatherMap.

- O sistema deve impedir que usuários não autenticados acessem rotas protegidas.

---

## Histórias de usuário ou casos de uso

As histórias de usuário representam situações reais de uso da plataforma, com foco nos objetivos e necessidades dos usuários.

### Morador

Como morador, quero buscar empreendimentos no meu bairro para encontrar serviços próximos sem precisar me deslocar para outras regiões.

### Empreendedor

Como empreendedor, quero cadastrar meu negócio na plataforma para divulgar meus produtos e serviços aos moradores da região.

### Usuário Autenticado

Como usuário autenticado, quero editar ou excluir meus empreendimentos para manter as informações sempre atualizadas.

### Usuário Curioso

Como usuário, quero visualizar o clima atual da cidade para decidir se saio para buscar um serviço presencial ou opto por contato remoto.

### Usuário Mobile

Como usuário em dispositivo móvel, quero acessar a plataforma com uma interface responsiva e intuitiva para consultar empreendimentos com facilidade.

---

## Perfis de usuários

A plataforma ConectaBairro prevê três perfis principais de usuários, cada um com permissões específicas:

### Morador

- Acesso público à listagem de empreendimentos

- Busca por localização ou palavras-chave

- Visualização de clima por cidade

- Não pode cadastrar, editar ou excluir empreendimentos

### Empreendedor

- Cadastro e autenticação via email e senha

- Criação, edição e exclusão de empreendimentos próprios

- Visualização de clima e endereço via APIs externas

- Proteção de dados via autenticação JWT

### Administrador (futuro)

- Acesso a todos os empreendimentos

- Gerenciamento de usuários e conteúdo

- Funções administrativas (a definir na Etapa 2)

---