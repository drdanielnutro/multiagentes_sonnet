# AGENTS – Regras de Operação para Atualização do Tutorial

## 1. Propósito
Coordenar o trabalho de implementação descrito em `tutorial_pratico_subagentes.md`. Cada atividade executada **deve** ser refletida na checklist `checklist_controle_implantacao.md`.

## 2. Arquivos de Referência
- Plano / tutorial base: `tutorial_pratico_subagentes.md`
- Checklist de controle: `checklist_controle_implantacao.md`

## 3. Fluxo de Trabalho Obrigatório
1. **Ler o tutorial/plano** antes de iniciar qualquer alteração, especialmente as seções 3 a 6.5.
2. Executar as tarefas na sequência apresentada no tutorial (`3.x → 4.x → 5.x → 6.x`).
3. A cada sub-tarefa concluída, localizar o(s) item(ns) correspondente(s) na checklist e marcar como concluído (`[x]`).
4. Registrar no histórico interno (logs do agente) qual seção do plano foi executada e quais itens da checklist foram marcados.

## 4. Mapeamento Plano → Checklist
| Seção do plano | Descrição | Itens da checklist a marcar após concluir |
| --- | --- | --- |
| 3.1 – 3.3 | Preparação do ambiente e estrutura | Checklist seções 1–3 |
| 4.1 | Orquestrador principal | Checklist seção 4 |
| 4.2 | Subagente Checklist | Checklist seção 5 |
| 4.3 | Subagente Escritor | Checklist seção 6 |
| 4.4 | Subagente Revisor | Checklist seção 7 |
| 4.5 | Subagente Corretor | Checklist seção 8 |
| 5.1 – 5.4 | Fluxo de trabalho compartilhado | Checklist seção 9 |
| 6.1 | Troubleshooting operacional | Checklist seção 10 |
| 6.2 – 6.5 | Otimizações, melhores práticas, QA e métricas | Checklist seção 11 |

> **Nota:** Se uma atividade tocar em múltiplas seções do plano, marque todos os itens da checklist associados.

## 5. Convenções de Registro
- Use o formato `[x]` / `[ ]` no próprio `checklist_controle_implantacao.md`.
- Manter marcações consistentes (não remover itens existentes).
- Em caso de revisão ou retrabalho, desmarcar (`[ ]`) apenas se o requisito deixou de ser atendido.

## 6. Verificações Finais
- Antes de encerrar o trabalho, validar que todas as seções relevantes do tutorial (3 a 6.5) tenham seus correspondentes marcados na checklist.
- Garantir que cada marcação na checklist tenha correspondência em commits/edições visíveis no repositório.
