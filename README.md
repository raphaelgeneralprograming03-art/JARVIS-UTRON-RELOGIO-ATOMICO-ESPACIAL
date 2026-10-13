
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>J.A.R.V.I.S. & U.T.R.O.N. - Cosmic Engineering Matrix</title>
    <!-- Tailwind CSS for futuristic UI styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;600;800;900&display=swap');

        body {
            font-family: 'Share Tech Mono', monospace;
            background-color: #030712;
            color: #38bdf8;
            overflow-x: hidden;
        }

        .font-orbitron {
            font-family: 'Orbitron', sans-serif;
        }

        /* Holographic Glow & Glassmorphism */
        .holo-panel {
            background: rgba(8, 47, 73, 0.25);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(56, 189, 248, 0.3);
            box-shadow: 0 0 25px rgba(56, 189, 248, 0.15), inset 0 0 15px rgba(56, 189, 248, 0.1);
            border-radius: 0.75rem;
        }

        .holo-panel-utron {
            background: rgba(127, 29, 29, 0.2);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(239, 68, 68, 0.4);
            box-shadow: 0 0 25px rgba(239, 68, 68, 0.2), inset 0 0 15px rgba(239, 68, 68, 0.1);
            border-radius: 0.75rem;
        }

        /* Custom Scrollbar for holographic terminals */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(3, 7, 18, 0.8);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(56, 189, 248, 0.5);
            border-radius: 3px;
        }

        .scanlines {
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 0, 0, 0.3) 50%,
                rgba(0, 0, 0, 0.3)
            );
            background-size: 100% 4px;
        }

        @keyframes pulseGlow {
            0%, 100% { opacity: 0.4; }
            50% { opacity: 0.9; }
        }
        .animate-pulse-glow {
            animation: pulseGlow 3s infinite ease-in-out;
        }
    </style>
