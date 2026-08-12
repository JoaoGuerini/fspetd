# Contexto do projeto

Documento de repasse: o que um agente (ou uma pessoa nova no grupo) precisa saber
antes de mexer neste repositório. O [README](README.md) explica o que é a página;
este arquivo explica **o estado das decisões, as armadilhas e o que está em aberto**.

## O que é

Página estática única com o **Project Model Canvas** (modelo do José Finocchio Júnior)
de um projeto da disciplina **Fábrica de Software I — IFRO Campus Vilhena, 2026/2**.

O projeto é uma plataforma que conecta tutores de pets a cuidadores em Vilhena.

⚠️ **Atenção ao nome.** O canvas foi escrito como **PetConecta**, mas os slides da
apresentação chamam o projeto de **"Petsitter de Bairro"**. O nome "PetConecta" vem
sendo removido da página aos poucos (saiu do `<title>` e do rodapé), mas ainda sobra
no `aria-label` do `<main>`. Confirme qual é o nome oficial antes de escrever mais.

## Onde está

| | |
|---|---|
| GitHub | https://github.com/Lizynmc/fspet (branch `main`) |
| Produção | https://fspet.vercel.app |
| Painel Vercel | https://vercel.com/lizzynmcs-projects/fspet |

**Deploy:** Vercel, site estático servido da raiz. O repositório GitHub está conectado
ao projeto, então **todo push na `main` publica automaticamente**. Não é preciso rodar
nada de CLI — basta commitar e dar push.

Existe um `.env` local com um `VERCEL_TOKEN` que **já foi revogado** (está morto).
O `.gitignore` cobre `.env` e `.vercel/`. Não tente usar o Vercel CLI com ele.

## Arquitetura

Um arquivo só: [index.html](index.html). HTML, CSS e JS inline. **Sem build, sem
dependências, sem `node_modules`.** Abrir o arquivo no navegador já funciona.

Única dependência externa: a fonte Poppins, via Google Fonts.

### Recursos da página

- **Modo slide 16:9** — botão "Project Model Canvas" no rodapé. Usa a Fullscreen API e,
  se o navegador bloquear, cai para um overlay. `Esc` sai.
- **Zoom de seção** — clicar no `<header>` de um bloco clona o bloco num card grande
  sobre o fundo desfocado. O clone troca a classe `.block` por `.zoom-card`.
- **Impressão** — `@media print` com A4 paisagem.
- **Responsivo** — abaixo de 900px a grade vira 2 colunas.

### Layout

Grade CSS de 5 colunas × 6 linhas. Cada bloco tem uma classe `.b-*`
(`.b-justificativas`, `.b-objsmart`, `.b-beneficios`, `.b-produto`, `.b-requisitos`,
`.b-stakeholders`, `.b-equipe`, `.b-restricoes`, `.b-premissas`, `.b-entregas`,
`.b-riscos`, `.b-tempo`, `.b-custos`) que define seu `grid-column` e `grid-row`.

Itens pendentes de decisão usam `<li class="open">` e aparecem destacados em rosa.

## Armadilhas conhecidas

**1. Corte em tela cheia.** No modo slide a folha é fixa em 1280×720 com
`overflow: hidden` nos blocos, então conteúdo que não cabe **é cortado
silenciosamente**. Fora do modo slide os blocos crescem e o problema não aparece.

Já existe um bloco de regras `body.slide-mode .block ...` que encolhe a tipografia
(11.5px → 10.2px, com entrelinha e paddings menores) apenas nesse modo.

> **Ao adicionar texto a qualquer bloco, confira em tela cheia.** Os mais apertados
> são Stakeholders externos, Restrições e Custos.

Como o slide é sempre 1280×720 e só depois recebe `scale()`, valores em px se comportam
igual em qualquer tela — dá para calcular o encaixe com precisão.

**2. O preview de HTML do VSCode não renderiza igual ao navegador.** Um layout já
pareceu quebrado no VSCode estando correto no navegador. Confira no navegador de
verdade, ou faça o deploy e olhe em produção.

**3. Encoding.** O arquivo original chegou com mojibake (`papÃ©is`, `restriÃ§Ãµes`).
Foi corrigido: hoje é **UTF-8 sem BOM**. Preserve os acentos ao editar. As aspas
tipográficas (`" "`) no bloco Obj SMART são intencionais.

