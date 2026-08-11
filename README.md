# webacademy-ci-lab01

Laboratório 01 do módulo **WACAD017 — Fundamentos de Integração Contínua**
(Web Academy / ICOMP-UFAM).

Primeiro contato com o **GitHub Actions**: um mesmo workflow
(`.github/workflows/helloFlow.yml`) acionado de três formas diferentes.

## Os três exercícios

Cada exercício é um commit deste repositório, editando o mesmo arquivo:

| Exercício | Gatilho (`on`) | Execução |
| --------- | -------------- | -------- |
| 01 — ativação manual | `workflow_dispatch` | [run 31443905489](../../actions/runs/31443905489) |
| 02 — ativação programada | `schedule` — `cron: '*/5 * * * *'` | [run 31448670168](../../actions/runs/31448670168) |
| 03 — ativação por evento | `push` | [run 31448737637](../../actions/runs/31448737637) |

Todas as execuções estão na aba [**Actions**](../../actions).

O job `first-job` roda em `ubuntu-latest` com dois steps:

```yaml
steps:
  - name: Diga oi
    run: echo "Hello World!"
  - name: Diga valeu
    run: echo "Valeu - bye!"
```

## O que cada gatilho muda

**`workflow_dispatch`** — o workflow só roda quando alguém aperta "Run workflow"
na aba Actions. É o único dos três que expõe esse botão.

**`schedule`** — o botão de execução manual desaparece; quem dispara é o
agendador do GitHub. Duas observações: o agendamento só vale para workflows na
branch default, e o GitHub atrasa o disparo em períodos de carga alta. Neste
laboratório, o primeiro disparo levou **1h22min**, e não os 5 minutos do cron.

**`push`** — qualquer push no repositório dispara o workflow, inclusive o push
que altera o próprio `.yml`, já que ele também faz parte do repositório. Foi
exatamente o que aconteceu: o commit do exercício 03 disparou a própria execução.

## Referências

- <https://docs.github.com/actions>
- [Eventos que disparam workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule)
