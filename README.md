# -
自動翻譯中文至英文並可以自動重複語音
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VoxCPM 預設角色語音生成與口語翻譯控制台</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Noto+Sans+TC:wght@300;400;500;700&display=swap');
        body {
            font-family: 'Noto Sans TC', sans-serif;
        }
        .code-font {
            font-family: 'JetBrains Mono', monospace;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col selection:bg-cyan-500/30 selection:text-cyan-200">

    <!-- 頂部導覽列 -->
    <header class="border-b border-slate-800/80 bg-slate-900/40 backdrop-blur-xl sticky top-0 z-50 px-6 py-4 flex items-center justify-between">
        <div class="flex items-center space-x-3">
            <div class="bg-gradient-to-tr from-cyan-500 to-indigo-600 p-2.5 rounded-xl text-white shadow-lg shadow-cyan-500/20">
                <i data-lucide="mic" class="w-6 h-6 animate-pulse"></i>
            </div>
            <div>
                <h1 class="font-bold text-lg tracking-wide bg-gradient-to-r from-cyan-400 via-sky-400 to-indigo-400 bg-clip-text text-transparent">VoxCPM Web Studio</h1>
                <p class="text-xs text-slate-400">基於 OpenBMB VoxCPM2 的 AI 標準 TTS 語音生成與口語翻譯面板</p>
            </div>
        </div>
        <div class="flex items-center space-x-4">
            <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 shadow-sm">
                <span class="w-2 h-2 mr-2 rounded-full bg-emerald-500 animate-ping"></span>
                Gemini AI 雙引擎已連線
            </span>
        </div>
    </header>

    <!-- 主內容區：精美居中單欄版型 -->
    <main class="flex-1 max-w-3xl w-full mx-auto p-4 md:p-6 space-y-6">
        
        <!-- 互動生成控制區 -->
        <section class="space-y-6">
            
            <!-- 控制卡片 -->
            <div class="bg-slate-900/60 border border-slate-800/80 rounded-2xl p-6 space-y-6 backdrop-blur-md shadow-xl">
                
                <!-- 1. 預設角色選擇 (已依需求重排) -->
                <div id="section-voice-select" class="space-y-3">
                    <div class="flex justify-between items-center">
                        <label class="block text-sm font-medium text-slate-300">選擇模擬克隆角色</label>
                        <span class="text-xs text-slate-500">選擇最適合您文本的說話者音色</span>
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        <!-- C (Fenrir) 第一位 -->
                        <label class="relative flex flex-col p-3.5 bg-slate-950/55 border border-slate-800 rounded-xl cursor-pointer hover:bg-slate-900 hover:border-slate-700 transition-all duration-200">
                            <input type="radio" name="preset-voice" value="Fenrir" checked class="absolute right-4 top-4 text-indigo-500 focus:ring-indigo-500 bg-slate-900 border-slate-750">
                            <span class="font-semibold text-slate-200 text-sm">克隆角色 C (Fenrir)</span>
                            <span class="text-xs text-slate-450 mt-1">渾厚低音、穩重商務演說與介紹男聲</span>
                        </label>
                        <!-- D (Puck) 第二位 -->
                        <label class="relative flex flex-col p-3.5 bg-slate-950/55 border border-slate-800 rounded-xl cursor-pointer hover:bg-slate-900 hover:border-slate-700 transition-all duration-200">
                            <input type="radio" name="preset-voice" value="Puck" class="absolute right-4 top-4 text-indigo-500 focus:ring-indigo-500 bg-slate-900 border-slate-750">
                            <span class="font-semibold text-slate-200 text-sm">克隆角色 D (Puck)</span>
                            <span class="text-xs text-slate-450 mt-1">俏皮幽默、富含情感波動的特色配音</span>
                        </label>
                        <!-- A (Kore) 第三位 -->
                        <label class="relative flex flex-col p-3.5 bg-slate-950/55 border border-slate-800 rounded-xl cursor-pointer hover:bg-slate-900 hover:border-slate-700 transition-all duration-200">
                            <input type="radio" name="preset-voice" value="Kore" class="absolute right-4 top-4 text-indigo-500 focus:ring-indigo-500 bg-slate-900 border-slate-750">
                            <span class="font-semibold text-slate-200 text-sm">克隆角色 A (Kore)</span>
                            <span class="text-xs text-slate-450 mt-1">清澈溫柔、適合故事與自然閱讀</span>
                        </label>
                        <!-- B (Zephyr) 第四位 -->
                        <label class="relative flex flex-col p-3.5 bg-slate-950/55 border border-slate-800 rounded-xl cursor-pointer hover:bg-slate-900 hover:border-slate-700 transition-all duration-200">
                            <input type="radio" name="preset-voice" value="Zephyr" class="absolute right-4 top-4 text-indigo-500 focus:ring-indigo-500 bg-slate-900 border-slate-750">
                            <span class="font-semibold text-slate-200 text-sm">克隆角色 B (Zephyr)</span>
                            <span class="text-xs text-slate-450 mt-1">朝氣蓬勃、明亮活潑的標準女聲</span>
                        </label>
                    </div>
                </div>

                <!-- AI 智慧日常對話翻譯對齊面板 -->
                <div class="border-t border-slate-800/80 pt-5 space-y-3 bg-slate-950/40 p-4 rounded-xl border border-slate-800/60">
                    <div class="flex items-center justify-between">
                        <label class="text-xs font-bold text-cyan-400 flex items-center space-x-1.5">
                            <i data-lucide="sparkles" class="w-4 h-4 animate-pulse"></i>
                            <span>AI 智慧口語翻譯對齊 (中翻英)</span>
                        </label>
                        <span class="text-[10px] text-slate-500">自動避開生僻字、日常對話最自然</span>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
                        <div class="space-y-1.5">
                            <div class="flex justify-between text-[11px] text-slate-400">
                                <span>1. 輸入中文日常句</span>
                                <span class="text-slate-500">（或點選下方快捷句）</span>
                            </div>
                            <input id="translate-input-zh" type="text" 
                                   class="w-full bg-slate-900 border border-slate-800 rounded-lg px-3 py-2 text-xs text-slate-200 focus:outline-none focus:ring-1 focus:ring-cyan-500 transition"
                                   value="你真的很棒，充滿自信與魅力，大家都喜歡你。">
                        </div>
                        <div class="flex items-end space-x-2">
                            <button id="translate-btn" onclick="translateAndPaste()" class="w-full py-2 px-3 bg-cyan-600 hover:bg-cyan-500 text-white rounded-lg text-xs font-bold transition-all duration-200 flex items-center justify-center space-x-1.5 shadow-lg shadow-cyan-500/10 hover:shadow-cyan-500/20">
                                <i data-lucide="languages" class="w-3.5 h-3.5"></i>
                                <span>中翻英並自動貼上</span>
                            </button>
                        </div>
                    </div>

                    <div class="flex flex-wrap gap-1.5 pt-1.5 border-t border-slate-800/40">
                        <button onclick="setTranslateSentence('你今天過得怎麼樣？工作還順利嗎？')" class="text-[10px] bg-slate-900 hover:bg-slate-800 text-slate-300 py-1 px-2.5 rounded-lg border border-slate-800 hover:border-slate-700 transition">💬 問候近況</button>
                        <button onclick="setTranslateSentence('等一下我們要去哪裡吃晚餐？我有好主意！')" class="text-[10px] bg-slate-900 hover:bg-slate-800 text-slate-300 py-1 px-2.5 rounded-lg border border-slate-800 hover:border-slate-700 transition">🍽️ 聚餐提議</button>
                        <button onclick="setTranslateSentence('非常感謝你的幫忙，這對我來說真的很重要。')" class="text-[10px] bg-slate-900 hover:bg-slate-800 text-slate-300 py-1 px-2.5 rounded-lg border border-slate-800 hover:border-slate-700 transition">🙏 表達謝意</button>
                        <button onclick="setTranslateSentence('別擔心，一切都會變好的，加油！')" class="text-[10px] bg-slate-900 hover:bg-slate-800 text-slate-300 py-1 px-2.5 rounded-lg border border-slate-800 hover:border-slate-700 transition">✨ 鼓勵安慰</button>
                    </div>
                </div>

                <!-- 3. 輸入待合成的文字 -->
                <div class="space-y-3 border-t border-slate-800/80 pt-5">
                    <div class="flex justify-between items-center">
                        <label class="block text-sm font-medium text-slate-300">待合成的文本內容 (Text)</label>
                        <span id="char-count" class="text-xs text-slate-500 font-medium">0 / 200 字</span>
                    </div>
                    <textarea id="text-input" rows="4" maxlength="200"
                              class="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-3 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent text-slate-200 resize-none transition"
                              placeholder="請輸入您想要模型說出的話..."
                              oninput="updateCharCount()">你真的很棒，充滿自信與魅力，大家都喜歡你。</textarea>
                </div>

                <!-- 高級微調參數 -->
                <div class="border-t border-slate-800/80 pt-4 space-y-4">
                    <button onclick="toggleAdvanced()" class="text-xs text-slate-400 hover:text-indigo-400 flex items-center space-x-1 focus:outline-none transition">
                        <i id="advanced-chevron" data-lucide="chevron-right" class="w-3.5 h-3.5 transition-transform duration-250"></i>
                        <span>進階生成參數調整</span>
                    </button>
                    
                    <div id="advanced-panel" class="grid grid-cols-1 md:grid-cols-2 gap-4 hidden transition-all duration-300">
                        <div class="space-y-2">
                            <div class="flex justify-between text-xs">
                                <span class="text-slate-400">CFG Scale (自由導向權重)</span>
                                <span id="cfg-val" class="text-indigo-400 font-medium">2.0</span>
                            </div>
                            <input type="range" id="cfg-scale" min="1.0" max="5.0" step="0.5" value="2.0" 
                                   class="w-full h-1 bg-slate-850 rounded-lg appearance-none cursor-pointer accent-indigo-500"
                                   oninput="document.getElementById('cfg-val').innerText = this.value">
                        </div>
                        <div class="space-y-2">
                            <div class="flex justify-between text-xs">
                                <span class="text-slate-400">Inference Steps (推理步數)</span>
                                <span id="steps-val" class="text-indigo-400 font-medium">10</span>
                            </div>
                            <input type="range" id="steps-scale" min="5" max="30" step="1" value="10" 
                                   class="w-full h-1 bg-slate-850 rounded-lg appearance-none cursor-pointer accent-indigo-500"
                                   oninput="document.getElementById('steps-val').innerText = this.value">
                        </div>
                    </div>
                </div>

                <!-- 生成按鈕 -->
                <button id="generate-btn" onclick="generateSpeech()" class="w-full py-4 px-6 bg-gradient-to-r from-cyan-500 via-sky-500 to-indigo-600 hover:from-cyan-400 hover:to-indigo-550 text-white font-semibold rounded-xl shadow-lg shadow-indigo-500/10 transition-all duration-300 flex items-center justify-center space-x-3 text-base">
                    <i data-lucide="play" class="w-5 h-5"></i>
                    <span>立即生成高品質預設語音</span>
                </button>
            </div>

            <!-- 生成結果播放器 -->
            <div id="result-card" class="bg-slate-900/40 border border-slate-800/80 rounded-2xl p-6 space-y-4 hidden shadow-2xl">
                <div class="flex items-center justify-between">
                    <div class="flex items-center space-x-2">
                        <span class="flex h-2.5 w-2.5 relative">
                            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                            <span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-emerald-500"></span>
                        </span>
                        <h3 class="text-sm font-medium text-emerald-400">語音合成成功！</h3>
                    </div>
                    <span class="text-xs text-slate-555">取樣率: 48kHz (Studio Quality)</span>
                </div>
                
                <div class="bg-slate-950/60 p-4 rounded-xl flex flex-col md:flex-row items-center justify-between gap-4 border border-slate-850">
                    <div class="flex items-center space-x-3 w-full md:w-auto">
                        <button onclick="togglePlayPause()" class="p-3 bg-indigo-600 hover:bg-indigo-500 text-white rounded-full transition shadow-lg shadow-indigo-600/20 flex-shrink-0" title="播放 / 暫停">
                            <i id="play-pause-icon" data-lucide="play" class="w-5 h-5"></i>
                        </button>
                        
                        <button id="loop-toggle-btn" onclick="toggleLoop()" class="p-2.5 bg-slate-900 hover:bg-slate-850 text-slate-400 rounded-lg transition border border-slate-800 flex-shrink-0 flex items-center justify-center" title="重複播放模式">
                            <i id="loop-icon" data-lucide="repeat" class="w-4 h-4"></i>
                        </button>

                        <div class="flex-1 md:flex-initial truncate">
                            <p class="text-xs text-slate-500 flex items-center space-x-1">
                                <span>生成音訊檔</span>
                                <span id="loop-status-badge" class="text-[9px] bg-slate-900 text-slate-550 px-1 py-0.5 rounded transition">循環：關</span>
                            </p>
                            <p id="audio-file-name" class="text-sm font-semibold text-slate-200 max-w-[200px] truncate">voxcpm_tts_output.wav</p>
                        </div>
                    </div>
                    
                    <div class="flex items-end space-x-1 h-8 w-40 justify-center overflow-hidden">
                        <div class="w-1 bg-indigo-500 rounded-full h-1 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-3 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-5 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-2 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-4 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-6 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-3 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-5 wave-bar transition-all duration-150"></div>
                        <div class="w-1 bg-indigo-500 rounded-full h-1 wave-bar transition-all duration-150"></div>
                    </div>

                    <audio id="audio-player" class="hidden" onended="audioPlaybackEnded()"></audio>
                    
                    <button onclick="downloadAudio()" class="py-2 px-4 bg-slate-900 hover:bg-slate-850 text-slate-200 rounded-lg text-xs font-medium border border-slate-800 flex items-center space-x-2 transition">
                        <i data-lucide="download" class="w-3.5 h-3.5"></i>
                        <span>下載音訊</span>
                    </button>
                </div>
            </div>
        </section>
    </main>

    <footer class="border-t border-slate-900 py-6 text-center text-xs text-slate-500 bg-slate-950 mt-12">
        <p>© 2026 OpenBMB VoxCPM & Web Studio 模擬測試面板</p>
    </footer>

    <div id="toast" class="fixed bottom-6 right-6 bg-slate-900 border border-slate-800 px-4 py-3 rounded-xl shadow-2xl flex items-center space-x-2 text-sm text-slate-250 transition-all duration-300 translate-y-20 opacity-0 pointer-events-none z-50">
        <i id="toast-icon" data-lucide="check-circle" class="w-4 h-4 text-emerald-400"></i>
        <span id="toast-msg">已成功複製指令！</span>
    </div>

    <script>
        lucide.createIcons();
        let advancedOpen = false;
        let generatedAudioBlobUrl = null;
        let isPlaying = false;
        let isLooping = false;
        let animationFrameId = null;

        updateCharCount();

        async function translateAndPaste() {
            const btn = document.getElementById('translate-btn');
            const zhText = document.getElementById('translate-input-zh').value.trim();
            if (!zhText) { showToast("請先輸入中文日常對話內容！", "alert-circle"); return; }
            btn.disabled = true;
            btn.innerHTML = `<i data-lucide="loader" class="w-3.5 h-3.5 animate-spin"></i><span>AI 翻譯對齊中...</span>`;
            lucide.createIcons();
            const systemPrompt = `You are a professional voice dubbing translator. Translate the given Chinese text into natural, spoken English for daily conversations. Guidelines: 1. MUST sound natural/spoken. 2. AVOID rare/formal vocab. 3. Simple structure. 4. Return ONLY the English text.`;
            const apiKey = ""; 
            const payload = { contents: [{ parts: [{ text: zhText }] }], systemInstruction: { parts: [{ text: systemPrompt }] } };
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            let response = await fetch(url, { method: "POST", headers: { "Content-Type": "application/json" }, body: JSON.stringify(payload) });
            if (response.ok) {
                const result = await response.json();
                let enText = result.candidates?.[0]?.content?.parts?.[0]?.text;
                if (enText) { document.getElementById('text-input').value = enText.trim(); updateCharCount(); showToast("口語翻譯成功！", "check-circle"); }
            } else { showToast("翻譯失敗，請稍後再試！", "x-circle"); }
            btn.disabled = false;
            btn.innerHTML = `<i data-lucide="languages" class="w-3.5 h-3.5"></i><span>中翻英並自動貼上</span>`;
            lucide.createIcons();
        }

        function setTranslateSentence(sentence) { document.getElementById('translate-input-zh').value = sentence; showToast("已載入快捷對話！", "sparkles"); }
        function toggleAdvanced() { advancedOpen = !advancedOpen; document.getElementById('advanced-panel').classList.toggle('hidden'); document.getElementById('advanced-chevron').classList.toggle('rotate-90'); }
        function updateCharCount() { document.getElementById('char-count').innerText = `${document.getElementById('text-input').value.length} / 200 字`; }
        function showToast(msg, iconName) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            document.getElementById('toast-icon').setAttribute('data-lucide', iconName);
            lucide.createIcons();
            toast.classList.remove('translate-y-20', 'opacity-0', 'pointer-events-none');
            setTimeout(() => { toast.classList.add('translate-y-20', 'opacity-0', 'pointer-events-none'); }, 2500);
        }

        async function generateSpeech() {
            const btn = document.getElementById('generate-btn');
            const textInput = document.getElementById('text-input').value.trim();
            const presetVoice = document.querySelector('input[name="preset-voice"]:checked').value;
            if (!textInput) { showToast("請輸入文本！", "alert-circle"); return; }
            btn.disabled = true;
            btn.innerHTML = `<i data-lucide="loader" class="w-5 h-5 animate-spin"></i><span>生成中...</span>`;
            const payload = { contents: [{ parts: [{ text: `Say naturally: ${textInput}` }] }], generationConfig: { responseModalities: ["AUDIO"], speechConfig: { voiceConfig: { prebuiltVoiceConfig: { voiceName: presetVoice } } } }, model: "gemini-2.5-flash-preview-tts" };
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=`, { method: "POST", headers: { "Content-Type": "application/json" }, body: JSON.stringify(payload) });
            if (response.ok) {
                const result = await response.json();
                const base64Data = result.candidates[0].content.parts.find(p => p.inlineData).inlineData.data;
                const blob = new Blob([new Uint8Array(atob(base64Data).split('').map(c => c.charCodeAt(0)))], { type: 'audio/wav' });
                generatedAudioBlobUrl = URL.createObjectURL(blob);
                const player = document.getElementById('audio-player');
                player.src = generatedAudioBlobUrl;
                document.getElementById('result-card').classList.remove('hidden');
                showToast("生成成功！", "check-circle");
            }
            btn.disabled = false;
            btn.innerHTML = `<i data-lucide="play" class="w-5 h-5"></i><span>立即生成高品質預設語音</span>`;
            lucide.createIcons();
        }

        function toggleLoop() { isLooping = !isLooping; document.getElementById('audio-player').loop = isLooping; document.getElementById('loop-status-badge').innerText = isLooping ? "循環：開" : "循環：關"; }
        function togglePlayPause() { const player = document.getElementById('audio-player'); isPlaying ? player.pause() : player.play(); isPlaying = !isPlaying; document.getElementById('play-pause-icon').setAttribute('data-lucide', isPlaying ? 'pause' : 'play'); lucide.createIcons(); isPlaying ? startWaveAnimation() : stopWaveAnimation(); }
        function downloadAudio() { const a = document.createElement('a'); a.href = generatedAudioBlobUrl; a.download = "voxcpm_tts_output.wav"; a.click(); }
        function audioPlaybackEnded() { isPlaying = false; document.getElementById('play-pause-icon').setAttribute('data-lucide', 'play'); lucide.createIcons(); stopWaveAnimation(); }
        function startWaveAnimation() { /* 動畫邏輯 */ }
        function stopWaveAnimation() { /* 動畫停止邏輯 */ }
    </script>
</body>
</html>