## Conteúdo já decidido

- **Equipe:** Amara, Erick, João G. e Mariana — todos atuando na elicitação de
  requisitos, modelagem de dados e produção de wireframes.
- **Cliente / stakeholder:** Matheus.
- **Obj SMART:** entregar até **08/12/2026** um "aplicativo" que permita ao tutor
  cadastrar pets e solicitar serviços (o termo "MVP" foi removido do texto — a
  disciplina entrega análise, não um produto mínimo viável rodando). Uma segunda linha
  explica que "aplicativo" entre aspas significa a junção das entregas de análise
  (requisitos, protótipos no Figma, modelagem do banco) — **não há software rodando**;
  a disciplina entrega análise, não código.
- **Linha do tempo:** 21 encontros, terças, 4h. Marcos: **15/09** Milestone 1 (PM Canvas,
  requisitos, métricas) · **20/10** Milestone 2 (wireframes, protótipos, site map) ·
  **08/12** Milestone 3 (modelagem do banco) · **15/12** Avaliação da Fábrica.
- **Custos:** removida a infraestrutura (domínio, Cloudflare Pro) e o curso Alura — os
  6 meses do projeto cobrem só elicitação de requisitos e prototipação, sem software
  rodando, então não fazia sentido pagar hospedagem/CDN. Ficou: 6 meses, média de
  6h/semana (150h por pessoa) a R$ 20,00/hora → R$ 3.000,00 por colaborador →
  R$ 12.000,00 (4 pessoas) + Claude Pro por 6 meses (US$ 20,00/mês, câmbio R$ 5,11 de
  11/08/2026) R$ 613,20 → **R$ 12.613,20** no total. As contas fecham.
- **Restrições:** prazo da disciplina, orçamento fixo de R$ 12.613,20 (equipe e
  ferramenta de IA), escopo simples. A inconsistência anterior (Custos com item de
  infraestrutura contradizendo "não há software rodando" do Obj SMART) foi resolvida
  removendo a infraestrutura do Custos.

### Pendências ainda marcadas em rosa

1. "Formato em aberto: app nativo ou site responsivo" — bloco **Produto**

Essa pendência conversa de perto com o primeiro risco listado ("Indecisão app x site
atrasar os protótipos") e com as aspas em "aplicativo" no Obj SMART. Se o grupo bater
o martelo nisso, dá para fechar os dois de uma vez.

### Informação conhecida que ainda NÃO está no canvas

- O trabalho é registrado num **board do grupo no GitLab**. O canvas só menciona Figma.
- As entregas de cada milestone estão detalhadas nas **Diretrizes Gerais (seções 8 e 9)**
  e nas **RFPs** de cada projeto.
- O cronograma completo tem 21 encontros, mas a decisão foi **manter só os marcos** no
  canvas. Um calendário completo chegou a ser feito e foi removido a pedido.
- No cronograma falta a terça **06/10** (provável feriado ou recesso). Não confirmado.

## Trabalho em aberto

**[roxo.html](roxo.html)** — variante de cores roxo/lilás baseada nos slides da
apresentação, publicada em https://fspet.vercel.app/roxo para comparação.
Folha branca, fundo lavanda `#E9DEF9`, roxo vivo `#7B10E8`, roxo profundo `#4E0B9E`,
roxo escuro `#26103F`. Nessa variante as variáveis CSS foram renomeadas de `--pink*`
para `--accent*`, então a paleta inteira troca mexendo só no `:root`.

É uma **cópia** do `index.html`, não um tema — as duas versões têm o mesmo conteúdo
duplicado. Enquanto as duas existirem, **toda edição de conteúdo precisa ser feita nos
dois arquivos**. Quando a decisão de cor for tomada, mantenha só uma.

Também foi sugerido e não feito: usar nos títulos a fonte condensada e pesada dos
slides, mantendo Poppins no corpo do texto.

## Como trabalhar neste repo

- Responda em **português**.
- **Não** adicione `Co-Authored-By` nas mensagens de commit.
- Mensagens de commit em português, sem acentos.
- **Quando pedirem para não commitar, não commite.** As mudanças são revisadas
  visualmente antes de ir para produção.
- Faça o que foi pedido e **sinalize** o resto em vez de já aplicar. Ampliar o escopo
  por conta própria tem sido rejeitado várias vezes.
