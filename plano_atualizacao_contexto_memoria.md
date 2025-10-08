# Plano de Integração das Ferramentas Nativas de Memória e Contexto

## 1. Objetivo e Escopo
- Atualizar `deep_research_claude.md` para ensinar o uso da `memory` tool (`memory_20250818`) e do `context editing` (`clear_tool_uses_20250919`) conforme a documentação oficial.
- Manter a arquitetura hub-and-spoke e o fluxo operacional já descritos, apenas modernizando instruções, exemplos e boas práticas.

## 2. Referências Técnicas
- `memory_tool.md`: header beta `context-management-2025-06-27`, comandos suportados (`view`, `create`, `str_replace`, `insert`, `delete`, `rename`), diretório `/memories`, políticas de segurança e erro, modelos compatíveis (Sonnet 4.5, Sonnet 4, Opus 4.1, Opus 4).
- `context_editing.md`: estratégia `clear_tool_uses_20250919`, parâmetros (`trigger`, `keep`, `clear_at_least`, `exclude_tools`, `clear_tool_inputs`), impacto em prompt caching, monitoramento (`applied_edits`).

## 3. Pré-Requisitos Obrigatórios
- **Software mínimo**: Claude Code CLI; Anthropic SDK (Python ou TypeScript) em versão com suporte à memory tool (recomenda-se usar a versão mais recente com os helpers oficiais).
- **Acesso beta**: habilitar `context-management-2025-06-27` em todas as chamadas relevantes.
- **Smoke test inicial**: incluir no tutorial um snippet que cria uma chamada `client.beta.messages.create(...)` com o tool `memory_20250818` e `max_tokens=1` para verificar rapidamente se o ambiente está apto.
- **Permissões**: garantir que o diretório `/memories` exista, seja gravável e esteja fora de versionamento público (documentar inclusão no `.gitignore`).

## 4. Guia de Implementação Client-Side (a ser incorporado ao tutorial)
- Explicar que a memory tool depende de handlers client-side.
- Incluir exemplo mínimo em Python (subclasse de `BetaAbstractMemoryTool`) e apontar para o helper TypeScript (`betaMemoryTool`).
- Destacar onde encontrar exemplos oficiais (`anthropic-sdk-python/examples/memory/basic.py`, `anthropic-sdk-typescript/examples/tools-helpers-memory.ts`).
- Ressaltar a necessidade de validar paths, controlar permissões e lidar com erros em cada comando.

## 5. Alterações Planejadas em `deep_research_claude.md`

### 5.1 Arquitetura e Estrutura de Projeto
| Trecho atual | Ação | Conteúdo proposto | Justificativa |
| --- | --- | --- | --- |
| `deep_research_claude.md:40-44` – bullet `- **Estado:** .claude/state/task-status.json` | Substituir (texto exato) | Antes: `- **Estado:** .claude/state/task-status.json`<br>Depois: `- **Persistência:** /memories/task-ledger.json (via memory tool \`memory_20250818\`)` | Refletir o armazenamento oficial com a memory tool. |
| `deep_research_claude.md:82-95` – script de setup | Expandir | Adicionar `mkdir -p memories` logo após a criação de `.claude/agents`, explicar permissões e incluir `echo "memories/" >> .gitignore`. | Preparar o ambiente para o diretório persistente. |
| `deep_research_claude.md:99-135` – “Configuração Global (CLAUDE.md)” | Reescrever bullets específicos (linhas 109-120) | - Instruir que o orquestrador sempre começa consultando `/memories/task-ledger.json` via comando `view`.<br>- Referenciar o header beta obrigatório e o smoke test.<br>- Atualizar “Gestão de Arquivos” (state → `/memories`).<br>- Registrar explicitamente o tool `{"type": "memory_20250818", "name": "memory"}` na lista `tools` do orquestrador. | Alinhar regras globais com o novo fluxo persistente. |
| `deep_research_claude.md:1781-1800` – árvore de diretórios | Atualizar | Incluir `memories/` com arquivos típicos (`task-ledger.json`, `snapshots/`), marcar `.claude/state` como legado/opcional. | Documentar a topologia revisada. |

### 5.2 Instruções dos Agentes
| Trecho atual | Ação | Conteúdo proposto | Justificativa |
| --- | --- | --- | --- |
| `deep_research_claude.md:142-215` – CLAUDE.md do orquestrador | Substituir seções “Fluxo” e “Persistência” | - Inserir passo inicial “Memory tool → `view /memories/task-ledger.json`”.<br>- Incluir blocos de exemplo (JSON) para `view`, `create`, `str_replace`, `insert`, `delete`, `rename`.<br>- Explicar configuração `context_management` e mencionar monitoramento (`applied_edits`).<br>- Destacar política de segurança (função `validate_path`). | Garante uso correto das ferramentas nativas. |
| `deep_research_claude.md:251-344` – Checklist agent | Ajustar instruções | - Informar que recebe snapshot via orquestrador (não acessa `/memories`).<br>- Adicionar bloco “Memory Tool Access: ignore instrução automática; dependa do orquestrador”. | Evitar acessos diretos à memória. |
| `deep_research_claude.md:345-704` – Writer, Reviewer, Fixer | Reescrever seção de policies | - Adicionar parágrafo padrão “Ignore a instrução ‘Always view your memory’; você não usa a memory tool diretamente”.<br>- Ajustar formatos de input/output conforme novos caminhos. | Padronizar override do prompt automático. |
| `deep_research_claude.md:1046-1231` – exemplos de JSON de estado | Atualizar | - Alterar paths para `/memories/...`.<br>- Incluir exemplos de respostas de context editing (`applied_edits`). | Evitar inconsistência com a nova arquitetura. |

