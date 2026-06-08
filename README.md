<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>小雨披大导演 · 锐因九号房</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: #0a0705;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: system-ui, -apple-system, 'Segoe UI', monospace;
            padding: 16px;
        }

        .control-room {
            max-width: 1400px;
            width: 100%;
            background: #11100e;
            border-radius: 40px;
            box-shadow: 0 30px 50px rgba(0,0,0,0.6), 0 0 0 1px #4a3524 inset;
            overflow: hidden;
        }

        .camera-wall {
            background: #050403;
            padding: 20px 24px 16px;
            border-bottom: 2px solid #b87c4a;
        }

        .cam-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 16px;
            color: #bfa98e;
            font-size: 12px;
            letter-spacing: 1px;
        }

        .live-dot {
            display: inline-block;
            width: 10px;
            height: 10px;
            background: #e34d4d;
            border-radius: 50%;
            box-shadow: 0 0 8px red;
            margin-right: 8px;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { opacity: 0.5; transform: scale(0.9);}
            100% { opacity: 1; transform: scale(1);}
        }

        .room-preview {
            background: #0c0a08;
            border-radius: 32px;
            padding: 20px;
            border: 1px solid #36281d;
        }

        .characters-area {
            display: flex;
            justify-content: center;
            gap: 50px;
            flex-wrap: wrap;
            margin: 10px 0 20px;
        }

        .char-card {
            background: #201a14;
            border-radius: 60px;
            padding: 12px 24px;
            display: flex;
            align-items: center;
            gap: 16px;
            box-shadow: 0 6px 0 #0b0805;
            border-bottom: 2px solid #d6955a;
        }

        .char-icon {
            width: 56px;
            height: 56px;
            background: #3f2c1d;
            border-radius: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
        }

        .char-name {
            color: #f3cf9a;
            font-weight: bold;
            font-size: 18px;
        }

        .char-tag {
            font-size: 12px;
            color: #b49470;
        }

        .mood-panel {
            background: #1f1914;
            border-radius: 30px;
            padding: 12px 20px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 16px;
            margin-top: 8px;
        }

        .mood-item {
            font-size: 13px;
            font-family: monospace;
            background: #2c241e;
            padding: 6px 16px;
            border-radius: 30px;
        }

        .action-log {
            background: #0d0b09;
            margin: 18px 20px 20px 20px;
            border-radius: 24px;
            padding: 14px 18px;
            color: #d7cdbc;
            font-size: 13px;
            font-family: monospace;
            border-left: 5px solid #d78c45;
            min-height: 100px;
        }

        .director-console {
            background: #1a1511;
            padding: 20px 24px 28px;
        }

        .section-title {
            font-size: 18px;
            font-weight: bold;
            color: #e7bc82;
            margin-bottom: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
            border-left: 3px solid #e2a15b;
            padding-left: 14px;
        }

        .command-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 30px;
        }

        .cmd-btn {
            background: #2c221b;
            border: 1px solid #745d45;
            color: #ffefdb;
            padding: 12px 18px;
            border-radius: 60px;
            font-family: monospace;
            font-weight: bold;
            font-size: 14px;
            cursor: pointer;
            flex: 1 0 auto;
            text-align: center;
            transition: 0.05s linear;
        }

        .cmd-btn:active {
            background: #4e3725;
            transform: scale(0.96);
        }

        .progress-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 16px;
            margin-top: 8px;
        }

        .escape-bar {
            background: #2a221c;
            height: 12px;
            flex: 1;
            border-radius: 20px;
            overflow: hidden;
        }

        .escape-fill {
            background: #d97838;
            width: 0%;
            height: 100%;
            transition: width 0.2s;
        }

        .reset-btn {
            background: #4f3824;
            border: none;
            padding: 6px 20px;
            border-radius: 40px;
            color: white;
            cursor: pointer;
            font-family: monospace;
        }

        .ending-box {
            background: #221c16e0;
            backdrop-filter: blur(12px);
            border-radius: 36px;
            padding: 28px;
            text-align: center;
            margin: 20px 0;
            border: 1px solid #e5a362;
        }

        @media (max-width: 700px) {
            .char-card { padding: 8px 16px; gap: 10px;}
            .cmd-btn { font-size: 11px; padding: 8px 10px;}
        }
    </style>
