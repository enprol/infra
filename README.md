# INFRA · Utilitários (ENPROL) — app HTML

Aplicativo single-file para cadastros, laudos e anexos de processos de
desapropriação. Todo o app está em `app.html` (HTML + CSS + JS embutidos).

> Este repositório é **só o canal de publicação**. O código é editado em
> `Pagina Infra\app-html\index.html`, na máquina da ENPROL.

## Como o app é usado

O app **não** é aberto por este endereço. Em cada máquina ele abre por
`http://localhost:3000/`, servido pelo programinha local
(`servidor-cadastros/server.js`), que o baixa daqui e o entrega na mesma origem
da API. O Chrome 152+ bloqueia página `https://` falando com `http://localhost`
(*Local Network Access*), e o app chama a API por caminho relativo — aberto
direto pelo GitHub Pages ele carrega mas **não salva**.

Os cadastros são gravados no servidor offline da empresa
(`\\10.0.0.251\sala tecnica\INFRA I\#Banco_de_dados_CADASTROS`), em subpastas
por seção, com as imagens como arquivos separados em `imagens/`. Não usa
Supabase nem nenhum serviço de nuvem.

- `CAD_salvarNuvem()` / `CAD_abrirNuvem()` → `PUT` / `GET` em
  `/api/cadastros/:secao/:ctd`
- login validado só no cliente (`sessionStorage`)

## Arquivos

| Arquivo | O que é |
|---|---|
| `app.html` | o app inteiro (~9 MB). É o que o servidor local baixa |
| `index.html` | página de entrada (~2,5 KB): botão para `localhost:3000` + botões das fichas de campo + instruções de instalar o PWA. **Não é o app** — quase nunca muda |
| `campo.html` | PWA de coleta em campo (técnico) |
| `campo-social.html` | PWA da assistência social |
| `campo*.webmanifest`, `campo*-sw.js` | manifesto e service worker dos PWAs |

## Publicar uma mudança

Rodar `Pagina Infra\servidor-cadastros\publicar.bat` — ele gera o app, copia
as cópias para todos os lugares (inclusive para este clone, **só como
`app.html`**) e imprime os comandos de git no final. Depois é só rodá-los de
dentro de `Pagina Infra\github-enprol-infra\`:

```
git add -A
git commit -m "..."
git push origin main
```

**Nunca sobrescrever o `index.html` com o app.** Ele é a porta de entrada de
quem trabalha em campo; se virar o app de 9 MB, o pessoal perde o acesso aos
PWAs e recebe um app que não salva (fora do localhost).

As máquinas pegam a versão nova sozinhas em até 5 minutos (o servidor local
revalida a cada 5 min e guarda uma cópia para funcionar offline).

Ver `Pagina Infra\servidor-cadastros\README.md` para o fluxo completo e a
instalação.