### 5.3 Gestão de Contexto
| Trecho atual | Ação | Conteúdo proposto | Justificativa |
| --- | --- | --- | --- |
| `deep_research_claude.md:1321-1343` – Problema 4 | Reescrever | - Explicar `context_management.edits` detalhado (parâmetros recomendados: `trigger`=60000 tokens, `keep`=5, `clear_at_least`=10000, `exclude_tools=["memory"]`, `clear_tool_inputs=false`).<br>- Reforçar que, por padrão, apenas resultados das tool calls são limpos (entradas só são removidas se `clear_tool_inputs=true`).<br>- Acrescentar nota sobre prompt caching e quando ajustar os valores. | Oferecer configuração pronta para multi-agente. |
| `deep_research_claude.md:1413-1416` – Consciência de contexto | Expandir | - Instruir leitura dos avisos `<system_warning>` e de `response.context_management.applied_edits`.<br>- Mostrar snippet Python/TypeScript para logar o que foi limpo. | Ensinar monitoramento prático. |
| `deep_research_claude.md:1723-1729` – cards rápidos | Atualizar | - Substituir `/clear` por “Como ativar/desativar context editing” e “Como checar applied_edits”.<br>- Adicionar comando para consultar tokens restantes. | Manter cartões alinhados às novas ferramentas. |

### 5.4 Segurança, Limites e Erros (novo bloco na seção de melhores práticas)
| Tema | Conteúdo proposto | Justificativa |
| --- | --- | --- |
| Validação de paths | Código exemplo com `Path.resolve()` garantindo prefixo `/memories`; lista de padrões proibidos (`../`, `..\\`, `%2e%2e%2f`, paths absolutos). | Evitar path traversal. |
| Limites de tamanho | Recomendar limite de 50 KB por arquivo e 500 KB total; sugerir rotação/arquivamento e uso de `view_range` para paginação. | Controlar custo e desempenho. |
| Tratamento de erros | Tabela com `FileNotFound`, `PermissionError`, `PathTraversalError`, `FileSizeError`, ações sugeridas; lembrar que seguir padrões do text editor tool. | Facilitar troubleshooting. |

### 5.5 Fontes e Apêndices
| Trecho atual | Ação | Conteúdo proposto | Justificativa |
| --- | --- | --- | --- |
| `deep_research_claude.md:1541-1555` | Atualizar | Adicionar referências explícitas para `memory_tool.md`, `context_editing.md`, links para SDKs e exemplos. | Garantir sustentação documental. |
| `deep_research_claude.md:1700+` | Revisar | Incluir cards “Memory Tool” e “Context Editing” com comandos principais, parâmetros recomendados e links rápidos. | Facilitar consulta rápida. |

## 6. Conteúdos Adicionais a Produzir
- Seção “Pré-Requisitos Obrigatórios” com checklist e smoke test.
- Guia “Implementação Client-side” (Python + TypeScript) enfatizando validação de paths e permissões.
- Política de segurança detalhada (path traversal, dados sensíveis, permissões).
- Exemplo completo de `context_management` com comentários sobre cada parâmetro, além de snippet de monitoramento (Python/TypeScript).
- Parágrafo padrão “Memory Tool Access Policy” para cada subagente.
- Mini seção “Monitoring & Debugging” detalhando `applied_edits`, token counting API e mensagens de erro frequentes.

## 7. Sequência Recomendada de Edição
1. Inserir seções de pré-requisitos e implementação client-side no início do tutorial.
2. Atualizar arquitetura geral e roteiro de setup (incluindo diretório `/memories`).
3. Reescrever CLAUDE.md global do orquestrador com exemplos de memory tool, segurança e context editing.
4. Atualizar cada subagente individualmente, adicionando overrides e ajustando inputs/outputs.
5. Revisar seções de troubleshooting/contexto e cartões rápidos com as novas recomendações.
6. Atualizar exemplos de JSON, apêndices e referências.
7. Revisar consistência terminológica (“estado” → “memória persistente”), removendo referências normativas a `.claude/state`.

## 8. Riscos e Mitigações
- **Falta de pré-requisitos**: destacar que sem SDK atualizado e header beta o processo falha; sugerir executar smoke test antes.
- **Implementação client-side incompleta**: incluir alerta visual e exemplo; recomendar uso das helpers oficiais.
- **Path traversal e segurança**: fornecer snippet obrigatório e checklist de validação; sugerir testes com entradas maliciosas.
- **Uso indevido da memória por subagentes**: documentar override explícito e reforçar que só o orquestrador usa a ferramenta.
- **Cache invalidation**: explicar impacto de `context editing` no prompt caching e orientar uso de `clear_at_least`.
- **Custos de tokens**: recomendar `view_range`, limites de arquivo e monitoração de `applied_edits` para ajustar parâmetros conforme necessário.

## 9. Checklist de Validação pós-edição
- [ ] Seção de pré-requisitos (SDK, header beta, smoke test) presente e destacada.
- [ ] Implementação client-side da memory tool descrita com exemplo ou links diretos.
- [ ] Políticas de segurança (validação de path, dados sensíveis, permissões) documentadas.
- [ ] Orquestrador referenciando `/memories` com exemplos de comandos e configuração `context_management`.
- [ ] Subagentes instruídos a ignorar o prompt automático da memory tool e a depender do orquestrador.
- [ ] Configuração de context editing completa, com parâmetros recomendados e monitoramento de `applied_edits`.
- [ ] Limites de tamanho e paginação para `/memories` definidos, junto com tratamento de erros.
- [ ] Exemplos JSON atualizados para caminhos `/memories` e inclusão de respostas `applied_edits`.
- [ ] Cards rápidos e apêndices com comandos da memory tool e parâmetros de context editing.
- [ ] Referências citando `context-management-2025-06-27` e links oficiais das ferramentas.
