# digital-security<!doctype html><html><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#fff;color:#000}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Segurança digital, na prática</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  /* Layout: coluna única de 760px, seções separadas por fios finos; testes e jogos em painéis com borda. Visual escuro único, mantido do site original. */
  :root {
    --bg: #0B0F14;
    --panel: #12181F;
    --panel-2: #171F28;
    --ink: #F3F5F7;
    --muted: #8B96A5;
    --yellow: #FFD23F;
    --mint: #5EEAD4;
    --red: #FF5468;
    --orange: #FF9F43;
    --line: rgba(255,255,255,0.08);
    --font-display: 'Space Grotesk', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    --font-mono: 'JetBrains Mono', 'SF Mono', Consolas, monospace;
    color-scheme: dark;
  }
  html { scroll-behavior: smooth; scroll-padding-top: calc(env(safe-area-inset-top, 0px) + 64px); }
  * { box-sizing: border-box; }
  [hidden] { display: none !important; }
  body {
    margin: 0;
    background: var(--bg);
    color: var(--ink);
    font-family: var(--font-display);
    font-size: 16px;
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
  }
  body::before {
    content: ""; position: fixed; inset: 0 0 auto; height: env(safe-area-inset-top, 0px);
    background: var(--bg); z-index: 20;
  }
  ::selection { background: var(--yellow); color: #0B0F14; }
  a { color: var(--mint); }

  .wrap {
    max-width: 760px; margin: 0 auto;
    padding-left: max(24px, env(safe-area-inset-left, 0px));
    padding-right: max(24px, env(safe-area-inset-right, 0px));
  }
  section { padding-block: 72px; border-bottom: 1px solid var(--line); }
  section:last-of-type { border-bottom: none; }

  /* nav */
  nav {
    position: sticky; top: env(safe-area-inset-top, 0px);
    background: rgba(11,15,20,0.9);
    backdrop-filter: blur(8px);
    border-bottom: 1px solid var(--line);
    z-index: 10;
  }
  nav .wrap { display: flex; gap: 10px; padding-block: 14px; overflow-x: auto; }
  nav a {
    font-family: var(--font-mono); font-size: 12.5px;
    color: var(--muted); text-decoration: none; white-space: nowrap;
    border: 1px solid var(--line); border-radius: 20px; padding: 6px 12px;
    transition: color .15s ease, border-color .15s ease;
  }
  nav a:hover { color: var(--ink); border-color: var(--muted); }

  /* hero */
  .hero { padding-top: clamp(44px, 8vh, 88px); padding-bottom: 60px; }
  .kicker { font-family: var(--font-mono); font-size: 14px; color: var(--mint); margin: 0 0 18px; }
  h1 {
    font-size: clamp(30px, 6vw, 48px);
    font-weight: 700; line-height: 1.1; letter-spacing: -0.02em;
    margin: 0 0 20px; max-width: 14ch; text-wrap: balance;
  }
  .sub { color: var(--muted); font-size: 18px; max-width: 52ch; margin: 0 0 16px; }
  .sub2 { color: var(--muted); font-size: 16px; max-width: 54ch; margin: 0; }

  h2 {
    font-size: clamp(22px, 4vw, 28px);
    font-weight: 700; letter-spacing: -0.01em;
    margin: 0 0 14px; max-width: 26ch; text-wrap: balance;
  }
  h3.sub-h {
    font-size: 18px; font-weight: 700; margin: 48px 0 8px;
  }
  p.lead { color: var(--muted); font-size: 16px; max-width: 56ch; margin: 0 0 32px; }
  p.lead.tight { margin-bottom: 20px; }

  /* numbered list */
  .numlist { display: flex; flex-direction: column; }
  .numlist .item { display: flex; gap: 18px; padding: 22px 0; border-top: 1px solid var(--line); }
  .numlist .item:last-child { border-bottom: 1px solid var(--line); }
  .numlist .mark { font-family: var(--font-mono); font-size: 13px; color: var(--yellow); padding-top: 3px; width: 26px; flex-shrink: 0; }
  .numlist .body { min-width: 0; }
  .numlist .body h3 { margin: 0 0 6px; font-size: 17px; font-weight: 600; }
  .numlist .body p { margin: 0; color: var(--muted); font-size: 15px; }

  /* password tester */
  .tester { background: var(--panel); border: 1px solid var(--line); border-radius: 14px; padding: 28px; }
  .tester label { display: block; font-size: 13px; color: var(--muted); margin-bottom: 10px; }
  .input-row { display: flex; gap: 10px; }
  #pwInput {
    flex: 1; min-width: 0;
    background: var(--bg); border: 1.5px solid var(--line); border-radius: 8px;
    padding: 14px 16px; font-family: var(--font-mono); font-size: 17px; color: var(--ink);
    outline: none; transition: border-color .2s ease;
  }
  #pwInput:focus { border-color: var(--mint); }
  .btn-ghost {
    background: var(--bg); border: 1.5px solid var(--line); border-radius: 8px;
    color: var(--muted); font-family: var(--font-mono); font-size: 13px;
    padding: 0 16px; cursor: pointer;
  }
  .btn-ghost:hover { color: var(--ink); border-color: var(--muted); }
  .meter-track { height: 6px; background: var(--bg); border-radius: 3px; margin-top: 18px; overflow: hidden; }
  .meter-fill { height: 100%; width: 0%; background: var(--red); border-radius: 3px; transition: width .35s ease, background-color .35s ease; }
  .result { margin-top: 22px; }
  .result-label { font-size: 13px; color: var(--muted); margin-bottom: 6px; }
  .result-time {
    font-family: var(--font-mono); font-size: clamp(24px, 5vw, 36px); font-weight: 700;
    color: var(--yellow); word-break: break-word;
  }
  .result-note { font-size: 14px; color: var(--muted); margin-top: 8px; min-height: 20px; }
  .fineprint { font-size: 13px; color: var(--muted); margin: 18px 0 0; max-width: 60ch; }

  /* comparison bars */
  .bars { display: flex; flex-direction: column; gap: 22px; margin-top: 8px; }
  .bar-label { display: flex; justify-content: space-between; gap: 14px; font-family: var(--font-mono); font-size: 14px; margin-bottom: 8px; }
  .bar-label .pw { color: var(--ink); min-width: 0; word-break: break-all; }
  .bar-label .t { color: var(--muted); text-align: right; }
  .bar-track { height: 10px; background: var(--panel); border-radius: 5px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 5px; }

  /* common passwords */
  .list-head { display: flex; justify-content: space-between; font-size: 12px; color: var(--muted); padding-bottom: 6px; }
  .list-row {
    display: flex; align-items: center; justify-content: space-between; gap: 16px;
    padding: 14px 0; border-top: 1px solid var(--line); font-family: var(--font-mono);
  }
  .list-row:last-child { border-bottom: 1px solid var(--line); }
  .list-row .rank { color: var(--muted); font-size: 13px; width: 24px; flex-shrink: 0; }
  .list-row .word { font-size: 16px; flex: 1; min-width: 0; }
  .list-row .time { color: var(--red); font-size: 14px; white-space: nowrap; }

  /* generator */
  .gen-box { background: var(--panel); border: 1px solid var(--line); border-radius: 14px; padding: 28px; }
  .gen-output {
    font-family: var(--font-mono); font-size: clamp(17px, 3.4vw, 24px); color: var(--mint);
    background: var(--bg); border-radius: 8px; padding: 16px; word-break: break-all;
    border: 1px solid var(--line); margin-bottom: 16px; user-select: all;
  }
  .gen-actions { display: flex; gap: 10px; flex-wrap: wrap; }

  /* buttons */
  .btn {
    border: none; border-radius: 10px; font-family: var(--font-display);
    font-weight: 700; font-size: 15px; padding: 13px 22px; cursor: pointer;
    color: #0B0F14; transition: transform .1s ease;
  }
  .btn:active { transform: scale(0.97); }
  .btn-mint { background: var(--mint); }
  .btn-yellow { background: var(--yellow); }
  .btn.copied { background: var(--yellow); }

  /* checklist */
  .check-item { display: flex; align-items: flex-start; gap: 14px; padding: 16px 0; border-top: 1px solid var(--line); cursor: pointer; }
  #checklistItems .check-item:last-child { border-bottom: 1px solid var(--line); }
  .check-box {
    width: 22px; height: 22px; flex-shrink: 0; margin-top: 1px;
    border: 1.5px solid var(--muted); border-radius: 6px;
    display: flex; align-items: center; justify-content: center;
    transition: border-color .15s ease, background-color .15s ease;
  }
  .check-item.done .check-box { background: var(--mint); border-color: var(--mint); }
  .check-box svg { width: 13px; height: 13px; opacity: 0; transition: opacity .1s ease; }
  .check-item.done .check-box svg { opacity: 1; }
  .check-text { font-size: 15.5px; color: var(--ink); min-width: 0; transition: color .15s ease, opacity .15s ease; }
  .check-item.done .check-text { color: var(--muted); text-decoration: line-through; opacity: 0.8; }
  .check-progress { font-family: var(--font-mono); font-size: 13px; color: var(--muted); margin: 18px 0 0; }

  /* glossary */
  .gloss { display: flex; flex-direction: column; gap: 10px; }
  .gloss details { background: var(--panel); border: 1px solid var(--line); border-radius: 10px; padding: 4px 18px; }
  .gloss summary {
    cursor: pointer; list-style: none; padding: 14px 0; font-weight: 600; font-size: 15.5px;
    display: flex; justify-content: space-between; align-items: center; gap: 12px;
  }
  .gloss summary::-webkit-details-marker { display: none; }
  .gloss summary .plus { font-family: var(--font-mono); color: var(--mint); font-size: 18px; transition: transform .2s ease; }
  .gloss details[open] summary .plus { transform: rotate(45deg); }
  .gloss .def { color: var(--muted); font-size: 14.5px; padding: 0 0 16px; margin: 0; }

  /* games */
  .games { display: flex; flex-direction: column; gap: 24px; }
  .game { background: var(--panel); border: 1px solid var(--line); border-radius: 14px; padding: 28px; min-width: 0; }
  .tag {
    display: inline-block; font-family: var(--font-mono); font-size: 11px; color: var(--mint);
    border: 1px solid var(--line); border-radius: 20px; padding: 3px 10px; margin: 0 0 14px;
  }
  .game h3 { margin: 0 0 8px; font-size: 21px; font-weight: 700; }
  .game-intro p.desc { margin: 0 0 20px; color: var(--muted); font-size: 15px; max-width: 52ch; }

  .hud { display: flex; align-items: center; gap: 12px; margin-bottom: 20px; }
  .track { flex: 1; height: 6px; background: var(--bg); border-radius: 3px; overflow: hidden; }
  .fill { height: 100%; width: 0%; background: var(--mint); border-radius: 3px; transition: width .35s ease; }
  .score { font-family: var(--font-mono); font-size: 13px; color: var(--muted); white-space: nowrap; }
  .timer { width: 56px; height: 6px; background: var(--bg); border-radius: 3px; overflow: hidden; flex-shrink: 0; }
  .timer .fill { width: 100%; transition: width .1s linear, background-color .2s ease; }

  .round-card { background: var(--bg); border: 1px solid var(--line); border-radius: 12px; padding: 22px; animation: cardIn .3s ease; }
  @keyframes cardIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  .msg-meta { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 14px; gap: 10px; }
  .msg-type { font-family: var(--font-mono); font-size: 11px; color: var(--muted); border: 1px solid var(--line); border-radius: 20px; padding: 3px 10px; white-space: nowrap; }
  .msg-from { font-family: var(--font-mono); font-size: 13px; color: var(--ink); word-break: break-all; min-width: 0; }
  .msg-body { font-size: 16px; line-height: 1.55; color: var(--ink); }
  .msg-body .subject { font-weight: 600; display: block; margin-bottom: 8px; }

  .choices { display: flex; gap: 12px; margin-top: 22px; }
  .choice-btn, .opt-btn {
    background: var(--panel); border: 1.5px solid var(--line); border-radius: 10px;
    color: var(--ink); cursor: pointer; transition: border-color .15s ease, transform .1s ease;
  }
  .choice-btn { flex: 1; font-family: var(--font-display); font-weight: 600; font-size: 15px; padding: 16px 10px; }
  .choice-btn:hover, .opt-btn:hover { border-color: var(--muted); }
  .choice-btn:active, .opt-btn:active { transform: scale(0.98); }
  .choice-btn:disabled, .opt-btn:disabled { cursor: default; }
  .choice-btn.correct, .opt-btn.correct { border-color: var(--mint); background: rgba(94,234,212,0.1); }
  .choice-btn.wrong, .opt-btn.wrong { border-color: var(--red); background: rgba(255,84,104,0.1); }

  .brand-name { font-size: 20px; font-weight: 700; margin: 0 0 4px; }
  .brand-hint { color: var(--muted); font-size: 14px; margin: 0 0 18px; }
  .options { display: flex; flex-direction: column; gap: 10px; }
  .opt-btn { text-align: left; font-family: var(--font-mono); font-size: 15px; padding: 14px 16px; word-break: break-all; }

  .feedback {
    margin-top: 18px; border-radius: 10px; padding: 16px 18px; font-size: 14px; line-height: 1.5;
    border: 1px solid var(--line); color: var(--muted); animation: cardIn .3s ease;
  }
  .feedback.correct { background: rgba(94,234,212,0.1); border-color: var(--mint); color: var(--ink); }
  .feedback.wrong { background: rgba(255,84,104,0.1); border-color: var(--red); color: var(--ink); }
  .feedback strong { color: var(--ink); font-family: var(--font-mono); font-weight: 600; word-break: break-all; }
  .fverdict { display: block; font-family: var(--font-mono); font-size: 12px; margin-bottom: 6px; }
  .feedback.correct .fverdict { color: var(--mint); }
  .feedback.wrong .fverdict { color: var(--red); }
  .next-btn { display: block; width: 100%; margin-top: 16px; }

  .end-score { font-family: var(--font-mono); font-size: clamp(44px, 14vw, 64px); font-weight: 700; color: var(--yellow); margin: 6px 0 4px; }
  .end-label { color: var(--muted); font-size: 14px; margin: 0 0 20px; }
  .end-msg { font-size: 16px; margin: 0 0 24px; max-width: 52ch; }

  footer { padding: 56px 0; color: var(--muted); font-size: 14px; }

  @media (max-width: 520px) {
    section { padding-block: 52px; }
    .tester, .gen-box, .game { padding: 20px; }
    .round-card { padding: 18px; }
    .input-row { flex-direction: column; }
    .btn-ghost { padding: 10px; }
  }
  @media (prefers-reduced-motion: reduce) {
    * { animation-duration: .01ms !important; transition-duration: .01ms !important; scroll-behavior: auto !important; }
  }
  :focus-visible { outline: 2px solid var(--mint); outline-offset: 2px; }
