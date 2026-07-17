# Spec de recriação — Portal de afiliados (engenharia reversa do Guia Qual Comprar)

> Documento para alimentar uma IA construtora de sites (Hostinger e afins).
> Objetivo: recriar o **modelo estrutural** com **nome, cores e formatos diferentes** — não copiar conteúdo.
> Fonte analisada: `https://guiaqualcomprar.com.br` (homepage, artigo, metodologia, footer).

---

## 0. Resumo do modelo em uma frase

Portal editorial de **guias de compra "Qual melhor X?"** que gera tráfego orgânico de cauda longa em escala e converte em cliques de afiliado para marketplaces. Cada artigo é um ranking comentado de 5–12 produtos com prós/contras, FAQ e CTAs para loja.

| Dimensão | Valor observado |
|---|---|
| Tecnologia | Next.js (SSR/SSG, `/_next/image`) |
| Cor de marca original | Verde `#47962d` (`meta-theme-color`) |
| Escala | ~166 páginas de paginação × ~40 artigos ≈ **6.600 URLs** |
| Marketplaces de destino | Mercado Livre + Shopee |
| Origem das imagens | CDN da Amazon (`m.media-amazon.com`) |
| Idioma | Português do Brasil (`pt_BR`) |
| Padrão de URL | `/qual-melhor-{produto}` (slug direto na raiz) |
| Padrão de título | "Qual [o] Melhor {Produto}? {N} {Modelos/Opções} para {Benefício}" |

---

## 1. Mapa de páginas (todas as rotas)

| Rota | Tipo | Indexação | Função |
|---|---|---|---|
| `/` | Homepage | index | Hero + destaques + grade de artigos + paginação |
| `/?page=N` | Paginação | index | Lista paginada (até 166) |
| `/qual-melhor-{produto}` | **Artigo** | index | Página-dinheiro: ranking + afiliados |
| `/autores/{slug}` | Autor | index | Bio e artigos do autor |
| `/sobre-nos` | Institucional | index | Quem somos |
| `/contato` | Institucional | index | Formulário / e-mail |
| `/diretrizes-de-conteudo` | Institucional | index | Metodologia "Como avaliamos" |
| `/politica-de-privacidade` | Legal | index | LGPD / cookies / afiliados |
| `/termos-de-uso` | Legal | index | Termos |

**Regra de ordem de rota:** o slug dinâmico `/{produto}` deve ser resolvido **depois** das rotas fixas (`/autores`, `/sobre-nos`, etc.) para não interceptá-las.

---

## 2. Anatomia da HOMEPAGE (bloco a bloco)

1. **Header fixo**
   - Logo (wordmark + ícone) à esquerda, link para `/`.
   - Sem menu horizontal extenso; navegação principal vive no footer.

2. **Faixa de destaques ("Destaque")**
   - 2–3 artigos em evidência com selo "Destaque" + data.

3. **Hero editorial**
   - H1: *"Reviews honestos para sua próxima compra"*
   - Subtítulo: *"Análises diretas, comparativos e recomendações baseadas em testes reais."*
   - Sem imagem de banner pesada; texto sobre fundo claro.

4. **Grade de artigos**
   - Cards uniformes: título + data + microlink "Ler análise".
   - ~40 cards por página, ordenados por data (mais recente primeiro).

5. **Paginação**
   - "← Anterior · Página X de 166 · Próxima →".

6. **Footer** (ver §6).

---

## 3. Anatomia do ARTIGO (a página que converte — detalhe máximo)

Ordem exata dos blocos, de cima para baixo:

1. **Breadcrumb** — `Início / {Título do artigo}`.
2. **H1** — título completo ("Qual Melhor {Produto}? {N} Opções para {Benefício}").
3. **Bloco do autor** — avatar circular + nome (linkado) + data + tempo de leitura ("11 min de leitura").
4. **"Destaques do Ranking"** — carrossel horizontal com N mini-cards (imagem + nome curto + "Ver detalhes"). Contador "10 itens".
5. **"Sumário do artigo"** — índice com âncoras (`#criterios...`, `#1-produto...`, `#perguntas-frequentes`).
6. **Parágrafo de introdução** — 4–6 linhas, promessa + escopo.
7. **"Critérios Essenciais na Escolha de {Produto}"** — lista de 6–8 critérios em negrito + explicação.
8. **Seção de contexto/comparação** — ex.: "Comum vs. Enriquecido: qual a melhor opção?" (texto corrido educativo).
9. **Disclaimer de afiliado inline** — "Nossas análises são independentes. Se você comprar usando nossos links… podemos receber uma pequena comissão — sem custo para você." + link para a metodologia.
10. **Cards de produto numerados (1…N)** — unidade repetível, ver §3.1.
11. **Guia de decisão** — ex.: "Qual tamanho/embalagem ideal para você?" (texto + bullets por perfil de uso).
12. **"Perguntas Frequentes"** — 5–8 pares pergunta/resposta.
13. **"Quem escreveu este artigo"** — 1–2 bios completas de autor.
14. **"Artigos Relacionados"** — grade de 6 cards.
15. **Footer**.

