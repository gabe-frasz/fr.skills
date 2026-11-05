# fr.skills

Skills de agentes instaláveis com o [Skills CLI](https://skills.sh) da Vercel.

## Skills

| Skill | Descrição |
| --- | --- |
| [`work-summary`](skills/work-summary/SKILL.md) | Resume o trabalho do usuário a partir do histórico Git local e de pull requests do GitHub. |
| [`deyvin-audit`](skills/deyvin-audit/SKILL.md) | Audita a segurança do projeto e gera um relatório em PDF com issues prontas para o GitHub. Invocação explícita. |

## Instalação

Requisito: Node.js 22.20 ou superior.

Instalar todos os skills no projeto atual:

```bash
npx skills add gabe-frasz/fr.skills
```

Instalar um skill específico:

```bash
npx skills add gabe-frasz/fr.skills --skill work-summary
npx skills add gabe-frasz/fr.skills --skill deyvin-audit
```

Instalar globalmente:

```bash
npx skills add -g gabe-frasz/fr.skills
```

Listar os skills sem instalar:

```bash
npx skills add gabe-frasz/fr.skills --list
```

`deyvin-audit` é invocado explicitamente (ex.: `/deyvin-audit`), sem ativação automática pelo modelo.

## Requisitos

- `work-summary`: Git e GitHub CLI (`gh`) autenticado.
- `deyvin-audit`: ferramenta local para gerar PDF (Python 3 com `reportlab` e `matplotlib`, navegador headless, `wkhtmltopdf` ou `pandoc`) e permissão de escrita em `docs/security-audit/`.

## Licença

MIT. Veja [LICENSE](LICENSE).
