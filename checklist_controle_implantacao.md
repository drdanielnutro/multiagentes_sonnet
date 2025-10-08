# Checklist de Controle – Sistema Multi-Subagente Claude Sonnet 4.5

> Use este checklist para acompanhar a implementação do tutorial `docs/deep_research_claude.md` (seções 3–6.5), marcando o que já foi colocado em prática.

## 1. Preparação do Ambiente
- [ ] Claude Code CLI instalada (`docs/deep_research_claude.md:69`).
- [ ] Autenticação concluída com `claude-code auth login` (`docs/deep_research_claude.md:75`).
- [ ] Versão da CLI verificada com `claude-code --version` (`docs/deep_research_claude.md:78`).

## 2. Estrutura do Projeto
- [ ] Diretórios `.claude/agents`, `.claude/state`, `.claude/plans`, `.claude/results` criados (`docs/deep_research_claude.md:82-92`).
- [ ] Repositório Git inicializado e `.claude/state/` registrado no `.gitignore` (`docs/deep_research_claude.md:93-95`).

## 3. Configuração Global `.claude/CLAUDE.md`
- [ ] Arquitetura hub-and-spoke documentada com 4 subagentes e limite de 3 iterações (`docs/deep_research_claude.md:101-108`).
- [ ] Regras do orquestrador registradas (ultrathink, contexto essencial, atualização de `task-status.json`, leitura via arquivos) (`docs/deep_research_claude.md:109-113`).
- [ ] Regras globais dos subagentes incluídas (locks, outputs em `.claude/results/`, reporte estruturado) (`docs/deep_research_claude.md:115-119`).
- [ ] Formato padrão de output JSON incorporado (`docs/deep_research_claude.md:121-129`).
- [ ] Política de gestão de arquivos (.claude/plans, .claude/results, .claude/state) adicionada (`docs/deep_research_claude.md:132-135`).

## 4. Orquestrador Principal
- [ ] Identidade, modelo e escopo documentados (`docs/deep_research_claude.md:145-158`).
- [ ] Fluxo da Fase 1 (Checklist) implementado com criação de brief e consumo de `.claude/results/checklist-output.json` (`docs/deep_research_claude.md:162-168`).
- [ ] Fluxo da Fase 2 (Writer) implementado com briefing e leitura de `writer-output.json` (`docs/deep_research_claude.md:170-176`).
- [ ] Fluxo da Fase 3 (Reviewer) com veredictos e caminhos de decisão configurados (`docs/deep_research_claude.md:178-187`).
- [ ] Fluxo da Fase 4 (Fixer) com controle de iterações e retorno à revisão preparado (`docs/deep_research_claude.md:189-195`).
- [ ] Diretrizes de gestão de contexto aplicadas (manter ledger, resumir decisões, evitar raciocínio bruto) (`docs/deep_research_claude.md:198-201`).
- [ ] Critérios de decisão (aprovar, iterar, escalar) formalizados (`docs/deep_research_claude.md:204-206`).
- [ ] Modelos de comunicação com o usuário (execução, sucesso, escalação) integrados (`docs/deep_research_claude.md:208-231`).
- [ ] Protocolos de erro configurados (retries, conflitos, timeouts, loops divergentes) (`docs/deep_research_claude.md:233-237`).
- [ ] Política de uso de extended thinking cadastrada (`docs/deep_research_claude.md:239-246`).

## 5. Subagente Checklist
- [ ] Frontmatter e definição do agente criados (`docs/deep_research_claude.md:255-259`).
- [ ] Responsabilidades e limites documentados (`docs/deep_research_claude.md:266-270`).
- [ ] Etapa de compreensão da tarefa implementada (`docs/deep_research_claude.md:274-278`).
- [ ] Checklist de completude para features e bugfixes adotado (`docs/deep_research_claude.md:281-294`).
- [ ] Sistema de scoring (clareza, completude, viabilidade, complexidade) aplicado (`docs/deep_research_claude.md:295-300`).
- [ ] Regras de veredito (complete, needs_clarification, incomplete) implementadas (`docs/deep_research_claude.md:301-306`).
- [ ] Inputs/outputs padronizados (`checklist-brief.json`, `checklist-output.json`) definidos (`docs/deep_research_claude.md:307-336`).
- [ ] Regras de reporte (gaps específicos, evidências, perguntas fechadas) ativas (`docs/deep_research_claude.md:339-344`).