### 3.1 Card de produto (componente-chave, repetido N vezes)

```
┌─────────────────────────────────────────────┐
│ [SELO: "Nossa escolha" / "Custo-benefício"]  │  ← badge opcional
│                                              │
│            [IMAGEM DO PRODUTO]               │  ← link p/ marketplace
│                                              │
│  Recomendado · Atualizado: DD/MM/AAAA        │
│                                              │
│  ### {Nome do produto}  (H3, linkado)        │
│  "Confira os detalhes e o preço atual        │
│   nos nossos parceiros."                     │
│                                              │
│  [ Mercado Livre ]  [ Shopee ]               │  ← botões de loja
│                                              │
│  {Parágrafo 1 — pontos positivos}            │
│  {Parágrafo 2 — ressalvas/limitações}        │
│                                              │
│  #### Prós                                    │
│   • item • item • item • item                │
│  #### Contras                                 │
│   • item • item • item                       │
└─────────────────────────────────────────────┘
```

**Selos usados no original:** `Maior desempenho`, `Nossa escolha`, `Custo-benefício`, `Bom e barato`, `Recomendado`. O primeiro card sempre recebe um selo; os demais podem vir sem.

---

## 4. Página de METODOLOGIA ("Como avaliamos")

Blocos: (1) headline "Transparência acima de tudo"; (2) "Pacto com o consumidor" — 3 pilares (Ética/Independência, Visão 360°, Ajuda Prática); (3) **"Metodologia em 5 fases"** numeradas (Seleção → Análise da comunidade → Validação de performance → Redação → Auditoria); (4) escala de pontuação por estrelas (1★ a 5★ com rótulos); (5) "O que priorizamos / O que nunca fazemos"; (6) citação assinada; (7) CTA para contato.

---

## 5. Sistema de afiliados e marketplaces

| Marketplace | Formato de link observado |
|---|---|
| Mercado Livre | `lista.mercadolivre.com.br/{busca}?matt_word=cortapreco&matt_tool={id}&forceInApp=true` |
| Shopee | `shopee.com.br/search?keyword={busca}&utm_medium=affiliates&utm_source={id}&utm_term={id}` |

Observações:
- Os links vão para **busca por palavra-chave**, não para SKU fixo (reduz link quebrado, mas perde precisão de preço).
- A imagem vem do CDN da Amazon, mas o **destino de compra é ML/Shopee** — descasamento imagem↔loja.
- **Sempre HTTPS** e host allowlisted. No seu app, mantenha o redirecionamento com registro de clique antes do `302`.

---

## 6. Footer (padrão em todas as páginas)

- **Logo + descrição** curta da marca.
- **Bloco "Transparência"** — aviso de comissão de afiliado.
- **Navegação:** Quem Somos · Fale Conosco · Como Avaliamos · Privacidade · Termos.
- **Social:** X, Instagram, Facebook, YouTube.
- **Copyright** + "CNPJ disponível mediante solicitação" + e-mail ofuscado.

---

## 7. SEO técnico a replicar

| Elemento | Regra |
|---|---|
| `<title>` | "{Título} \| {MARCA}" |
| `meta-description` | Promessa + número de opções + benefício |
| `meta-keywords` | Cauda longa por variação de intenção |
| Open Graph + Twitter | `summary_large_image`, imagem 1200×628 |
| `og:type` | `website` na home, `article` no post |
| Canonical | Absoluto, sem barra final |
| `theme-color` | Cor de marca |
| Robots | `index, follow, max-image-preview:large` |
| JSON-LD recomendado | `Article`, `FAQPage`, `BreadcrumbList` |
| Sitemap | Home + artigos publicados |

---

## 8. CAMADA DE DIFERENCIAÇÃO (para o novo site não ser clone)

### 8.1 Nome (escolher 1 — evitar "Guia/Qual/Compare")

| Opção | Tom | Voz sugerida |
|---|---|---|
| **Vale o Clique** | direto, memorável | "Decida antes de gastar." |
| **Antes de Comprar** | consultivo | "A pesquisa que faltava." |
| **Ponto de Escolha** | editorial | "Menos dúvida, melhor compra." |
| **Achado Certo** | popular/BR | "O que vale a pena, sem enrolação." |

### 8.2 Paleta (fugir do verde `#47962d` do original)

**Direção A — "Índigo & Âmbar" (recomendada):** confiável e diferente do verde padrão do nicho.

| Papel | Hex |
|---|---|
| Fundo | `#FAFAF9` (off-white quente) |
| Texto | `#1C1917` (quase-preto) |
| Primária | `#4338CA` (índigo) |
| Acento/CTA | `#F59E0B` (âmbar) |
| Sucesso/prós | `#15803D` |
| Alerta/contras | `#B91C1C` |

**Direção B — "Grafite & Coral":** fundo `#FDFCFB`, texto `#18181B`, primária grafite `#27272A`, acento coral `#FB7185`.

