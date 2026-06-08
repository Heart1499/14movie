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
            max-width: 1300px;
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
            0% { opacity: 0.5; transform: scale(0.8);}
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
            min-height: 110px;
            max-height: 150px;
            overflow-y: auto;
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
            max-height: 400px;
            overflow-y: auto;
            padding-bottom: 8px;
        }

        .cmd-btn {
            background: #2c221b;
            border: 1px solid #745d45;
            color: #ffefdb;
            padding: 12px 18px;
            border-radius: 60px;
            font-family: monospace;
            font-weight: bold;
            font-size: 13px;
            cursor: pointer;
            flex: 1 0 auto;
            min-width: 100px;
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
            .cmd-btn { font-size: 11px; padding: 8px 12px; min-width: 80px;}
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
                    <div><div class="char-name">申惟</div><div class="char-tag">队长 · 年上克制 · 易红温</div></div>
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
    (function() {
        let tensionS = 68;   // 申惟紧张/忍耐
        let tensionH = 65;   // 韩振羞耻
        let escape = 0;
        let gameActive = true;
        let ended = false;
        let logs = [];

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
            if(logs.length > 10) logs.pop();
            const logDiv = getActionLog();
            if(logDiv) {
                logDiv.innerHTML = `🎬 ${msg}<br>` + logs.slice(1).map(l => `&nbsp;&nbsp;${l}`).join('<br>');
            }
        }

        // 执行指令 — 丰富版
        function executeCommand(cmdId) {
            if(!gameActive) { addLog("游戏已结束，请按重新开拍。"); return; }
            if(escape >= 100) { addLog("房间已解锁，不用再指令。按重新开拍继续导演。"); return; }

            let deltaS = 0, deltaH = 0, deltaEsc = 0;
            let flavorText = "";

            switch(cmdId) {
                // 基础亲密
                case "kiss_deep":
                    addLog("🎥 指令: 深吻三十秒，韩振主动踮脚。");
                    deltaS = -14; deltaH = -12; deltaEsc = 11+Math.floor(Math.random()*7);
                    flavorText = "申惟被动接受，手慢慢扶上韩振的腰，分开时两人都在喘。";
                    break;
                case "neck_bite":
                    addLog("🎥 指令: 韩振轻咬申惟喉结，申惟不能躲。");
                    deltaS = -16; deltaH = -8; deltaEsc = 12+Math.floor(Math.random()*8);
                    flavorText = "申惟仰头闭上眼睛，喉结滚动，韩振牙齿碰到皮肤的瞬间两个人都僵了。";
                    break;
                case "lap_grind":
                    addLog("🎥 指令: 韩振跨坐在申惟腿上，缓慢磨蹭。");
                    deltaS = -18; deltaH = -15; deltaEsc = 14+Math.floor(Math.random()*9);
                    flavorText = "申惟手不知道该放哪，最后扣住韩振的腰，韩振把脸埋进他肩膀。";
                    break;
                case "shirt_off":
                    addLog("🎥 指令: 申惟帮韩振脱掉上衣，指尖故意滑过皮肤。");
                    deltaS = -12; deltaH = -18; deltaEsc = 13+Math.floor(Math.random()*7);
                    flavorText = "申惟从下摆往上掀，韩振举手配合，耳朵红透。";
                    break;
                // 进阶玩法
                case "wall_press":
                    addLog("🎥 指令: 申惟把韩振按在墙上，单手撑头。");
                    deltaS = -10; deltaH = -14; deltaEsc = 12+Math.floor(Math.random()*6);
                    flavorText = "申惟靠近又不敢真的亲下去，韩振拽住他的衣领拉近。";
                    break;
                case "ear_whisper_ch":
                    addLog("🎥 指令: 韩振用中文在申惟耳边说骚话。");
                    deltaS = -15; deltaH = -10; deltaEsc = 10+Math.floor(Math.random()*8);
                    flavorText = "韩振说“哥想不想更过分一点”，申惟耳朵瞬间血红。";
                    break;
                case "blindfold":
                    addLog("🎥 指令: 蒙住申惟眼睛，韩振用手指描摹他的脸。");
                    deltaS = -20; deltaH = -8; deltaEsc = 15+Math.floor(Math.random()*7);
                    flavorText = "申惟失去视觉后触觉放大，韩振指尖划过嘴唇时他轻颤了一下。";
                    break;
                case "thigh_rub":
                    addLog("🎥 指令: 韩振用大腿蹭申惟腿间，申惟不准逃。");
                    deltaS = -22; deltaH = -20; deltaEsc = 16+Math.floor(Math.random()*10);
                    flavorText = "申惟抓住韩振的腿想阻止又没用力，呼吸彻底乱了。";
                    break;
                case "back_hug_chest":
                    addLog("🎥 指令: 申惟从背后抱住韩振，手放在他胸口。");
                    deltaS = -13; deltaH = -16; deltaEsc = 11+Math.floor(Math.random()*7);
                    flavorText = "申惟手心滚烫，韩振按住他的手不让拿开。";
                    break;
                case "floor_press":
                    addLog("🎥 指令: 两人滚到地板上，申惟在上方俯视韩振。");
                    deltaS = -14; deltaH = -13; deltaEsc = 13+Math.floor(Math.random()*8);
                    flavorText = "申惟撑在韩振上方，发丝垂下来碰到韩振额头，两个人都忘了动作。";
                    break;
                // 更刺激
                case "belt_remove":
                    addLog("🎥 指令: 韩振解开申惟的皮带，慢慢抽出来。");
                    deltaS = -24; deltaH = -18; deltaEsc = 18+Math.floor(Math.random()*9);
                    flavorText = "金属扣碰撞的声音在房间里格外响，申惟呼吸一滞。";
                    break;
                case "hand_down":
                    addLog("🎥 指令: 申惟的手从韩振腰侧滑进裤腰。");
                    deltaS = -20; deltaH = -24; deltaEsc = 17+Math.floor(Math.random()*10);
                    flavorText = "申惟指尖碰到皮肤时韩振轻哼了一声，申惟立刻停住，韩振却按着他的手不放。";
                    break;
                case "missionary":
                    addLog("🎥 指令: 申惟把韩振压在床上，膝盖顶开他双腿。");
                    deltaS = -25; deltaH = -22; deltaEsc = 20+Math.floor(Math.random()*8);
                    flavorText = "申惟俯下身，额头抵着韩振的额头，两人呼吸交缠。";
                    break;
                case "spoon":
                    addLog("🎥 指令: 侧躺从背后紧贴，申惟环住韩振的腰。");
                    deltaS = -12; deltaH = -11; deltaEsc = 9+Math.floor(Math.random()*7);
                    flavorText = "申惟下巴抵着韩振后脑勺，安静地抱了很久，心跳却越来越快。";
                    break;
                case "teasing_deny":
                    addLog("🎥 指令: 韩振逗申惟但不让他碰，申惟急了。");
                    deltaS = -8; deltaH = -6; deltaEsc = 8+Math.floor(Math.random()*6);
                    flavorText = "韩振笑着往后躲，申惟一把拽回来，小声说“别闹了”。";
                    break;
                case "praise_kink":
                    addLog("🎥 指令: 申惟边亲韩振边夸他“做得真好”。");
                    deltaS = -11; deltaH = -14; deltaEsc = 12+Math.floor(Math.random()*7);
                    flavorText = "韩振把脸埋进申惟胸口，闷闷地说“哥别说了”。";
                    break;
                case "hair_pull":
                    addLog("🎥 指令: 韩振揪着申惟后脑头发接吻。");
                    deltaS = -13; deltaH = -9; deltaEsc = 11+Math.floor(Math.random()*6);
                    flavorText = "申惟吃痛反而吻得更用力，韩振手指收紧。";
                    break;
                case "table_edge":
                    addLog("🎥 指令: 申惟把韩振抱上书桌边缘，站在他两腿之间。");
                    deltaS = -17; deltaH = -15; deltaEsc = 15+Math.floor(Math.random()*8);
                    flavorText = "韩振双腿夹住申惟的腰，申惟手撑在桌面上把韩振圈在怀里。";
                    break;
                case "knee_ride":
                    addLog("🎥 指令: 韩振跪在床上仰头看申惟，慢慢靠近。");
                    deltaS = -14; deltaH = -19; deltaEsc = 14+Math.floor(Math.random()*8);
                    flavorText = "韩振从下往上的眼神让申惟喉结一紧，伸手把他拉起来。";
                    break;
                case "aftercare":
                    addLog("🎥 指令: 结束后申惟帮韩振擦汗，轻声问他疼不疼。");
                    deltaS = -8; deltaH = -10; deltaEsc = 7+Math.floor(Math.random()*5);
                    flavorText = "韩振摇头又点头，申惟亲了亲他额头。气氛突然变得很温柔。";
                    break;
                default: return;
            }

            tensionS = Math.min(98, Math.max(5, tensionS + deltaS));
            tensionH = Math.min(98, Math.max(5, tensionH + deltaH));
            escape = Math.min(100, escape + deltaEsc);
            
            addLog(`${flavorText} (申惟${deltaS>=0?'+':''}${deltaS}, 韩振${deltaH>=0?'+':''}${deltaH} | 逃脱+${deltaEsc}%)`);
            
            // 彩蛋
            if(tensionS < 28 && tensionH < 30 && escape < 90 && !ended) {
                let extra = 8;
                escape = Math.min(100, escape + extra);
                addLog(`💘 两人同时笑了，申惟主动牵住韩振的手。门锁大幅度松动 +${extra}%`);
            }
            if(tensionS > 75 && deltaS < -10) addLog(`🐺 申惟声音发哑: “韩振……你故意的吧。”`);
            if(tensionH > 75 && deltaH < -12) addLog(`🐰 韩振揪住申惟衣角不肯松手。`);

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
            if(tensionS <= 30 && tensionH <= 32) {
                endingMsg = "九号房门缓缓打开。申惟牵着韩振走出来，韩振脖子上有浅浅的红痕。之后团综里两人对视终于不再躲闪，粉丝锐评:导演功德无量。";
            } else if(tensionS > 60 || tensionH > 62) {
                endingMsg = "门开了，申惟耳朵还是红的，韩振走路有点不自然。两人一前一后出去，但第二天机场申惟给韩振整理了围巾。别扭但更真了。";
            } else {
                endingMsg = "房间解锁。申惟把外套披在韩振身上，两人并排走出去，肩膀偶尔碰到也没有躲。没有轰轰烈烈，但所有人都看得出有什么不一样了。";
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
            
            const actions = [
                { id: "kiss_deep", label: "💋 深吻" },
                { id: "neck_bite", label: "🦷 喉结轻咬" },
                { id: "lap_grind", label: "💺 腿上磨蹭" },
                { id: "shirt_off", label: "👕 脱上衣" },
                { id: "wall_press", label: "🧱 壁咚" },
                { id: "ear_whisper_ch", label: "👂 中文耳语" },
                { id: "blindfold", label: "🎭 蒙眼描摹" },
                { id: "thigh_rub", label: "🦵 大腿蹭" },
                { id: "back_hug_chest", label: "🤗 背后抱胸" },
                { id: "floor_press", label: "📌 地板压制" },
                { id: "belt_remove", label: "🎀 解皮带" },
                { id: "hand_down", label: "👇 手探裤腰" },
                { id: "missionary", label: "🛏️ 传教士" },
                { id: "spoon", label: "🥄 汤匙抱" },
                { id: "teasing_deny", label: "😏 逗弄不许碰" },
                { id: "praise_kink", label: "📢 边亲边夸" },
                { id: "hair_pull", label: "💇 揪头发吻" },
                { id: "table_edge", label: "📚 书桌边缘" },
                { id: "knee_ride", label: "🦵 跪姿仰视" },
                { id: "aftercare", label: "🩹 事后安抚" }
            ];
            
            const grid = document.getElementById('commandGrid');
            if(grid) {
                grid.innerHTML = "";
                actions.forEach(act => {
                    let btn = document.createElement('button');
                    btn.className = "cmd-btn";
                    btn.innerText = act.label;
                    btn.onclick = (function(cmd) { return function() { executeCommand(cmd); }; })(act.id);
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
                { id: "kiss_deep", label: "💋 深吻" },
                { id: "neck_bite", label: "🦷 喉结轻咬" },
                { id: "lap_grind", label: "💺 腿上磨蹭" },
                { id: "shirt_off", label: "👕 脱上衣" },
                { id: "wall_press", label: "🧱 壁咚" },
                { id: "ear_whisper_ch", label: "👂 中文耳语" },
                { id: "blindfold", label: "🎭 蒙眼描摹" },
                { id: "thigh_rub", label: "🦵 大腿蹭" },
                { id: "back_hug_chest", label: "🤗 背后抱胸" },
                { id: "floor_press", label: "📌 地板压制" },
                { id: "belt_remove", label: "🎀 解皮带" },
                { id: "hand_down", label: "👇 手探裤腰" },
                { id: "missionary", label: "🛏️ 传教士" },
                { id: "spoon", label: "🥄 汤匙抱" },
                { id: "teasing_deny", label: "😏 逗弄不许碰" },
                { id: "praise_kink", label: "📢 边亲边夸" },
                { id: "hair_pull", label: "💇 揪头发吻" },
                { id: "table_edge", label: "📚 书桌边缘" },
                { id: "knee_ride", label: "🦵 跪姿仰视" },
                { id: "aftercare", label: "🩹 事后安抚" }
            ];
            
            const grid = document.getElementById('commandGrid');
            if(grid) {
                actions.forEach(act => {
                    let btn = document.createElement('button');
                    btn.className = "cmd-btn";
                    btn.innerText = act.label;
                    btn.onclick = (function(cmd) { return function() { executeCommand(cmd); }; })(act.id);
                    grid.appendChild(btn);
                });
            }
            
            const resetBtn = document.getElementById('resetGameBtn');
            if(resetBtn) resetBtn.addEventListener('click', resetGame);
            
            addLog("🎬 小雨披导演上线。九号房规则: 必须完成亲密任务才能逃脱。申惟容易红温，韩振推拉但会害羞。请开始导戏。");
            updateUI();
        }
        
        init();
    })();
</script>
</body>
</html>
