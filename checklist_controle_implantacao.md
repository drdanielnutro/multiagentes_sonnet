# Checklist de Controle – Sistema Multi-Subagente Claude Sonnet 4.5

> Use este checklist para acompanhar a implementação do tutorial `docs/deep_research_claude.md` (seções 3–6.5), marcando o que já foi colocado em prática.
>
> **Nota:** As etapas da seção 1 foram documentadas no repositório como referência operacional; execute os comandos correspondentes no ambiente desejado antes do uso em produção.

## 1. Preparação do Ambiente
- [x] Claude Code CLI instalada (`docs/deep_research_claude.md:69`).
- [x] Autenticação concluída com `claude-code auth login` (`docs/deep_research_claude.md:75`).
- [x] Versão da CLI verificada com `claude-code --version` (`docs/deep_research_claude.md:78`).

## 2. Estrutura do Projeto
- [x] Diretórios `.claude/agents`, `.claude/state`, `.claude/plans`, `.claude/results` criados (`docs/deep_research_claude.md:82-92`).
- [x] Repositório Git inicializado e `.claude/state/` registrado no `.gitignore` (`docs/deep_research_claude.md:93-95`).

## 3. Configuração Global `.claude/CLAUDE.md`
- [x] Arquitetura hub-and-spoke documentada com 4 subagentes e limite de 3 iterações (`docs/deep_research_claude.md:101-108`).
- [x] Regras do orquestrador registradas (ultrathink, contexto essencial, atualização de `task-status.json`, leitura via arquivos) (`docs/deep_research_claude.md:109-113`).
- [x] Regras globais dos subagentes incluídas (locks, outputs em `.claude/results/`, reporte estruturado) (`docs/deep_research_claude.md:115-119`).
- [x] Formato padrão de output JSON incorporado (`docs/deep_research_claude.md:121-129`).
- [x] Política de gestão de arquivos (.claude/plans, .claude/results, .claude/state) adicionada (`docs/deep_research_claude.md:132-135`).

## 4. Orquestrador Principal
- [x] Identidade, modelo e escopo documentados (`docs/deep_research_claude.md:145-158`).
- [x] Fluxo da Fase 1 (Checklist) implementado com criação de brief e consumo de `.claude/results/checklist-output.json` (`docs/deep_research_claude.md:162-168`).
- [x] Fluxo da Fase 2 (Writer) implementado com briefing e leitura de `writer-output.json` (`docs/deep_research_claude.md:170-176`).
- [x] Fluxo da Fase 3 (Reviewer) com veredictos e caminhos de decisão configurados (`docs/deep_research_claude.md:178-187`).
- [x] Fluxo da Fase 4 (Fixer) com controle de iterações e retorno à revisão preparado (`docs/deep_research_claude.md:189-195`).
- [x] Diretrizes de gestão de contexto aplicadas (manter ledger, resumir decisões, evitar raciocínio bruto) (`docs/deep_research_claude.md:198-201`).
- [x] Critérios de decisão (aprovar, iterar, escalar) formalizados (`docs/deep_research_claude.md:204-206`).
- [x] Modelos de comunicação com o usuário (execução, sucesso, escalação) integrados (`docs/deep_research_claude.md:208-231`).
- [x] Protocolos de erro configurados (retries, conflitos, timeouts, loops divergentes) (`docs/deep_research_claude.md:233-237`).
- [x] Política de uso de extended thinking cadastrada (`docs/deep_research_claude.md:239-246`).

## 5. Subagente Checklist
- [x] Frontmatter e definição do agente criados (`docs/deep_research_claude.md:255-259`).
- [x] Responsabilidades e limites documentados (`docs/deep_research_claude.md:266-270`).
- [x] Etapa de compreensão da tarefa implementada (`docs/deep_research_claude.md:274-278`).
- [x] Checklist de completude para features e bugfixes adotado (`docs/deep_research_claude.md:281-294`).
- [x] Sistema de scoring (clareza, completude, viabilidade, complexidade) aplicado (`docs/deep_research_claude.md:295-300`).
- [x] Regras de veredito (complete, needs_clarification, incomplete) implementadas (`docs/deep_research_claude.md:301-306`).
- [x] Inputs/outputs padronizados (`checklist-brief.json`, `checklist-output.json`) definidos (`docs/deep_research_claude.md:307-336`).
- [x] Regras de reporte (gaps específicos, evidências, perguntas fechadas) ativas (`docs/deep_research_claude.md:339-344`).

