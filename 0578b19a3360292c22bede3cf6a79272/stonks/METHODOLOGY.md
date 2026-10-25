# Metodologia — Roadmap de CTF e segurança ofensiva

## Objetivo

Documentar uma abordagem adaptável para investigar aplicações e sistemas em laboratórios controlados e avaliações com autorização explícita.

## Fase 1 — Reconhecimento

- Identificar os serviços e as superfícies disponíveis.
- Fazer fingerprint das tecnologias quando possível.
- Registrar observações iniciais e delimitar o escopo.

**Resultado esperado:** mapa inicial da superfície de ataque.

## Fase 2 — Enumeração

- Mapear funcionalidades, rotas, parâmetros e áreas autenticadas.
- Procurar documentação, arquivos e endpoints expostos.
- Usar ferramentas de descoberta de conteúdo de forma orientada por hipóteses.
- Registrar respostas relevantes e comportamentos inesperados.

**Resultado esperado:** inventário de recursos e possíveis pontos de investigação.

## Fase 3 — Análise de entradas e controles

- Interceptar requisições e compreender o fluxo de dados.
- Identificar entradas controladas pelo usuário.
- Examinar autenticação, autorização e validação de entradas.
- Comparar o comportamento normal com resultados de testes controlados.

**Resultado esperado:** hipóteses de vulnerabilidade priorizadas por evidência e impacto potencial.

## Fase 4 — Investigação e validação

- Formular uma hipótese específica para cada comportamento suspeito.
- Escolher testes proporcionais e adequados ao ambiente.
- Confirmar ou descartar cada hipótese com evidências.
- Investigar serviços internos ou APIs quando houver indícios técnicos que justifiquem essa linha de análise.
- Documentar pré-condições, resultado observado e limitações.

**Resultado esperado:** vulnerabilidades confirmadas ou hipóteses claramente identificadas como inconclusivas.

## Fase 5 — Avaliação de impacto

- Determinar o acesso efetivamente obtido.
- Verificar a identidade e as permissões associadas.
- Avaliar exposição de dados, acesso a arquivos e possíveis caminhos adicionais.
- Investigar escalada de privilégios somente quando houver evidências e dentro do escopo autorizado.
- Evitar alterações desnecessárias no sistema.

**Resultado esperado:** impacto demonstrado sem extrapolar as permissões do laboratório ou da autorização.

## Fase 6 — Evidências e documentação

- Registrar requisições, respostas, mensagens de erro e resultados relevantes.
- Organizar capturas de tela na sequência em que são citadas.
- Explicar o raciocínio por trás de cada etapa.
- Separar fatos observados de inferências.
- Remover credenciais, tokens e outros segredos antes da publicação.

**Resultado esperado:** documentação clara, reproduzível e segura para publicação.

## Fase 7 — Mitigação e retrospectiva

- Identificar a causa-raiz de cada vulnerabilidade.
- Recomendar medidas preventivas e corretivas.
- Registrar o que funcionou, o que não funcionou e quais conhecimentos precisam ser aprofundados.
- Atualizar o roadmap com lições que possam ser reutilizadas em outros alvos.

**Resultado esperado:** aprendizado transferível para futuras avaliações.

## Princípio de adaptação

A sequência acima é uma referência, não uma receita obrigatória. A arquitetura, a tecnologia, o escopo e as evidências do alvo determinam quais fases são relevantes e em que ordem devem ser executadas.

Todas as atividades devem permanecer restritas a ambientes controlados ou sistemas com autorização explícita.
