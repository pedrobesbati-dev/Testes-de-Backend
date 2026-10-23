Arquitetura planejada

Organização lógica

backend/
  rotas/       Declara métodos/caminhos HTTP e aponta para controllers
  controllers/ Recebe req/res, valida formato HTTP e chama services
  services/    Regras de negócio e coordenação de operações
  repositories/Consultas e persistência no banco
  models/      Entidades/representações dos dados
  middlewares/ Autenticação, autorização, validação e tratamento de erros
  config/      Configuração carregada de variáveis de ambiente(.env)

Acima está a estrutura de pastas de como irá ficar quando iniciarmos a codificação

Caminho de uma requisição

Router → Middleware → Controller → Service → Repository → Banco

Router: associa método e caminho ao controller; não consulta o banco nem decide regras de negócio.
Middleware: trata autenticação, autorização e validações transversais.
Controller (MVC): traduz HTTP para chamada do serviço e transforma o resultado em status e JSON.
Service: aplica regras, por exemplo unicidade do documento e transição válida de status.
Repository: concentra SQL e operações de persistência; o Service não escreve SQL.
Model: representa entidades e relações do domínio.
Tratamento central de erros: padroniza respostas e evita enviar detalhes internos ao cliente.

Decisões de qualidade

Prefixo versionado /api/v1, JSON e códigos HTTP coerentes.
Paginação nas listagens para evitar respostas excessivas.
Restrições no banco (chaves, `NOT NULL`, `UNIQUE`, `CHECK`) complementam validações da API.
Log técnico com identificador de requisição; resposta pública sem stack trace, credenciais ou dados sensíveis.
Segredos lidos do ambiente; `.env` local nunca entra no Git.
