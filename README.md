# Skill de captação de conferências BRASA

Skill para o Claude organizar a captação de foto e vídeo do time de Comunicação (Comun) em conferências da BRASA: a BRASA Summit Américas, a BRASA Summit Europa, a BRASA Summit Innovation e as próximas.

A skill nasceu da BRASA Summit Américas 2026 (BSA26). Lá, o cronograma de captação funcionou bem. Já a planilha precisou ser refeita no meio do evento: tinha gente demais, séries difíceis de gravar e um status por pessoa que não dava conta do que acontecia. As regras da skill juntam esse aprendizado com o feedback da Dalila Figueiras (COO) para que a próxima conferência já comece no formato certo.

## O que ela entrega

Quando você pede a captação de uma conferência, o Claude segue esta ordem:

1. **Seleção de quem gravar.** Uma lista curta e cumprível, com o motivo e a prioridade de cada pessoa. Também lista quem ficou de fora e por quê.
2. **Séries de conteúdo.** De 4 a 6 perguntas de uma frase, cada uma com um destino concreto, um dono e uma meta.
3. **Planilha de captação no Google Sheets.** Uma linha por gravação (pessoa × série), com status por pergunta.
4. **Cronograma de captação no Canva.** Uma cópia do cronograma oficial da Conf com uma bolinha para cada pessoa que cobre cada sessão. É o modelo aprovado na BSA26.
5. **Briefing dos videomakers.** Um doc com o roteiro do aftermovie em blocos, as perguntas dos âncoras, a lista de b-roll e as regras de captura.
6. **Pastas no Drive.** Uma pasta por dia e por iniciativa, e uma pasta Séries com uma subpasta para cada pessoa.
7. **Slides de treinamento do time.**
8. **Web app de controle (Vercel).** O time usa no celular durante o evento: sobe o arquivo e o app atualiza a planilha sozinho.

Antes de montar a planilha, o cronograma e o briefing, o Claude mostra a seleção e as séries e espera o seu ok. No Canva, nada é salvo sem a sua aprovação.

## Como instalar

### No Claude (app ou web)

1. Ative a execução de código. Nos planos Free, Pro e Max, é em Settings > Capabilities > "Code execution and file creation". Nos planos Team e Enterprise, quem ativa é um owner da organização.
2. Gere o ZIP da pasta da skill. A pasta precisa ficar na raiz do ZIP, com o mesmo nome da skill:

   ```bash
   git clone https://github.com/Hoffalo/brasa-captacao-confs-skill.git
   cd brasa-captacao-confs-skill
   zip -r captacao-conferencias-brasa.zip captacao-conferencias-brasa
   ```

3. Em Customize > Skills, clique em "+", depois em "Create skill" e em "Upload a skill". Envie o ZIP.
4. Confira se a chave da skill está ligada.

### No Claude Code

A skill ativada na conta do Claude sincroniza sozinha quando você entra no Claude Code com a mesma conta. Para instalar só localmente, copie a pasta para a pasta de skills:

```bash
cp -r captacao-conferencias-brasa ~/.claude/skills/
```

## Como usar

### 1. Junte as entradas

A skill não inventa nada. Antes de começar, tenha em mãos:

- **Cronograma oficial da conferência:** o link do Canva da Conf ou a página do guia, com dias, horários e salas.
- **Listas de pessoas:**
  - palestrantes, mentores e reps de empresa (normalmente a Intertimes);
  - bolsistas (Impacto);
  - lideranças das BRASA Locais (Rede).
- **Time de captação:** nome completo de cada pessoa, função, chegada e saída, e equipamento.
- **Âncoras do aftermovie:** quem só vai falar com os videomakers.
- **Campanhas que vão usar o material:** por exemplo, a campanha de vendas da próxima conferência ou a Passaporte BRASA, cada uma com o time dono.
- **Pasta da conferência** no drive compartilhado e o **template de slides** BRASA.

### 2. Peça ao Claude

Escreva algo como:

> Vamos preparar a captação da BRASA Summit Europa 2026. O cronograma está neste link [...], as listas estão nestas planilhas [...], o time é [...] e os âncoras do aftermovie são [...]. Usa a skill de captação.

### 3. Aprove em etapas

1. **Seleção e séries.** Revise quem entrou, quem ficou de fora e as perguntas. Este é o momento de cortar ou incluir gente.
2. **Planilha.** Ela é montada e enviada para o Drive como Google Sheets. Valide a lista com a Conf e com a Dalila antes do evento.
3. **Cronograma no Canva.** O Claude mostra o resumo das mudanças e só salva com a sua aprovação. Se a Conf mudar a grade, até no dia, peça para atualizar: a página é corrigida no lugar.
4. **Briefing dos videomakers, pastas e slides.**
5. **Web app.** Peça para construir quando a planilha estiver fechada. Teste com uma cópia da planilha antes do evento.

### 4. Durante e depois da conferência

- O time atualiza tudo pelo web app, não editando a planilha à mão no celular.
- Depois do evento, anote o que funcionou e o que não funcionou e atualize o `SKILL.md`. É assim que a skill melhora de uma conferência para a outra.

## Conectores que a skill usa

| Conector | Para quê |
|---|---|
| Google Drive | Ler as listas, criar pastas, subir a planilha e conferir as edições exportando a planilha. |
| Canva | Copiar e editar o cronograma de captação. |
| Claude in Chrome | Editar Google Sheets, Docs e Slides quando não há conector para isso. |
| Vercel | Publicar o web app. |
| Slack e Granola (opcionais) | Buscar contexto em threads e reuniões. |

## Regras principais

- **Âncoras só falam com os videomakers.** A Comun não aborda essas pessoas para vídeo.
- **Uma pessoa, uma gravação.** Quem é palestrante e rep ao mesmo tempo grava como palestrante, com foco no conteúdo. O vídeo de empresa, com foco na delegação, fica com outro rep.
- **No máximo um rep por empresa,** priorizando anfitriã e patrocinadoras, depois empresas com workshop ou case.
- **Séries viáveis no dia:** uma pergunta de uma frase, gravada num take, sem variantes nem corrente.
- **Teto de capacidade:** cerca de 8 depoimentos por pessoa de vídeo por dia.
- **BRASA Locais:** gravação coletiva no Encontro de BLs, sem uma linha por BL na planilha.
- **Nomes do time:** sempre os da lista fornecida, nunca deduzidos.

## Estrutura do repositório

```
captacao-conferencias-brasa/
  SKILL.md      instruções completas que o Claude segue
README.md       este guia
```

## Como atualizar

1. Edite `captacao-conferencias-brasa/SKILL.md`.
2. Mantenha o `description` do topo com até 200 caracteres.
3. Faça o commit e gere o ZIP de novo para reenviar no Claude.