## 6. Subagente Escritor
- [x] Frontmatter configurado com ferramentas e modelo corretos (`docs/deep_research_claude.md:352-355`).
- [x] Responsabilidades e restrições registradas (`docs/deep_research_claude.md:360-369`).
- [x] Processo de preparação seguido (brief, arquivos, locks, planejamento) (`docs/deep_research_claude.md:373-378`).
- [x] Processo de implementação alinhado (requisitos, erros, logging, clean code) (`docs/deep_research_claude.md:379-385`).
- [x] Processo de testes estabelecido (unit tests, coverage ≥80%, casos variados) (`docs/deep_research_claude.md:386-391`).
- [x] Auto-validação obrigatória antes de entregar (linter, type checker, testes, build) (`docs/deep_research_claude.md:392-397`).
- [x] Padrões de qualidade adotados (funções curtas, nomes descritivos, DRY, type safety) (`docs/deep_research_claude.md:398-404`).
- [x] Output JSON do writer configurado (mudanças, testes, validações, self-assessment) (`docs/deep_research_claude.md:405-444`).
- [x] Checklist pré-submissão aplicado (`docs/deep_research_claude.md:446-454`).
- [x] Regras finais respeitadas (ler análise antes, validar, commits atômicos, sem scope creep) (`docs/deep_research_claude.md:455-461`).

## 7. Subagente Revisor
- [x] Frontmatter do reviewer definido (`docs/deep_research_claude.md:469-473`).
- [x] Responsabilidades e escopo de decisão estabelecidos (`docs/deep_research_claude.md:480-486`).
- [x] Preparação do review implementada (brief, outputs, arquivos) (`docs/deep_research_claude.md:490-494`).
- [x] Checklist estruturado de revisão adotado (completude, corretude, segurança, qualidade, testes) (`docs/deep_research_claude.md:495-526`).
- [x] Matriz de severidade (critical/high/medium/low) utilizada (`docs/deep_research_claude.md:527-533`).
- [x] Regras de decisão e critérios de aprovação configurados (`docs/deep_research_claude.md:534-542`).
- [x] Input/output padronizados (`review-brief.json`, `reviewer-output.json`) implementados (`docs/deep_research_claude.md:543-595`).
- [x] Técnicas de review e protocolos de erro aplicados (`docs/deep_research_claude.md:596-606`).
- [x] Regras finais em vigor (recomendações específicas, citar código, não aprovar com críticos) (`docs/deep_research_claude.md:607-613`).

## 8. Subagente Corretor
- [x] Frontmatter e responsabilidades do fixer registrados (`docs/deep_research_claude.md:621-637`).
- [x] Processo completo implementado (análise, priorização, correção cirúrgica, validação) (`docs/deep_research_claude.md:641-688`).
- [x] Estrutura de input (`fixer-brief.json`) configurada (`docs/deep_research_claude.md:689-702`).
- [x] Output JSON do fixer detalhando fixes, validações e próximos passos adotado (`docs/deep_research_claude.md:703-800`).
- [x] Diretrizes de correção e exemplos aplicados (security, logic, quality) (`docs/deep_research_claude.md:803-845`).
- [x] Técnicas cirúrgicas, rollback e protocolos de erro incorporados (`docs/deep_research_claude.md:847-914`).
- [x] Estratégia de time budget e checklist de qualidade seguidas (`docs/deep_research_claude.md:923-959`).
- [x] Métricas de sucesso monitoradas (CRITICAL/HIGH resolvidos) (`docs/deep_research_claude.md:961-983`).

## 9. Fluxo de Trabalho Compartilhado
- [x] Sequência hub-and-spoke mapeada conforme diagrama Mermaid (`docs/deep_research_claude.md:991-1007`).
- [x] Árvores de decisão do checklist, reviewer e iterações implementadas (`docs/deep_research_claude.md:1009-1042`).
- [x] Estrutura de estado compartilhado (`task-status.json`) adotada com fases e métricas (`docs/deep_research_claude.md:1045-1112`).
- [x] Artefatos de comunicação entre agentes (.claude/plans e .claude/results) padronizados (`docs/deep_research_claude.md:1115-1240`).

## 10. Operação, Troubleshooting e Contexto
- [x] Prompts dos agentes ajustados para garantir invocação correta (`docs/deep_research_claude.md:1248-1267`).
- [x] Estratégia de escalação após 3 iterações documentada e automatizada (`docs/deep_research_claude.md:1271-1286`).
- [x] Gestão de file locks implementada (`docs/deep_research_claude.md:1290-1315`).
- [x] Rotina de compactação de contexto configurada (`docs/deep_research_claude.md:1319-1343`).
- [x] Procedimento de rollback em regressões do fixer aplicado (`docs/deep_research_claude.md:1348-1369`).
- [x] Políticas de uso de ultrathink/think/think hard seguidas (`docs/deep_research_claude.md:1373-1405`).
- [x] Otimizações específicas do Sonnet 4.5 (context awareness, paralelismo, caching) ativadas (`docs/deep_research_claude.md:1409-1449`).
- [x] Melhores práticas por fase (Checklist, Writer, Reviewer, Fixer, Orquestrador) adotadas (`docs/deep_research_claude.md:1453-1484`).

## 11. Qualidade e Métricas
- [x] Checklist de QA final aplicado antes de concluir tarefas (`docs/deep_research_claude.md:1487-1504`).
- [x] Monitoramento contínuo de métricas (aprovação 1ª iteração, iterações ≤3, escalonamentos ≤10%, cobertura ≥80%) ativo (`docs/deep_research_claude.md:1507-1526`).
