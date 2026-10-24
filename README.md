# KingSkill

Skill para o Claude Code que faz uma **análise completa de um projeto**: construção, segurança, desempenho, qualidade de código, testes, banco de dados, interface e deploy.

Ela mede antes de mexer, procura no [skills.sh](https://skills.sh) as skills especializadas para os pontos fracos do projeto (usando a `find-skills` da Vercel), aplica as melhorias seguras e entrega um relatório com o antes e depois. Antes de mexer em banco, produção, deploy ou commit, ela pede autorização.

## Instalar

No terminal:

```bash
npx skills add ReeiKing/kingskill -g
```

O `-g` instala para todos os projetos. Ou peça direto no Claude Code: *"instala globalmente a skill github.com/ReeiKing/kingskill"*.

Depois, abra o Claude Code de novo.

## Usar

Dentro da pasta do projeto, digite:

```
Analise projeto
```

ou `/kingskill`.

## Atualizar

```bash
npx skills update
```

## Requisitos

- Claude Code
- Node.js (para `npx`). Sem ele a análise roda, mas não busca skills novas.