</head>
<body>
<div class="control-room" id="appRoot">
    <div class="camera-wall">
        <div class="cam-header">
            <span><span class="live-dot"></span> 九号房 · 封闭监控</span>
            <span>🎬 小雨披导演指令系统</span>
        </div>
        <div class="room-preview">
            <div class="characters-area">
                <div class="char-card">
                    <div class="char-icon">🐺</div>
                    <div><div class="char-name">申惟</div><div class="char-tag">队长 · 年上 · 容易红温</div></div>
                </div>
                <div class="char-card">
                    <div class="char-icon">🐰</div>
                    <div><div class="char-name">韩振</div><div class="char-tag">中国弟 · 推拉 · 爱逗哥哥</div></div>
                </div>
            </div>
            <div class="mood-panel">
                <span class="mood-item">🔥 申惟忍耐值: <span id="tensionS">68</span>%</span>
                <span class="mood-item">💗 韩振羞耻值: <span id="tensionH">65</span>%</span>
                <span class="mood-item">🔓 逃脱进度: <span id="escapeVal">0</span>%</span>
            </div>
        </div>
        <div class="action-log" id="actionLog">
            📼 系统: 房间规则——身体接触指数达标才能开门。导演请下达指令。
        </div>
    </div>
    <div class="director-console" id="directorConsole"></div>
</div>

