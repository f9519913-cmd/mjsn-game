```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>苗疆 · 蜉蝣 | 接API文游</title>
    <style>
        /* 全局沉浸风格 - 优化手机显示 */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background: #1d2b35;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'Segoe UI', '华文楷体', 'KaiTi', 'Microsoft YaHei', serif;
            padding: 10px;
            background-image: radial-gradient(circle at 30% 30%, #2f4b3c 0%, #10221b 100%);
            font-size: 14px;
        }

        /* ----- 独立链接入口 ----- */
        .entry-portal {
            text-align: center;
            background: rgba(240, 235, 215, 0.15);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 2px solid #b69e7c;
            border-radius: 40px 40px 20px 20px;
            padding: 2rem 2rem;
            box-shadow: 0 30px 40px #00000060, 0 0 0 2px #5f7b68 inset;
            max-width: 500px;
            width: 100%;
        }

        .entry-portal h1 {
            font-size: 2.5rem;
            color: #fbefcf;
            text-shadow: 0 4px 0 #3d523c, 0 8px 8px #0a0f0a;
            letter-spacing: 4px;
            margin-bottom: 15px;
        }

        .entry-portal p {
            font-size: 1.1rem;
            color: #dcd0b3;
            margin-bottom: 30px;
        }

        .enter-game-link {
            display: inline-block;
            background: linear-gradient(145deg, #ebc47f, #c89f4a);
            color: #17281f;
            font-size: 1.8rem;
            font-weight: bold;
            padding: 15px 40px;
            border-radius: 50px;
            text-decoration: none;
            box-shadow: 0 10px 0 #7a6138, 0 10px 20px black;
            border: 2px solid #ffeec2;
            cursor: pointer;
        }

        /* ----- 游戏主界面 ----- */
        .game-main {
            max-width: 500px;
            width: 100%;
            background: #1d382bc0;
            backdrop-filter: blur(18px);
            -webkit-backdrop-filter: blur(18px);
            border-radius: 30px 30px 20px 20px;
            padding: 15px;
            border: 2px solid #b39260;
            box-shadow: 0 20px 30px #000000b0;
            color: #f4ecd9;
            display: none;
        }

        /* 头部 */
        .game-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 2px solid #a98f5f;
            padding-bottom: 8px;
            margin-bottom: 10px;
            flex-wrap: wrap;
        }

        .game-title {
            font-size: 1.4rem;
            background: linear-gradient(135deg, #f7e1a4, #e7b86b);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            display: flex;
            align-items: center;
            gap: 5px;
            flex-wrap: wrap;
        }

        .player-tags {
            font-size: 0.7rem;
            color: #f8b56c;
            background: #264e38;
            padding: 2px 6px;
            border-radius: 15px;
            display: inline-flex;
            gap: 3px;
        }

        .api-badge {
            background: #1f4030;
            padding: 5px 12px;
            border-radius: 30px;
            border: 1px solid #efc48c;
            color: #fbddb5;
            font-size: 0.8rem;
        }

        /* 属性栏 */
        .stats-panel {
            background: #103326d0;
            border-radius: 20px;
            padding: 10px;
            border: 1px solid #baa06a;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
            margin-bottom: 8px;
            font-size: 0.8rem;
        }

        .stat-item {
            display: flex;
            align-items: center;
            gap: 3px;
            background: #08211460;
            border-radius: 20px;
            padding: 3px 6px;
            border-left: 2px solid #a57c4b;
        }

        .stat-label {
            color: #e5ca92;
            min-width: 30px;
        }

        .stat-value {
            font-weight: 700;
            color: #f2e0b5;
        }

        .time-loc {
            grid-column: span 4;
            display: flex;
            justify-content: space-between;
            color: #ffddaa;
            background: #08211460;
            border-radius: 20px;
            padding: 5px 10px;
        }

        /* 故事区 */
        .story-narrative {
            background: #102d1dd9;
            border-radius: 20px;
            padding: 15px;
            margin: 8px 0;
            border: 1px solid #caae77;
            font-size: 0.95rem;
            line-height: 1.5;
            max-height: 150px;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
        }

        /* 标签导航栏 */
        .tab-nav {
            display: flex;
            background: #1b3427e0;
            border-radius: 30px;
            padding: 5px;
            margin: 8px 0;
            border: 1px solid #a4824e;
            justify-content: space-around;
        }

        .tab-item {
            color: #e5ca92;
            padding: 8px 0;
            font-size: 0.9rem;
            font-weight: 500;
            text-align: center;
            flex: 1;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .tab-item.active {
            background: #264e38;
            color: #f8d58c;
            border: 1px solid #dbb063;
        }

        /* 内容面板 */
        .content-panel {
            background: #1b3427e0;
            border-radius: 20px;
            padding: 12px;
            border: 1px solid #a4824e;
            margin: 8px 0;
            min-height: 200px;
            max-height: 300px;
            overflow-y: auto;
        }

        .panel-hidden {
            display: none;
        }

        /* 人际关系 - 人物卡片 */
        .character-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 8px;
        }

        .character-card {
            background: #08211460;
            border-radius: 15px;
            padding: 8px;
            border: 1px solid #a57c4b;
            cursor: pointer;
        }

        .character-card.selected {
            border: 2px solid #f8d58c;
            background: #264e38;
        }

        .character-name {
            color: #f8d58c;
            font-weight: bold;
            font-size: 0.9rem;
        }

        .character-relation {
            font-size: 0.7rem;
            color: #e5ca92;
            margin: 2px 0;
        }

        .character-detail {
            margin-top: 10px;
            padding: 12px;
            background: #103326d0;
            border-radius: 15px;
            border: 1px solid #a57c4b;
        }

        .detail-row {
            display: flex;
            justify-content: space-between;
            margin: 6px 0;
            font-size: 0.9rem;
            border-bottom: 1px dashed #a57c4b;
            padding-bottom: 4px;
        }

        .detail-label {
            color: #e5ca92;
            font-weight: 500;
        }

        .detail-value {
            color: #f8d58c;
            text-align: right;
        }

        .detail-desc {
            margin-top: 8px;
            padding: 8px;
            background: #08211460;
            border-radius: 10px;
            font-size: 0.85rem;
            color: #ffddaf;
            line-height: 1.4;
        }

        /* 地图网格 */
        .map-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-bottom: 10px;
        }

        .map-cell {
            background: #264e38;
            border: 1px solid #dbb063;
            border-radius: 15px;
            padding: 12px 5px;
            text-align: center;
            font-size: 0.8rem;
            cursor: pointer;
        }

        .map-cell.explored {
            background: #3a7054;
            border-color: #f8d58c;
        }

        .map-cell.disabled {
            opacity: 0.5;
            pointer-events: none;
        }

        .map-legend {
            display: flex;
            gap: 10px;
            font-size: 0.7rem;
            color: #e5ca92;
            margin-top: 5px;
        }

        /* 物品列表 */
        .items-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
        }

        .item-card {
            background: #264e38;
            border: 1px solid #b3915a;
            border-radius: 15px;
            padding: 8px;
            text-align: center;
            font-size: 0.8rem;
        }

        /* 设置面板 */
        .settings-group {
            margin-bottom: 15px;
        }

        .settings-label {
            color: #f8d58c;
            font-size: 0.9rem;
            margin-bottom: 5px;
        }

        .settings-input, .settings-select {
            width: 100%;
            background: #103326;
            border: 1px solid #a4824e;
            border-radius: 15px;
            padding: 8px 12px;
            color: #f4ecd9;
            margin-bottom: 10px;
        }

        .model-selector {
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .model-selector select {
            flex: 1;
            background: #103326;
            border: 1px solid #a4824e;
            border-radius: 15px;
            padding: 8px 12px;
            color: #f4ecd9;
        }

        .refresh-models {
            background: #96734a;
            border: none;
            color: #faf0ce;
            padding: 8px 12px;
            border-radius: 15px;
            cursor: pointer;
            white-space: nowrap;
        }

        .settings-textarea {
            width: 100%;
            background: #103326;
            border: 1px solid #a4824e;
            border-radius: 15px;
            padding: 8px 12px;
            color: #f4ecd9;
            min-height: 80px;
            margin-bottom: 10px;
        }

        .settings-save {
            background: #96734a;
            border: none;
            color: #faf0ce;
            padding: 10px 20px;
            border-radius: 30px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
        }

        /* API 指示器 */
        .api-indicator {
            display: flex;
            align-items: center;
            background: #263f30;
            border-radius: 30px;
            padding: 5px 15px;
            gap: 10px;
            border: 1px solid #dcaa5e;
            margin: 5px 0;
            color: #ffddaf;
            font-size: 0.8rem;
        }

        .spinner {
            width: 16px;
            height: 16px;
            border: 2px solid #fad68f;
            border-top: 2px solid transparent;
            border-radius: 50%;
            animation: spin 0.9s linear infinite;
        }

        @keyframes spin { 0% { transform: rotate(0); } 100% { transform: rotate(360deg); } }

        /* 选项按钮 */
        .choice-buttons {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 6px;
            margin: 8px 0;
        }

        .choice-btn {
            background: #264e38;
            border: 2px solid #dbb063;
            color: #ffefcf;
            padding: 8px 4px;
            font-size: 0.8rem;
            border-radius: 25px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 3px 0 #153a25;
        }

        /* 自由输入 */
        .free-input-area {
            display: flex;
            gap: 6px;
            background: #1b3427e0;
            border-radius: 30px;
            padding: 3px 3px 3px 15px;
            border: 2px solid #a4824e;
            margin: 8px 0;
        }

        .free-input-area input {
            flex: 1;
            background: transparent;
            border: none;
            color: #f5e1b9;
            font-size: 0.9rem;
            outline: none;
            padding: 6px 0;
        }

        .free-submit {
            background: #96734a;
            border: none;
            color: #faf0ce;
            font-size: 0.9rem;
            padding: 6px 15px;
            border-radius: 30px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 2px 0 #4d3e28;
        }

        /* 底部 */
        .footer-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
            gap: 5px;
        }

        .back-to-entry, .restart-story {
            background: #1f4430;
            border: 1px solid #c2a062;
            color: #ead5b0;
            padding: 8px 12px;
            border-radius: 25px;
            text-decoration: none;
            font-size: 0.8rem;
            cursor: pointer;
        }

        .hint-message {
            color: #d5c09f;
            font-size: 0.75rem;
        }
    </style>
</head>
<body>

<!-- 独立链接入口 -->
<div id="entryPortal" class="entry-portal">
    <h1>🌺 苗疆 · 蜉蝣</h1>
    <p>—— 扮演一位少女，度过她的一生 ——</p>
    <a href="#" id="enterGameLink" class="enter-game-link">🔍 进入寨子 🔍</a>
    <div class="entry-footer" style="margin-top:20px; color:#b4bb9e; font-size:0.9rem;">
        <span>🎋 依山结寨 · 接入DeepSeek 🎋</span>
    </div>
</div>

<!-- 游戏主界面 -->
<div id="gameMain" class="game-main">
    <!-- 头部 -->
    <div class="game-header">
        <div class="game-title">
            <span>🌱 <span id="playerNameDisplay">阿苗</span></span>
            <span id="playerTags" class="player-tags"></span>
        </div>
        <span class="api-badge" id="apiModeBadge">⚡ 本地模式</span>
    </div>

    <!-- 属性栏 -->
    <div class="stats-panel" id="statsPanel">
        <div class="time-loc">
            <span>📆 <span id="weekDisplay">春二月·第1周</span></span>
            <span>📍 <span id="locationDisplay">青榕寨</span></span>
        </div>
        <div class="stat-item"><span class="stat-label">魅</span><span class="stat-value" id="statCha">52</span></div>
        <div class="stat-item"><span class="stat-label">智</span><span class="stat-value" id="statWis">48</span></div>
        <div class="stat-item"><span class="stat-label">体</span><span class="stat-value" id="statPhys">55</span></div>
        <div class="stat-item"><span class="stat-label">才</span><span class="stat-value" id="statArt">44</span></div>
        <div class="stat-item"><span class="stat-label">❤️</span><span class="stat-value" id="statHp">100</span></div>
        <div class="stat-item"><span class="stat-label">⚡</span><span class="stat-value" id="statStam">100</span></div>
        <div class="stat-item"><span class="stat-label">🌿</span><span class="stat-value" id="statHealth">95</span></div>
        <div class="stat-item"><span class="stat-label">🧠</span><span class="stat-value" id="statMind">92</span></div>
        <div class="stat-item"><span class="stat-label">💰</span><span class="stat-value" id="statMoney">25</span></div>
    </div>

    <!-- 故事区 -->
    <div id="storyDisplay" class="story-narrative">
        <p>晨雾还挂在吊脚楼角，你推开竹窗，青榕寨在鸟鸣中醒来。</p>
    </div>

    <!-- 标签导航栏 -->
    <div class="tab-nav">
        <div class="tab-item active" data-tab="story">剧情</div>
        <div class="tab-item" data-tab="relation">人脉</div>
        <div class="tab-item" data-tab="map">地图</div>
        <div class="tab-item" data-tab="items">资产</div>
        <div class="tab-item" data-tab="settings">设置</div>
    </div>

    <!-- 剧情面板 -->
    <div id="storyPanel" class="content-panel">
        <div id="storyContent">
            <p>晨雾还挂在吊脚楼角，你推开竹窗，青榕寨在鸟鸣中醒来。阿妈在火塘边蒸糯米，香气混着柴烟钻进鼻腔。今天，是你十六岁成年礼前的最后一次赶场。</p>
            <p>你摸了摸衣袋里的三个贝币——是上月帮邻寨染布换来的。山脚榕树下，年轻人们正在扎堆，似乎要比试芦笙。</p>
        </div>
    </div>

    <!-- 人际关系面板 -->
    <div id="relationPanel" class="content-panel panel-hidden">
        <div class="character-grid" id="characterGrid"></div>
        <div id="characterDetail" class="character-detail panel-hidden">
            <div class="detail-row"><span class="detail-label">姓名</span><span class="detail-value" id="detailName">阿妈</span></div>
            <div class="detail-row"><span class="detail-label">年龄</span><span class="detail-value" id="detailAge">45</span></div>
            <div class="detail-row"><span class="detail-label">身份</span><span class="detail-value" id="detailRole">母亲</span></div>
            <div class="detail-row"><span class="detail-label">性格</span><span class="detail-value" id="detailPersonality">慈祥温和</span></div>
            <div class="detail-row"><span class="detail-label">外貌</span><span class="detail-value" id="detailAppearance">头发花白，面容和善</span></div>
            <div class="detail-row"><span class="detail-label">好感度</span><span class="detail-value" id="detailFavor">80</span></div>
            <div class="detail-row"><span class="detail-label">爱慕值</span><span class="detail-value" id="detailLove">0</span></div>
            <div class="detail-row"><span class="detail-label">当前状态</span><span class="detail-value" id="detailStatus">健康</span></div>
            <div class="detail-desc" id="detailDesc">你的母亲，从小把你抚养长大，精通染布和刺绣。</div>
            <div style="display:flex; gap:5px; margin-top:8px;">
                <button class="choice-btn" style="flex:1;" id="talkBtn">交谈</button>
                <button class="choice-btn" style="flex:1;" id="giftBtn">送礼</button>
            </div>
        </div>
    </div>

    <!-- 地图面板 -->
    <div id="mapPanel" class="content-panel panel-hidden">
        <div class="map-grid" id="mapGrid"></div>
        <div class="map-legend">
            <span>🟩 未探索</span>
            <span>🟨 已探索</span>
            <span>⏳ 今日已探</span>
        </div>
        <div style="margin-top:8px; font-size:0.8rem; color:#e5ca92;" id="mapMessage"></div>
    </div>

    <!-- 资产面板 -->
    <div id="itemsPanel" class="content-panel panel-hidden">
        <div class="items-grid" id="itemsGrid"></div>
    </div>

    <!-- 设置面板 -->
    <div id="settingsPanel" class="content-panel panel-hidden">
        <div class="settings-group">
            <div class="settings-label">主角姓名</div>
            <input type="text" id="playerName" class="settings-input" value="阿苗" placeholder="输入你的名字">
        </div>
        <div class="settings-group">
            <div class="settings-label">AI模式</div>
            <select id="apiMode" class="settings-select">
                <option value="local">本地模式（模拟API）</option>
                <option value="deepseek">DeepSeek API</option>
                <option value="claude">Claude API</option>
                <option value="custom">自定义API</option>
            </select>
        </div>
        <div class="settings-group" id="apiKeyGroup" style="display:none;">
            <div class="settings-label">API Key</div>
            <input type="password" id="apiKey" class="settings-input" placeholder="输入你的API Key">
        </div>
        <div class="settings-group" id="apiUrlGroup" style="display:none;">
            <div class="settings-label">API 地址</div>
            <input type="text" id="apiUrl" class="settings-input" value="https://api.deepseek.com/v1/chat/completions">
        </div>
        <div class="settings-group" id="modelSelectGroup" style="display:none;">
            <div class="settings-label">选择模型</div>
            <div class="model-selector">
                <select id="modelSelect">
                    <option value="">请先获取模型列表</option>
                </select>
                <button id="refreshModels" class="refresh-models">🔄 获取</button>
            </div>
        </div>
        <div class="settings-group">
            <div class="settings-label">世界观设定</div>
            <textarea id="worldSetting" class="settings-textarea">古代苗疆，少女成长，部落寨子，自然崇拜</textarea>
        </div>
        <button id="saveSettings" class="settings-save">保存设置</button>
    </div>
<!-- API 指示器 -->
    <div class="api-indicator" id="apiIndicator">
        <span id="apiMessage">⏳ 尚未召唤API</span>
        <span id="apiSpinner" class="spinner" style="display: none;"></span>
    </div>

    <!-- 选项按钮 -->
    <div id="choiceButtons" class="choice-buttons">
        <button class="choice-btn" data-action="market">🌽 赶场</button>
        <button class="choice-btn" data-action="lusheng">🎵 芦笙</button>
        <button class="choice-btn" data-action="rest">🛏️ 帮阿妈</button>
    </div>

    <!-- 自由输入 -->
    <div class="free-input-area">
        <input type="text" id="freeActionInput" placeholder="✍️ 输入你想做的事...">
        <button id="submitFreeAction" class="free-submit">召唤</button>
    </div>

    <!-- 底部 -->
    <div class="footer-bar">
        <a href="#" id="backToEntryBtn" class="back-to-entry">⏮ 返回入口</a>
        <button id="restartGameBtn" class="restart-story">🔄 重开</button>
        <span class="hint-message" id="gameHint">苗寨深处</span>
    </div>
</div>

<script>
    (function(){
        // ==================== 确保所有元素都存在 ====================
        function getElement(id) {
            const el = document.getElementById(id);
            return el;
        }

        // ==================== 元素获取 ====================
        const entryPortal = getElement('entryPortal');
        const gameMain = getElement('gameMain');
        const enterLink = getElement('enterGameLink');
        const backBtn = getElement('backToEntryBtn');
        const restartBtn = getElement('restartGameBtn');

        const storyDisplay = getElement('storyDisplay');
        const storyContent = getElement('storyContent');
        const choiceButtonsDiv = getElement('choiceButtons');
        const apiMessageSpan = getElement('apiMessage');
        const apiSpinner = getElement('apiSpinner');
        const gameHint = getElement('gameHint');
        const freeInput = getElement('freeActionInput');
        const freeSubmit = getElement('submitFreeAction');
        const apiModeBadge = getElement('apiModeBadge');
        const playerNameDisplay = getElement('playerNameDisplay');
        const playerTags = getElement('playerTags');

        // 属性显示
        const statCha = getElement('statCha');
        const statWis = getElement('statWis');
        const statPhys = getElement('statPhys');
        const statArt = getElement('statArt');
        const statHp = getElement('statHp');
        const statStam = getElement('statStam');
        const statHealth = getElement('statHealth');
        const statMind = getElement('statMind');
        const statMoney = getElement('statMoney');
        const weekDisplay = getElement('weekDisplay');
        const locationDisplay = getElement('locationDisplay');

        // 标签导航
        const tabItems = document.querySelectorAll('.tab-item');
        const storyPanel = getElement('storyPanel');
        const relationPanel = getElement('relationPanel');
        const mapPanel = getElement('mapPanel');
        const itemsPanel = getElement('itemsPanel');
        const settingsPanel = getElement('settingsPanel');

        // 人际关系元素
        const characterGrid = getElement('characterGrid');
        const characterDetail = getElement('characterDetail');
        const detailName = getElement('detailName');
        const detailAge = getElement('detailAge');
        const detailRole = getElement('detailRole');
        const detailPersonality = getElement('detailPersonality');
        const detailAppearance = getElement('detailAppearance');
        const detailFavor = getElement('detailFavor');
        const detailLove = getElement('detailLove');
        const detailStatus = getElement('detailStatus');
        const detailDesc = getElement('detailDesc');
        const talkBtn = getElement('talkBtn');
        const giftBtn = getElement('giftBtn');

        // 地图元素
        const mapGrid = getElement('mapGrid');
        const mapMessage = getElement('mapMessage');

        // 物品元素
        const itemsGrid = getElement('itemsGrid');

        // 设置元素
        const playerName = getElement('playerName');
        const apiMode = getElement('apiMode');
        const apiKey = getElement('apiKey');
        const apiUrl = getElement('apiUrl');
        const apiKeyGroup = getElement('apiKeyGroup');
        const apiUrlGroup = getElement('apiUrlGroup');
        const modelSelectGroup = getElement('modelSelectGroup');
        const modelSelect = getElement('modelSelect');
        const refreshModels = getElement('refreshModels');
        const worldSetting = getElement('worldSetting');
        const saveSettings = getElement('saveSettings');

        // ==================== 属性标签配置 ====================
        const TRAITS = [
            { name: '明眸皓齿', effect: { cha: 5 }, desc: '初始魅力+5' },
            { name: '冰肌玉骨', effect: { cha: 10 }, desc: '初始魅力+10' },
            { name: '貌若无盐', effect: { cha: -10 }, desc: '初始魅力-10' },
            { name: '多智近妖', effect: { wis: 15, wisGrowth: 1.1 }, desc: '智慧+15，获取经验+10%' },
            { name: '天资愚钝', effect: { wis: -10, wisGrowth: 0.9 }, desc: '智慧-10，获取经验-10%' },
            { name: '天生病弱', effect: { phys: -10, physGrowth: 0.9 }, desc: '体魄-10，获取经验-10%' },
            { name: '多才多艺', effect: { art: 10 }, desc: '初始才艺+10' },
            { name: '体魄强健', effect: { phys: 10 }, desc: '初始体魄+10' },
            { name: '才疏学浅', effect: { art: -10 }, desc: '初始才艺-10' }
        ];

        // ==================== 游戏状态 ====================
        let currentState = {
            playerName: '阿苗',
            traitNames: [],
            traitEffects: { cha: 0, wis: 0, phys: 0, art: 0, wisGrowth: 1.0, physGrowth: 1.0 },
            week: 1,
            season: '春二月',
            location: '青榕寨',
            baseCha: 50, baseWis: 50, basePhys: 50, baseArt: 50,
            hp: 100, stam: 100, health: 95, mind: 92,
            money: 25,
            exploredMap: {},
            mapCells: [],
            exploredCount: 0,
            items: { ricecake: 0, thread: 0, silver: 0, herb: 0 },
            characters: {
                '阿妈': { age: 45, role: '母亲', personality: '慈祥温和', appearance: '头发花白，面容和善', desc: '你的母亲，从小把你抚养长大，精通染布和刺绣。', favor: 80, love: 0, status: '健康', canLove: false },
                '彩': { age: 19, role: '好友', personality: '活泼开朗', appearance: '扎着双马尾，眼睛明亮', desc: '从小一起长大的玩伴，总是充满活力。', favor: 50, love: 0, status: '健康', canLove: true },
                '寨公': { age: 52, role: '寨中长老', personality: '威严公正', appearance: '花白胡须，目光深邃', desc: '寨子里的长老，掌管祭祀和族规。', favor: 20, love: 0, status: '健康', canLove: false },
                '姜央': { age: 20, role: '寨主', personality: '勇敢果断', appearance: '身材挺拔，眼神坚毅', desc: '年轻的寨主，深受寨民爱戴。', favor: 20, love: 0, status: '健康', canLove: true }
            },
            settings: { apiMode: 'local', apiKey: '', apiUrl: 'https://api.deepseek.com/v1/chat/completions', selectedModel: '', worldSetting: '古代苗疆，少女成长，部落寨子，自然崇拜' },
            availableModels: []
        };

        let isApiCalling = false;
        let selectedCharacter = null;
        let todayExplored = {};

        // ==================== 计算最终属性
====================
        function calculateStats() {
            return {
                cha: Math.min(100, Math.max(0, currentState.baseCha + currentState.traitEffects.cha)),
                wis: Math.min(100, Math.max(0, currentState.baseWis + currentState.traitEffects.wis)),
                phys: Math.min(100, Math.max(0, currentState.basePhys + currentState.traitEffects.phys)),
                art: Math.min(100, Math.max(0, currentState.baseArt + currentState.traitEffects.art))
            };
        }

        // ==================== 随机分配标签 ====================
        function assignRandomTraits() {
            const numTraits = Math.floor(Math.random() * 3) + 1;
            const shuffled = [...TRAITS].sort(() => 0.5 - Math.random());
            const selected = shuffled.slice(0, numTraits);
            
            let traitNames = [];
            let traitEffects = { cha: 0, wis: 0, phys: 0, art: 0, wisGrowth: 1.0, physGrowth: 1.0 };

            selected.forEach(trait => {
                traitNames.push(trait.name);
                if (trait.effect.cha) traitEffects.cha += trait.effect.cha;
                if (trait.effect.wis) traitEffects.wis += trait.effect.wis;
                if (trait.effect.phys) traitEffects.phys += trait.effect.phys;
                if (trait.effect.art) traitEffects.art += trait.effect.art;
                if (trait.effect.wisGrowth) traitEffects.wisGrowth = trait.effect.wisGrowth;
                if (trait.effect.physGrowth) traitEffects.physGrowth = trait.effect.physGrowth;
            });

            return { traitNames, traitEffects };
        }

        // ==================== 初始化地图 ====================
        function initMap() {
            const mapTypes = ['青榕寨', '溪边', '竹林', '药田', '集市', '祠堂', '山脚', '梯田', '枫树林'];
            const mapDesc = {
                '青榕寨': '寨子中心，热闹非凡',
                '溪边': '清澈的溪水流过，女子们在此洗衣',
                '竹林': '翠竹成林，偶尔有竹笋可挖',
                '药田': '阿婆的草药田，弥漫着药香',
                '集市': '交易物品的地方',
                '祠堂': '供奉祖先的地方，庄严肃穆',
                '山脚': '通往深山的入口',
                '梯田': '层层梯田，稻谷飘香',
                '枫树林': '秋天枫叶似火'
            };
            
            currentState.mapCells = [];
            for (let i = 0; i < 9; i++) {
                const type = mapTypes[Math.floor(Math.random() * mapTypes.length)];
                currentState.mapCells.push({
                    id: i,
                    name: type,
                    desc: mapDesc[type] || '未知地点',
                    explored: false,
                    danger: Math.random() > 0.7 ? '低' : '无'
                });
            }
            currentState.exploredMap = {};
            todayExplored = {};
            if (mapGrid) renderMap();
        }

        // ==================== 渲染地图 ====================
        function renderMap() {
            if (!mapGrid) return;
            mapGrid.innerHTML = '';
            currentState.mapCells.forEach((cell, index) => {
                const cellDiv = document.createElement('div');
                cellDiv.className = `map-cell ${cell.explored ? 'explored' : ''} ${todayExplored[index] ? 'disabled' : ''}`;
                cellDiv.innerText = cell.name;
                cellDiv.dataset.index = index;
                cellDiv.addEventListener('click', () => exploreMap(index));
                mapGrid.appendChild(cellDiv);
            });
        }

        // ==================== 探索地图 ====================
        function exploreMap(index) {
            if (isApiCalling) return;
            if (todayExplored[index]) {
                if (mapMessage) mapMessage.innerText = '⚠️ 这个地方本回合已经探索过了';
                return;
            }
            if (currentState.stam < 10) {
                if (mapMessage) mapMessage.innerText = '⚠️ 体力不足，无法探索';
                return;
            }

            const cell = currentState.mapCells[index];
            todayExplored[index] = true;
            cell.explored = true;
            currentState.exploredCount++;
            currentState.stam -= 10;
            
            let exploreResult = `你探索了${cell.name}，${cell.desc}`;
            if (Math.random() > 0.5) {
                const found = Math.random() > 0.5 ? '贝币' : '草药';
                if (found === '贝币') {
                    currentState.money += 5;
                    exploreResult += '，发现了5个贝币';
                } else {
                    currentState.items.herb = (currentState.items.herb || 0) + 1;
                    exploreResult += '，采到了草药';
                }
            }
            
            if (storyDisplay) storyDisplay.innerHTML = `<p>${exploreResult}</p>`;
            renderMap();
            refreshUI();
            callAdventureAPI(`探索${cell.name}`);
        }

        // ==================== 渲染人际关系 ====================
        function renderCharacters() {
            if (!characterGrid) return;
            characterGrid.innerHTML = '';
            Object.keys(currentState.characters).forEach(name => {
                const char = currentState.characters[name];
                const card = document.createElement('div');
                card.className = `character-card ${selectedCharacter === name ? 'selected' : ''}`;
                card.innerHTML = `
                    <div class="character-name">${name}</div>
                    <div class="character-relation">${char.role}</div>
                    <div class="character-relation">❤️ ${char.favor}/${char.love}</div>
                `;
                card.addEventListener('click', () => selectCharacter(name));
                characterGrid.appendChild(card);
            });
        }

        // ==================== 选择人物 ====================
        function selectCharacter(name) {
            selectedCharacter = name;
            const char = currentState.characters[name];
            if (!char) return;
            
            if (detailName) detailName.innerText = name;
            if (detailAge) detailAge.innerText = char.age || '?';
            if (detailRole) detailRole.innerText = char.role || '?';
            if (detailPersonality) detailPersonality.innerText = char.personality || '?';
            if (detailAppearance) detailAppearance.innerText = char.appearance || '?';
            if (detailFavor) detailFavor.innerText = char.favor || 0;
            if (detailLove) detailLove.innerText = char.love || 0;
            if (detailStatus) detailStatus.innerText = char.status || '健康';
            if (detailDesc) detailDesc.innerText = char.desc || '暂无描述';
            if (characterDetail) characterDetail.classList.remove('panel-hidden');
            renderCharacters();
        }

        // ==================== 人物交互 ====================
        function handleCharacterInteraction(action) {
            if (!selectedCharacter || isApiCalling) return;
            const char = currentState.characters[selectedCharacter];
            if (!char) return;
            
            if (action === 'talk') {
                if (!char.canLove) {
                    char.favor = (char.favor || 0) + 1;
                    if (storyDisplay) storyDisplay.innerHTML = `<p>你和${selectedCharacter}聊了家常，感觉很温暖。</p>`;
                } else {
                    char.favor = (char.favor || 0) + 2;
                    if (storyDisplay) storyDisplay.innerHTML = `<p>你和${selectedCharacter}交谈甚欢，好感度增加了。</p>`;
                }
            } else if (action === 'gift') {
                if (currentState.items.ricecake > 0) {
                    currentState.items.ricecake--;
                    if (char.canLove) {
                        char.favor = (char.favor || 0) + 5;
                        char.love = (char.love || 0) + 2;
                        if (storyDisplay) storyDisplay.innerHTML = `<p>你送给${selectedCharacter}糯米糕，他/她很高兴，爱慕值上升了。</p>`;
                    } else {
                        char.favor = (char.favor || 0) + 3;
                        if (storyDisplay) storyDisplay.innerHTML = `<p>你送给${selectedCharacter}糯米糕，他/她表示感谢。</p>`;
                    }
                } else {
                    alert('没有糯米糕可以送');
                    return;
                }
            }
            
            refreshUI();
            callAdventureAPI(`${action} ${selectedCharacter}`);
        }

        // ==================== 渲染物品 ====================
        function renderItems() {
            if (!itemsGrid) return;
            itemsGrid.innerHTML = `
                <div class="item-card">贝币<br>💰 ${currentState.money || 0}</div>
                <div class="item-card">糯米糕<br>🍚 ${currentState.items.ricecake || 0}</div>
                <div class="item-card">绣线<br>🧵 ${currentState.items.thread || 0}</div>
                <div class="item-card">银镯<br>✨ ${currentState.items.silver || 0}</div>
                <div class="item-card">草药<br>🌿 ${currentState.items.herb || 0}</div>
            `;
        }

        // ==================== 刷新UI ====================
        function refreshUI() {
            const stats = calculateStats();
            if (statCha) statCha.innerText = stats.cha;
            if (statWis) statWis.innerText = stats.wis;
            if (statPhys) statPhys.innerText = stats.phys;
            if (statArt) statArt.innerText = stats.art;
            if (statHp) statHp.innerText = currentState.hp;
            if (statStam) statStam.innerText = currentState.stam;
            if (statHealth) statHealth.innerText = currentState.health;
            if (statMind) statMind.innerText = currentState.mind;
            if (statMoney) statMoney.innerText = currentState.money;
            if (weekDisplay) weekDisplay.innerText = `${currentState.season}·第${currentState.week}周`;
            if (locationDisplay) locationDisplay.innerText = currentState.location;
            if (playerNameDisplay) playerNameDisplay.innerText = currentState.playerName;
            
            if (playerTags) {
                playerTags.innerHTML = currentState.traitNames.map(t => `#${t}`).join(' ');
            }
            
            renderCharacters();
            renderItems();
        }

        // ==================== 获取模型列表 ====================
        function fetchModelList() {
            if (apiMessageSpan) apiMessageSpan.innerText = '🔮 获取模型列表中...';
            if (apiSpinner) apiSpinner.style.display = 'inline-block';
            
            setTimeout(() => {
                let models = [];
                if (apiMode && apiMode.value === 'deepseek') {
                    models = ['deepseek-chat', 'deepseek-coder', 'deepseek-v2'];
                } else if (apiMode && apiMode.value === 'claude') {
                    models = ['claude-3-opus', 'claude-3-sonnet', 'claude-3-haiku'];
                } else {
                    models = ['gpt-4', 'gpt-3.5-turbo', 'custom-model'];
                }
                
                currentState.availableModels = models;
                if (modelSelect) {
                    modelSelect.innerHTML = '';
                    models.forEach(m => {
                        const option = document.createElement('option');
                        option.value = m;
                        option.text = m;
                        modelSelect.appendChild(option);
                    });
                }
                
                if (apiMessageSpan) apiMessageSpan.innerText = '✅ 模型列表已获取';
                if (apiSpinner) apiSpinner.style.display = 'none';
            }, 1000);
        }

        // ==================== 标签切换
