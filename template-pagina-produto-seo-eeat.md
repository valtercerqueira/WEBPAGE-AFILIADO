# Template padrão — Página "Qual Melhor {Produto}" (SEO + EEAT)

> Baseado na engenharia reversa de `guiaqualcomprar.com.br/qual-melhor-ventilador-de-teto-silencioso-com-controle`.
> Uso: copiar a Parte 3 como esqueleto de cada artigo e o schema da Parte 4 no `<head>`.
> Regra de ouro: só afirme "testado/medido" onde houver dado real. O resto é "análise/curadoria".

---

## PARTE 1 — Engenharia reversa da página (estrutura confirmada)

Padrão de URL: `/{slug-com-keyword-exata}` — sem data, sem categoria, keyword no início.
Padrão de título: `Qual [o] Melhor {Produto} {Modificador}? {N} {Modelos/Opções} {Benefício}`

Ordem dos blocos, de cima para baixo:

| # | Bloco | Conteúdo |
|---|---|---|
| 1 | Breadcrumb | `Início / {título}` |
| 2 | H1 | Título completo com keyword + número + benefício |
| 3 | Autor | Avatar + nome (link) + data + tempo de leitura |
| 4 | Destaques do Ranking | Carrossel horizontal de N mini-cards ("Ver detalhes") |
| 5 | Sumário | Índice com âncoras para cada seção e produto |
| 6 | Introdução | 3–5 linhas: dor + promessa + escopo |
| 7 | "Como Escolher o Melhor {Produto}?" | Parágrafo + 6–8 critérios em bullet |
| 8 | Disclaimer de afiliado | Inline + link para metodologia |
| 9 | "Análise Detalhada dos N Modelos" | H2 de abertura do ranking |
| 10 | Cards de produto (1…N) | Ver Parte 1.1 |
| 11 | Seção educativa A | Ex.: "Motor Inverter vs Convencional" (H2 + texto + bullets) |
| 12 | Seção educativa B | Ex.: "Funcionalidades Essenciais" (H2 + texto + bullets) |
| 13 | Perguntas Frequentes | 5–8 pares Q/A |
| 14 | "Quem escreveu este artigo" | 1–2 bios de autor |
| 15 | Artigos Relacionados | Grade de 6 cards |
| 16 | Footer | Marca + transparência + navegação + social |

### 1.1 — Card de produto (unidade repetível)

```
[SELO opcional: "Maior desempenho" / "Nossa escolha" / "Custo-benefício" / "Bom e barato"]
[IMAGEM do produto → link marketplace]
Recomendado · Atualizado: DD/MM/AAAA
### H3: {Nome/keyword do produto}: {benefício curto}
"Confira os detalhes e o preço atual nos nossos parceiros."
[ Botão Mercado Livre ] [ Botão Shopee ]
{Parágrafo 1 — para quem serve + pontos fortes}
{Parágrafo 2 — ressalvas + limitações}
#### Prós  → 3–4 bullets
#### Contras → 2–3 bullets
```

Diferenças observadas entre nichos: em produto técnico (ventilador) os H3 são descritivos com keyword secundária ("Motor DC e Controle Preciso") e há 2 seções educativas; em consumo (arroz) o H3 é só o nome. **Adote sempre o padrão técnico** (H3 descritivo) — captura mais cauda longa.

---

## PARTE 2 — Diagnóstico SEO + EEAT (o que corrigir para superar)

### O que o original acerta (manter)
- Keyword no slug, H1, title, meta e primeiro parágrafo.
- Sumário com âncoras (bom para sitelinks e navegação).
- Prós/Contras escaneáveis + FAQ (formato de resposta direta).
- Disclaimer de afiliado visível (sinal de Trust).
- Autor nomeado + página de metodologia.

### O que o original erra (sua vantagem competitiva)

