<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Para Malu</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    background: linear-gradient(to bottom right, #fff0f5, #ffe4e1);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    height: 100vh; display: flex; justify-content: center; align-items: center;
  }
  .container { text-align: center; }
  .start-screen { transition: opacity 0.8s ease, transform 0.8s ease; }
  .hidden { opacity: 0; pointer-events: none; transform: scale(0.95); }
  .start-screen h1 { font-size: 2em; color: #6b2c2c; margin-bottom: 20px; }
  .start-screen button {
    background-color: #ff5e99; border: none; border-radius: 8px; padding: 12px 24px;
    font-size: 1.1em; color: white; cursor: pointer; box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    transition: background-color 0.3s ease;
  }
  .start-screen button:hover { background-color: #ff3c85; }
  .envelope-wrapper {
    position: relative; width: 280px; height: 200px; margin: auto; cursor: pointer;
    perspective: 800px; -webkit-perspective: 800px;
  }
  .envelope {
    position: relative; width: 100%; height: 130px;
    background: linear-gradient(135deg, #ffd6dd 0%, #ffb6c1 100%);
    border: 2px solid #e88; border-bottom: 4px solid #d47282;
    box-shadow: 0 4px 10px rgba(232, 136, 136, 0.3); overflow: visible;
    transform-style: preserve-3d; -webkit-transform-style: preserve-3d;
  }
  .envelope-flap {
    position: absolute; top: -80px; left: 0; width: 0; height: 0;
    border-left: 140px solid transparent; border-right: 140px solid transparent;
    border-bottom: 80px solid #ff9db6; box-shadow: 0 2px 6px rgba(0,0,0,0.15);
    transition: transform 0.7s ease; transform-origin: bottom center; z-index: 5;
    /* Começa FECHADA (aba embaixo) */
    transform: rotateX(0deg);
    background-image:
      repeating-linear-gradient(45deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.1) 1px, transparent 1px, transparent 5px);
  }
  /* Quando envelope abre, rotaciona a aba pra cima */
  .envelope.open .envelope-flap { transform: rotateX(180deg); }
  .sticker {
    position: absolute; top: 15px; left: 50%; transform: translateX(-50%);
    width: 40px; height: 40px; background: #ff5e99; border-radius: 50%;
    box-shadow: 0 2px 6px rgba(255, 94, 153, 0.6); display: flex; justify-content: center; align-items: center;
    font-size: 22px; color: white; user-select: none; transition: opacity 0.4s ease; z-index: 10;
  }
  .sticker.removed { opacity: 0; pointer-events: none; }
  .letter {
    position: absolute; top: 130px; left: 20px; right: 20px; height: 130px;
    background: linear-gradient(135deg, #fff9f9 0%, #ffe6eb 100%);
    border: 2px solid #e88; border-bottom: 4px solid #d47282; box-shadow: 0 4px 8px rgba(232, 136, 136, 0.2);
    padding: 20px 15px; font-size: 1.1em; color: #6b2c2c; line-height: 1.5;
    opacity: 0; transform: translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease;
    user-select: text;
    background-image:
      repeating-linear-gradient(45deg, rgba(255, 192, 203, 0.15), rgba(255, 192, 203, 0.15) 1px, transparent 1px, transparent 7px),
      repeating-linear-gradient(-45deg, rgba(255, 192, 203, 0.15), rgba(255, 192, 203, 0.15) 1px, transparent 1px, transparent 7px);
    z-index: 2;
  }
  .letter.show { opacity: 1; transform: translateY(-140px); z-index: 8; }
</style>
</head>
<body>
  <div class="container">
    <div class="start-screen" id="start">
      <h1>Oi, Malu... Escrevi algo pra você</h1>
      <button onclick="showEnvelope()">Quero ver!</button>
    </div>
    <div class="envelope-stage hidden" id="envelopeStage">
      <div class="envelope-wrapper" id="envelopeWrapper" onclick="interactEnvelope()">
        <div class="envelope" id="envelope">
          <div class="envelope-flap"></div>
          <div class="sticker" id="sticker">💌</div>
          <div class="letter" id="letter">
            Querida Malu,<br><br>
            Escrevi essa mensagem para te lembrar o quanto você é especial pra mim.<br>
            Espero que goste dessa surpresa feita com muito carinho!<br><br>
            Com amor, sempre.
          </div>
        </div>
      </div>
    </div>
  </div>
<script>
  let step = 0;
  function showEnvelope() {
    document.getElementById('start').classList.add('hidden');
    setTimeout(() => {
      document.getElementById('envelopeStage').classList.remove('hidden');
    }, 500);
  }
  function interactEnvelope() {
    const sticker = document.getElementById('sticker');
    const envelope = document.getElementById('envelope');
    const letter = document.getElementById('letter');
    step++;
    if (step === 1) {
      sticker.classList.add('removed'); // adesivo some
    } else if (step === 2) {
      envelope.classList.add('open');   // abrir aba pra cima
    } else if (step === 3) {
      letter.classList.add('show');     // papel aparece saindo
    }
  }
</script>
</body>
</html>
