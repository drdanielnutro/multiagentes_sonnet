# AGENTS – Regras de Operação para Atualização do Tutorial

## 1. Propósito
Coordenar o trabalho de revisão do arquivo `deep_research_claude.md` utilizando o plano em `plano_atualizacao_contexto_memoria.md`. Cada atividade executada **deve** ser refletida na checklist `checklist_plano_atualizacao.md`.

## 2. Arquivos de Referência
- Plano mestre: `plano_atualizacao_contexto_memoria.md`
- Checklist de controle: `checklist_plano_atualizacao.md`
- Arquivo alvo (tutorial): `deep_research_claude.md`

## 3. Fluxo de Trabalho Obrigatório
1. **Ler o plano** antes de iniciar qualquer alteração para conhecer as seções 1–9.
2. Executar as tarefas na ordem sugerida no item 7 do plano (Sequência Recomendada de Edição).
3. A cada sub-tarefa concluída, localizar o(s) item(ns) correspondente(s) na checklist e marcar como concluído (`[x]`).
4. Registrar no histórico interno (logs do agente) qual item do plano foi executado e quais itens da checklist foram marcados.

## 4. Mapeamento Plano → Checklist
| Seção do plano | Descrição | Itens da checklist a marcar após concluir |
| --- | --- | --- |
| 3 | Pré-requisitos obrigatórios | 1.1–1.5 |
| 4 | Guia de implementação client-side | 2.2, 2.3, 2.9, 2.10 |
| 5.1 | Arquitetura e estrutura de projeto | 2.4, 2.5, 4.3 |
| 5.2 | Instruções dos agentes | 2.6, 3.1–3.4 |
| 5.3 | Gestão de contexto | 2.7, 2.8, 4.4 |
| 5.4 | Segurança, limites e erros | 2.3, 2.9, 2.10 |
| 5.5 | Fontes e apêndices | 4.4, 4.5 |
| 6 | Conteúdos adicionais a produzir | 2.1, 2.2, 2.3, 2.8 |
| 7 | Sequência recomendada (uso interno) | Não gera marcação direta; serve como roteiro |
| 8 | Riscos e mitigações | Usar como referência; sem marcação obrigatória |
| 9 | Checklist de validação pós-edição | 5.1–5.3 (apenas após revisão final) |

> **Nota:** Se uma atividade tocar em múltiplas seções do plano, marque todos os itens da checklist associados.

## 5. Convenções de Registro
- Use o formato `[x]` / `[ ]` no próprio `checklist_plano_atualizacao.md`.
- Manter marcações consistentes (não remover itens existentes).
- Em caso de revisão ou retrabalho, desmarcar (`[ ]`) apenas se o requisito deixou de ser atendido.

## 6. Verificações Finais
- Antes de encerrar o trabalho, validar que todos os itens da seção 9 do plano (e 5.x da checklist) estejam marcados.
- Garantir que cada marcação na checklist tenha correspondência em commits/edições visíveis no repositório.
