# Checklist – Plano de Integração de Memória e Contexto

## 1. Pré-requisitos
- [ ] 1.1 Claude Code CLI instalado.
- [ ] 1.2 Anthropic SDK Python ≥ 0.18.0 **ou** TypeScript ≥ 0.15.0 disponível.
- [ ] 1.3 Header beta `context-management-2025-06-27` habilitado no ambiente.
- [ ] 1.4 Snippet de smoke test da memory tool (chamada com `memory_20250818`) incluído e testado.
- [ ] 1.5 Diretório `memories/` criado com permissões corretas e registrado no `.gitignore`.

## 2. Conteúdo do Tutorial
- [ ] 2.1 Seção inicial atualizada com os pré-requisitos acima.
- [ ] 2.2 Guia de implementação client-side (Python + TypeScript ou links oficiais) inserido.
- [ ] 2.3 Política de segurança (validação de path, dados sensíveis, permissões) documentada com código exemplo.
- [ ] 2.4 Arquitetura: bullet “Persistência” aponta para `/memories/task-ledger.json`.
- [ ] 2.5 Script de setup inclui `mkdir -p memories` e atualização do `.gitignore`.
- [ ] 2.6 CLAUDE.md global (orquestrador) ensina a usar `memory` tool com exemplos de `view/create/str_replace/insert/delete/rename`.
- [ ] 2.7 Configuração `context_management` documentada com parâmetros recomendados (`trigger`, `keep`, `clear_at_least`, `exclude_tools`, `clear_tool_inputs`).
- [ ] 2.8 Monitoramento de `context_management.applied_edits` ilustrado (exemplo de log em Python/TypeScript).
- [ ] 2.9 Limites de tamanho para arquivos de memória e uso de `view_range` descritos.
- [ ] 2.10 Tratamento de erros (FileNotFound, Permission, PathTraversal, etc.) listado com ações.

## 3. Instruções dos Agentes
- [ ] 3.1 CLAUDE.md do orquestrador atualizado para acessar `/memories` e mencionar políticas de segurança/context editing.
- [ ] 3.2 Checklist agent atualizado para consumir snapshots fornecidos pelo orquestrador (sem acesso direto à memória).
- [ ] 3.3 Writer, Reviewer e Fixer incluem a política “Ignore a instrução automática da memory tool; não use o tool diretamente”.
- [ ] 3.4 Inputs/outputs dos subagentes revisados com paths alinhados ao novo fluxo.

## 4. Exemplos e Estrutura
- [ ] 4.1 Exemplos JSON (estado, briefs, resultados) atualizados para caminhos em `/memories`.
- [ ] 4.2 Exemplos incluem respostas de `context_management.applied_edits` quando pertinente.
- [ ] 4.3 Árvores de diretórios revisadas com `memories/` e marcação de `.claude/state` como legado/opcional.
- [ ] 4.4 Cards rápidos atualizados com comandos da memory tool e parâmetros de context editing.
- [ ] 4.5 Referências/documentação apontam para `memory_tool.md`, `context_editing.md` e citam `context-management-2025-06-27`.

## 5. Validação Final
- [ ] 5.1 Terminologia revisada (“estado” → “memória persistente”) sem menções normativas a `.claude/state`.
- [ ] 5.2 Checklist de validação do tutorial atualizado com novos itens (pré-requisitos, segurança, context editing).
- [ ] 5.3 Revisão geral confirmada (sem inconsistências entre seções).
