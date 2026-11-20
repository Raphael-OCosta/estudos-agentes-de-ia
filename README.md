# Estudos — *Building Applications with AI Agents* (Michael Albada)

> **A melhor forma de estudar um livro técnico é ler e praticar ao mesmo tempo.**
> Leia uma seção, feche o livro e escreva o código com as próprias mãos. Só depois confira o gabarito.

Este repositório registra meu estudo de *Building Applications with AI Agents* (O'Reilly, em inglês). O livro cobre como projetar, orquestrar, avaliar, monitorar e proteger sistemas com agentes de IA.
Os cadernos estão em português e mantêm os termos técnicos no original. Cada seção aponta para a página do PDF e, quando cabe, traz um exercício que constrói **uma peça de um agente do zero**, sem frameworks.

## O método

| Passo | O que fazer | Onde |
|---|---|---|
| 1. Ler | Ler a seção indicada | PDF do livro (página no caderno) |
| 2. Praticar | Escrever a solução do exercício **sem olhar a resposta** | `praticar/capXX_*.ipynb` |
| 3. Conferir | Comparar com o gabarito | `resolvidos/capXX_*.ipynb` |
| 4. Resumir | Explicar com as próprias palavras nas células | `praticar/` |
| 5. Registrar | Commit + push | GitHub |

## Conteúdo (33 exercícios)

| Cap. | Tema | O que se constrói |
|---|---|---|
| 1–2 | agentes e componentes | workflow × agente, custo por modelo, **laço de agente com function calling**, esquema de ferramenta gerado por `inspect`, memória com orçamento de tokens, série × paralelo |
| 3–4 | UX e ferramentas | escopo claro no *system prompt*, confirmação antes de ação irreversível, validação de argumentos com **pydantic**, `tool_choice` |
| 5 | orquestração | **ReAct com modelo falso** (testar sem gastar), seleção de ferramentas por similaridade, retentativas com espera exponencial, topologias, *context engineering* |
| 6–7 | memória e aprendizado | janela + resumo, memória semântica, **grafo de conhecimento** com vários saltos, reflexão (lições), JSONL de *fine-tuning* a partir de *traces* |
| 8 | multiagentes | supervisor que roteia, escritor × revisor, barramento de eventos, salvar e retomar o estado |
| 9–11 | avaliação e operação | acurácia da escolha de ferramenta, juiz que detecta invenção, **spans de tracing**, PSI para mudança de distribuição, A/B de prompts |
| 12–13 | segurança e humanos | **injeção de prompt** via ferramenta, mascaramento de PII, menor privilégio com auditoria, níveis de autonomia por risco |

## Escolhas

- O livro usa LangChain/LangGraph. Aqui cada mecanismo é feito **à mão** com o SDK da OpenAI, apontado para o **OpenRouter** (`comum/ia.py`, com controle de gasto). Assim fica claro o que os *frameworks* fazem por baixo.
- A lógica dos agentes é testada com um **modelo falso roteirizado**: 23 dos 33 exercícios rodam sem internet e sem custo.
- A chave do OpenRouter fica **cifrada pelo Windows (DPAPI)** ou na variável `OPENROUTER_API_KEY`. Ela nunca vai para o código.
- O teste automático (`ferramentas/testar_cadernos.py`) roda o gabarito offline: 0 erros de código.

## Como usar

```powershell
python -m venv .venv
.venv\Scripts\python.exe -m pip install -r requirements-estudos.txt
# chave: variável OPENROUTER_API_KEY (ou arquivo DPAPI, ver comum/ia.py)
$env:OPENROUTER_API_KEY="teste"; $env:IA_BASE_URL="http://127.0.0.1:9/v1"
.venv\Scripts\python.exe ferramentas\testar_cadernos.py resolvidos   # teste offline do gabarito
```

Abra `praticar/cap01_*.ipynb` no VS Code e escolha o kernel `.venv`. O [Guia de Estudos (PDF)](Guia_de_Estudos.pdf) explica o passo a passo.

## Direitos autorais

O livro **não** está neste repositório. Para estudar, use a sua própria cópia.
Os exercícios, os cadernos, os scripts e o guia são autorais e estão sob licença [MIT](LICENSE).