| Fator | Falha | Correção no seu site |
|---|---|---|
| **Experiência (1º E do EEAT)** | Diz "testados" sem qualquer prova de uso real | Box "Como analisamos" por artigo: método, o que foi verificado, o que NÃO foi. Se não testou, escreva "seleção e análise", nunca "testado em laboratório" |
| **Dado mensurável** | Query é "silencioso", mas não há dB por modelo | Coluna de ruído (dB) na tabela; se não medir, citar spec do fabricante com fonte |
| **Tabela comparativa** | Ausente | Tabela no topo (modelo × 4–5 critérios × faixa de preço) → alvo de featured snippet |
| **Preço** | Oculto | "Faixa estimada: R$X–R$Y · confirme na loja" (transparência + intenção comercial) |
| **Autoridade** | Zero fontes externas | Bloco "Fontes": Inmetro, Procel, manual do fabricante, laudos |
| **Autor (Expertise)** | Persona sem credencial verificável | Nome real + cargo + link externo (LinkedIn/perfil) + `sameAs` no schema |
| **Consistência de data** | Meta cita ano defasado vs data do post | `datePublished` e `dateModified` corretos e iguais ao texto |
| **Arquitetura** | Tudo na raiz, sem categorias | Categorias/pilares + links internos contextuais no corpo |
| **Schema** | Sem Product/ItemList/FAQ marcados | JSON-LD completo (Parte 4) |
| **Match imagem↔loja** | Imagem Amazon, link ML/Shopee | Usar imagem da loja de destino ou própria |
| **Link de afiliado** | Vai para busca, não para SKU | Link direto ao produto (menos bounce, mais conversão) |
| **Duplicação em escala** | 6.600 páginas "qual melhor" = risco de conteúdo raso | Ângulo único por página + dado próprio, senão canibaliza |

---

## PARTE 3 — MODELO PADRÃO (copie e preencha os {{campos}})

```markdown
<!-- URL: /qual-melhor-{{keyword-slug}} -->
<!-- Title: Qual Melhor {{Produto}} {{Modificador}}? {{N}} Opções Analisadas ({{Ano}}) | {{Marca}} -->
<!-- Meta description (150–160 car.): Compare os {{N}} melhores {{produto}} {{modificador}}. {{Diferencial: dado/critério}}. Análise com prós, contras e faixa de preço para você decidir. -->

# Qual Melhor {{Produto}} {{Modificador}}? {{N}} Opções Analisadas em {{Ano}}

Por {{Autor}} · {{Cargo/credencial}} · Atualizado em {{DD/MM/AAAA}} · {{X}} min de leitura

> **Como analisamos:** {{método honesto — ex.: "Comparamos especificações oficiais, medimos o ruído de 3 unidades com decibelímetro e cruzamos com avaliações verificadas de compradores." OU, se não houver teste físico: "Análise baseada em especificações do fabricante, dados do Inmetro/Procel e leitura de avaliações públicas de compradores."}} Nossas recomendações são independentes e podem conter links de afiliado — [entenda como avaliamos]({{/metodologia}}).

## Comparativo rápido

| Modelo | {{Critério-chave (ex.: Ruído)}} | {{Critério 2 (ex.: Motor)}} | {{Critério 3}} | Faixa de preço | Melhor para |
|---|---|---|---|---|---|
| {{Modelo 1}} | {{dado}} | {{dado}} | {{dado}} | R$ {{x–y}} | {{caso de uso}} |
| {{Modelo 2}} | {{dado}} | {{dado}} | {{dado}} | R$ {{x–y}} | {{caso de uso}} |
| … | … | … | … | … | … |

## Sumário
- [Como escolher](#como-escolher)
- [As {{N}} melhores opções](#analise)
- [{{Seção educativa A}}](#edu-a)
- [{{Seção educativa B}}](#edu-b)
- [Perguntas frequentes](#faq)

## Como escolher o melhor {{produto}} {#como-escolher}
{{Parágrafo de contexto: 3–4 linhas explicando o critério decisivo do nicho.}}

- **{{Critério 1}}:** {{explicação prática}}
- **{{Critério 2}}:** {{explicação}}
- **{{Critério 3}}:** {{explicação}}
- **{{Critério 4}}:** {{explicação}}
- **{{Critério 5}}:** {{explicação}}
- **{{Critério 6}}:** {{explicação}}

## As {{N}} melhores opções de {{produto}} {#analise}

### 1. {{Nome do Produto}}: {{benefício/keyword secundária}}
**Veredito: {{selo textual — ex.: "Melhor no geral"}}** · Faixa de preço: R$ {{x–y}} · Atualizado em {{DD/MM/AAAA}}

![{{alt descritivo com keyword}}]({{imagem}})

[Ver no Mercado Livre]({{link-sku}}) · [Ver na Shopee]({{link-sku}})

{{Parágrafo 1: para quem serve + pontos fortes com dado concreto.}}
{{Parágrafo 2: ressalvas honestas + limitações.}}

**Prós**
- {{pró 1}}
- {{pró 2}}
- {{pró 3}}

**Contras**
- {{contra 1}}
- {{contra 2}}

<!-- Repetir o bloco para os produtos 2…N -->

## {{Seção educativa A — ex.: "Motor Inverter vs Convencional"}} {#edu-a}
{{Parágrafo + bullets. Aqui você captura keywords informacionais e gera dwell time.}}

## {{Seção educativa B — ex.: "Funcionalidades Essenciais"}} {#edu-b}
{{Parágrafo + bullets.}}

## Perguntas frequentes {#faq}
**{{Pergunta 1?}}**
{{Resposta objetiva em 2–3 frases.}}

**{{Pergunta 2?}}**
{{Resposta.}}
<!-- 5 a 8 perguntas, priorize as do "People Also Ask" do Google -->

## Fontes e referências
- {{Fonte 1 — ex.: Inmetro / Procel / manual do fabricante}}
- {{Fonte 2}}

## Quem escreveu este artigo
**{{Autor}}** — {{cargo e credencial real}}. {{1–2 frases de experiência}}. [Perfil]({{link-externo-verificável}})

## Artigos relacionados
- [{{Artigo pilar da categoria}}]({{url}})
- [{{Artigo relacionado 1}}]({{url}})
- [{{Artigo relacionado 2}}]({{url}})
```

