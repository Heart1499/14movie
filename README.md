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
            min-height: 140px;
            max-height: 180px;
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
            margin-bottom: 24px;
            max-height: 280px;
            overflow-y: auto;
            padding-bottom: 8px;
        }

        .cmd-btn {
            background: #2c221b;
            border: 1px solid #745d45;
            color: #ffefdb;
            padding: 10px 16px;
            border-radius: 60px;
            font-family: monospace;
            font-weight: bold;
            font-size: 12px;
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

        .director-talk {
            background: #2a221c;
            border-radius: 28px;
            padding: 16px;
            margin: 16px 0 20px;
            border: 1px solid #594f43;
        }

        .talk-label {
            font-size: 12px;
            color: #e2bc89;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .talk-input-area {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }

        .talk-input {
            flex: 1;
            background: #1a1511;
            border: 1px solid #6a5642;
            border-radius: 60px;
            padding: 12px 18px;
            color: #f0e2d0;
            font-family: monospace;
            font-size: 14px;
            outline: none;
        }

        .talk-input::placeholder {
            color: #7a6856;
            font-size: 12px;
        }

        .send-btn {
            background: #4f3824;
            border: none;
            padding: 8px 24px;
            border-radius: 60px;
            color: white;
            cursor: pointer;
            font-family: monospace;
            font-weight: bold;
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

        .share-hint {
            background: #2e241d;
            border-radius: 28px;
            padding: 10px 16px;
            margin-top: 16px;
            font-size: 11px;
            color: #b9a78e;
            text-align: center;
            cursor: pointer;
        }

        @media (max-width: 700px) {
            .char-card { padding: 8px 16px; gap: 10px;}
            .cmd-btn { font-size: 10px; padding: 8px 10px; min-width: 75px;}
            .talk-input { font-size: 12px; padding: 10px 14px;}
        }
    </style>
</head>
<body>
<div class="control-room" id="appRoot">
    <div class="camera-wall">
        <div class="cam-header">
            <span><span class="live-dot"></span> 九号房 · 封闭监控</span>
            <span>小雨披大导演</span>
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
        // ---------- 游戏状态 ----------
        let tensionS = 68;
        let tensionH = 65;
        let escape = 0;
        let gameActive = true;
        let ended = false;
        let logs = [];
        let lastCommandDesc = ""; // 记录上一个动作描述，用于衔接
        let consecutiveCount = 0;

        // DOM 元素
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

        function addLog(msg, isSystem = false) {
            logs.unshift(msg);
            if(logs.length > 12) logs.pop();
            const logDiv = getActionLog();
            if(logDiv) {
                logDiv.innerHTML = (isSystem ? "📼 " : "🎬 ") + msg + "<br>" + logs.slice(1).map(l => "&nbsp;&nbsp;" + l).join('<br>');
            }
        }

        // 导演自由发言（玩家对话框）
        function directorSay(text) {
            if(!gameActive || escape >= 100) {
                addLog("导演话筒没声了，房间已经解锁或者游戏结束。重置再喊话吧。");
                return;
            }
            addLog(`【导演对讲机】“${text}”`);
            // 根据玩家说的话，轻微影响气氛
            if(text.includes("亲") || text.includes("吻") || text.includes("抱")) {
                tensionS = Math.min(98, tensionS - 2);
                tensionH = Math.min(98, tensionH - 2);
                addLog(` 导演的指令让两人有点紧张，数值略微下降。`);
                updateUI();
            } else if(text.includes("快") || text.includes("速度")) {
                let extra = Math.floor(Math.random() * 4) + 2;
                escape = Math.min(100, escape + extra);
                addLog(` 导演催进度，房门似乎松动了一点 +${extra}%`);
                updateUI();
            } else if(text.includes("尴尬") || text.includes("别扭")) {
                tensionS = Math.min(98, tensionS + 3);
                tensionH = Math.min(98, tensionH + 2);
                addLog(` 导演提到尴尬，两人更不自在了。`);
                updateUI();
            }
            if(escape >= 100 && !ended) checkEnding();
        }

        function checkEnding() {
            if(escape >= 100 && !ended) {
                escape = 100;
                showEnding();
            }
        }

        // 核心指令：带剧情衔接的丰富动作
        function executeCommand(cmdId) {
            if(!gameActive) { addLog("游戏已结束，请按重新开拍。"); return; }
            if(escape >= 100) { addLog("房间已解锁，不用再指令。按重新开拍继续导演。"); return; }

            let deltaS = 0, deltaH = 0, deltaEsc = 0;
            let flavorText = "";
            let transitionText = ""; // 衔接上文

            // 根据上一个动作生成自然的过渡描述
            if(lastCommandDesc) {
                transitionText = "刚才的余韵还没散，" + lastCommandDesc.slice(0, 20) + "…… ";
            } else {
                transitionText = "空气安静了几秒，导演再次开口。";
            }

            switch(cmdId) {
                case "kiss_deep":
                    addLog("指令: 深吻三十秒，韩振主动踮脚。");
                    deltaS = -14; deltaH = -12; deltaEsc = 11+Math.floor(Math.random()*7);
                    flavorText = "申惟被动接受，手慢慢扶上韩振的腰，分开时两人都在喘。韩振耳朵红到脖子根，申惟低头不敢看他的眼睛。";
                    break;
                case "neck_bite":
                    addLog("指令: 韩振轻咬申惟喉结，申惟不能躲。");
                    deltaS = -16; deltaH = -8; deltaEsc = 12+Math.floor(Math.random()*8);
                    flavorText = "申惟仰头闭上眼睛，喉结滚动，韩振牙齿碰到皮肤的瞬间两个人都僵了。申惟闷哼一声，手指攥紧了韩振的衣服。";
                    break;
                case "lap_grind":
                    addLog("指令: 韩振跨坐在申惟腿上，缓慢磨蹭。");
                    deltaS = -18; deltaH = -15; deltaEsc = 14+Math.floor(Math.random()*9);
                    flavorText = "申惟手不知道该放哪，最后扣住韩振的腰，韩振把脸埋进他肩膀，声音闷闷的:“哥……你心跳好快。”";
                    break;
                case "shirt_off":
                    addLog("指令: 申惟帮韩振脱掉上衣，指尖故意滑过皮肤。");
                    deltaS = -12; deltaH = -18; deltaEsc = 13+Math.floor(Math.random()*7);
                    flavorText = "申惟从下摆往上掀，韩振举手配合。指尖碰到肋骨时韩振抖了一下，申惟动作突然变慢，像是在描摹。";
                    break;
                case "wall_press":
                    addLog("指令: 申惟把韩振按在墙上，单手撑头。");
                    deltaS = -10; deltaH = -14; deltaEsc = 12+Math.floor(Math.random()*6);
                    flavorText = "申惟靠近又不敢真的亲下去，韩振拽住他的衣领拉近。两人鼻尖快碰到时，申惟偏过头，呼吸全落在韩振耳侧。";
                    break;
                case "ear_whisper_ch":
                    addLog("指令: 韩振用中文在申惟耳边说骚话。");
                    deltaS = -15; deltaH = -10; deltaEsc = 10+Math.floor(Math.random()*8);
                    flavorText = "韩振凑过去轻声说“哥想不想更过分一点”，申惟耳朵瞬间血红，整个人僵在原地，过了好几秒才找回声音:“……别说这种话。”";
                    break;
                case "blindfold":
                    addLog("指令: 蒙住申惟眼睛，韩振用手指描摹他的脸。");
                    deltaS = -20; deltaH = -8; deltaEsc = 15+Math.floor(Math.random()*7);
                    flavorText = "申惟失去视觉后触觉放大，韩振指尖划过嘴唇时他轻颤了一下。韩振低声说:“哥别怕，是我。”";
                    break;
                case "thigh_rub":
                    addLog("指令: 韩振用大腿蹭申惟腿间，申惟不准逃。");
                    deltaS = -22; deltaH = -20; deltaEsc = 16+Math.floor(Math.random()*10);
                    flavorText = "申惟抓住韩振的腿想阻止又没用力，呼吸彻底乱了。韩振感觉到手下腰腹的紧绷，自己脸也烧起来。";
                    break;
                case "back_hug_chest":
                    addLog("指令: 申惟从背后抱住韩振，手放在他胸口。");
                    deltaS = -13; deltaH = -16; deltaEsc = 11+Math.floor(Math.random()*7);
                    flavorText = "申惟手心滚烫，韩振按住他的手不让拿开。两个人像连体婴一样贴在一起，心跳隔着皮肤互相传递。";
                    break;
                case "floor_press":
                    addLog("指令: 两人滚到地板上，申惟在上方俯视韩振。");
                    deltaS = -14; deltaH = -13; deltaEsc = 13+Math.floor(Math.random()*8);
                    flavorText = "申惟撑在韩振上方，发丝垂下来碰到韩振额头。韩振抬手摸了摸申惟的脸，申惟闭上眼睛，把脸埋进韩振颈窝。";
                    break;
                case "belt_remove":
                    addLog("指令: 韩振解开申惟的皮带，慢慢抽出来。");
                    deltaS = -24; deltaH = -18; deltaEsc = 18+Math.floor(Math.random()*9);
                    flavorText = "金属扣碰撞的声音在房间里格外响，申惟呼吸一滞。韩振抽到一半时申惟握住了他的手，却又慢慢松开。";
                    break;
                case "hand_down":
                    addLog("指令: 申惟的手从韩振腰侧滑进裤腰。");
                    deltaS = -20; deltaH = -24; deltaEsc = 17+Math.floor(Math.random()*10);
                    flavorText = "申惟指尖碰到皮肤时韩振轻哼了一声，申惟立刻停住，韩振却按着他的手不放，小声说:“……哥继续。”";
                    break;
                case "missionary":
                    addLog("指令: 申惟把韩振压在床上，膝盖顶开他双腿。");
                    deltaS = -25; deltaH = -22; deltaEsc = 20+Math.floor(Math.random()*8);
                    flavorText = "申惟俯下身，额头抵着韩振的额头，两人呼吸交缠。韩振勾住申惟的脖子，把最后一点距离也吞没了。";
                    break;
                case "spoon":
                    addLog("指令: 侧躺从背后紧贴，申惟环住韩振的腰。");
                    deltaS = -12; deltaH = -11; deltaEsc = 9+Math.floor(Math.random()*7);
                    flavorText = "申惟下巴抵着韩振后脑勺，安静地抱了很久，心跳却越来越快。韩振往后又贴紧了一点，两个人的身体曲线完美嵌合。";
                    break;
                case "teasing_deny":
                    addLog("指令: 韩振逗申惟但不让他碰，申惟急了。");
                    deltaS = -8; deltaH = -6; deltaEsc = 8+Math.floor(Math.random()*6);
                    flavorText = "韩振笑着往后躲，申惟一把拽回来，小声说“别闹了”。韩振愣了一下，发现申惟眼眶有点红。";
                    break;
                case "praise_kink":
                    addLog("指令: 申惟边亲韩振边夸他“做得真好”。");
                    deltaS = -11; deltaH = -14; deltaEsc = 12+Math.floor(Math.random()*7);
                    flavorText = "韩振把脸埋进申惟胸口，闷闷地说“哥别说了”。申惟反而笑了，又在他头顶落下一个吻。";
                    break;
                case "hair_pull":
                    addLog("指令: 韩振揪着申惟后脑头发接吻。");
                    deltaS = -13; deltaH = -9; deltaEsc = 11+Math.floor(Math.random()*6);
                    flavorText = "申惟吃痛反而吻得更用力，韩振手指收紧。分开时申惟嘴唇红红的，韩振帮他理了理被揪乱的头发。";
                    break;
                case "table_edge":
                    addLog("指令: 申惟把韩振抱上书桌边缘，站在他两腿之间。");
                    deltaS = -17; deltaH = -15; deltaEsc = 15+Math.floor(Math.random()*8);
                    flavorText = "韩振双腿夹住申惟的腰，申惟手撑在桌面上把韩振圈在怀里。桌面上的东西被扫到一边，发出哗啦的声响。";
                    break;
                case "knee_ride":
                    addLog("指令: 韩振跪在床上仰头看申惟，慢慢靠近。");
                    deltaS = -14; deltaH = -19; deltaEsc = 14+Math.floor(Math.random()*8);
                    flavorText = "韩振从下往上的眼神让申惟喉结一紧，伸手把他拉起来。韩振被拉起来时顺势倒在申惟怀里，两个人一起摔进枕头里。";
                    break;
                case "aftercare":
                    addLog("指令: 结束后申惟帮韩振擦汗，轻声问他疼不疼。");
                    deltaS = -8; deltaH = -10; deltaEsc = 7+Math.floor(Math.random()*5);
                    flavorText = "韩振摇头又点头，申惟亲了亲他额头。韩振把脸往申惟掌心蹭了蹭，小声说“哥抱紧一点”。气氛突然变得很温柔。";
                    break;
                default: return;
            }

            // 应用数值变化
            tensionS = Math.min(98, Math.max(5, tensionS + deltaS));
            tensionH = Math.min(98, Math.max(5, tensionH + deltaH));
            escape = Math.min(100, escape + deltaEsc);
            
            // 完整剧情日志，包含衔接过渡
            const fullText = transitionText + flavorText + ` (申惟${deltaS>=0?'+':''}${deltaS}, 韩振${deltaH>=0?'+':''}${deltaH} | 逃脱+${deltaEsc}%)`;
            addLog(fullText);
            
            // 记录上一个动作，用于下一次衔接
            lastCommandDesc = flavorText.substring(0, 40);
            consecutiveCount++;
            
            // 彩蛋：连续三个动作后触发额外小剧情
            if(consecutiveCount % 3 === 0 && escape < 90 && !ended) {
                let extra = 5;
                escape = Math.min(100, escape + extra);
                addLog(`💘 连续指导下，两人的默契悄然生长。房门又松动了一些 +${extra}%`);
            }
            
            if(tensionS < 25 && tensionH < 28 && escape < 90 && !ended) {
                let extra = 8;
                escape = Math.min(100, escape + extra);
                addLog(`✨ 申惟和韩振不约而同看向对方，然后同时笑了。门锁咔哒一声 +${extra}%`);
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
                        <div class="share-hint" id="copyEndingBtn">📸 点击复制结局，分享到豆瓣/微博</div>
                        <button class="reset-btn" id="resetEndBtn" style="background:#b46f3a; margin-top:16px; padding:10px 26px;">🎬 重新开拍</button>
                    </div>
                    <div class="progress-row" style="margin-top:18px;">
                        <div class="escape-bar"><div class="escape-fill" style="width:100%"></div></div>
                        <button class="reset-btn" id="resetEndBtn2">重置</button>
                    </div>
                `;
                const reset1 = document.getElementById('resetEndBtn');
                const reset2 = document.getElementById('resetEndBtn2');
                const copyBtn = document.getElementById('copyEndingBtn');
                const resetFunc = () => resetGame();
                if(reset1) reset1.addEventListener('click', resetFunc);
                if(reset2) reset2.addEventListener('click', resetFunc);
                if(copyBtn) {
                    copyBtn.addEventListener('click', () => {
                        const shareText = `【小雨披大导演】锐因九号房结局达成！\n${endingMsg}\n申惟忍耐值${Math.floor(tensionS)}% 韩振羞耻值${Math.floor(tensionH)}% 逃脱进度100%\n玩到这里，我的导演心得: 锐因是真的。`;
                        navigator.clipboard.writeText(shareText).then(() => {
                            copyBtn.innerText = "✓ 已复制，去发帖吧！";
                            setTimeout(() => { copyBtn.innerText = "📸 点击复制结局，分享到豆瓣/微博"; }, 2000);
                        });
                    });
                }
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
            lastCommandDesc = "";
            consecutiveCount = 0;
            
            const consoleDiv = document.getElementById('directorConsole');
            if(consoleDiv) {
                consoleDiv.innerHTML = `
                    <div class="section-title">
                        🎙️ 指令台 · 让锐因完成任务
                    </div>
                    <div class="command-grid" id="commandGrid"></div>
                    <div class="director-talk">
                        <div class="talk-label">🎙️ 导演对讲机 (你的话会被两人听到，影响气氛)</div>
                        <div class="talk-input-area">
                            <input type="text" class="talk-input" id="directorTalkInput" placeholder="比如: 申惟你别躲了 / 韩振再主动一点 / 你们两个快点..." autocomplete="off">
                            <button class="send-btn" id="sendTalkBtn">喊话</button>
                        </div>
                    </div>
                    <div class="progress-row">
                        <div class="escape-bar"><div class="escape-fill" id="escapeFill"></div></div>
                        <button class="reset-btn" id="resetGameBtn">🎞️ 重新开拍</button>
                    </div>
                `;
            }
            
            const actions = [
                { id: "kiss_deep", label: "深吻" }, { id: "neck_bite", label: "喉结轻咬" },
                { id: "lap_grind", label: "腿上磨蹭" }, { id: "shirt_off", label: "脱上衣" },
                { id: "wall_press", label: "壁咚" }, { id: "ear_whisper_ch", label: "中文耳语" },
                { id: "blindfold", label: "蒙眼描摹" }, { id: "thigh_rub", label: "大腿蹭" },
                { id: "back_hug_chest", label: "背后抱胸" }, { id: "floor_press", label: "地板压制" },
                { id: "belt_remove", label: "解皮带" }, { id: "hand_down", label: "手探裤腰" },
                { id: "missionary", label: "传教士" }, { id: "spoon", label: "汤匙抱" },
                { id: "teasing_deny", label: "逗弄不许碰" }, { id: "praise_kink", label: "边亲边夸" },
                { id: "hair_pull", label: "揪头发吻" }, { id: "table_edge", label: "书桌边缘" },
                { id: "knee_ride", label: "跪姿仰视" }, { id: "aftercare", label: "事后安抚" }
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
            
            // 绑定导演喊话功能
            const sendBtn = document.getElementById('sendTalkBtn');
            const talkInput = document.getElementById('directorTalkInput');
            if(sendBtn && talkInput) {
                sendBtn.onclick = () => {
                    let msg = talkInput.value.trim();
                    if(msg) {
                        directorSay(msg);
                        talkInput.value = "";
                    } else {
                        directorSay("导演清了清嗓子，没说话。");
                    }
                };
                talkInput.addEventListener('keypress', (e) => {
                    if(e.key === 'Enter') {
                        let msg = talkInput.value.trim();
                        if(msg) {
                            directorSay(msg);
                            talkInput.value = "";
                        }
                    }
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
                    <div class="director-talk">
                        <div class="talk-label">🎙️ 导演对讲机 (你的话会被两人听到，影响气氛)</div>
                        <div class="talk-input-area">
                            <input type="text" class="talk-input" id="directorTalkInput" placeholder="比如: 申惟你别躲了 / 韩振再主动一点 / 你们两个快点..." autocomplete="off">
                            <button class="send-btn" id="sendTalkBtn">喊话</button>
                        </div>
                    </div>
                    <div class="progress-row">
                        <div class="escape-bar"><div class="escape-fill" id="escapeFill"></div></div>
                        <button class="reset-btn" id="resetGameBtn">🎞️ 重新开拍</button>
                    </div>
                `;
            }
            
            const actions = [
                { id: "kiss_deep", label: "深吻" }, { id: "neck_bite", label: "喉结轻咬" },
                { id: "lap_grind", label: "腿上磨蹭" }, { id: "shirt_off", label: "脱上衣" },
                { id: "wall_press", label: "壁咚" }, { id: "ear_whisper_ch", label: "中文耳语" },
                { id: "blindfold", label: "蒙眼描摹" }, { id: "thigh_rub", label: "大腿蹭" },
                { id: "back_hug_chest", label: "背后抱胸" }, { id: "floor_press", label: "地板压制" },
                { id: "belt_remove", label: "解皮带" }, { id: "hand_down", label: "手探裤腰" },
                { id: "missionary", label: "传教士" }, { id: "spoon", label: "汤匙抱" },
                { id: "teasing_deny", label: "逗弄不许碰" }, { id: "praise_kink", label: "边亲边夸" },
                { id: "hair_pull", label: "揪头发吻" }, { id: "table_edge", label: "书桌边缘" },
                { id: "knee_ride", label: "跪姿仰视" }, { id: "aftercare", label: "事后安抚" }
            ];
            
            const grid = document.getElementById('commandGrid');
            if(grid) {
                actions.forEach(act => {
                    let btn = document.createElement('button');
                    btn.className = "cmd-btn";
                    btn.innerText = act.label;
                    btn.on
