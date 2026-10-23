LogiTech Express — planejamento do back-end

Objetivo e escopo

Este repositório prepara o terreno para a próxima Unidade Curricular. Contém documentação, contratos HTTP, modelo de dados e SQL inicial.
Diagnóstico

Motoristas duplicados indicam ausência de identificador único e validações de integridade.
Itens de frota armazenados em texto com vírgulas impedem busca, estoque e auditoria confiáveis.
Rotas, regras e persistência misturadas dificultam manutenção e causam respostas inconsistentes.
Segredos no código expõem banco e integrações.

Estrutura planejada

text
backend/
  login/              Descrição do contrato HTTP de autenticação
  cadastro/           Descrição das rotas de motoristas
  estoque/            Descrição das rotas de itens e movimentações
  rotas/              Catálogo detalhado dos endpoints HTTP
  arquitetura.md      Responsabilidades das camadas MVC + Repository
database/
  DER.md              Diagrama lógico e decisões de normalização
  schema.sql          Estrutura relacional inicial (PostgreSQL)
TESTS.md              Cenários para implementar na próxima UC
.env.example          Nomes de variáveis, sem credenciais reais
.gitignore            Ignora arquivos locais e segredos


Arquitetura sugerida

Separar as responsabilidades em Router → Controller → Service → Repository → Banco de Dados. O Controller trata HTTP e delega; o Service concentra regras de negócio; o Repository concentra persistência. Respostas e erros seguem um contrato JSON uniforme. Veja [backend/arquitetura.md](backend/arquitetura.md).

Banco de dados

O modelo separa motoristas, frotas, itens, associação de itens à frota, usuários de acesso e coletas. A associação `frota_itens` permite vários itens por frota e várias frotas por item sem listas em texto. O documento do motorista e o e-mail de acesso têm restrições de unicidade. Veja [database/DER.md](database/DER.md) e [database/schema.sql](database/schema.sql).

Segurança

Copiar `.env.example` para `.env` no ambiente local e preencher os valores fora do repositório. Nunca commitar `.env`, tokens ou senhas. O arquivo `.gitignore` já ignora `.env`.

Roadmap da próxima UC

1. Implementar a API e validações de entrada conforme o catálogo HTTP.
2. Implementar persistência com as tabelas e restrições do `schema.sql`.
3. Implementar autenticação e autorização das rotas protegidas.
4. Implementar os cenários documentados em `TESTS.md` (unitários, integração e contrato).
5. Revisar logs, mensagens de erro, paginação, segurança e documentação de execução.

Entrega

O projeto está preparado como base documental para o repositório do grupo.