</style>

<nav>
  <div class="wrap">
    <a href="#riscos">golpes comuns</a>
    <a href="#senhas">senhas</a>
    <a href="#checklist">checklist</a>
    <a href="#glossario">glossário</a>
    <a href="#socorro">se você caiu em um golpe</a>
    <a href="#testar">testar</a>
  </div>
</nav>

<div class="wrap">

  <section class="hero">
    <p class="kicker">segurança digital</p>
    <h1>A maioria dos golpes não precisa de hacker nenhum — só de um clique apressado</h1>
    <p class="sub">Senha fraca, link disfarçado e e-mail com pressa artificial resolvem a maior parte do trabalho de quem quer te enganar.</p>
    <p class="sub2">Esta página reúne o básico que realmente importa: os golpes mais comuns, como montar uma senha que aguenta, um checklist rápido, um glossário dos termos que aparecem por aí, o que fazer se você já caiu em algum golpe — e três testes práticos: um medidor de senha e dois jogos contra o relógio.</p>
  </section>

  <section id="riscos">
    <h2>Os golpes mais comuns</h2>
    <p class="lead">Táticas diferentes, mesmo objetivo: te fazer agir rápido demais para pensar.</p>
    <div class="numlist">
      <div class="item">
        <div class="mark">01</div>
        <div class="body">
          <h3>Phishing</h3>
          <p>E-mails que imitam bancos, lojas ou serviços, geralmente com um domínio levemente diferente do real, pedindo para "atualizar dados" ou "confirmar acesso".</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">02</div>
        <div class="body">
          <h3>Smishing</h3>
          <p>A mesma lógica do phishing, mas por SMS — avisos falsos de Pix recebido, fatura vencendo ou encomenda retida, sempre com um link curto e atraente.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">03</div>
        <div class="body">
          <h3>Vishing</h3>
          <p>Golpe por ligação telefônica. Alguém se passa por "segurança do banco" e, com calma e autoridade na voz, convence a vítima a passar senhas ou códigos de confirmação.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">04</div>
        <div class="body">
          <h3>Quishing</h3>
          <p>A versão em QR code do phishing. O código leva a uma página falsa, e como ninguém "lê" um QR code antes de escanear, o golpe passa mais despercebido.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">05</div>
        <div class="body">
          <h3>Engenharia social</h3>
          <p>Manipulação psicológica pura — golpe do parente em apuros, falso suporte técnico, falsa doação urgente. Não precisa invadir nada: só precisa que você confie na hora errada.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">06</div>
        <div class="body">
          <h3>Links e domínios falsos</h3>
          <p>Endereços quase idênticos aos originais — uma letra trocada, um hífen a mais, um "0" no lugar de um "o" — levam a páginas feitas só para roubar dados digitados nelas.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">07</div>
        <div class="body">
          <h3>Wi-Fi público sem proteção</h3>
          <p>Em redes abertas, o tráfego pode ser interceptado por quem estiver na mesma rede. Evite login em contas sensíveis assim, a menos que use uma VPN.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="senhas">
    <h2>Como montar uma senha que aguenta</h2>
    <p class="lead">Não é sobre decorar símbolos malucos — é sobre comprimento e imprevisibilidade.</p>

    <div class="tester" id="medidor">
      <label for="pwInput">Teste uma senha (de verdade ou fake: nada sai do seu navegador)</label>
      <div class="input-row">
        <input id="pwInput" type="password" autocomplete="off" spellcheck="false" placeholder="digite aqui..." />
        <button id="pwToggle" class="btn-ghost" type="button">mostrar</button>
      </div>
      <div class="meter-track"><div class="meter-fill" id="meterFill"></div></div>
      <div class="result">
        <div class="result-label">tempo estimado para quebrar</div>
        <div class="result-time" id="resultTime">—</div>
        <div class="result-note" id="resultNote"></div>
      </div>
      <p class="fineprint">Estimativa simples: considera o comprimento, os tipos de caractere e um ataque offline de 10 bilhões de tentativas por segundo. Senhas feitas de palavras comuns ou padrões previsíveis caem bem mais rápido do que o número mostra.</p>
    </div>

    <h3 class="sub-h">Comprimento e variedade mudam tudo</h3>
    <p class="lead tight">Cada caractere extra multiplica as combinações possíveis. Veja quatro escolhas comuns, calculadas com a mesma conta do medidor.</p>
    <div class="bars" id="barList"></div>

    <h3 class="sub-h">Cinco hábitos que fazem a diferença</h3>
    <div class="numlist" style="margin-top: 16px;">
      <div class="item">
        <div class="mark">01</div>
        <div class="body">
          <h3>Priorize o comprimento</h3>
          <p>16 caracteres aleatórios batem qualquer senha curta cheia de símbolos. Cada caractere a mais multiplica o número de combinações possíveis.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">02</div>
        <div class="body">
          <h3>Use frases, não palavras</h3>
          <p>Quatro palavras sem relação entre si — "girafa-toalha-cometa-42" — são longas, fáceis de lembrar e difíceis de adivinhar por tentativa.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">03</div>
        <div class="body">
          <h3>Nunca reutilize</h3>
          <p>Uma senha vazada em um site vira a chave de todos os outros onde você a usou. Cada conta importante merece a sua própria.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">04</div>
        <div class="body">
          <h3>Ative a autenticação de dois fatores</h3>
          <p>Mesmo que a senha vaze, um segundo código (no celular ou num app autenticador) impede o acesso. É a camada que realmente detém a maioria dos ataques.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">05</div>
        <div class="body">
          <h3>Deixe um gerenciador lembrar por você</h3>
          <p>Ninguém decora vinte senhas fortes. Um gerenciador de senhas cria e guarda isso — você só precisa lembrar de uma.</p>
        </div>
      </div>
    </div>

    <h3 class="sub-h">As senhas favoritas do mundo inteiro</h3>
    <p class="lead tight">Algumas das senhas mais usadas globalmente. Todas caem instantaneamente, porque estão na primeira lista que qualquer invasor testa.</p>
    <div class="list-head"><span>senha</span><span>tempo até quebrar</span></div>
    <div id="commonList"></div>

    <h3 class="sub-h">Ou gere uma agora</h3>
    <p class="lead tight">Uma senha aleatória de 16 caracteres, criada no seu navegador.</p>
    <div class="gen-box">
      <div class="gen-output" id="genOutput" aria-live="polite"></div>
      <div class="gen-actions">
        <button class="btn btn-mint" id="genBtn" type="button">gerar outra</button>
        <button class="btn-ghost" id="copyBtn" type="button" style="padding: 12px 18px;">copiar</button>
      </div>
    </div>
  </section>

  <section id="checklist">
    <h2>Checklist rápido</h2>
    <p class="lead">Sete hábitos que cobrem a maior parte do risco. Marque o que você já faz.</p>
    <div id="checklistItems"></div>
    <p class="check-progress" id="checkProgress"></p>
  </section>

  <section id="glossario">
    <h2>Glossário</h2>
    <p class="lead">Os termos que aparecem quando o assunto é golpe digital.</p>
    <div class="gloss">
      <details>
        <summary>Phishing <span class="plus">+</span></summary>
        <p class="def">Tentativa de roubar dados se passando por uma empresa ou pessoa confiável, geralmente por e-mail.</p>
      </details>
      <details>
        <summary>Smishing <span class="plus">+</span></summary>
        <p class="def">A mesma tática do phishing, só que aplicada por SMS.</p>
      </details>
      <details>
        <summary>Vishing <span class="plus">+</span></summary>
        <p class="def">Golpe aplicado por ligação telefônica, muitas vezes fingindo ser o banco ou um órgão oficial.</p>
      </details>
      <details>
        <summary>Quishing <span class="plus">+</span></summary>
        <p class="def">Phishing feito através de QR codes que levam a páginas falsas em vez de um link de texto clicável.</p>
      </details>
      <details>
        <summary>Engenharia social <span class="plus">+</span></summary>
        <p class="def">Manipulação psicológica para fazer alguém revelar informações ou agir contra o próprio interesse, sem precisar invadir nada tecnicamente.</p>
      </details>
      <details>
        <summary>Malware <span class="plus">+</span></summary>
        <p class="def">Qualquer programa malicioso criado para roubar dados, espionar ou danificar um dispositivo.</p>
      </details>
      <details>
        <summary>Ransomware <span class="plus">+</span></summary>
        <p class="def">Tipo de malware que bloqueia ou criptografa seus arquivos e exige pagamento para liberá-los.</p>
      </details>
      <details>
        <summary>Autenticação de dois fatores (2FA) <span class="plus">+</span></summary>
        <p class="def">Uma segunda confirmação além da senha — como um código enviado ao celular — que impede acesso mesmo se a senha vazar.</p>
      </details>
      <details>
        <summary>VPN <span class="plus">+</span></summary>
        <p class="def">Camada que criptografa sua conexão com a internet, útil principalmente para navegar com mais segurança em redes Wi-Fi públicas.</p>
      </details>
      <details>
        <summary>Typosquatting <span class="plus">+</span></summary>
        <p class="def">Registro de domínios com erros de digitação propositais de marcas reais (ex: "amaz0n.com"), usados em golpes de link falso.</p>
      </details>
    </div>
  </section>

  <section id="socorro">
    <h2>Se você já caiu em um golpe</h2>
    <p class="lead">Agir rápido limita o estrago. A ordem importa.</p>
    <div class="numlist">
      <div class="item">
        <div class="mark">01</div>
        <div class="body">
          <h3>Troque a senha na hora</h3>
          <p>Da conta afetada e de qualquer outro lugar onde você usava a mesma senha.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">02</div>
        <div class="body">
          <h3>Ative a autenticação de dois fatores</h3>
          <p>Se a conta ainda não tinha, esse é o momento. Isso bloqueia a maioria das tentativas de reacesso.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">03</div>
        <div class="body">
          <h3>Contate o serviço pelo canal oficial</h3>
          <p>Use o app ou o telefone impresso no cartão — nunca um link ou número que veio na própria mensagem suspeita.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">04</div>
        <div class="body">
          <h3>Monitore extratos e faturas</h3>
          <p>Acompanhe os próximos dias de perto. Movimentações estranhas, mesmo pequenas, valem contestação imediata.</p>
        </div>
      </div>
      <div class="item">
        <div class="mark">05</div>
        <div class="body">
          <h3>Denuncie</h3>
          <p>Pelo canal do banco ou serviço afetado e, se fizer sentido, em uma delegacia ou no gov.br. Isso ajuda a bloquear o golpe para outras pessoas também.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="testar">
    <h2>Teste na prática</h2>
    <p class="lead">Três exercícios rápidos. O primeiro, o <a href="#medidor">medidor de senha</a>, fica na seção de senhas. Os outros dois são jogos contra o relógio e estão aqui.</p>
    <div class="games">

      <div class="game" id="gamePhish">
        <div data-view="start">
          <p class="tag">e-mail e SMS · modo difícil</p>
          <h3>Isso é phishing?</h3>
          <p class="desc">14 mensagens sutis: algumas legítimas parecem alarmantes, algumas falsas parecem profissionais. Você tem 10 segundos por rodada para decidir se é golpe ou não.</p>
          <button type="button" class="btn btn-mint" data-act="start">começar</button>
        </div>
        <div data-view="play" hidden>
          <div class="hud">
            <div class="track"><div class="fill" data-el="progress"></div></div>
            <span class="score" data-el="score">0 / 14</span>
            <div class="timer"><div class="fill" data-el="timer"></div></div>
          </div>
          <div data-el="stage"></div>
        </div>
        <div data-view="end" hidden>
          <p class="tag">resultado</p>
          <div class="end-score" data-el="endScore">0/14</div>
          <p class="end-label">mensagens identificadas corretamente</p>
          <p class="end-msg" data-el="endMsg"></p>
          <button type="button" class="btn btn-mint" data-act="restart">jogar de novo</button>
        </div>
      </div>

      <div class="game" id="gameLinks">
        <div data-view="start">
          <p class="tag">links falsos</p>
          <h3>Ache o link verdadeiro</h3>
          <p class="desc">Golpistas registram domínios quase idênticos aos originais. Em 14 rodadas de 8 segundos, clique no único endereço que pertence de verdade à marca.</p>
          <button type="button" class="btn btn-yellow" data-act="start">começar</button>
        </div>
        <div data-view="play" hidden>
          <div class="hud">
            <div class="track"><div class="fill" data-el="progress"></div></div>
            <span class="score" data-el="score">0 / 14</span>
            <div class="timer"><div class="fill" data-el="timer"></div></div>
          </div>
          <div data-el="stage"></div>
        </div>
        <div data-view="end" hidden>
          <p class="tag">resultado</p>
          <div class="end-score" data-el="endScore">0/14</div>
          <p class="end-label">domínios reais identificados</p>
          <p class="end-msg" data-el="endMsg"></p>
          <button type="button" class="btn btn-yellow" data-act="restart">jogar de novo</button>
        </div>
      </div>

    </div>
  </section>

  <footer>
    nenhum dado digitado em nenhum teste desta página sai do seu navegador.
  </footer>