====================
        if (tabItems && tabItems.length > 0) {
            tabItems.forEach(tab => {
                tab.addEventListener('click', (e) => {
                    tabItems.forEach(t => t.classList.remove('active'));
                    tab.classList.add('active');
                    
                    if (storyPanel) storyPanel.classList.add('panel-hidden');
                    if (relationPanel) relationPanel.classList.add('panel-hidden');
                    if (mapPanel) mapPanel.classList.add('panel-hidden');
                    if (itemsPanel) itemsPanel.classList.add('panel-hidden');
                    if (settingsPanel) settingsPanel.classList.add('panel-hidden');
                    
                    const tabName = tab.dataset.tab;
                    if (tabName === 'story' && storyPanel) storyPanel.classList.remove('panel-hidden');
                    else if (tabName === 'relation' && relationPanel) {
                        relationPanel.classList.remove('panel-hidden');
                        renderCharacters();
                    }
                    else if (tabName === 'map' && mapPanel) {
                        mapPanel.classList.remove('panel-hidden');
                        renderMap();
                    }
                    else if (tabName === 'items' && itemsPanel) {
                        itemsPanel.classList.remove('panel-hidden');
                        renderItems();
                    }
                    else if (tabName === 'settings' && settingsPanel) settingsPanel.classList.remove('panel-hidden');
                });
            });
        }

        // ==================== API模式切换 ====================
        if (apiMode) {
            apiMode.addEventListener('change', () => {
                if (apiMode.value === 'custom') {
                    if (apiUrlGroup) apiUrlGroup.style.display = 'block';
                } else {
                    if (apiUrlGroup) apiUrlGroup.style.display = 'none';
                }
                
                if (apiMode.value === 'local') {
                    if (apiKeyGroup) apiKeyGroup.style.display = 'none';
                    if (modelSelectGroup) modelSelectGroup.style.display = 'none';
                    if (apiModeBadge) apiModeBadge.innerText = '⚡ 本地模式';
                } else {
                    if (apiKeyGroup) apiKeyGroup.style.display = 'block';
                    if (modelSelectGroup) modelSelectGroup.style.display = 'block';
                    if (apiModeBadge) apiModeBadge.innerText = apiMode.value === 'deepseek' ? '🔮 DeepSeek' : '🤖 Claude';
                }
            });
        }

        // ==================== 刷新模型 ====================
        if (refreshModels) {
            refreshModels.addEventListener('click', fetchModelList);
        }

        // ==================== 保存设置 ====================
        if (saveSettings) {
            saveSettings.addEventListener('click', () => {
                currentState.playerName = playerName ? playerName.value : '阿苗';
                currentState.settings = {
                    apiMode: apiMode ? apiMode.value : 'local',
                    apiKey: apiKey ? apiKey.value : '',
                    apiUrl: apiUrl ? apiUrl.value : 'https://api.deepseek.com/v1/chat/completions',
                    selectedModel: modelSelect ? modelSelect.value : '',
                    worldSetting: worldSetting ? worldSetting.value : '古代苗疆，少女成长，部落寨子，自然崇拜'
                };
                if (playerNameDisplay) playerNameDisplay.innerText = currentState.playerName;
                alert('设置已保存');
            });
        }

        // ==================== 模拟API调用 ====================
        function callAdventureAPI(actionDescription) {
            if (isApiCalling) return;

            isApiCalling = true;
            if (apiMessageSpan) apiMessageSpan.innerText = '🔮 API呼唤中......';
            if (apiSpinner) apiSpinner.style.display = 'inline-block';
            if (gameHint) gameHint.innerText = '天命流转';

            setTimeout(() => {
                let storyAddition = '';
                let promptLine = '';
                let newChoices = [];
                let hintUpdate = '';

                if (actionDescription.includes('赶场') || actionDescription.includes('market')) {
                    storyAddition = '你来到市集，买了糯米糕和绣线。遇见了彩。';
                    promptLine = '她朝你招招手。';
                    newChoices = ['💬 和彩聊天', '🎁 买绣线', '🌿 买草药'];
                    currentState.money = (currentState.money || 0) - 5;
                    currentState.items.ricecake = (currentState.items.ricecake || 0) + 2;
                    currentState.items.thread = (currentState.items.thread || 0) + 1;
                    hintUpdate = '糯米糕+2，绣线+1';
                } 
                else if (actionDescription.includes('芦笙') || actionDescription.includes('lusheng')) {
                    storyAddition = '芦笙比试上，你舞步轻盈。寨公点头称赞。';
                    promptLine = '才艺得到了认可。';
                    newChoices = ['🏅 接受指点', '💧 去溪边', '🍠 买红薯'];
                    currentState.baseArt = (currentState.baseArt || 50) + 3;
                    currentState.stam = (currentState.stam || 100) - 5;
                    if (currentState.characters['寨公']) currentState.characters['寨公'].favor += 5;
                    hintUpdate = '才艺+3，寨公好感+5';
                } 
                else if (actionDescription.includes('帮阿妈') || actionDescription.includes('rest')) {
                    storyAddition = '你帮阿妈染布，她教你新的绣法。';
                    promptLine = '阿妈给了你一块银饰。';
                    newChoices = ['🌸 试戴', '🍲 找彩玩', '🪡 继续学'];
                    currentState.baseArt = (currentState.baseArt || 50) + 2;
                    currentState.mind = (currentState.mind || 92) + 5;
                    currentState.items.silver = (currentState.items.silver || 0) + 1;
                    if (currentState.characters['阿妈']) currentState.characters['阿妈'].favor += 3;
                    hintUpdate = '银饰+1，阿妈好感+3';
                }
                else {
                    storyAddition = `你：${actionDescription}`;
                    promptLine = '山神默默注视着你。';
                    newChoices = ['🌾 继续', '🗣️ 找人', '🏡 回家'];
                    currentState.baseCha = (currentState.baseCha || 50) + 1;
                    hintUpdate = '魅力+1';
                }

                // 边界限制
                if (currentState.hp > 100) currentState.hp = 100;
                if (currentState.stam > 100) currentState.stam = 100;
                if (currentState.health > 100) currentState.health = 100;
                if (currentState.mind > 100) currentState.mind = 100;
                if (currentState.hp < 0) currentState.hp = 0;
                if (currentState.stam < 0) currentState.stam = 0;
                if (currentState.health < 0) currentState.health = 0;
                if (currentState.mind < 0) currentState.mind = 0;

                if (storyContent) {
                    storyContent.innerHTML = `
                        <p>${storyAddition}</p>
                        <p style="color:#f8d58c; margin-top:8px;">✨ ${promptLine}</p>
                    `;
                }
                if (storyDisplay) {
                    storyDisplay.innerHTML = `<p>${storyAddition}</p><div style="color:#f8d58c;">✨ ${promptLine}</div>`;
                }

                renderChoiceButtons(newChoices);
                currentState.week = (currentState.week || 1) + 1;
                todayExplored = {};
                refreshUI();

                isApiCalling = false;
                if (apiMessageSpan) apiMessageSpan.innerText = '✅ API已回应';
                if (apiSpinner) apiSpinner.style.display = 'none';
                if (gameHint) gameHint.innerText = hintUpdate || '命运流转';
            }, 800);
        }

        // ==================== 渲染选项按钮 ====================
        function renderChoiceButtons(buttonLabels) {
            if (!choiceButtonsDiv) return;
            choiceButtonsDiv.innerHTML = '';
            if (!buttonLabels || buttonLabels.length === 0) {
                buttonLabels = ['🌽 赶场', '🎵 芦笙', '🛏️ 帮阿妈'];
            }
            buttonLabels.forEach(label => {
                const btn = document.createElement('button');
                btn.className = 'choice-btn';
                btn.innerText = label;
                btn.addEventListener('click', () => {
                    if (isApiCalling) return;
                    callAdventureAPI(label);
                });
                choiceButtonsDiv.appendChild(btn);
            });
        }

        // ==================== 自由输入 ====================
        if (freeSubmit) {
            freeSubmit.addEventListener('click', () => {
                const custom = freeInput ? freeInput.value.trim() : '';
                if (custom === '') {
                    alert('请输入你想做的事');
                    return;
                }
                callAdventureAPI(custom);
                if (freeInput) freeInput.value = '';
            });
        }

        // ==================== 重置游戏
