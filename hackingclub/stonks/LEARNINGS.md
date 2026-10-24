# Stonks — Aprendizados e habilidades

## Visão geral

A máquina Stonks permitiu praticar uma cadeia de investigação que começou na aplicação web e avançou para serviços internos, execução de comandos e análise pós-exploração em um ambiente controlado.

## Principais aprendizados

- Reconhecer funcionalidades e mapear a superfície de ataque de uma aplicação web.
- Identificar rotas e recursos por meio de fuzzing.
- Interceptar e analisar requisições e respostas HTTP.
- Compreender o risco de SSRF e sua utilização para investigar serviços internos.
- Consultar documentação Swagger para entender endpoints e parâmetros de uma API.
- Investigar possíveis falhas de command injection em funcionalidades que interagem com o sistema operacional.
- Compreender a importância de analisar permissões, arquivos acessíveis e informações disponíveis após o acesso inicial.
- Reconhecer os riscos associados a credenciais armazenadas em perfis de aplicações.
- Relacionar vulnerabilidades individuais para compreender o impacto de uma cadeia de exploração.

## Habilidades e ferramentas praticadas

| Área | Habilidade ou ferramenta |
|---|---|
| Descoberta de conteúdo | ffuf e wordlists |
| Análise HTTP | Burp Suite |
| Enumeração interna | Testes controlados de SSRF |
| Análise de API | Swagger e JSON |
| Validação de vulnerabilidades | Investigação de command injection |
| Linux | Navegação pelo sistema de arquivos e análise de permissões |
| Pós-exploração | Investigação de perfis e credenciais locais |
| Documentação | Registro de evidências e organização do write-up |

## Pontos para aprofundar

- Diferenciar uma evidência de vulnerabilidade de uma hipótese ainda não confirmada.
- Entender as causas-raiz de SSRF e command injection e suas respectivas mitigações.
- Aprofundar conhecimentos sobre permissões Linux, gerenciamento de credenciais e escalada de privilégios.
- Praticar a produção de evidências claras e reproduzíveis.
- Relacionar cada etapa da exploração ao risco de segurança correspondente.

## Resultado do aprendizado

O principal aprendizado foi entender como uma investigação estruturada pode conectar diferentes superfícies e vulnerabilidades. A enumeração deve orientar os próximos testes, e cada avanço precisa ser sustentado por evidências observáveis.
