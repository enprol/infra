# INFRA · Utilitários (ENPROL) — app HTML

Aplicativo single-file para elaboração de anexos, laudos e cadastros de projetos
de infraestrutura. Todo o app está em `index.html` (HTML + CSS + JS embutidos).

## Armazenamento — servidor da empresa

Os cadastros (DESP 1, 2 e 3) são gravados no **servidor offline da empresa**
(`\\10.0.0.251\sala tecnica\INFRA I\#Banco_de_dados_CADASTROS`), em subpastas por
seção. Não usa mais Supabase nem qualquer serviço de nuvem.

O `index.html` fala com a API local (`/api/cadastros`) servida pelo
`../servidor-cadastros/server.js`, que roda em cada máquina em
`http://localhost:3000/` e é quem entrega a própria app (mesma origem — o Chrome
não deixa a página `https://` do GitHub falar direto com `http://localhost`).

- `CAD_salvarNuvem()` / `CAD_abrirNuvem()` → `PUT` / `GET` em `/api/cadastros/:secao/:ctd`
- imagens vão embutidas em base64 no próprio `cadastro.json`
- login validado só no cliente (`sessionStorage`)

## Rodar / publicar

- Dia a dia: abrir pelo atalho **"Cadastros ENPROL"** (`http://localhost:3000/`).
- Publicar mudança de layout: `../servidor-cadastros/gerar-app.bat` copia este
  `index.html` para `servidor-cadastros/app.html`; suba esse `app.html` no
  repositório GitHub `enprol/infra`. As máquinas baixam a versão nova sozinhas.
- Ver `../servidor-cadastros/README.md` para o fluxo completo e a instalação.

## Migração do Supabase antigo

`../servidor-cadastros/migrar-supabase.js` — ferramenta de uso único para trazer
os cadastros que ainda estavam no Supabase. Não faz parte da app.