====================
        function resetGame() {
            const { traitNames, traitEffects } = assignRandomTraits();
            
            currentState = {
                playerName: (playerName ? playerName.value : '阿苗') || '阿苗',
                traitNames: traitNames,
                traitEffects: traitEffects,
                week: 1,
                season: '春二月',
                location: '青榕寨',
                baseCha: 50, baseWis: 50, basePhys: 50, baseArt: 50,
                hp: 100, stam: 100, health: 95, mind: 92,
                money: 25,
                mapCells: [],
                exploredMap: {},
                exploredCount: 0,
                items: { ricecake: 0, thread: 0, silver: 0, herb: 0 },
                characters: {
                    '阿妈': { age: 45, role: '母亲', personality: '慈祥温和', appearance: '头发花白，面容和善', desc: '你的母亲，从小把你抚养长大，精通染布和刺绣。', favor: 80, love: 0, status: '健康', canLove: false },
                    '彩': { age: 19, role: '好友', personality: '活泼开朗', appearance: '扎着双马尾，眼睛明亮', desc: '从小一起长大的玩伴，总是充满活力。', favor: 50, love: 0, status: '健康', canLove: true },
                    '寨公': { age: 52, role: '寨中长老', personality: '威严公正', appearance: '花白胡须，目光深邃', desc: '寨子里的长老，掌管祭祀和族规。', favor: 20, love: 0, status: '健康', canLove: false },
                    '姜央': { age: 20, role: '寨主', personality: '勇敢果断', appearance: '身材挺拔，眼神坚毅', desc: '年轻的寨主，深受寨民爱戴。', favor: 20, love: 0, status: '健康', canLove: true }
                },
                settings: currentState.settings || { apiMode: 'local', apiKey: '', apiUrl: 'https://api.deepseek.com/v1/chat/completions', selectedModel: '', worldSetting: '古代苗疆，少女成长，部落寨子，自然崇拜' }
            };
            
            initMap();
            if (storyContent) {
                storyContent.innerHTML = `
                    <p>晨雾还挂在吊脚楼角，你推开竹窗，青榕寨在鸟鸣中醒来。阿妈在火塘边蒸糯米，香气混着柴烟钻进鼻腔。今天，是你十六岁成年礼前的最后一次赶场。</p>
                    <p>你摸了摸衣袋里的三个贝币——是上月帮邻寨染布换来的。山脚榕树下，年轻人们正在扎堆，似乎要比试芦笙。</p>
                `;
            }
            if (storyDisplay) {
                storyDisplay.innerHTML = `
                    <p>晨雾还挂在吊脚楼角，你推开竹窗，青榕寨在鸟鸣中醒来。</p>
                    <div style="color:#f8d58c;">“要去看看吗？也许会遇见那个人……”</div>
                `;
            }
            renderChoiceButtons(['🌽 赶场', '🎵 芦笙', '🛏️ 帮阿妈']);
            refreshUI();
            if (apiMessageSpan) apiMessageSpan.innerText = '⏳ 尚未召唤API';
            if (apiSpinner) apiSpinner.style.display = 'none';
            selectedCharacter = null;
        }

        // ==================== 进入/退出游戏 ====================
        function enterGame() {
            if (entryPortal) entryPortal.style.display = 'none';
            if (gameMain) gameMain.style.display = 'block';
            resetGame();
        }

        function backToEntry() {
            if (gameMain) gameMain.style.display = 'none';
            if (entryPortal) entryPortal.style.display = 'block';
        }

        // ==================== 事件绑定 ====================
        if (enterLink) {
            enterLink.addEventListener('click', (e) => {
                e.preventDefault();
                enterGame();
            });
        }

        if (backBtn) {
            backBtn.addEventListener('click', (e) => {
                e.preventDefault();
                backToEntry();
            });
        }

        if (restartBtn) {
            restartBtn.addEventListener('click', () => {
                if (isApiCalling) return;
                resetGame();
            });
        }

        if (talkBtn) {
            talkBtn.addEventListener('click', () => handleCharacterInteraction('talk'));
        }

        if (giftBtn) {
            giftBtn.addEventListener('click', () => handleCharacterInteraction('gift'));
        }

        // ==================== 为选项按钮添加点击事件 ====================
        const choiceBtns = document.querySelectorAll('.choice-btn');
        choiceBtns.forEach(btn => {
            btn.addEventListener('click', function() {
                if (isApiCalling) return;
                const action = this.innerText;
                callAdventureAPI(action);
            });
        });

        // ==================== 初始化 ====================
        if (entryPortal) entryPortal.style.display = 'block';
        if (gameMain) gameMain.style.display = 'none';
        initMap();
    })();
</script>
</body>
</html>
```
