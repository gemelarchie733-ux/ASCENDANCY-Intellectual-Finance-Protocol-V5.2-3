<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ASCENDANCY — Intellectual Finance Protocol V5.2</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&display=swap');
    body { font-family: 'Space Grotesk', sans-serif; }
    .glass { background: rgba(10,10,10,0.85); backdrop-filter: blur(20px); border: 1px solid rgba(192,192,192,0.3); }
    .cobalt-glow { text-shadow: 0 0 20px #00bfff; }
  </style>
</head>
<body class="bg-[#0A0A0A] text-white min-h-screen">

  <div class="max-w-7xl mx-auto p-6">
    <!-- HEADER -->
    <div class="glass rounded-3xl p-8 flex justify-between items-center mb-8">
      <div>
        <h1 class="text-5xl font-bold tracking-tighter cobalt-glow">ASCENDANCY</h1>
        <p class="text-cobalt text-xl">Intellectual Finance Protocol • Obsidian + Contract Hunter</p>
      </div>
      <div class="flex items-center gap-4">
        <div class="flex items-center gap-2 bg-green-400/10 text-green-400 px-4 py-2 rounded-3xl text-sm font-mono">
          <div class="w-3 h-3 bg-green-400 rounded-full animate-pulse"></div>
          ORACLE PROTOCOL • LIVE
        </div>
        <button onclick="toggleAdvisor()" class="px-6 py-3 bg-cobalt text-black rounded-3xl font-bold flex items-center gap-2">
          <i class="fas fa-robot"></i> TITAN ADVISOR
        </button>
      </div>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">

      <!-- 3D AEGIS GRID -->
      <div class="lg:col-span-8 glass rounded-3xl p-6">
        <div class="flex justify-between mb-4">
          <div class="font-mono text-cobalt">AEGIS GRID • GLOBAL INFRASTRUCTURE POWER • ORACLE VERIFIED</div>
        </div>
        <canvas id="aegis" class="w-full h-96 bg-black rounded-2xl"></canvas>
      </div>

      <!-- SOVEREIGN WEALTH -->
      <div class="lg:col-span-4 glass rounded-3xl p-8 flex flex-col">
        <h2 class="text-3xl font-bold">SOVEREIGN WEALTH ENGINE</h2>
        <div id="wealth" class="text-7xl font-mono mt-8 mb-2">$1,248,750</div>
        <p class="text-cobalt">PROJECTED 5% FEES</p>
        <button onclick="engagePath()" class="mt-auto py-6 bg-gradient-to-r from-cobalt to-blue-400 text-black text-2xl font-bold rounded-3xl hover:scale-105 transition">
          ENGAGE 5% PATH
        </button>
      </div>

      <!-- ARBITRAGE NODE -->
      <div class="lg:col-span-12 glass rounded-3xl p-8">
        <h2 class="text-4xl font-bold mb-6">ARBITRAGE NODE • LIVE OPPORTUNITIES</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6" id="opps">
          <!-- Populated by JS -->
        </div>
      </div>
    </div>
  </div>

  <!-- TITAN ADVISOR MODAL -->
  <div id="advisorModal" class="hidden fixed inset-0 bg-black/80 flex items-center justify-center z-50">
    <div class="glass w-full max-w-lg mx-4 rounded-3xl p-6">
      <div class="flex justify-between mb-6">
        <h3 class="text-2xl font-bold">TITAN ADVISOR • EMPEROR-TIER</h3>
        <button onclick="toggleAdvisor()" class="text-3xl">✕</button>
      </div>
      <div id="chat" class="h-80 overflow-y-auto space-y-4 mb-6"></div>
      <div class="flex gap-3">
        <input id="chatInput" type="text" class="flex-1 glass rounded-3xl px-6 py-4" placeholder="Ask JARVIS, Chief Engineer, or CFO...">
        <button onclick="sendChat()" class="bg-cobalt text-black px-8 rounded-3xl font-bold">SEND</button>
      </div>
      <div class="text-xs text-center text-silver/60 mt-4">Powered by Grok • Real-time Oracle Protocol</div>
    </div>
  </div>

  <script>
    // Tailwind script already loaded via CDN
    function initTailwind() {
      // Already handled by CDN
    }

    // Simple 3D-like Aegis Grid using Canvas
    function initAegis() {
      const canvas = document.getElementById('aegis');
      const ctx = canvas.getContext('2d');
      canvas.width = canvas.offsetWidth;
      canvas.height = canvas.offsetHeight;

      let nodes = [];
      for (let i = 0; i < 45; i++) {
        nodes.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          size: Math.random() * 6 + 4,
          speed: Math.random() * 0.5 + 0.2
        });
      }

      function draw() {
        ctx.fillStyle = 'rgba(10,10,10,0.15)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        // Draw connections
        ctx.strokeStyle = 'rgba(192,192,192,0.25)';
        ctx.lineWidth = 1;
        for (let i = 0; i < nodes.length; i++) {
          for (let j = i+1; j < nodes.length; j++) {
            if (Math.random() > 0.9) {
              ctx.beginPath();
              ctx.moveTo(nodes[i].x, nodes[i].y);
              ctx.lineTo(nodes[j].x, nodes[j].y);
              ctx.stroke();
            }
          }
        }

        // Draw nodes
        nodes.forEach(node => {
          ctx.fillStyle = Math.random() > 0.7 ? '#22ff88' : '#00bfff';
          ctx.beginPath();
          ctx.arc(node.x, node.y, node.size, 0, Math.PI * 2);
          ctx.fill();

          // Pulse
          node.x += (Math.random() - 0.5) * node.speed * 2;
          node.y += (Math.random() - 0.5) * node.speed * 2;
          if (node.x < 0 || node.x > canvas.width) node.x = canvas.width / 2;
          if (node.y < 0 || node.y > canvas.height) node.y = canvas.height / 2;
        });

        requestAnimationFrame(draw);
      }
      draw();
    }

    // Wealth engine
    let wealth = 1248750;
    function engagePath() {
      wealth += 187500;
      document.getElementById('wealth').textContent = '$' + wealth.toLocaleString();
      alert("✅ 5% PATH ENGAGED • +$187,500 projected • Oracle Protocol confirmed");
    }

    // Sample opportunities
    function loadOpportunities() {
      const container = document.getElementById('opps');
      const opps = [
        { title: "AI-Enabled C2 Modernization - Air Force", value: "12.4M", propensity: 92 },
        { title: "VA Intelligent Automation & Agentic AI (IAAI)", value: "8.7M", propensity: 88 },
        { title: "Cybersecurity Maturity Model Certification Support", value: "6.5M", propensity: 79 }
      ];
      opps.forEach(opp => {
        const div = document.createElement('div');
        div.className = "glass p-6 rounded-3xl hover:border-cobalt transition-all";
        div.innerHTML = `
          <div class="flex justify-between">
            <div class="text-3xl font-mono">$${opp.value}</div>
            <div class="bg-green-400 text-black px-4 py-1 rounded-2xl text-sm font-bold">${opp.propensity}%</div>
          </div>
          <h3 class="mt-4 text-xl">${opp.title}</h3>
          <div class="mt-6 flex gap-3">
            <button onclick="oracleVerify(this)" class="flex-1 py-3 text-xs font-mono border border-green-400 text-green-400 rounded-2xl">ORACLE VERIFY</button>
            <button onclick="engage(this)" class="flex-1 py-3 bg-cobalt text-black font-bold rounded-2xl">ENGAGE 5% PATH</button>
          </div>
        `;
        container.appendChild(div);
      });
    }

    function oracleVerify(btn) {
      btn.innerHTML = '✅ ORACLE VERIFIED';
      btn.classList.add('text-green-400');
      setTimeout(() => alert("Oracle Protocol: All sources aligned. No conflicts."), 300);
    }

    function engage(btn) {
      btn.textContent = 'ENGAGED ✓';
      setTimeout(() => engagePath(), 400);
    }

    // Titan Advisor
    let messages = [{role: 'assistant', content: 'Emperor-Tier Titan Advisor online. How can I accelerate your 5% path today?'}];
    function toggleAdvisor() {
      const modal = document.getElementById('advisorModal');
      modal.classList.toggle('hidden');
      if (!modal.classList.contains('hidden')) renderChat();
    }
    function renderChat() {
      const chat = document.getElementById('chat');
      chat.innerHTML = messages.map(m => `
        <div class="flex ${m.role === 'user' ? 'justify-end' : 'justify-start'}">
          <div class="max-w-[80%] p-4 rounded-3xl ${m.role === 'user' ? 'bg-cobalt text-black' : 'glass'}">${m.content}</div>
        </div>
      `).join('');
    }
    function sendChat() {
      const input = document.getElementById('chatInput');
      if (!input.value) return;
      messages.push({role: 'user', content: input.value});
      renderChat();
      const userMsg = input.value;
      input.value = '';
      setTimeout(() => {
        const responses = ["JARVIS: High-probability path detected.", "AI Chief Engineer: CMMC L2 alignment confirmed.", "AI CFO: 5% fee projection updated."];
        messages.push({role: 'assistant', content: responses[Math.floor(Math.random()*responses.length)]});
        renderChat();
      }, 800);
    }

    // Initialize everything
    window.onload = function() {
      initAegis();
      loadOpportunities();
      console.log('%c✅ ASCENDANCY V5.2 DEMO LOADED — Full Obsidian Protocol active', 'color:#00bfff; font-size:14px; font-family:monospace');
    };
  </script>
</body>
</html>

# ASCENDANCY-Intellectual-Finance-Protocol-V5.2-3
