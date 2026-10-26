# 🎭 Adivinha o Meu Número — Carnaval

Jogo de carnaval em formato **PWA**: o vendedor da barraca escolhe um número de **1 a 10** e escreve no papel. Você tem **3 tentativas** para adivinhar. Acertar na mosca vale o **prêmio máximo**; chegar a um número vizinho (aproximado) vale um **brinde de consolação**.

Feito com HTML, CSS e JavaScript puro — sem dependências, sem build e funcionando **offline** após a primeira visita.

## Como jogar

1. Toque em um número de 1 a 10.
2. Se errar, o vendedor diz se o número é **maior** ou **menor**.
3. Você tem 3 tentativas por rodada.
4. Acertou? 🏆 Máscara de Ouro. Passou pertinho? 🎊 Confetes premiados.
5. O placar (prêmios, rodadas e melhor sequência) fica salvo no aparelho.

No teclado: teclas **1–9** e **0** (para o 10).

## Rodar localmente

O service worker (modo offline/instalação) só funciona em **localhost** ou **HTTPS**. Abrir o `index.html` direto com `file://` não ativa o PWA.

```bash
# na pasta do projeto
python3 -m http.server 8080
```

Depois abra <http://localhost:8080>.

Alternativas: `npx serve .`, `npx http-server .` ou publique em qualquer hospedagem estática com HTTPS (GitHub Pages, Netlify, Vercel etc.).

## Instalar como aplicativo

- **Android / Chrome:** toque no botão **Instalar** no topo ou no aviso do navegador.
- **iPhone / Safari:** toque em **Compartilhar** → **Adicionar à Tela de Início** (o app mostra um guia).
- **Desktop / Chrome ou Edge:** use o ícone de instalação na barra de endereço ou o botão **Instalar**.

O app instalado abre em tela cheia, com ícone próprio e funciona sem internet.

## Recursos

- Mobile first, layout fluido de 320 px a desktop, com áreas seguras (notch).
- Botões grandes (≥ 44 px), foco visível e suporte a teclado.
- Feedback acessível com `aria-live`, `role="status"` e rótulos descritivos.
- Sons gerados via WebAudio (com botão para ligar/desligar e preferência salva).
- Confete em canvas, respeitando `prefers-reduced-motion`.
- Placar persistido em `localStorage`.
- Service worker com cache do app shell, funcionamento offline e aviso de atualização.
- Manifest com ícones `any` + `maskable`, atalho "Jogar agora" e modo `standalone`.

## Estrutura

```
.
├── index.html            # marcação e telas
├── style.css             # tema de carnaval, responsivo
├── app.js                # lógica do jogo, som, confete, PWA
├── manifest.json         # configuração de instalação
├── sw.js                 # service worker (cache/offline)
└── icons/                # ícones 192/512, maskable, Apple e favicon
```

## Personalizar

- **Número máximo / tentativas:** constantes `MAX_NUMBER` e `MAX_ATTEMPTS` no topo de `app.js`.
- **Cores:** variáveis `--pink`, `--gold`, `--teal`, `--purple` e `--bg` em `style.css`.
- **Textos dos prêmios:** função `showPrizeDialog()` em `app.js`.
- **Cache:** ao publicar mudanças, incremente `CACHE_NAME` em `sw.js` (ex.: `v2`) para os usuários receberem a atualização.