**Direção C — "Petróleo & Mostarda":** primária `#0F766E`, acento `#CA8A04` (aproxima da linha editorial do seu Compare Mais, se quiser coerência de portfólio).

### 8.3 Tipografia (diferente do sans genérico)

- **Títulos:** serifa de alto contraste (ex.: *Fraunces*, *Playfair Display*, *Lora*).
- **Corpo:** sans legível (ex.: *Inter*, *Source Sans 3*).
- **Dados/preço:** mono ou tabular (ex.: *IBM Plex Mono*) para o bloco de preço estimado.

### 8.4 Variações de formato (para não repetir o layout)

| Original | Troca sugerida |
|---|---|
| Carrossel "Destaques do Ranking" | **Tabela comparativa fixa** no topo (produto × critério) |
| Nota em estrelas 1★–5★ | **Barra "índice de recomendação"** ou selo "Veredito" textual (evita nota fabricada) |
| Cards empilhados verticais | **Linha comparativa horizontal** com "melhor escolha" fixa (sticky) |
| Selo só no 1º card | Selos por **caso de uso** ("Melhor p/ quem tem pressa", "Melhor barato") |

---

## 9. AJUSTE EDITORIAL OBRIGATÓRIO (risco a corrigir na cópia)

O original apoia-se em afirmações que **não se deve reproduzir** sem lastro (risco CONAR/CDC e ToS de afiliados):

| Não replicar | Substituir por |
|---|---|
| "10 Modelos **Testados**" / "testes reais" | "10 opções analisadas" / "seleção comentada" |
| Notas em estrelas fabricadas | "Veredito" qualitativo sustentado pelo texto |
| Persona que "testa em laboratório" | Autoria real ou "Redação" + método honesto |
| "Milhares de opiniões de compradores" | "Leitura de avaliações públicas" (sem número inventado) |
| Preço como garantia | "Preço estimado — confirme na loja" |

Manter **sempre** o disclaimer de afiliado visível.

---

## 10. PROMPT PRONTO PARA A HOSTINGER (colar no builder)

> A IA da Hostinger gera o **esqueleto visual e páginas-modelo**. A escala de milhares de artigos e o redirecionamento de afiliado exigem app próprio depois. Use o prompt abaixo para o visual + páginas-base.

```
Crie um site editorial de guias de compra em português do Brasil chamado
"Vale o Clique" (voz: "Decida antes de gastar").

Tipo: blog/portal de reviews e comparativos de produtos com links de afiliado
para Mercado Livre e Shopee. NÃO é loja virtual.

Identidade visual:
- Fundo off-white quente (#FAFAF9), texto quase-preto (#1C1917)
- Cor primária índigo (#4338CA), botões/CTA em âmbar (#F59E0B)
- Prós em verde (#15803D), contras em vermelho (#B91C1C)
- Títulos em fonte serifada de alto contraste (Fraunces); corpo em Inter
- Muito espaço em branco, cards limpos, regras finas, zero cara de marketplace

Páginas:
1. Home: cabeçalho com logo; hero com headline "Reviews honestos para sua
   próxima compra" e subtítulo curto; grade de cards de artigo (título + data
   + "Ler análise"); paginação no rodapé.
2. Modelo de Artigo "Qual melhor {produto}": breadcrumb; título H1; bloco de
   autor (foto, nome, data, tempo de leitura); tabela comparativa no topo;
   sumário com âncoras; introdução; seção "Critérios essenciais"; aviso de
   afiliado; lista numerada de 5 a 10 produtos, cada um com imagem, selo de
   destaque, botões "Mercado Livre" e "Shopee", 2 parágrafos, listas de Prós
   e Contras; seção FAQ; bio do autor; artigos relacionados.
3. Como Avaliamos: pilares de transparência + metodologia em 5 fases.
4. Sobre Nós, Fale Conosco (formulário), Política de Privacidade, Termos de Uso.

Rodapé em todas as páginas: descrição da marca, aviso de comissão de afiliado,
links de navegação e ícones sociais (X, Instagram, Facebook, YouTube).

SEO: títulos no formato "{Título} | Vale o Clique", meta description com
benefício, Open Graph com imagem grande, dados estruturados de Article e FAQ.

Regras de conteúdo: não afirmar que produtos foram testados em laboratório,
não usar notas em estrelas inventadas, tratar preço como "estimado — confirme
na loja". Sempre exibir o aviso de transparência de afiliado.
```

---

## 11. Checklist do que a Hostinger NÃO resolve sozinha

- [ ] Geração programática de milhares de artigos (precisa de CMS/app + pipeline).
- [ ] Rota de redirecionamento com **registro de clique** antes do `302`.
- [ ] Allowlist de hosts de afiliado + validação HTTPS.
- [ ] Sitemap dinâmico de artigos publicados.
- [ ] JSON-LD por artigo (Article/FAQ/Breadcrumb).
- [ ] Painel editorial para publicar/editar em escala.

> Para esses itens, o stack do Compare Mais (React + Vite SSR + Express + tRPC + Drizzle) já entrega o motor; a Hostinger cobre hospedagem Node e o visual-base.
