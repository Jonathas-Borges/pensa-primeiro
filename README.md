# pensa-primeiro

Skill para o Claude que evita terceirizar o raciocínio para a IA.

Em vez de entregar a conclusão pronta, o Claude pede o **seu palpite primeiro**. Quando você não tem como opinar sem dados, ele levanta e mostra só os fatos, sem interpretação, e pergunta: *"O que você lê nesses dados?"*. Depois do seu palpite, ele compara com a evidência, aponta o que você não considerou (incluindo a melhor objeção à sua leitura) e deixa a decisão com você.

Cada palpite vai para um **log de calibração**, então dá para acompanhar com que frequência você acerta.

## Como funciona

| Situação | O que o Claude faz |
|---|---|
| Tarefa mecânica (formatar, renomear, código já especificado) | Executa normal |
| Você escreveu **"só faz"** | Executa normal, sem palpite |
| Você já trouxe uma hipótese | Usa como palpite e compara com a evidência |
| Você tem contexto para opinar | Pede o palpite em 1 linha antes de investigar |
| Opinar exige dados que você não tem | Mostra só os fatos e pergunta o que você lê neles |

Depois do palpite, a resposta tem três blocos: **seu palpite vs evidência**, **o que você não considerou** e **a decisão é sua** (recomendação só se você pedir).

## Instalação

### Claude Code

```bash
git clone https://github.com/Jonathas-Borges/pensa-primeiro.git
mkdir -p ~/.claude/skills
cp -r pensa-primeiro/skills/pensa-primeiro ~/.claude/skills/
```

Para valer só em um projeto, copie para `.claude/skills/` dentro do projeto.

### claude.ai

Compacte a pasta `skills/pensa-primeiro` em um `.zip` e envie em **Settings → Capabilities → Skills**.

## Recomendado: reforçar o gatilho

A skill dispara pela própria descrição, mas o Claude às vezes responde direto em perguntas que parecem simples. Para ela disparar sempre, cole o trecho de [`exemplos/CLAUDE.md`](exemplos/CLAUDE.md) no seu `~/.claude/CLAUDE.md` (Claude Code) ou nas preferências (claude.ai).

## Log de calibração

Por padrão o log fica em `~/calibracao-de-julgamento.md`. Para mudar o caminho (ex.: para dentro do seu vault do Obsidian), adicione esta linha ao seu `CLAUDE.md`:

```
pensa-primeiro-log: ~/Vaults/Notas/Calibração de Julgamento.md
```

O arquivo é criado na primeira vez. Cada linha registra data, pergunta, modo, seu palpite, o que a evidência mostrou e o veredito (S = acertou, N = errou, P = parcial).

No claude.ai, sem acesso a arquivos, o Claude mostra a linha pronta no fim da resposta para você copiar.

## Ajustando

É um arquivo Markdown só: [`skills/pensa-primeiro/SKILL.md`](skills/pensa-primeiro/SKILL.md). Edite à vontade: exemplos do seu domínio, mais ou menos atrito, outra forma de log.
