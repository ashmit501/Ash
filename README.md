<!DOCTYPE html>
<html>
<head>
  <title>SpaceX Battlegrounds</title>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <style>
    body { background:#111; color:#eee; font-family:sans-serif; text-align:center; padding:20px; }
    button { margin:10px; padding:12px 24px; font-size:18px; border:none; border-radius:8px; background:#38bdf8; color:#0f172a; }
  </style>
</head>
<body>
  <h1>🚀 SpaceX Battlegrounds</h1>
  <p><strong>Commander:</strong> Ashmit Verma</p>
  <div id="story">You drop into the warzone. What's your move?</div>
  <div id="options"></div>

<script>
const story = document.getElementById('story');
const opts = document.getElementById('options');
let alive = true;

function choose(options) {
  opts.innerHTML = '';
  options.forEach(({ text, act }) => {
    const btn = document.createElement('button');
    btn.textContent = text;
    btn.onclick = act;
    opts.appendChild(btn);
  });
}

function start() {
  choose([
    { text: '🔥 Rush with AshBlaster', act: () => outcome('rush') },
    { text: '🛡 Hide in cover', act: () => outcome('hide') },
    { text: '💣 Throw AshGrenade', act: () => outcome('grenade') }
  ]);
}

function outcome(choice) {
  const r = Math.random();
  let msg = '';
  if (choice === 'rush') {
    msg = r < 0.5 ? 'You cleared the area with AshBlaster! 💥' : 'You were ambushed!';
    alive = r < 0.5;
  } else if (choice === 'hide') {
    msg = r < 0.7 ? 'You’re safe... enemy passed by.' : 'You got flanked!';
    alive = r < 0.7;
  } else {
    msg = r < 0.6 ? 'Perfect throw! Enemies down.' : 'Grenade bounced back!';
    alive = r < 0.6;
  }

  story.textContent = msg;
  if (alive) {
    choose([
      { text: '▶️ Continue', act: start },
      { text: '🏁 End Game', act: () => story.textContent = 'You survived. Mission success! 🎉' }
    ]);
  } else {
    opts.innerHTML = '<button onclick="location.reload()">💀 Play Again</button>';
  }
}

start();
</script>
</body>
</html>