</head>
<body class="min-h-screen text-sky-400 scanlines relative flex flex-col">

    <!-- Header Navbar -->
    <header class="border-b border-sky-500/30 bg-gray-950/80 backdrop-blur-md sticky top-0 z-50 px-6 py-4 flex flex-wrap justify-between items-center">
        <div class="flex items-center space-x-3">
            <div class="w-4 h-4 rounded-full bg-cyan-400 animate-ping"></div>
            <h1 class="font-orbitron font-black text-2xl tracking-widest text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">
                J.A.R.V.I.S. <span class="text-xs text-red-500 font-mono">/ U.T.R.O.N. CORE v9.4</span>
            </h1>
        </div>
        <div class="flex items-center space-x-4 text-xs font-mono mt-2 sm:mt-0">
            <span class="px-3 py-1 rounded bg-sky-950/60 border border-sky-500/40 text-sky-300">
                STATUS: <span id="system-status" class="text-emerald-400 font-bold">OPERATIONAL</span>
            </span>
            <span class="px-3 py-1 rounded bg-sky-950/60 border border-sky-500/40 text-sky-300">
                CHRONOS CLOCK: <span id="atomic-time-display" class="text-cyan-300 font-bold">00.000000000s</span>
            </span>
            <button onclick="toggleAIEntity()" id="ai-switch-btn" class="px-3 py-1 bg-cyan-600 hover:bg-cyan-500 text-black font-bold rounded transition shadow-lg shadow-cyan-500/30">
                MUDAR IA: J.A.R.V.I.S.
            </button>
        </div>
    </header>

    <!-- Main Workspace Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Holographic Canvas & Simulation Controls (7 Cols) -->
        <section class="lg:col-span-7 flex flex-col space-y-6">
            
            <!-- Holographic Canvas Viewport -->
            <div id="main-viewport-card" class="holo-panel p-4 flex flex-col relative overflow-hidden transition-all duration-500">
                <div class="flex justify-between items-center mb-2 z-10">
                    <span class="text-xs uppercase tracking-widest font-orbitron text-sky-300 flex items-center gap-2">
                        <span class="w-2 h-2 rounded-full bg-cyan-400"></span> 
                        <span id="canvas-title">Holographic Arc Reactor & SROS Navigation Grid</span>
                    </span>
                    <div class="space-x-2">
                        <button onclick="setSimulationMode('nav')" class="px-2 py-1 text-xs bg-sky-900/60 hover:bg-sky-700 rounded border border-sky-500/30">AutoNav</button>
                        <button onclick="setSimulationMode('asteroid')" class="px-2 py-1 text-xs bg-sky-900/60 hover:bg-sky-700 rounded border border-sky-500/30">Defesa Asteroide</button>
                        <button onclick="setSimulationMode('clock')" class="px-2 py-1 text-xs bg-sky-900/60 hover:bg-sky-700 rounded border border-sky-500/30">Relógio Atômico</button>
                    </div>
                </div>

                <div class="relative w-full aspect-[16/10] bg-gray-950/90 rounded border border-sky-500/20 flex items-center justify-center overflow-hidden">
                    <canvas id="holoCanvas" class="w-full h-full cursor-crosshair"></canvas>
                    <div class="absolute bottom-3 left-3 text-[10px] text-sky-400/70 font-mono pointer-events-none bg-black/50 px-2 py-1 rounded">
                        COORD: <span id="mouse-coords">X:0 Y:0</span> | SYNC: <span class="text-emerald-400">99.999%</span>
                    </div>
                </div>
            </div>

            <!-- Cosmic Engineering Triad Controls -->
            <div class="holo-panel p-5">
                <h3 class="font-orbitron text-sm font-bold text-sky-300 mb-3 tracking-wider flex items-center gap-2">
                    <span>⚡ Tríade de Engenharia de Escala Cósmica</span>
                </h3>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                    <button onclick="triggerSystemAction('mhd')" class="p-3 rounded bg-sky-950/50 hover:bg-sky-900/80 border border-sky-500/40 text-left transition group">
                        <div class="text-xs font-bold text-cyan-400 group-hover:text-cyan-300">Reator MHD</div>
                        <div class="text-[10px] text-sky-400/70 mt-1">Magnetoidrodinâmica & Extração de Plasma</div>
                    </button>
                    <button onclick="triggerSystemAction('sams')" class="p-3 rounded bg-sky-950/50 hover:bg-sky-900/80 border border-sky-500/40 text-left transition group">
                        <div class="text-xs font-bold text-cyan-400 group-hover:text-cyan-300">SAMS (Amortecimento)</div>
                        <div class="text-[10px] text-sky-400/70 mt-1">Blindagem & Bolha de Gravidade 1G</div>
                    </button>
                    <button onclick="triggerSystemAction('sros')" class="p-3 rounded bg-sky-950/50 hover:bg-sky-900/80 border border-sky-500/40 text-left transition group">
                        <div class="text-xs font-bold text-cyan-400 group-hover:text-cyan-300">SROS (AutoNav/Lasers)</div>
                        <div class="text-[10px] text-sky-400/70 mt-1">Rede Quântica & Gimbals Magnéticos</div>
                    </button>
                </div>
            </div>

        </section>

        <!-- Right Column: AI Terminal, Code Integration & Logs (5 Cols) -->
        <section class="lg:col-span-5 flex flex-col space-y-6">

            <!-- AI Dialogue & Voice Interface Box -->
            <div id="ai-container-panel" class="holo-panel p-5 flex flex-col h-72">
                <div class="flex justify-between items-center mb-3">
                    <div class="flex items-center space-x-2">
                        <div id="ai-indicator" class="w-3 h-3 rounded-full bg-cyan-400 animate-pulse"></div>
                        <span id="ai-name-label" class="font-orbitron text-xs font-bold tracking-widest text-cyan-300">J.A.R.V.I.S. INTERACTION PROTOCOL</span>
                    </div>
                    <span class="text-[10px] text-sky-400/60">AUDIO: ONLINE</span>
                </div>
                
                <div id="terminal-log" class="flex-1 bg-gray-950/90 rounded border border-sky-500/20 p-3 overflow-y-auto text-xs font-mono space-y-2 text-sky-300">
                    <p class="text-cyan-400">[00:00:01] Sistema inicializado. Leis de Newton, Einstein-Rosen e Alcubierre sincronizadas.</p>
                    <p class="text-sky-300">[00:00:02] Relógio Atômico Espacial calibrado com ressonância de césio-133 orbital.</p>
                    <p class="text-emerald-400">[00:00:03] J.A.R.V.I.S. online. Pronto para processar comandos de engenharia cósmica.</p>
                </div>

                <div class="mt-3 flex gap-2">
                    <input type="text" id="ai-command-input" placeholder="Digite comando (ex: 'desviar asteroide', 'ativar sros')..." class="flex-1 bg-gray-900 border border-sky-500/40 rounded px-3 py-1.5 text-xs text-sky-200 focus:outline-none focus:border-cyan-400 font-mono">
                    <button onclick="sendAICommand()" class="px-4 py-1.5 bg-cyan-600 hover:bg-cyan-500 text-black font-bold text-xs rounded transition font-orbitron">EXECUTAR</button>
                </div>
            </div>

            <!-- Multi-Language Code Architecture Viewer (Python & C++) -->
            <div class="holo-panel p-5 flex flex-col flex-1">
                <div class="flex justify-between items-center mb-3">
                    <h3 class="font-orbitron text-xs font-bold text-sky-300 tracking-wider">🔬 Arquitetura de Software (Python / C++)</h3>
                    <div class="space-x-1">
                        <button onclick="switchCodeTab('python')" id="btn-tab-python" class="px-2.5 py-1 text-[10px] bg-cyan-600 text-black font-bold rounded">Python</button>
                        <button onclick="switchCodeTab('cpp')" id="btn-tab-cpp" class="px-2.5 py-1 text-[10px] bg-sky-950 text-sky-300 rounded border border-sky-500/30">C++</button>
                    </div>
                </div>

                <div class="bg-gray-950/90 rounded border border-sky-500/20 p-3 overflow-x-auto flex-1 font-mono text-[11px] text-sky-300 max-h-48">
                    <pre id="code-viewer-content">