<script>
    // 游戏状态
    let tensionS = 68;
    let tensionH = 65;
    let escape = 0;
    let gameActive = true;
    let ended = false;
    let logs = [];

    // 获取DOM元素
    function getTensionS() { return document.getElementById('tensionS'); }
    function getTensionH() { return document.getElementById('tensionH'); }
    function getEscapeVal() { return document.getElementById('escapeVal'); }
    function getEscapeFill() { return document.getElementById('escapeFill'); }
    function getActionLog() { return document.getElementById('actionLog'); }

    function updateUI() {
        const ts = getTensionS();
        const th = getTensionH();
        const ev = getEscapeVal();
        const fill = getEscapeFill();
        if(ts) ts.innerText = Math.min(99, Math.max(0, Math.floor(tensionS)));
        if(th) th.innerText = Math.min(99, Math.max(0, Math.floor(tensionH)));
        const escPercent = Math.min(100, Math.max(0, Math.floor(escape)));
        if(ev) ev.innerText = escPercent;
        if(fill) fill.style.width = escPercent + '%';
    }

    function addLog(msg) {
        logs.unshift(msg);
        if(logs.length > 9) logs.pop();
        const logDiv = getActionLog();
        if(logDiv) {
            logDiv.innerHTML = `🎬 ${msg}<br>` + logs.slice(1).map(l => `&nbsp;&nbsp;${l}`).join('<br>');
        }
    }

    // 执行指令
    function executeCommand(cmdId) {
        if(!gameActive) {
            addLog("游戏已结束，请按重新开拍。");
            return;
        }
        if(escape >= 100) {
            addLog("房间已解锁，不用再指令。按重新开拍继续导演。");
            return;
        }

        let deltaS = 0, deltaH = 0, deltaEsc = 0;
        let flavorText = "";

        switch(cmdId) {
            case "kiss_cmd":
                addLog("🎥 导演指令:“韩振，去亲一下申惟的嘴角。”");
                if(tensionS > 55) { deltaS = -12; flavorText = "申惟僵住没敢动，耳尖烧红，被轻轻啄了一下。"; }
                else { deltaS = -6; flavorText = "申惟闭了一下眼，韩振飞快碰了一下，两人都懵了。"; }
                deltaH = -8; deltaEsc = 9 + Math.floor(Math.random() * 7);
                break;
            case "lap_cmd":
                addLog("🎥 导演指令:“申惟，让韩振坐你腿上。”");
                if(tensionS > 60) { deltaS = -14; flavorText = "申惟耳朵滴血，韩振小心翼翼坐上去，两个人都不敢看对方。"; }
                else { deltaS = -7; flavorText = "韩振笑着坐下，申惟的手犹豫半天才放到腰侧。"; }
                deltaH = -10; deltaEsc = 10 + Math.floor(Math.random() * 8);
                break;
            case "neck_cmd":
                addLog("🎥 导演指令:“韩振在申惟脖子旁边说话。”");
                deltaS = -9; deltaH = -5; deltaEsc = 7 + Math.floor(Math.random() * 6);
                flavorText = "韩振凑近耳边用中文说了句“哥好香”，申惟差点跳起来。";
                break;
            case "hand_cmd":
                addLog("🎥 导演指令:“申惟牵住韩振的手，十指相扣。”");
                deltaS = -8; deltaH = -7; deltaEsc = 6 + Math.floor(Math.random() * 6);
                flavorText = "申惟慢慢扣住韩振的手指，韩振回握，掌心出汗也没松开。";
                break;
            case "undress_cmd":
                addLog("🎥 导演指令:“韩振帮申惟解开最上面两颗扣子。”");
                if(tensionS > 70) { deltaS = -16; flavorText = "申惟喉结滚动，韩振手指发抖解了两颗，锁骨露出来。"; }
                else { deltaS = -8; flavorText = "韩振动作轻缓，申惟屏住呼吸。"; }
                deltaH = -9; deltaEsc = 12 + Math.floor(Math.random() * 7);
                break;
            case "whisper_cmd":
                addLog("🎥 导演指令:“申惟对韩振耳边说韩语情话。”");
                deltaS = -6; deltaH = -11; deltaEsc = 8 + Math.floor(Math.random() * 6);
                flavorText = "申惟磕磕巴巴说“예뻐요”，韩振瞬间脸红到脖子。";
                break;
            case "cuddle_cmd":
                addLog("🎥 导演指令:“从背后抱住韩振，下巴抵肩膀。”");
                deltaS = -10; deltaH = -6; deltaEsc = 7 + Math.floor(Math.random() * 7);
                flavorText = "申惟犹豫后轻轻环住，韩振靠进他怀里。两人安静了几秒。";
                break;
            case "tease_cmd":
                addLog("🎥 导演指令:“韩振用手指戳申惟的腰。”");
                deltaS = -5; deltaH = -4; deltaEsc = 5 + Math.floor(Math.random() * 5);
                flavorText = "韩振坏笑着戳了两下，申惟闷哼一声抓住他手腕。";
                break;
            case "pillow_cmd":
                addLog("🎥 导演指令:“两人躺床上对视三十秒。”");
                deltaS = -9; deltaH = -9; deltaEsc = 9 + Math.floor(Math.random() * 6);
                flavorText = "鼻尖快碰到一起，申惟先移开眼睛，耳朵彻底红透。";
                break;
            case "confess_cmd":
                addLog("🎥 导演指令:“韩振用中文说‘哥我喜欢你’，申惟用韩语回。”");
                deltaS = -11; deltaH = -12; deltaEsc = 11 + Math.floor(Math.random() * 9);
                flavorText = "韩振说完垂下眼睛，申惟憋了半天小声重复，两个人都笑了。";
                break;
            case "belt_cmd":
                addLog("🎥 导演指令:“申惟帮韩振整理皮带。”");
                deltaS = -13; deltaH = -14; deltaEsc = 10 + Math.floor(Math.random() * 8);
                flavorText = "申惟半跪着调整皮带扣，韩振咬住嘴唇不敢低头看。";
                break;
            default: return;
        }

        tensionS = Math.min(98, Math.max(8, tensionS + deltaS));
        tensionH = Math.min(98, Math.max(8, tensionH + deltaH));
        escape = Math.min(100, escape + deltaEsc);
        
        addLog(`${flavorText} (申惟${deltaS>=0?'+':''}${deltaS}, 韩振${deltaH>=0?'+':''}${deltaH} | 逃脱+${deltaEsc}%)`);
        
        // 特殊彩蛋
        if(tensionS < 30 && tensionH < 35 && escape < 90 && !ended) {
            let extra = 6;
            escape = Math.min(100, escape + extra);
            addLog(`💘 申惟主动摸了摸韩振的头发，韩振下意识靠过去。门锁响了一声 +${extra}%`);
        }
        if(tensionS > 80 && deltaS < 0) {
            addLog(`🐺 申惟小声说: “韩振啊… 你这样我真的会..” 话没说完自己闭嘴了。`);
        }
        if(tensionH > 80 && deltaH < 0) {
            addLog(`🐰 韩振把脸埋进申惟肩膀，闷闷地说了一句“哥是坏人”。`);
        }

        updateUI();
        
        if(escape >= 100 && !ended) {
            escape = 100;
            showEnding();
        }
        updateUI();
    }

    function showEnding() {
        ended = true;
        gameActive = false;
        
        let endingMsg = "";
        if(tensionS <= 35 && tensionH <= 38) {
            endingMsg = "房门自动打开。申惟牵着韩振的手走出来，韩振眼角有点红。申惟转头看他，忽然笑了。那天之后，锐因对视不再躲闪。导演你促成了真正的亲密。";
        } else if(tensionS > 65 || tensionH > 68) {
            endingMsg = "门开了，但申惟快步走在前面，韩振跟在后面偷看他。出来后虽然还是别扭，但粉丝拍到机场申惟给韩振拉了拉口罩。暧昧持久战，但更涩了。";
        } else {
            endingMsg = "九号房终于解锁。两人沉默着走出，申惟外套披在韩振肩上。没有多说话，但回去直播时韩振说“申惟哥很温柔”。一切都变了又好像没变。";
        }
        
        const consoleDiv = document.getElementById('directorConsole');
        if(consoleDiv) {
            consoleDiv.innerHTML = `
                <div class="ending-box">
                    <div style="font-size: 44px;">🔓</div>
                    <h2 style="color:#eebb77; margin: 10px 0;">杀青 · 九号房逃脱</h2>
                    <p style="color:#efdbbc; margin: 16px 0;">${endingMsg}</p>
                    <button class="reset-btn" id="resetEndBtn" style="background:#b46f3a; padding:10px 26px;">🎬 重新开拍</button>
                </div>
                <div class="progress-row" style="margin-top:18px;">
                    <div class="escape-bar"><div class="escape-fill" style="width:100%"></div></div>
                    <button class="reset-btn" id="resetEndBtn2">重置</button>
                </div>
            `;
            const reset1 = document.getElementById('resetEndBtn');
            const reset2 = document.getElementById('resetEndBtn2');
            const resetFunc = () => resetGame();
            if(reset1) reset1.addEventListener('click', resetFunc);
            if(reset2) reset2.addEventListener('click', resetFunc);
        }
        updateUI();
    }

    function resetGame() {
        tensionS = 68;
        tensionH = 65;
        escape = 0;
        gameActive = true;
        ended = false;
        logs = [];
        
        const consoleDiv = document.getElementById('directorConsole');
        if(consoleDiv) {
            consoleDiv.innerHTML = `
                <div class="section-title">
                    🎙️ 指令台 · 让锐因完成任务
                </div>
                <div class="command-grid" id="commandGrid"></div>
                <div class="progress-row">
                    <div class="escape-bar"><div class="escape-fill" id="escapeFill"></div></div>
                    <button class="reset-btn" id="resetGameBtn">🎞️ 重新开拍</button>
                </div>
            `;
        }
        
        // 重新绑定按钮
        const actions = [
            { id: "kiss_cmd", label: "💋 嘴角亲吻" },
            { id: "lap_cmd", label: "💺 膝上拥抱" },
            { id: "neck_cmd", label: "🌬️ 颈侧气息" },
            { id: "hand_cmd", label: "🤝 十指相扣" },
            { id: "undress_cmd", label: "👕 解衣扣" },
            { id: "whisper_cmd", label: "👂 耳畔情话" },
            { id: "cuddle_cmd", label: "🫂 背后环抱" },
            { id: "tease_cmd", label: "👉 戳腰逗弄" },
            { id: "pillow_cmd", label: "🛏️ 枕边对视" },
            { id: "confess_cmd", label: "💌 双语告白" },
            { id: "belt_cmd", label: "🎀 整理皮带" }
        ];
        
        const grid = document.getElementById('commandGrid');
        if(grid) {
            grid.innerHTML = "";
            actions.forEach(act => {
                let btn = document.createElement('button');
                btn.className = "cmd-btn";
                btn.innerText = act.label;
                btn.onclick = () => executeCommand(act.id);
                grid.appendChild(btn);
            });
        }
        
        const newReset = document.getElementById('resetGameBtn');
        if(newReset) newReset.addEventListener('click', resetGame);
        
        const logDiv = getActionLog();
        if(logDiv) logDiv.innerHTML = "📼 系统: 房间规则——身体接触指数达标才能开门。导演请下达指令。";
        logs = [];
        addLog("🎞️ 导演重置九号房，申惟和韩振又被关进来了。新的一轮。");
        updateUI();
    }

    // 初始化
    function init() {
        const consoleDiv = document.getElementById('directorConsole');
        if(consoleDiv) {
            consoleDiv.innerHTML = `
                <div class="section-title">
                    🎙️ 指令台 · 让锐因完成任务
                </div>
                <div class="command-grid" id="commandGrid"></div>
                <div class="progress-row">
                    <div class="escape-bar"><div class="escape-fill" id="escapeFill"></div></div>
                    <button class="reset-btn" id="resetGameBtn">🎞️ 重新开拍</button>
                </div>
            `;
        }
        
        const actions = [
            { id: "kiss_cmd", label: "💋 嘴角亲吻" },
            { id: "lap_cmd", label: "💺 膝上拥抱" },
            { id: "neck_cmd", label: "🌬️ 颈侧气息" },
            { id: "hand_cmd", label: "🤝 十指相扣" },
            { id: "undress_cmd", label: "👕 解衣扣" },
            { id: "whisper_cmd", label: "👂 耳畔情话" },
            { id: "cuddle_cmd", label: "🫂 背后环抱" },
            { id: "tease_cmd", label: "👉 戳腰逗弄" },
            { id: "pillow_cmd", label: "🛏️ 枕边对视" },
            { id: "confess_cmd", label: "💌 双语告白" },
            { id: "belt_cmd", label: "🎀 整理皮带" }
        ];
        
        const grid = document.getElementById('commandGrid');
        if(grid) {
            actions.forEach(act => {
                let btn = document.createElement('button');
                btn.className = "cmd-btn";
                btn.innerText = act.label;
                btn.onclick = () => executeCommand(act.id);
                grid.appendChild(btn);
            });
        }
        
        const resetBtn = document.getElementById('resetGameBtn');
        if(resetBtn) resetBtn.addEventListener('click', resetGame);
        
        addLog("🎬 小雨披导演上线。九号房规则: 必须完成亲密任务才能逃脱。申惟容易红温，韩振推拉但会害羞。请开始导戏。");
        updateUI();
    }
    
    init();
</script>
</body>
</html>