---

## PARTE 4 — Schema JSON-LD pronto (colar no `<head>` de cada página)

Substitua os `{{campos}}`. Um único `<script>` com um `@graph` cobrindo Article, Breadcrumb, ItemList/Product e FAQ.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Article",
      "headline": "Qual Melhor {{Produto}} {{Modificador}}? {{N}} Opções Analisadas em {{Ano}}",
      "description": "{{meta description}}",
      "image": "{{og-image-1200x628}}",
      "datePublished": "{{AAAA-MM-DD}}",
      "dateModified": "{{AAAA-MM-DD}}",
      "author": {
        "@type": "Person",
        "name": "{{Autor}}",
        "jobTitle": "{{Cargo}}",
        "url": "{{/autores/slug}}",
        "sameAs": ["{{link LinkedIn ou perfil externo}}"]
      },
      "publisher": {
        "@type": "Organization",
        "name": "{{Marca}}",
        "logo": { "@type": "ImageObject", "url": "{{logo}}" }
      },
      "mainEntityOfPage": "{{url-canônica}}"
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "name": "Início", "item": "{{origin}}" },
        { "@type": "ListItem", "position": 2, "name": "{{Categoria}}", "item": "{{/categoria}}" },
        { "@type": "ListItem", "position": 3, "name": "{{Título}}", "item": "{{url-canônica}}" }
      ]
    },
    {
      "@type": "ItemList",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "item": {
            "@type": "Product",
            "name": "{{Produto 1}}",
            "image": "{{imagem}}",
            "description": "{{resumo}}",
            "brand": { "@type": "Brand", "name": "{{Marca do produto}}" },
            "offers": {
              "@type": "AggregateOffer",
              "priceCurrency": "BRL",
              "lowPrice": "{{x}}",
              "highPrice": "{{y}}",
              "availability": "https://schema.org/InStock",
              "url": "{{link-afiliado}}"
            }
          }
        }
        // repetir para os produtos 2…N
      ]
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "{{Pergunta 1?}}",
          "acceptedAnswer": { "@type": "Answer", "text": "{{Resposta 1}}" }
        }
        // repetir para cada pergunta
      ]
    }
  ]
}
</script>
```

> Nota: só inclua `Review`/`aggregateRating` no schema se você **de fato** tiver uma nota própria e metodologia por trás. Marcar nota inventada = risto de ação manual do Google por *spam de dados estruturados*.

---

## PARTE 5 — Checklist de publicação (por artigo)

**On-page**
- [ ] Keyword exata no slug, H1, title, meta e 1º parágrafo
- [ ] Title ≤ 60 caracteres; meta 150–160
- [ ] Tabela comparativa no topo com ≥1 dado mensurável
- [ ] Alt de imagem descritivo com keyword
- [ ] 3–5 links internos contextuais (pilar + relacionados)
- [ ] 1–2 links externos para fontes de autoridade

**EEAT**
- [ ] Box "Como analisamos" honesto (sem "testado" falso)
- [ ] Autor real com credencial + link externo (`sameAs`)
- [ ] Bloco "Fontes e referências" preenchido
- [ ] Disclaimer de afiliado visível
- [ ] Faixa de preço com "confirme na loja"

**Técnico**
- [ ] JSON-LD Article + Breadcrumb + ItemList + FAQ validado no Rich Results Test
- [ ] Canonical absoluto, sem barra final
- [ ] `dateModified` = data real da última edição
- [ ] Página no sitemap.xml → enviar/pingar no Search Console
- [ ] Core Web Vitals ok (imagens lazy + comprimidas + LiteSpeed/cache)

**Anti-canibalização (escala)**
- [ ] Ângulo/intenção único vs artigos irmãos
- [ ] Ao menos 1 dado ou seção que nenhum concorrente tem