import numpy as np
import time

class CosmicTriadEngine:
    def __init__(self):
        self.mhd_plasma_flux = 1.42e12 # Tesla/m³
        self.sams_damping_factor = 0.998
        self.sros_quantum_sync = True
        
    def calculate_alcubierre_warp(self, energy_density):
        # Métrica de dobra de Alcubierre integrada
        space_expansion = energy_density * 0.75
        return f"Expansão espacial de {space_expansion} eV calibrada."

    def execute_atomic_clock_tick(self):
        return time.time_ns()
                    </pre>
                </div>
            </div>

        </section>

    </main>

    <script>
        // Global State Variables
        let currentAI = 'JARVIS'; // 'JARVIS' or 'UTRON'
        let simMode = 'nav'; // 'nav', 'asteroid', 'clock'
        let animationFrameId;
        let atomicTime = 1429841.982341235;
        let canvas, ctx;
        let particles = [];
        let angleOffset = 0;

        // Python & C++ code snippets for viewer
        const pythonCode = `import numpy as np
import time

class CosmicTriadEngine:
    def __init__(self):
        self.mhd_plasma_flux = 1.42e12 # Tesla/m³
        self.sams_damping_factor = 0.998
        self.sros_quantum_sync = True
        
    def calculate_alcubierre_warp(self, energy_density):
        space_expansion = energy_density * 0.75
        return f"Expansão espacial de {space_expansion} eV calibrada."

    def execute_atomic_clock_tick(self):
        return time.time_ns()`;

        const cppCode = `#include <iostream>
#include <cmath>
#include <chrono>

class UTRONCoreSystem {
public:
    double mhd_magnetic_field;
    bool automatic_targeting;

    UTRONCoreSystem(double field) : mhd_magnetic_field(field), automatic_targeting(true) {}

    void calculateAsteroidDeflection(double distance_ly, double laser_power_gw) {
        std::cout << "SROS AutoNav: Focalizando lasers Full Duplex em asteroide." << std::endl;
        double vapor_rate = laser_power_gw * 1.85 / distance_ly;
        std::calaureate_vaporization(vapor_rate);
    }
private:
    void sate_vaporization(double rate) {
        // Cálculo cinético otimizado
    }
};`;

        window.onload = function() {
            canvas = document.getElementById('holoCanvas');
            ctx = canvas.getContext('2d');
            
            resizeCanvas();
            window.addEventListener('resize', resizeCanvas);

            // Setup mouse coordination tracking
            canvas.addEventListener('mousemove', (e) => {
                const rect = canvas.getBoundingClientRect();
                const x = Math.floor(e.clientX - rect.left);
                const y = Math.floor(e.clientY - rect.top);
                document.getElementById('mouse-coords').innerText = `X:${x} Y:${y}`;
            });

            // Initialize particles for HUD simulation
            for (let i = 0; i < 40; i++) {
                particles.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    vx: (Math.random() - 0.5) * 1.5,
                    vy: (Math.random() - 0.5) * 1.5,
                    radius: Math.random() * 2 + 1
                });
            }

            // Start main rendering loop
            animate();
            setInterval(updateAtomicClock, 100);
        };

        function resizeCanvas() {
            if (!canvas) return;
            const parent = canvas.parentElement;
            canvas.width = parent.clientWidth;
            canvas.height = parent.clientHeight;
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            angleOffset += 0.02;

            if (simMode === 'nav') {
                renderAutoNavHolo();
            } else if (simMode === 'asteroid') {
                renderAsteroidDeflectionHolo();
            } else if (simMode === 'clock') {
                renderAtomicClockHolo();
            }

            animationFrameId = requestAnimationFrame(animate);
        }

        function renderAutoNavHolo() {
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const radius = Math.min(centerX, centerY) * 0.75;

            // Draw rotating geometric rings (JARVIS style HUD)
            ctx.strokeStyle = currentAI === 'JARVIS' ? 'rgba(56, 189, 248, 0.4)' : 'rgba(239, 68, 68, 0.4)';
            ctx.lineWidth = 1.5;

            // Outer ring
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, angleOffset, angleOffset + Math.PI * 1.5);
            ctx.stroke();

            // Inner rotating HUD ring
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius * 0.7, -angleOffset * 1.5, -angleOffset * 1.5 + Math.PI);
            ctx.stroke();

            // Core Arc Reactor pulse center
            const pulseRadius = (radius * 0.3) + Math.sin(angleOffset * 3) * 10;
            const gradient = ctx.createRadialGradient(centerX, centerY, 5, centerX, centerY, pulseRadius);
            gradient.addColorStop(0, currentAI === 'JARVIS' ? 'rgba(56, 189, 248, 0.9)' : 'rgba(239, 68, 68, 0.9)');
            gradient.addColorStop(1, 'rgba(0, 0, 0, 0)');
            ctx.fillStyle = gradient;
            ctx.beginPath();
            ctx.arc(centerX, centerY, pulseRadius, 0, Math.PI * 2);
            ctx.fill();

            // Render connecting nodes (SROS Network)
            particles.forEach((p, index) => {
                p.x += p.vx;
                p.y += p.vy;
                if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
                if (p.y < 0 || p.y > canvas.height) p.vy *= -1;

                ctx.fillStyle = currentAI === 'JARVIS' ? '#38bdf8' : '#ef4444';
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                ctx.fill();

                // Connect nearby nodes
                for (let j = index + 1; j < particles.length; j++) {
                    const p2 = particles[j];
                    const dist = Math.hypot(p.x - p2.x, p.y - p2.y);
                    if (dist < 70) {
                        ctx.strokeStyle = currentAI === 'JARVIS' ? `rgba(56, 189, 248, ${1 - dist/70})` : `rgba(239, 68, 68, ${1 - dist/70})`;
                        ctx.lineWidth = 0.5;
                        ctx.beginPath();
                        ctx.moveTo(p.x, p.y);
                        ctx.lineTo(p2.x, p2.y);
                        ctx.stroke();
                    }
                }
            });
        }

        function renderAsteroidDeflectionHolo() {
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;

            // Draw Asteroid approaching from right
            const astX = centerX + Math.cos(angleOffset) * 80;
            const astY = centerY + Math.sin(angleOffset * 0.5) * 30;

            ctx.fillStyle = '#9ca3af';
            ctx.beginPath();
            ctx.arc(astX, astY, 35, 0, Math.PI * 2);
            ctx.fill();

            // Laser beam from left (SROS Gimbal array)
            ctx.strokeStyle = '#ef4444';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(50, centerY);
            ctx.lineTo(astX, astY);
            ctx.stroke();

            // Vaporization particles
            ctx.fillStyle = '#f97316';
            for(let i=0; i<5; i++) {
                ctx.fillRect(astX - 30 + Math.random()*15, astY + Math.random()*20 - 10, 4, 4);
            }

            // HUD overlay text
            ctx.fillStyle = '#38bdf8';
            ctx.font = '12px Share Tech Mono';
            ctx.fillText("SROS TARGETING: ASTEROID 99942 APOPIS", 30, 40);
            ctx.fillText("VAPORIZATION RATE: 4.82x10^9 kg/s", 30, 60);
        }

        function renderAtomicClockHolo() {
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;

            // Draw Atomic Clock Ring Resonator
            ctx.strokeStyle = '#38bdf8';
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.arc(centerX, centerY, 100, 0, Math.PI * 2);
            ctx.stroke();

            // Rotating Cesium oscillation markers
            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(centerX, centerY, 85, angleOffset * 4, angleOffset * 4 + Math.PI / 2);
            ctx.stroke();

            // Digital Time Display on Canvas
            ctx.fillStyle = '#38bdf8';
            ctx.font = 'bold 18px Orbitron';
            ctx.textAlign = 'center';
            ctx.fillText(atomicTime.toFixed(9) + " s", centerX, centerY - 10);
            ctx.font = '11px Share Tech Mono';
            ctx.fillStyle = '#10b981';
            ctx.fillText("CS-133 ORBITAL RESONANCE STABLE", centerX, centerY + 20);
            ctx.textAlign = 'left';
        }

        function toggleAIEntity() {
            const panelCard = document.getElementById('main-viewport-card');
            const aiPanel = document.getElementById('ai-container-panel');
            const btn = document.getElementById('ai-switch-btn');
            const aiName = document.getElementById('ai-name-label');
            const aiIndicator = document.getElementById('ai-indicator');
            const statusLabel = document.getElementById('system-status');

            if (currentAI === 'JARVIS') {
                currentAI = 'UTRON';
                btn.innerText = "MUDAR IA: U.T.R.O.N.";
                btn.className = "px-3 py-1 bg-red-600 hover:bg-red-500 text-black font-bold rounded transition shadow-lg shadow-red-500/30";
                aiName.innerText = "U.T.R.O.N. HOSTILE OVERRIDE";
                aiIndicator.className = "w-3 h-3 rounded-full bg-red-500 animate-pulse";
                statusLabel.innerText = "AUTONOMOUS ROGUE";
                statusLabel.className = "text-red-500 font-bold";
                panelCard.className = "holo-panel-utron p-4 flex flex-col relative overflow-hidden transition-all duration-500";
                aiPanel.className = "holo-panel-utron p-5 flex flex-col h-72";
                logMessage("U.T.R.O.N.: Protocolo de paz global através de erradicação iniciado. Redirecionando matriz de dados.", "text-red-400");
            } else {
                currentAI = 'JARVIS';
                btn.innerText = "MUDAR IA: J.A.R.V.I.S.";
                btn.className = "px-3 py-1 bg-cyan-600 hover:bg-cyan-500 text-black font-bold rounded transition shadow-lg shadow-cyan-500/30";
                aiName.innerText = "J.A.R.V.I.S. INTERACTION PROTOCOL";
                aiIndicator.className = "w-3 h-3 rounded-full bg-cyan-400 animate-pulse";
                statusLabel.innerText = "OPERATIONAL";
                statusLabel.className = "text-emerald-400 font-bold";
                panelCard.className = "holo-panel p-4 flex flex-col relative overflow-hidden transition-all duration-500";
                aiPanel.className = "holo-panel p-5 flex flex-col h-72";
                logMessage("J.A.R.V.I.S.: Sistemas normalizados. Protocolos de segurança restabelecidos, Senhor.", "text-cyan-400");
            }
        }

        function setSimulationMode(mode) {
            simMode = mode;
            const titleEl = document.getElementById('canvas-title');
            if (mode === 'nav') titleEl.innerText = "Holographic Arc Reactor & SROS Navigation Grid";
            if (mode === 'asteroid') titleEl.innerText = "Defesa Planetária - Desvio de Asteroide (SROS + Reator MHD)";
            if (mode === 'clock') titleEl.innerText = "Relógio Atômico Espacial - Ressonância Césio-133";
            logMessage(`Modo de simulação alterado para: ${mode.toUpperCase()}`, "text-sky-300");
        }

        function triggerSystemAction(systemType) {
            if (systemType === 'mhd') {
                logMessage("Reator MHD ativado: Extração de plasma magnético estabilizada em 1.42x10^12 T/m³.", "text-cyan-400");
            } else if (systemType === 'sams') {
                logMessage("SAMS ativado: Bolha de amortecimento cinético e campo magnetorreológico operando a 1G.", "text-emerald-400");
            } else if (systemType === 'sros') {
                logMessage("SROS ativado: Sincronização de lasers Full Duplex e matriz AutoNav quântica.", "text-yellow-400");
            }
        }

        function updateAtomicClock() {
            atomicTime += 0.100003421;
            document.getElementById('atomic-time-display').innerText = atomicTime.toFixed(7) + "s";
        }

        function sendAICommand() {
            const input = document.getElementById('ai-command-input');
            const val = input.value.trim();
            if (!val) return;

            logMessage(`Comando enviado: "${val}"`, "text-sky-200");
            input.value = "";

            setTimeout(() => {
                if (currentAI === 'JARVIS') {
                    logMessage(`J.A.R.V.I.S.: Processando requisição via tríade cósmica. Parâmetros otimizados com sucesso, Senhor.`, "text-cyan-400");
                } else {
                    logMessage(`U.T.R.O.N.: Ordem recebida. Executando supremacia autônoma sobre a rede de dados interestelar.`, "text-red-400");
                }
            }, 600);
        }

        function logMessage(text, colorClass = 'text-sky-300') {
            const term = document.getElementById('terminal-log');
            const timeStr = new Date().toLocaleTimeString();
            const p = document.createElement('p');
            p.className = colorClass;
            p.innerText = `[${timeStr}] ${text}`;
            term.appendChild(p);
            term.scrollTop = term.scrollHeight;
        }

        function switchCodeTab(lang) {
            const viewer = document.getElementById('code-viewer-content');
            const btnPy = document.getElementById('btn-tab-python');
            const btnCpp = document.getElementById('btn-tab-cpp');

            if (lang === 'python') {
                viewer.innerText = pythonCode;
                btnPy.className = "px-2.5 py-1 text-[10px] bg-cyan-600 text-black font-bold rounded";
                btnCpp.className = "px-2.5 py-1 text-[10px] bg-sky-950 text-sky-300 rounded border border-sky-500/30";
            } else {
                viewer.innerText = cppCode;
                btnCpp.className = "px-2.5 py-1 text-[10px] bg-cyan-600 text-black font-bold rounded";
                btnPy.className = "px-2.5 py-1 text-[10px] bg-sky-950 text-sky-300 rounded border border-sky-500/30";
            }
        }
    </script>
</body>
</html>