## 6. Subagente Escritor
- [ ] Frontmatter configurado com ferramentas e modelo corretos (`docs/deep_research_claude.md:352-355`).
- [ ] Responsabilidades e restrições registradas (`docs/deep_research_claude.md:360-369`).
- [ ] Processo de preparação seguido (brief, arquivos, locks, planejamento) (`docs/deep_research_claude.md:373-378`).
- [ ] Processo de implementação alinhado (requisitos, erros, logging, clean code) (`docs/deep_research_claude.md:379-385`).
- [ ] Processo de testes estabelecido (unit tests, coverage ≥80%, casos variados) (`docs/deep_research_claude.md:386-391`).
- [ ] Auto-validação obrigatória antes de entregar (linter, type checker, testes, build) (`docs/deep_research_claude.md:392-397`).
- [ ] Padrões de qualidade adotados (funções curtas, nomes descritivos, DRY, type safety) (`docs/deep_research_claude.md:398-404`).
- [ ] Output JSON do writer configurado (mudanças, testes, validações, self-assessment) (`docs/deep_research_claude.md:405-444`).
- [ ] Checklist pré-submissão aplicado (`docs/deep_research_claude.md:446-454`).
- [ ] Regras finais respeitadas (ler análise antes, validar, commits atômicos, sem scope creep) (`docs/deep_research_claude.md:455-461`).

## 7. Subagente Revisor
- [ ] Frontmatter do reviewer definido (`docs/deep_research_claude.md:469-473`).
- [ ] Responsabilidades e escopo de decisão estabelecidos (`docs/deep_research_claude.md:480-486`).
- [ ] Preparação do review implementada (brief, outputs, arquivos) (`docs/deep_research_claude.md:490-494`).
- [ ] Checklist estruturado de revisão adotado (completude, corretude, segurança, qualidade, testes) (`docs/deep_research_claude.md:495-526`).
- [ ] Matriz de severidade (critical/high/medium/low) utilizada (`docs/deep_research_claude.md:527-533`).
- [ ] Regras de decisão e critérios de aprovação configurados (`docs/deep_research_claude.md:534-542`).
- [ ] Input/output padronizados (`review-brief.json`, `reviewer-output.json`) implementados (`docs/deep_research_claude.md:543-595`).
- [ ] Técnicas de review e protocolos de erro aplicados (`docs/deep_research_claude.md:596-606`).
- [ ] Regras finais em vigor (recomendações específicas, citar código, não aprovar com críticos) (`docs/deep_research_claude.md:607-613`).

## 8. Subagente Corretor
- [ ] Frontmatter e responsabilidades do fixer registrados (`docs/deep_research_claude.md:621-637`).
- [ ] Processo completo implementado (análise, priorização, correção cirúrgica, validação) (`docs/deep_research_claude.md:641-688`).
- [ ] Estrutura de input (`fixer-brief.json`) configurada (`docs/deep_research_claude.md:689-702`).
- [ ] Output JSON do fixer detalhando fixes, validações e próximos passos adotado (`docs/deep_research_claude.md:703-800`).
- [ ] Diretrizes de correção e exemplos aplicados (security, logic, quality) (`docs/deep_research_claude.md:803-845`).
- [ ] Técnicas cirúrgicas, rollback e protocolos de erro incorporados (`docs/deep_research_claude.md:847-914`).
- [ ] Estratégia de time budget e checklist de qualidade seguidas (`docs/deep_research_claude.md:923-959`).
- [ ] Métricas de sucesso monitoradas (CRITICAL/HIGH resolvidos) (`docs/deep_research_claude.md:961-983`).

## 9. Fluxo de Trabalho Compartilhado
- [ ] Sequência hub-and-spoke mapeada conforme diagrama Mermaid (`docs/deep_research_claude.md:991-1007`).
- [ ] Árvores de decisão do checklist, reviewer e iterações implementadas (`docs/deep_research_claude.md:1009-1042`).
- [ ] Estrutura de estado compartilhado (`task-status.json`) adotada com fases e métricas (`docs/deep_research_claude.md:1045-1112`).
- [ ] Artefatos de comunicação entre agentes (.claude/plans e .claude/results) padronizados (`docs/deep_research_claude.md:1115-1240`).

## 10. Operação, Troubleshooting e Contexto
- [ ] Prompts dos agentes ajustados para garantir invocação correta (`docs/deep_research_claude.md:1248-1267`).
- [ ] Estratégia de escalação após 3 iterações documentada e automatizada (`docs/deep_research_claude.md:1271-1286`).
- [ ] Gestão de file locks implementada (`docs/deep_research_claude.md:1290-1315`).
- [ ] Rotina de compactação de contexto configurada (`docs/deep_research_claude.md:1319-1343`).
- [ ] Procedimento de rollback em regressões do fixer aplicado (`docs/deep_research_claude.md:1348-1369`).
- [ ] Políticas de uso de ultrathink/think/think hard seguidas (`docs/deep_research_claude.md:1373-1405`).
- [ ] Otimizações específicas do Sonnet 4.5 (context awareness, paralelismo, caching) ativadas (`docs/deep_research_claude.md:1409-1449`).
- [ ] Melhores práticas por fase (Checklist, Writer, Reviewer, Fixer, Orquestrador) adotadas (`docs/deep_research_claude.md:1453-1484`).

## 11. Qualidade e Métricas
- [ ] Checklist de QA final aplicado antes de concluir tarefas (`docs/deep_research_claude.md:1487-1504`).
- [ ] Monitoramento contínuo de métricas (aprovação 1ª iteração, iterações ≤3, escalonamentos ≤10%, cobertura ≥80%) ativo (`docs/deep_research_claude.md:1507-1526`).
