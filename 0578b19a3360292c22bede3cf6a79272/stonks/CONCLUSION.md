# Stonks — Conclusão e retrospectiva

## Resumo

O laboratório Stonks proporcionou a prática de uma investigação que partiu do reconhecimento de uma aplicação web e avançou pela enumeração de serviços internos, análise de API, validação de vulnerabilidades e investigação pós-exploração.

## O que a máquina demonstrou

A principal lição foi a importância de analisar o comportamento da aplicação e seguir as evidências. Uma funcionalidade aparentemente comum pode revelar interações com outros serviços, e essas interações podem ampliar o impacto de uma falha quando existem controles insuficientes.

O laboratório também reforçou a importância de compreender o contexto de execução, as permissões do usuário e os riscos de credenciais armazenadas localmente.

## Retrospectiva técnica

- **Ponto forte:** encadear etapas de enumeração e investigação em vez de depender de uma única ferramenta.
- **Aprendizado central:** validar hipóteses com evidências e compreender como cada vulnerabilidade contribui para o impacto final.
- **Oportunidade de melhoria:** aprofundar a análise das causas-raiz, das permissões Linux e das medidas de mitigação.
- **Próximo passo:** aplicar a mesma metodologia em outras máquinas, adaptando as técnicas à arquitetura e às evidências encontradas.

## Conclusão

Stonks reforçou uma abordagem metódica de segurança ofensiva: reconhecer, enumerar, formular hipóteses, validar, avaliar impacto e documentar.

O objetivo não é apenas concluir um desafio, mas compreender por que cada falha ocorre, quais condições permitem sua exploração e como o problema pode ser corrigido.

Este documento descreve aprendizados obtidos em um laboratório controlado. As técnicas devem ser aplicadas somente em ambientes autorizados.