</div>

<script>
(function () {
  // ---------- helpers ----------
  function esc(s) {
    return String(s).replace(/[&<>"']/g, function (c) {
      return { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c];
    });
  }
  function shuffle(arr) {
    var a = arr.slice();
    for (var i = a.length - 1; i > 0; i--) {
      var j = Math.floor(Math.random() * (i + 1));
      var t = a[i]; a[i] = a[j]; a[j] = t;
    }
    return a;
  }

  // ---------- password strength ----------
  var COMMON = ["123456","password","123456789","12345678","qwerty","abc123","password1","111111","123123","letmein","welcome","monkey","dragon","iloveyou","admin"];
  var YEAR = 3600 * 24 * 365;

  function charsetSize(pw) {
    var size = 0;
    if (/[a-z]/.test(pw)) size += 26;
    if (/[A-Z]/.test(pw)) size += 26;
    if (/[0-9]/.test(pw)) size += 10;
    if (/[^a-zA-Z0-9]/.test(pw)) size += 32;
    return size || 1;
  }
  function secondsToCrack(pw) {
    if (!pw) return 0;
    if (COMMON.indexOf(pw.toLowerCase()) !== -1) return 0.0001;
    var entropy = pw.length * Math.log2(charsetSize(pw));
    return Math.pow(2, entropy) / (2 * 1e10); // ataque offline, hardware moderno
  }
  function formatTime(s) {
    if (s < 0.01) return "instantâneo";
    if (s < 1) return "menos de 1 segundo";
    var units = [
      [60, 1, "segundo", "segundos"],
      [3600, 60, "minuto", "minutos"],
      [86400, 3600, "hora", "horas"],
      [YEAR, 86400, "dia", "dias"],
      [YEAR * 1000, YEAR, "ano", "anos"],
      [YEAR * 1e6, YEAR * 1000, "mil anos", "mil anos"],
      [YEAR * 1e9, YEAR * 1e6, "milhão de anos", "milhões de anos"]
    ];
    for (var i = 0; i < units.length; i++) {
      var u = units[i];
      if (s < u[0]) {
        var v = s / u[1];
        var r = v < 10 ? Math.round(v * 10) / 10 : Math.round(v);
        return String(r).replace(".", ",") + " " + (r === 1 ? u[2] : u[3]);
      }
    }
    return "mais de um bilhão de anos";
  }
  function strengthColor(s) {
    if (s < 1) return "var(--red)";
    if (s < 3600 * 24 * 30) return "var(--orange)";
    if (s < YEAR * 10) return "var(--yellow)";
    return "var(--mint)";
  }
  function strengthPercent(s) {
    if (s <= 0) return 2;
    var years = s / YEAR;
    return Math.max(2, Math.min(100, (Math.log10(years + 1) / 12) * 100));
  }

  var pwInput = document.getElementById('pwInput');
  var meterFill = document.getElementById('meterFill');
  var resultTime = document.getElementById('resultTime');
  var resultNote = document.getElementById('resultNote');
  var pwToggle = document.getElementById('pwToggle');

  pwInput.addEventListener('input', function () {
    var val = pwInput.value;
    if (!val) {
      meterFill.style.width = "0%";
      resultTime.textContent = "—";
      resultTime.style.color = "";
      resultNote.textContent = "";
      return;
    }
    var seconds = secondsToCrack(val);
    var color = strengthColor(seconds);
    meterFill.style.width = strengthPercent(seconds) + "%";
    meterFill.style.background = color;
    resultTime.textContent = formatTime(seconds);
    resultTime.style.color = color;
    if (COMMON.indexOf(val.toLowerCase()) !== -1) {
      resultNote.textContent = "essa está entre as senhas mais usadas do mundo.";
    } else if (val.length < 8) {
      resultNote.textContent = "curta demais — cada caractere a mais ajuda muito.";
    } else if (seconds > YEAR * 100) {
      resultNote.textContent = "essa aguentaria uma tentativa séria de invasão.";
    } else {
      resultNote.textContent = "dá pra melhorar: mais comprimento, menos padrão previsível.";
    }
  });
  pwToggle.addEventListener('click', function () {
    var showing = pwInput.type === 'text';
    pwInput.type = showing ? 'password' : 'text';
    pwToggle.textContent = showing ? 'mostrar' : 'ocultar';
  });

  // comparison bars (mesma conta do medidor)
  var COMPARE = ["senha123", "Senha123!", "girafa-azul-42", "K9#mQ2$vL8@pX4nR"];
  var barList = document.getElementById('barList');
  var maxLog = Math.log10(secondsToCrack(COMPARE[COMPARE.length - 1]) + 1);
  COMPARE.forEach(function (pw) {
    var s = secondsToCrack(pw);
    var pct = Math.max(3, (Math.log10(s + 1) / maxLog) * 100);
    var row = document.createElement('div');
    row.innerHTML =
      '<div class="bar-label"><span class="pw">' + esc(pw) + '</span><span class="t">' + esc(formatTime(s)) + '</span></div>' +
      '<div class="bar-track"><div class="bar-fill" style="width:' + pct.toFixed(1) + '%;background:' + strengthColor(s) + '"></div></div>';
    barList.appendChild(row);
  });

  // common passwords
  var commonList = document.getElementById('commonList');
  COMMON.slice(0, 10).forEach(function (pw, i) {
    var row = document.createElement('div');
    row.className = 'list-row';
    row.innerHTML = '<span class="rank">' + (i + 1) + '</span><span class="word">' + esc(pw) + '</span><span class="time">instantâneo</span>';
    commonList.appendChild(row);
  });

  // generator
  var CHARS = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*-_=+";
  function randInt(max) {
    var limit = Math.floor(4294967296 / max) * max;
    var buf = new Uint32Array(1);
    do { crypto.getRandomValues(buf); } while (buf[0] >= limit);
    return buf[0] % max;
  }
  function generatePassword(len) {
    var out = "";
    for (var i = 0; i < len; i++) out += CHARS[randInt(CHARS.length)];
    return out;
  }
  var genOutput = document.getElementById('genOutput');
  var genBtn = document.getElementById('genBtn');
  var copyBtn = document.getElementById('copyBtn');
  genOutput.textContent = generatePassword(16);
  genBtn.addEventListener('click', function () {
    genOutput.textContent = generatePassword(16);
    copyBtn.textContent = "copiar";
  });
  copyBtn.addEventListener('click', function () {
    var text = genOutput.textContent;
    function selectFallback() {
      var range = document.createRange();
      range.selectNodeContents(genOutput);
      var sel = window.getSelection();
      sel.removeAllRanges();
      sel.addRange(range);
      copyBtn.textContent = "selecionada";
    }
    try {
      navigator.clipboard.writeText(text).then(function () {
        copyBtn.textContent = "copiada!";
        setTimeout(function () { copyBtn.textContent = "copiar"; }, 1400);
      }, selectFallback);
    } catch (e) { selectFallback(); }
  });

  // ---------- checklist ----------
  var CHECKLIST_ITEMS = [
    "Ativei a autenticação de dois fatores nas contas mais importantes (e-mail, banco, redes sociais)",
    "Uso um gerenciador de senhas",
    "Nunca reutilizo a mesma senha em mais de um lugar",
    "Verifico o domínio antes de clicar em links recebidos por e-mail ou SMS",
    "Desconfio de qualquer mensagem com urgência artificial",
    "Evito login em contas sensíveis em Wi-Fi público sem VPN",
    "Mantenho o sistema e os apps atualizados"
  ];
  var STORAGE_KEY = "seguranca-digital-checklist";
  function loadState() {
    try { var raw = localStorage.getItem(STORAGE_KEY); return raw ? JSON.parse(raw) : {}; }
    catch (e) { return {}; }
  }
  function saveState(st) {
    try { localStorage.setItem(STORAGE_KEY, JSON.stringify(st)); } catch (e) { /* segue sem salvar */ }
  }
  var listEl = document.getElementById('checklistItems');
  var progressEl = document.getElementById('checkProgress');
  var state = loadState();
  function renderChecklist() {
    listEl.innerHTML = "";
    CHECKLIST_ITEMS.forEach(function (text, i) {
      var row = document.createElement('div');
      row.className = 'check-item' + (state[i] ? ' done' : '');
      row.setAttribute('role', 'checkbox');
      row.setAttribute('aria-checked', state[i] ? 'true' : 'false');
      row.tabIndex = 0;
      row.innerHTML =
        '<div class="check-box"><svg viewBox="0 0 24 24" fill="none" stroke="#0B0F14" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg></div>' +
        '<div class="check-text">' + esc(text) + '</div>';
      function toggle() { state[i] = !state[i]; saveState(state); renderChecklist(); var rows = listEl.children; if (rows[i]) rows[i].focus(); }
      row.addEventListener('click', toggle);
      row.addEventListener('keydown', function (e) {
        if (e.key === ' ' || e.key === 'Enter') { e.preventDefault(); toggle(); }
      });
      listEl.appendChild(row);
    });
    var count = Object.keys(state).filter(function (k) { return state[k]; }).length;
    progressEl.textContent = count + " de " + CHECKLIST_ITEMS.length + " hábitos já em dia";
  }
  renderChecklist();

  // ---------- game engine ----------
  function makeGame(root, cfg) {
    function el(n) { return root.querySelector('[data-el="' + n + '"]'); }
    function view(n) { return root.querySelector('[data-view="' + n + '"]'); }
    var progress = el('progress'), scoreEl = el('score'), timerEl = el('timer'), stage = el('stage');
    var endScore = el('endScore'), endMsg = el('endMsg');
    var total = cfg.rounds.length;
    var order = [], current = 0, score = 0, answered = false, raf = 0;

    function show(name) {
      ['start', 'play', 'end'].forEach(function (n) { view(n).hidden = (n !== name); });
    }
    function hud() {
      scoreEl.textContent = score + " / " + total;
      progress.style.width = (current / total * 100) + "%";
    }
    function revealNext() {
      var next = stage.querySelector('[data-act="next"]');
      next.hidden = false;
      next.scrollIntoView({ block: 'nearest' });
    }
    function begin() {
      order = shuffle(cfg.rounds.map(function (_, i) { return i; }));
      current = 0; score = 0;
      show('play');
      hud();
      round();
      root.scrollIntoView({ block: 'nearest' });
    }
    function round() {
      if (current >= total) { finish(); return; }
      answered = false;
      var r = cfg.rounds[order[current]];
      stage.innerHTML = cfg.card(r);
      var next = stage.querySelector('[data-act="next"]');
      next.textContent = current === total - 1 ? 'ver resultado' : 'próxima';
      next.addEventListener('click', function () { current++; hud(); round(); });
      cfg.wire(stage, function (value) { pick(r, value); });
      runTimer(r);
    }
    function pick(r, value) {
      if (answered) return;
      answered = true;
      cancelAnimationFrame(raf);
      var correct = cfg.judge(r, value);
      if (correct) score++;
      scoreEl.textContent = score + " / " + total;
      cfg.reveal(stage, r, { value: value, correct: correct, timedOut: false });
      revealNext();
    }
    function runTimer(r) {
      var t0 = performance.now();
      timerEl.style.width = "100%";
      timerEl.style.background = "var(--mint)";
      cancelAnimationFrame(raf);
      function tick(now) {
        if (answered) return;
        var pct = Math.min(1, Math.max(0, 1 - (now - t0) / cfg.time));
        timerEl.style.width = (pct * 100) + "%";
        timerEl.style.background = pct < 0.3 ? "var(--red)" : pct < 0.6 ? "var(--yellow)" : "var(--mint)";
        if (pct <= 0) {
          answered = true;
          cfg.reveal(stage, r, { value: null, correct: false, timedOut: true });
          revealNext();
          return;
        }
        raf = requestAnimationFrame(tick);
      }
      raf = requestAnimationFrame(tick);
    }
    function finish() {
      cancelAnimationFrame(raf);
      progress.style.width = "100%";
      stage.innerHTML = "";
      endScore.textContent = score + "/" + total;
      endMsg.textContent = cfg.endText(score, total);
      show('end');
    }
    root.querySelector('[data-act="start"]').addEventListener('click', begin);
    root.querySelector('[data-act="restart"]').addEventListener('click', begin);
  }

  // ---------- game 1: isso é phishing? ----------
  var PHISH = [
    { type: "e-mail", from: "Banco Itaú <atendimento@itau-atualiza.com.br>", subject: "Atualização cadastral obrigatória",
      body: "Para continuar usando sua conta normalmente, atualize seus dados cadastrais pelo aplicativo até o fim do mês.", isPhishing: true,
      why: "O domínio real é itau.com.br — 'itau-atualiza.com.br' é um domínio parecido, mas diferente. Sem a urgência de horas, fica mais difícil perceber, então o hábito de checar o domínio é o que salva aqui." },
    { type: "e-mail", from: "Nubank <no-reply@nubank.com.br>", subject: "Detectamos uma tentativa de login incomum",
      body: "Se foi você, pode ignorar esta mensagem. Se não reconhece esse acesso, abra o app e revise os dispositivos conectados.", isPhishing: false,
      why: "Domínio oficial nubank.com.br, e o alerta direciona para dentro do app em vez de um link externo — mesmo soando alarmante, é o padrão real de segurança." },
    { type: "e-mail", from: "Suporte Google <security-noreply@accounts-google.com>", subject: "Alguém tentou acessar sua conta Google",
      body: "Clique para revisar a atividade recente e proteger sua conta agora.", isPhishing: true,
      why: "O domínio oficial do Google é accounts.google.com (subdomínio de google.com). 'accounts-google.com' é um domínio totalmente diferente, só parecido na aparência." },
    { type: "e-mail", from: "Uber <uber@uber.com>", subject: "",
      body: "Sua viagem terminou. Avalie o motorista e confira o recibo no app.", isPhishing: false,
      why: "Domínio oficial uber.com, mensagem curta e informativa, sem link pedindo dados — típico e-mail pós-viagem real." },
    { type: "e-mail", from: "Amazon <pedidos@amazon-br.shop>", subject: "Problema com o pedido #482910",
      body: "Não conseguimos processar o pagamento do seu pedido. Atualize o cartão para evitar o cancelamento.", isPhishing: true,
      why: "'amazon-br.shop' não é domínio da Amazon (o real é amazon.com.br). O número de pedido específico é só um detalhe pra parecer mais real." },
    { type: "e-mail", from: "Banco Bradesco <fraude@bradesco.com.br>", subject: "Bloqueio preventivo de cartão",
      body: "Identificamos uma compra fora do padrão e bloqueamos seu cartão por segurança. Ligue para o número no verso do cartão para confirmar.", isPhishing: false,
      why: "Domínio oficial bradesco.com.br, e a ação pedida é ligar para o número impresso no próprio cartão — um canal que você mesmo verifica, não um link." },
    { type: "SMS", from: "BANCO", subject: "",
      body: "Sua fatura de R$ 2.340,00 vence hoje. Evite juros, pague agora: bradesc0-pagamentos.com", isPhishing: true,
      why: "Repare no '0' no lugar do 'o' em 'bradesc0' — troca de caractere clássica. O remetente 'BANCO' genérico também pode ser forjado em SMS." },
    { type: "e-mail", from: "Spotify <no-reply@spotify.com>", subject: "Sua assinatura foi renovada",
      body: "Cobramos R$ 21,90 referente ao plano Premium deste mês. Veja os detalhes no app.", isPhishing: false,
      why: "Domínio oficial spotify.com, tom informativo e rotineiro, sem link pressionando clique — cobrança normal de assinatura." },
    { type: "e-mail", from: "RH <rh@empresa-corp.com>", subject: "Atualize seus dados bancários",
      body: "Para o próximo pagamento de salário, confirme seus dados bancários preenchendo o formulário em anexo.", isPhishing: true,
      why: "O domínio da empresa real seria algo como empresa.com.br — 'empresa-corp.com' é diferente. RH raramente pede dados bancários por formulário de e-mail." },
    { type: "SMS", from: "PIX RECEBIDO", subject: "",
      body: "Você recebeu R$ 45,00 via Pix de Maria Souza às 14:32.", isPhishing: false,
      why: "Apenas informa o recebimento, sem pedir clique, confirmação ou dado nenhum — é exatamente como uma notificação real de Pix se parece." },
    { type: "e-mail", from: "Correios <rastreio@correios-entrega.com>", subject: "Encomenda retida por falta de pagamento de taxa",
      body: "Sua encomenda está retida na unidade de triagem. Pague a taxa de R$ 14,90 para liberar a entrega.", isPhishing: true,
      why: "O domínio oficial é correios.com.br. Os Correios não cobram 'taxas de liberação' por link em SMS ou e-mail — é um dos golpes mais comuns no Brasil." },
    { type: "e-mail", from: "GitHub <noreply@github.com>", subject: "New sign-in to your account",
      body: "We noticed a new sign-in to your account from a new device. If this was you, no action is needed.", isPhishing: false,
      why: "Domínio oficial github.com, apenas informa sem exigir ação nem link de 'verificação' — padrão real de aviso de segurança." },
    { type: "e-mail", from: "WhatsApp <verificacao@whatsapp-suporte.com>", subject: "",
      body: "Seu WhatsApp será desativado em 24h por violar os termos de uso. Cancele o processo clicando no link abaixo.", isPhishing: true,
      why: "'whatsapp-suporte.com' não pertence à Meta/WhatsApp. Na prática, o WhatsApp praticamente não manda avisos assim por e-mail." },
    { type: "e-mail", from: "Banco Inter <atendimento@bancointer.com.br>", subject: "Seu limite do cartão foi aumentado",
      body: "Boas notícias! Seu limite passou para R$ 3.200,00. Consulte os detalhes no app Inter.", isPhishing: false,
      why: "Domínio oficial bancointer.com.br, conteúdo positivo e não urgente, direciona para o app oficial em vez de um link externo." }
  ];

  makeGame(document.getElementById('gamePhish'), {
    rounds: PHISH,
    time: 10000,
    card: function (r) {
      return '<div class="round-card">' +
        '<div class="msg-meta"><span class="msg-from">' + esc(r.from) + '</span><span class="msg-type">' + esc(r.type) + '</span></div>' +
        '<div class="msg-body">' + (r.subject ? '<span class="subject">' + esc(r.subject) + '</span>' : '') + esc(r.body) + '</div>' +
        '<div class="choices">' +
          '<button type="button" class="choice-btn" data-choice="legit">É real</button>' +
          '<button type="button" class="choice-btn" data-choice="scam">É golpe</button>' +
        '</div>' +
        '<div class="feedback" hidden></div>' +
        '<button type="button" class="btn btn-yellow next-btn" data-act="next" hidden>próxima</button>' +
      '</div>';
    },
    wire: function (stage, pick) {
      stage.querySelectorAll('.choice-btn').forEach(function (b) {
        b.addEventListener('click', function () { pick(b.dataset.choice); });
      });
    },
    judge: function (r, value) { return (value === 'scam') === r.isPhishing; },
    reveal: function (stage, r, res) {
      var correctChoice = r.isPhishing ? 'scam' : 'legit';
      stage.querySelectorAll('.choice-btn').forEach(function (b) {
        b.disabled = true;
        if (b.dataset.choice === correctChoice) b.classList.add('correct');
        else if (!res.timedOut && b.dataset.choice === res.value) b.classList.add('wrong');
      });
      var fb = stage.querySelector('.feedback');
      fb.hidden = false;
      fb.className = 'feedback ' + (res.correct ? 'correct' : 'wrong');
      var lead = res.timedOut ? 'tempo esgotado — ' : res.correct ? 'certo — ' : 'quase — ';
      var verdict = r.isPhishing ? 'isso era golpe' : 'isso era legítimo';
      fb.innerHTML = '<span class="fverdict">' + lead + verdict + '</span>' + esc(r.why);
    },
    endText: function (score, total) {
      if (score === total) return "Perfeito. Nem as mensagens mais sutis passaram batido.";
      if (score >= total * 0.7) return "Muito bom — você pega a maioria dos sinais, mesmo os disfarçados.";
      if (score >= total * 0.4) return "Deu pra pegar alguns, mas os disfarces mais sutis ainda enganam. Vale sempre checar o domínio com calma.";
      return "Modo difícil de verdade: aqui nem tom alarmante nem tom calmo é garantia de nada — o domínio é o que conta.";
    }
  });

  // ---------- game 2: ache o link verdadeiro ----------
  var LINKS = [
    { brand: "Banco do Brasil", real: "bb.com.br", fakes: ["bancodobrasil-online.com", "bb-seguranca.net", "bb.com.br.acesso.com"] },
    { brand: "Mercado Livre", real: "mercadolivre.com.br", fakes: ["mercadolivre-promocoes.com", "mercado-livre.com", "mercadolivree.com.br"] },
    { brand: "WhatsApp Web", real: "web.whatsapp.com", fakes: ["whatsapp-web.net", "web-whatsapp.com", "whatsappweb.com.br"] },
    { brand: "Receita Federal", real: "gov.br/receitafederal", fakes: ["receita.gov.com", "receitafederal.net", "receita-restituicao.com"] },
    { brand: "Netflix", real: "netflix.com", fakes: ["netflix-br-cobranca.com", "netflix.com.atualizacao.net", "netflix-login.com"] },
    { brand: "Instagram", real: "instagram.com", fakes: ["instagram-verificacao.com", "instagran.com", "insta-gram.com"] },
    { brand: "PayPal", real: "paypal.com", fakes: ["paypal-secure.net", "paypa1.com", "paypal.com-verificar.info"] },
    { brand: "Nubank", real: "nubank.com.br", fakes: ["nu-bank.com", "nubank-app.net", "nubankoficial.com"] },
    { brand: "Google", real: "google.com", fakes: ["goog1e.com", "google-verificacao.com", "google.com.acesso.net"] },
    { brand: "Caixa Econômica Federal", real: "caixa.gov.br", fakes: ["caixa-economica.net", "caixa.com.br.acesso.com", "caixaonline.info"] },
    { brand: "Amazon", real: "amazon.com.br", fakes: ["amazon-br.shop", "amaz0n.com", "amazon.com.br.pedidos.net"] },
    { brand: "iFood", real: "ifood.com.br", fakes: ["i-food.com", "ifood-promocoes.com", "ifoodbrasil.net"] },
    { brand: "99", real: "99app.com", fakes: ["99-taxi.com", "noventaenove.com.br", "99app.com.br-oficial.com"] },
    { brand: "Correios", real: "correios.com.br", fakes: ["correios-entrega.com", "correios.gov.com", "rastreio-correios.net"] }
  ];

  makeGame(document.getElementById('gameLinks'), {
    rounds: LINKS,
    time: 8000,
    card: function (r) {
      var options = shuffle([r.real].concat(r.fakes));
      return '<div class="round-card">' +
        '<p class="brand-name">' + esc(r.brand) + '</p>' +
        '<p class="brand-hint">Qual destes é o endereço oficial?</p>' +
        '<div class="options">' +
          options.map(function (o) { return '<button type="button" class="opt-btn" data-opt="' + esc(o) + '">' + esc(o) + '</button>'; }).join('') +
        '</div>' +
        '<div class="feedback" hidden></div>' +
        '<button type="button" class="btn btn-yellow next-btn" data-act="next" hidden>próxima</button>' +
      '</div>';
    },
    wire: function (stage, pick) {
      stage.querySelectorAll('.opt-btn').forEach(function (b) {
        b.addEventListener('click', function () { pick(b.dataset.opt); });
      });
    },
    judge: function (r, value) { return value === r.real; },
    reveal: function (stage, r, res) {
      stage.querySelectorAll('.opt-btn').forEach(function (b) {
        b.disabled = true;
        if (b.dataset.opt === r.real) b.classList.add('correct');
        else if (!res.timedOut && b.dataset.opt === res.value) b.classList.add('wrong');
      });
      var fb = stage.querySelector('.feedback');
      fb.hidden = false;
      fb.className = 'feedback ' + (res.correct ? 'correct' : 'wrong');
      var real = '<strong>' + esc(r.real) + '</strong>';
      if (res.timedOut) fb.innerHTML = 'Tempo esgotado. O endereço real é ' + real + '; os outros são domínios parecidos criados para enganar.';
      else if (res.correct) fb.innerHTML = 'Isso mesmo. ' + real + ' é o endereço oficial de ' + esc(r.brand) + '.';
      else fb.innerHTML = 'Esse era falso. O endereço real é ' + real + '; os demais imitam a grafia para parecer confiáveis.';
    },
    endText: function (score, total) {
      if (score === total) return "Perfeito — nenhum domínio falso escapou.";
      if (score >= total * 0.7) return "Muito bom olho para detalhes de URL.";
      if (score >= total * 0.4) return "Vale o hábito de conferir o domínio antes de clicar, sempre.";
      return "Golpistas contam com pressa. Antes de clicar, olhe o endereço com calma.";
    }
  });
})();
</script>

</body></html>
