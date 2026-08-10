# Projeto · Advertorial "Purelly" (Cannella di Ceylon) — Clone + Tracking 🇮🇹

> Workspace **separado** do projeto de copy. Aqui é a **página advertorial** (clone Shopify + PostHog), não os criativos.
> A base de copy/criativos vive em `~/copys-bb-skool` (outro projeto). Cruzar quando precisar alinhar copy da página com os anúncios.

## O que é
Advertorial de **Cannella di Ceylon** para o mercado **italiano**, clonado da loja Shopify `purelywell.online/pages/purelly`.
- **Local:** `~/purelly-clone` · **GitHub:** `caiqueads1-oss/purelly-clone` (branch `main`)
- **No ar:** https://purelly-canella.vercel.app  (domínio futuro: migrar p/ um `.online` mais confiável — a definir)
- **Como funciona:** snapshot **HTML estático** (`index.html`, ~707KB) com `<base href="https://purelywell.online/">` injetado → CSS/JS/imagens e links de compra resolvem para a Shopify real.
- **Botão de compra →** `purelywell.online/products/cannella-di-ceylon-equivalente-a-7200-mg-con-olio-mct`
- **Limitações:** não atualiza sozinho se editarem no GemPages; depende da Shopify no ar; carrinho AJAX pode falhar (compra funciona via redirect).

## Contas
- GitHub `caiqueads1-oss` · Vercel `caiqueads1-3619` · PostHog região **US** (`https://us.i.posthog.com`).
- Deploy: `vercel --prod` (CLI em `~/.local/bin/vercel`). `gh` em `~/.local/bin/gh`.

## Tracking (PostHog no advertorial)
- Ativos e verificados ao vivo (`200 OK`): autocapture, pageview/pageleave, heatmaps.
- **Eventos customizados:** `scroll_depth` (25/50/75/90/100), `section_viewed` (onde abandonam), `cta_click` (`text`, `href`, `scroll_percent`, `seconds_on_page`).
- **Session Replay: DESLIGADO** (escolha do usuário — ligar em Settings → Project → Replay se quiser).
- **Divisão:** PostHog só no advertorial; **WeTracked** na página de produto (Shopify). O `cta_click` é a ponte entre os dois.
- Funil sugerido: `$pageview → scroll_depth(50) → scroll_depth(90) → cta_click`.

## Estado vigente da página
- **Descontos nos CTAs:** os **4** botões dizem "Risparmia fino al **50%**" (um deles "+ Spedizione Gratuita"), alinhados à página de produto.
- **Avaliações:** **9.584** em todos os pontos (mesmo número da página de produto).
- **Headline atual:** *"Il Motivo per cui Migliaia di Italiani con Glicemia Alta Stanno Passando alla Cannella di Ceylon"* (sub: *"E Perché i Loro Medici Notano la Differenza nei Valori di Glicemia e Reni"*).
- **Título da aba / og:title / twitter:title:** "Cannella di Ceylon Purelly | Supporto Glicemia e Energia".
- **FAQ de farmacoterapia** ("Posso Prenderla Insieme alle Mie Medicine?") no fim da página, antes da barra sticky.

> ⚠️ **A página de produto é a fonte da verdade.** Ela não deve ser editada (decisão do usuário: está boa, tem FAQ, garantia, comparativo e assinatura). Quando um número divergir, ajuste o **advertorial** para bater com ela.

> ⚠️ **Editar CTA = 2 ocorrências por botão.** O GemPages guarda cada botão duas vezes no HTML: uma escapada dentro de atributo (`&lt;/p&gt;`) e uma renderizada. Trocar só uma quebra a consistência.

## ⚠️ Pendências abertas (auditoria da copy — NÃO corrigidas)
1. **Compliance (mais grave):** a copy faz **alegações de doença** (reduzir dano renal, melhorar GFR/creatinina, baixar A1C, "médico dividiu a metformina", evitar diálise). Na UE/Itália suplemento **não pode** alegar tratar/prevenir doença → risco de ban Meta/Google + risco legal. (Mesmo alerta do concorrente Gluconol, desmascarado pelo BUTAC.)
2. **Marca inconsistente:** alterna "PurelyWell" (22×) vs "Purelly" (5×), inclusive nas reviews e na embalagem das fotos → padronizar.
3. **Urgência artificial:** countdown + "Rischio Esaurimento Scorte: Alto" → pode reduzir confiança.
4. **Asterisco (\*) sem legenda** nas estatísticas (84/79/76/71%).
5. **Estatísticas divergem entre as páginas:** advertorial 84/79/76/71% vs produto 86/72/91/79%.
6. **Oferta "compra 2 leva 3"** ainda convive com o "fino al 50%" — idealmente 1 oferta principal.

### Imagens com texto em inglês (não dá pra corrigir por HTML)
O texto está **nos pixels**, nos assets do CDN da Shopify. Corrigir exige refazer a imagem (GemPages/Shopify) ou hospedar substituta no próprio repo e trocar o `src`.
- `DM_20260615180052_002.jpg` — "Before / Insulin Resistance" · "After / Healthy Insulin Signaling"
- `DM_20260615180052_006.jpg` — "Cassia Cinnamon" · "Ceylon Cinnamon"
- `DM_20260615180052_007.jpg` — selo "Fairtrade Farmers" + "Mathew Reed, RD" (credencial anglófona)
- `9.jpg`, `7_*.jpg`, `8_*.jpg` — embalagem diz **"Equivalente a 1200mg"** (o texto da página alega 7.200 mg) e traz texto de IA corrompido ("Setiea Glutiha", "Tectito in Lsberatorio")

## Pendências técnicas
- [ ] Definir/configurar domínio `.online` no Vercel (+ opcional: PostHog → Toolbar → Authorized URLs).
- [ ] (Opcional) Funil de abandono no PostHog (precisa Personal API Key).
- [ ] (Opcional) Ajustar título da aba/favicon (hoje mostra nome interno do GemPages).
- [ ] (Futuro) Cross-domain PostHog: advertorial → produto → compra.

## Histórico completo
Nota detalhada no Obsidian: `Sessões Claude/2026-07-05 - Setup GitHub, Vercel, Clone Purelly, PostHog e Obsidian.md`.
