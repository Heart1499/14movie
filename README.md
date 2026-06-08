<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>小雨披大导演 · 锐因困境逃生模拟器</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            background: #0f0e0c;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Courier New', 'SF Mono', 'Segoe UI', monospace;
            padding: 20px;
        }

        /* 导演控制台风格 宽屏精致感 */
        .studio {
            max-width: 1300px;
            width: 100%;
            background: #1a1a1a;
            border-radius: 32px;
            box-shadow: 0 25px 45px rgba(0,0,0,0.6), 0 0 0 1px #3a2c24 inset, 0 0 0 2px #2f241d inset;
            overflow: hidden;
            backdrop-filter: blur(2px);
        }

        /* 监控区域 */
        .camera-feed {
            background: #010101;
            position: relative;
            padding: 20px 24px 24px;
            border-bottom: 3px solid #e09d5e;
        }

        .cam-label {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 12px;
            color: #b0b7bc;
            font-size: 13px;
            letter-spacing: 1px;
        }

        .red-dot {
            display: inline-block;
            width: 10px;
            height: 10px;
            background: #e34d4d;
            border-radius: 50%;
            box-shadow: 0 0 6px red;
            margin-right: 8px;
            animation: pulse 1.2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 0.4; transform: scale(0.8);}
            100% { opacity: 1; transform: scale(1);}
        }

        .room-canvas {
            background: #0a0a0a;
            border-radius: 28px;
            padding: 16px;
            border: 1px solid #3e2e24;
        }

        .scene-graphic {
            background: #1b1917;
            border-radius: 24px;
            min-height: 280px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
            background-image: radial-gradient(circle at 20% 40%, #2c241e 1%, transparent 1%);
            background-size: 18px 18px;
        }

        .character-row {
            display: flex;
            justify-content: center;
            gap: 60px;
            flex-wrap: wrap;
            margin: 20px 0;
        }

        .character-card {
            background: #2b241f;
            border-radius: 48px;
            padding: 12px 30px 12px 20px;
            display: flex;
            align-items: center;
            gap: 18px;
            box-shadow: 0 5px 0 #0f0b08;
            border-bottom: 2px solid #e2a267;
        }

        .avatar {
            width: 64px;
            height: 64px;
            background: #4a3729;
            border-radius: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 36px;
            font-weight: bold;
            color: #f0cfaa;
        }

        .info h3 {
            color: #f3d382;
            font-size: 20px;
        }

        .info p {
            color: #bcafa2;
            font-size: 13px;
        }

        .status-meter {
            margin-top: 12px;
            background: #2c241e;
            border-radius: 40px;
            padding: 10px 16px;
            display: flex;
            gap: 24px;
            justify-content: center;
            font-size: 13px;
            font-family: monospace;
        }

        .meter span:first-child {
            color: #e6bc8b;
        }

        .action-log {
            background: #0c0b0a;
            margin: 16px 20px 20px 20px;
            border-radius: 20px;
            padding: 12px 18px;
            color: #dad1c4;
            font-size: 14px;
            font-family: monospace;
            border-left: 6px solid #cb7b3c;
        }

        /* 导戏控制区 */
        .director-panel {
            background: #1f1b17;
            padding: 20px 24px 28px;
        }

        .script-title {
            font-size: 18px;
            font-weight: bold;
            color: #f2cd9b;
            margin-bottom: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
            border-left: 3px solid #f3b467;
            padding-left: 12px;
        }

        .action-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 14px;
            margin-bottom: 30px;
        }

        .director-btn {
            background: #31281f;
            border: 1px solid #6c4f35;
            color: #fee3bf;
            padding: 12px 20px;
            border-radius: 80px;
            font-weight: bold;
            font-family: monospace;
            font-size: 15px;
            cursor: pointer;
            transition: 0.07s linear;
            flex: 1 0 auto;
            text-align: center;
        }

        .director-btn:active {
            background: #4e3928;
            transform: scale(0.96);
        }

        .progress-area {
            margin-top: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .escape-meter {
            background: #2a241f;
            height: 12px;
            width: 70%;
            border-radius: 20px;
            overflow: hidden;
        }

        .fill {
            background: #da873f;
            width: 0%;
            height: 100%;
            transition: width 0.2s;
        }

        .reset-btn {
            background: #4f3b2b;
            border: none;
            padding: 6px 18px;
            border-radius: 30px;
            color: white;
            cursor: pointer;
        }

        .ending-card {
            background: #211b15e6;
            backdrop-filter: blur(8px);
            border-radius: 40px;
            padding: 28px;
            text-align: center;
            margin: 20px;
            border: 1px solid #dda15e;
        }

        @media (max-width: 700px) {
            .character-card { padding: 8px 16px; gap: 10px;}
            .avatar { width: 48px; height: 48px; font-size: 28px;}
            .director-btn { font-size: 12px; padding: 8px 12px;}
        }
        button {
            background: none;
            border: none;
            cursor: pointer;
        }
    </style>
</head>
<body>
<div class="studio" id="studioApp">
    <div class="camera-feed">
        <div class="cam-label">
            <span><span class="red-dot"></span> LIVE · 密闭房间监控</span>
            <span>导演视角 | 强制剧情</span>
        </div>
        <div class="room-canvas">
            <div class="scene-graphic" id="sceneGraphic">
                <div class="character-row">
                    <div class="character-card">
                        <div class="avatar">🐺</div>
                        <div class="info"><h3>申惟</h3><p>队长 · 试图冷静但耳朵发烫</p></div>
                    </div>
                    <div class="character-card">
                        <div class="avatar">🐰</div>
                        <div class="info"><h3>韩振</h3><p>中国弟 · 假装淡定实则抠手</p></div>
                    </div>
                </div>
                <div class="status-meter">
                    <span>🧊 申惟紧绷值: <span id="tensionS">72</span>%</span>
                    <span>🍃 韩振回避值: <span id="tensionH">68</span>%</span>
                    <span>🚪 逃脱进度: <span id="escapeVal">0</span>%</span>
                </div>
            </div>
        </div>
        <div class="action-log" id="actionLog">
            📹 系统: 不do就不能出去的房间。摄像头已就位，导演请指示。
        </div>
    </div>
    <div class="director-panel" id="directorPanel">
        <div class="script-title">
            🎬 小雨披大导演 · 指令台
        </div>
        <div class="action-buttons" id="actionGrid">
            <!-- 动态按钮会在这里刷新 但为了方便 写成静态但逻辑重置可用 -->
        </div>
        <div class="progress-area">
            <div class="escape-meter"><div class="fill" id="escapeFill"></div></div>
            <button class="reset-btn" id="resetGameBtn">🎞️ 重新开拍</button>
        </div>
    </div>
</div>

<script>
    // ---------- 锐因 困境模拟器 ----------
    // 完全基于真实物料风格：躲闪，信息差，语言小暧昧，不do不出门规则
    // 状态变量
    let tensionS = 72;    // 申惟紧张/躲避值 越高越不敢对视
    let tensionH = 68;    // 韩振局促值 高时会回避互动
    let escape = 0;       // 逃脱进度 满100则通关
    
    let round = 0;
    let gameActive = true;
    let endingTriggered = false;
    
    // 存储对话记录
    let logEntries = [];
    
    // DOM 元素
    const tensionSEl = document.getElementById('tensionS');
    const tensionHEl = document.getElementById('tensionH');
    const escapeValSpan = document.getElementById('escapeVal');
    const escapeFillDiv = document.getElementById('escapeFill');
    const actionLogDiv = document.getElementById('actionLog');
    const actionGrid = document.getElementById('actionGrid');
    const resetBtn = document.getElementById('resetGameBtn');
    
    function addLog(msg) {
        logEntries.unshift(msg);
        if(logEntries.length > 8) logEntries.pop();
        actionLogDiv.innerHTML = `🎥 ${msg}<br>` + logEntries.slice(1).map(l => `&nbsp;&nbsp;${l}`).join('<br>');
    }
    
    function updateUI() {
        tensionSEl.innerText = Math.min(100, Math.max(0, Math.floor(tensionS)));
        tensionHEl.innerText = Math.min(100, Math.max(0, Math.floor(tensionH)));
        let escPercent = Math.min(100, Math.max(0, Math.floor(escape)));
        escapeValSpan.innerText = escPercent;
        escapeFillDiv.style.width = escPercent + '%';
        if(escapeFillDiv.style.width === '100%') escapeFillDiv.style.background = "#b3d160";
        else escapeFillDiv.style.background = "#da873f";
    }
    
    // 核心互动方法 (导演指令)
    function applyAction(cmdId) {
        if(!gameActive) return;
        if(escape >= 100) {
            addLog("⚠️ 房间已经解锁，无需再导演。按重新开拍继续玩");
            return;
        }
        // 记录执行前的值
        let oldEscape = escape;
        let oldTensionS = tensionS;
        let oldTensionH = tensionH;
        
        // 根据指令改变数值，基于真实物料习性: 躲闪, 语言梗, 异国推拉
        switch(cmdId) {
            case "demand_eye":   // 强制对视指令
                addLog("📢 导演: “申惟韩振，现在对视十秒！不许躲！”");
                if(tensionS > 55) {
                    let reduce = Math.floor(Math.random() * 12) + 5;
                    tensionS = Math.max(20, tensionS - reduce);
                    addLog(`👀 申惟脖子僵硬但被迫对视，耳朵红透，紧张值-${reduce}。`);
                } else {
                    tensionS = Math.max(15, tensionS - 3);
                    addLog(`👀 申惟飞快扫一眼又转开，但总算没逃跑。紧张值-3。`);
                }
                if(tensionH > 60) {
                    let reduceH = Math.floor(Math.random() * 10) + 4;
                    tensionH = Math.max(25, tensionH - reduceH);
                    addLog(`🍃 韩振咬了下嘴唇，笑了一下，局促感-${reduceH}。`);
                } else {
                    tensionH = Math.max(20, tensionH - 2);
                    addLog(`🍃 韩振努力直视回去，气氛微妙缓和。`);
                }
                // 对视促进逃脱 +3~7
                let gain = Math.floor(Math.random() * 7) + 4;
                escape = Math.min(100, escape + gain);
                addLog(`🔓 空气里有点不对劲... 房门好像松动了一点 (+${gain}%逃脱进度)`);
                break;
            case "teach_lang":   // 教中文/韩语
                addLog("🎙️ 导演: “韩振，教申惟一句中文情话，申惟你跟着念。”");
                tensionS = Math.max(20, tensionS - 8);
                tensionH = Math.max(20, tensionH - 5);
                let langGain = Math.floor(Math.random() * 9) + 5;
                escape = Math.min(100, escape + langGain);
                addLog(`🇨🇳 韩振小声说“我爱你”，申惟跟着念但发音跑调，两人都笑了。紧张值双双下降，逃脱进度+${langGain}%。`);
                break;
            case "acc_touch":    // 不经意触碰
                addLog("✋ 导演: “假装整理衣领，来一个不小心碰到手。”");
                if(tensionS > 50) {
                    tensionS = Math.max(30, tensionS - 9);
                    addLog(`⚡ 申惟被碰到瞬间抖了一下，但没躲开，紧张值-9。`);
                } else {
                    tensionS = Math.max(10, tensionS - 4);
                }
                tensionH = Math.max(25, tensionH - 6);
                let touchEscape = Math.floor(Math.random() * 12) + 3;
                escape = Math.min(100, escape + touchEscape);
                addLog(`🤏 韩振指尖碰到申惟手腕，两个人安静了三秒，进度+${touchEscape}%。`);
                break;
            case "confess_rumor": // 提及匿名短信/锐化事件
                addLog("📨 导演: “韩振，你告诉他‘锐化的原因’小号是你。”);
                tensionS = Math.max(18, tensionS - 15);
                tensionH = Math.max(15, tensionH - 10);
                let bigEscape = 14 + Math.floor(Math.random() * 9);
                escape = Math.min(100, escape + bigEscape);
                addLog(`📝 申惟愣了:“原来是你…” 韩振低头笑。气氛突然不尴尬了。紧张值骤降，逃脱进度+${bigEscape}%。`);
                break;
            case "fake_fight":    // 假装吵架推拉
                addLog("🤬 导演指令:“你们现在冷战三分钟不许说话。”");
                tensionS = Math.min(95, tensionS + 12);
                tensionH = Math.min(92, tensionH + 10);
                addLog(`❄️ 两人背对背坐着，申惟抠手指，韩振叹气。紧张值回升，房门纹丝不动。`);
                break;
            case "backhug_dare":  // 背后抱指导
                addLog("🧥 导演:“申惟，从后面帮韩振整理外套，靠近一点”");
                if(tensionS > 60) {
                    tensionS = Math.max(25, tensionS - 14);
                    addLog(`🐺 申惟犹豫几秒最终轻轻碰了韩振肩膀，韩振僵住但没躲，紧张值骤降。`);
                } else {
                    tensionS = Math.max(10, tensionS - 6);
                }
                tensionH = Math.max(28, tensionH - 7);
                let hugEscape = Math.floor(Math.random() * 10) + 7;
                escape = Math.min(100, escape + hugEscape);
                addLog(`🤲 非常接近，韩振耳尖红了，进度+${hugEscape}%。`);
                break;
            case "memory_jeju":    // 济州岛约定
                addLog("🏝️ 导演:“问申惟，你还记得韩振说想和你去济州岛吗？”");
                tensionS = Math.max(25, tensionS - 8);
                tensionH = Math.max(20, tensionH - 6);
                let memEsc = Math.floor(Math.random() * 9) + 6;
                escape = Math.min(100, escape + memEsc);
                addLog(`🌊 申惟结巴: “记得… 等出去以后。” 韩振偷笑。进度+${memEsc}%。`);
                break;
            case "random_dodge":   // 故意让申惟躲避
                addLog("🎭 导演:“韩振突然凑近申惟，申惟必须瞬间躲开。”");
                tensionS = Math.min(99, tensionS + 15);
                tensionH = Math.max(40, tensionH - 3);
                addLog(`💨 申惟差点从沙发弹起来，韩振一脸无辜: “哥怎么了？” 申惟又怂又气，紧张值↑。但躲避增加了喜剧效果。`);
                break;
            case "whisper_secret": // 耳语悄悄话
                addLog("👂🏻 导演:“韩振对申惟说韩语悄悄话，内容随便。”");
                tensionS = Math.max(20, tensionS - 12);
                tensionH = Math.max(18, tensionH - 7);
                let whisperEscape = Math.floor(Math.random() * 10) + 5;
                escape = Math.min(100, escape + whisperEscape);
                addLog(`🤫 韩振用刚学的韩语说“申惟哥帅气”，申惟笑了。房门锁咔哒一声(+${whisperEscape}%)。`);
                break;
            default: break;
        }
        
        // 边界钳制
        tensionS = Math.min(99, Math.max(5, tensionS));
        tensionH = Math.min(99, Math.max(5, tensionH));
        
        // 特殊逻辑: 如果双方紧张值同时低于30，自动增加额外逃脱进度(敞开心扉)
        if(tensionS < 35 && tensionH < 35 && escape < 95 && !endingTriggered) {
            let extra = 8;
            escape = Math.min(100, escape + extra);
            addLog(`💞 两人突然对视后同时叹气笑了，好像默认了什么，心防解除 +${extra}% 逃脱。`);
        }
        
        // 检查逃脱结局
        if(escape >= 100 && !endingTriggered) {
            escape = 100;
            gameActive = true; // 展示结局但不再接受新指令
            showEnding();
            return;
        }
        updateUI();
        
        // 增加回合计数器，氛围彩蛋
        round++;
        if(escape < 30 && round>6 && tensionS>70 && tensionH>70) {
            addLog("🎬 导演头疼: 两个人像鱼和自行车一样尴尬，房门纹丝不动！再多给点刺激吧。");
        }
        if(escape > 70 && tensionS<40 && tensionH<40) {
            addLog("✨ 监控收音: 韩振小声哼歌，申惟悄悄靠近了。门缝透进来一点光。");
        }
        updateUI();
    }
    
    function showEnding() {
        endingTriggered = true;
        gameActive = false;
        let endingMsg = "";
        // 根据最终数值生成多样结局 (基于互动结果)
        if(tensionS <= 30 && tensionH <= 35) {
            endingMsg = "🎬 大结局: 门终于打开，申惟和韩振一前一后走出来，申惟耳朵还是红的，韩振笑着说了句中文“谢谢导演”。他们好像变成真正能对视的关系了。小雨披导演！你成功促成锐因大和谐！";
        } else if(tensionS > 60 || tensionH > 65) {
            endingMsg = "🎬 房门是开了，但申惟快步走在前面，韩振跟在后面低着头。出来后两人还是别扭，但粉丝拍到了申惟回头看韩振的瞬间。暧昧延续，导演你走了一条缺德但余韵悠长的路。";
        } else {
            endingMsg = "🎬 门在沉默中打开。申惟韩振同时松了一口气，并排走出去时肩膀偶尔碰到也没有躲。算不上轰轰烈烈，但气氛微妙变成熟了。导演你的调教有方，这也许是最好的he。";
        }
        // 将原有导演面板替换为结局卡
        const directorPanelDiv = document.getElementById('directorPanel');
        const originalInner = directorPanelDiv.innerHTML;
        directorPanelDiv.innerHTML = `
            <div class="ending-card">
                <div style="font-size: 40px; margin-bottom: 12px;">🏆</div>
                <h2 style="color:#f2bc7a;">杀青 · 密室逃脱成功</h2>
                <p style="margin: 16px 0; color:#e2cfb3; font-size: 16px;">${endingMsg}</p>
                <button class="reset-btn" id="resetAfterEnd" style="background:#c28242; padding:10px 24px;">🎬 重新开机 再导一遍</button>
            </div>
            <div class="progress-area" style="margin-top: 20px;">
                <div class="escape-meter"><div class="fill" style="width:100%"></div></div>
                <button class="reset-btn" id="resetAfterEnd2">🎞️ 重置</button>
            </div>
        `;
        const resetEnd = document.getElementById('resetAfterEnd');
        const resetEnd2 = document.getElementById('resetAfterEnd2');
        const resetFunc = () => { resetGame(); };
        if(resetEnd) resetEnd.addEventListener('click', resetFunc);
        if(resetEnd2) resetEnd2.addEventListener('click', resetFunc);
        updateUI();
    }
    
    function resetGame() {
        tensionS = 72;
        tensionH = 68;
        escape = 0;
        round = 0;
        gameActive = true;
        endingTriggered = false;
        logEntries = [];
        updateUI();
        // 还原导演面板的按钮布局
        const directorDiv = document.getElementById('directorPanel');
        directorDiv.innerHTML = `
            <div class="script-title">
                🎬 小雨披大导演 · 指令台
            </div>
            <div class="action-buttons" id="actionGrid"></div>
            <div class="progress-area">
                <div class="escape-meter"><div class="fill" id="escapeFill"></div></div>
                <button class="reset-btn" id="resetGameBtn">🎞️ 重新开拍</button>
            </div>
        `;
        // 重置填充条和绑定变量
        const newFill = document.getElementById('escapeFill');
        if(newFill) newFill.style.width = '0%';
        const newReset = document.getElementById('resetGameBtn');
        if(newReset) newReset.addEventListener('click', resetGame);
        initActionButtons();
        addLog("🎬 导演重启摄像机，申惟韩振又被关回房间，一切从头。紧张值回归初始。");
        updateUI();
    }
    
    function initActionButtons() {
        const container = document.getElementById('actionGrid');
        if(!container) return;
        // 动作库 符合真实相处模式 基于锐因的躲闪/教语言/济州岛/保护/暗号
        const actions = [
            { id: "demand_eye", label: "🎥 强制对视指令" },
            { id: "teach_lang", label: "📖 教一句中文情话" },
            { id: "acc_touch", label: "✋ 不经意触碰手背" },
            { id: "confess_rumor", label: "📱 坦白锐化小号" },
            { id: "fake_fight", label: "❄️ 安排冷战五分钟" },
            { id: "backhug_dare", label: "🧥 背后整理衣领" },
            { id: "memory_jeju", label: "🏝️ 提起济州岛旅行约定" },
            { id: "random_dodge", label: "💨 设计突然躲避环节" },
            { id: "whisper_secret", label: "👂 耳语悄悄话" }
        ];
        container.innerHTML = "";
        actions.forEach(act => {
            let btn = document.createElement('button');
            btn.className = "director-btn";
            btn.innerText = act.label;
            btn.onclick = () => { applyAction(act.id); };
            container.appendChild(btn);
        });
        // 确保reset重新绑定
        const resetBtnElem = document.getElementById('resetGameBtn');
        if(resetBtnElem) resetBtnElem.onclick = () => resetGame();
    }
    
    // 初始化整个页面
    function initGame() {
        initActionButtons();
        addLog("🎞️ 雨披导演上线！ 房间规则: 不do就不能出去 (do指的是打破尴尬对视或者敞开心扉)。使用指令推动二人关系。");
        updateUI();
    }
    
    resetBtn.addEventListener('click', resetGame);
    initGame();
</script>
</body>
</html>
