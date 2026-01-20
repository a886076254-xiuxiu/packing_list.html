<!DOCTYPE html>
<html lang="zh-TW">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>HK 2026 行李確認</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #F2F4F8;
            --primary: #2D3436;
            --accent: #6C5CE7;
            /* 質感紫 */
            --accent-light: #A29BFE;
            --success: #00B894;
            --warning: #FD79A8;
            --card-bg: #FFFFFF;
            --shadow: 0 8px 20px rgba(0, 0, 0, 0.06);
            --radius: 24px;
        }

        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: var(--bg-color);
            color: var(--primary);
            margin: 0;
            padding-bottom: 140px;
            -webkit-font-smoothing: antialiased;
        }

        /* --- Header --- */
        .header {
            padding: 40px 24px 20px;
            background: #fff;
            border-bottom-left-radius: 30px;
            border-bottom-right-radius: 30px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.03);
            position: relative;
            z-index: 10;
        }

        .header h1 {
            margin: 0;
            font-size: 1.8rem;
            background: linear-gradient(45deg, #2D3436, #636e72);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -0.5px;
        }

        .header p {
            margin: 8px 0 0;
            color: #b2bec3;
            font-size: 0.9rem;
            font-weight: 500;
        }

        /* --- Outfit Scroller (穿搭區) --- */
        .outfit-section {
            padding: 24px 0 0 24px;
            /* 右邊不留白讓卡片可以滑出去 */
            overflow: hidden;
        }

        .section-label {
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            color: #b2bec3;
            font-weight: 700;
            margin-bottom: 12px;
            display: block;
        }

        .outfit-scroller {
            display: flex;
            overflow-x: auto;
            padding-bottom: 20px;
            /* 為了顯示陰影 */
            padding-right: 24px;
            scroll-behavior: smooth;
            -webkit-overflow-scrolling: touch;
        }

        /* 隱藏捲軸但保留功能 */
        .outfit-scroller::-webkit-scrollbar {
            display: none;
        }

        .outfit-card {
            min-width: 260px;
            /* 卡片寬度 */
            background: var(--card-bg);
            border-radius: 20px;
            padding: 20px;
            margin-right: 16px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
            position: relative;
            flex-shrink: 0;
            border: 1px solid rgba(0, 0, 0, 0.02);
        }

        .outfit-day {
            font-size: 0.8rem;
            font-weight: 700;
            color: var(--accent);
            background: #EEEBFF;
            padding: 4px 10px;
            border-radius: 12px;
            display: inline-block;
            margin-bottom: 12px;
        }

        .outfit-title {
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 12px;
            display: block;
        }

        .outfit-items {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .outfit-items li {
            font-size: 0.9rem;
            color: #636e72;
            margin-bottom: 6px;
            display: flex;
            align-items: center;
        }

        .outfit-items li::before {
            content: '';
            width: 6px;
            height: 6px;
            background: #dfe6e9;
            border-radius: 50%;
            margin-right: 8px;
        }

        /* --- Packing List Section --- */
        .container {
            padding: 10px 24px;
        }

        .list-group {
            margin-bottom: 30px;
        }

        .group-header {
            display: flex;
            align-items: center;
            margin-bottom: 16px;
        }

        .group-icon {
            width: 36px;
            height: 36px;
            background: var(--card-bg);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            margin-right: 12px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
        }

        .group-title {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--primary);
        }

        .group-desc {
            font-size: 0.8rem;
            color: #b2bec3;
            margin-left: 8px;
            font-weight: normal;
        }

        /* Checkbox Item */
        .item {
            background: var(--card-bg);
            border-radius: 16px;
            padding: 16px;
            margin-bottom: 12px;
            display: flex;
            align-items: flex-start;
            transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
            cursor: pointer;
            border: 2px solid transparent;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.02);
        }

        .item:active {
            transform: scale(0.98);
        }

        .checkbox-custom {
            width: 24px;
            height: 24px;
            border-radius: 8px;
            border: 2px solid #dfe6e9;
            margin-right: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            transition: all 0.2s;
            margin-top: 2px;
        }

        .checkbox-custom svg {
            width: 14px;
            height: 14px;
            fill: white;
            transform: scale(0);
            transition: transform 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .item-content {
            flex: 1;
        }

        .item-name {
            font-size: 1rem;
            font-weight: 600;
            color: #2d3436;
            margin-bottom: 4px;
            display: block;
            transition: color 0.2s;
        }

        .item-note {
            font-size: 0.8rem;
            color: #b2bec3;
            line-height: 1.4;
        }

        /* Tags */
        .tag {
            font-size: 0.7rem;
            padding: 3px 8px;
            border-radius: 6px;
            margin-left: 6px;
            font-weight: 700;
            vertical-align: middle;
            display: inline-block;
        }

        .tag-red {
            background: #ffebee;
            color: #ff7675;
        }

        .tag-blue {
            background: #e3f2fd;
            color: #74b9ff;
        }

        .tag-yel {
            background: #fff3e0;
            color: #fab1a0;
        }

        /* Checked State */
        .item.checked {
            background: #F9F9F9;
            border-color: transparent;
            box-shadow: none;
        }

        .item.checked .checkbox-custom {
            background: var(--success);
            border-color: var(--success);
        }

        .item.checked .checkbox-custom svg {
            transform: scale(1);
        }

        .item.checked .item-name {
            color: #dcdde1;
            text-decoration: line-through;
        }

        .item.checked .item-note {
            color: #dfe6e9;
        }

        .item.checked .tag {
            opacity: 0.3;
        }

        /* --- Footer Progress --- */
        .footer-nav {
            position: fixed;
            bottom: 20px;
            left: 20px;
            right: 20px;
            background: rgba(45, 52, 54, 0.95);
            backdrop-filter: blur(10px);
            padding: 16px 24px;
            border-radius: 24px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
            z-index: 100;
            color: white;
        }

        .progress-info {
            display: flex;
            flex-direction: column;
        }

        .progress-label {
            font-size: 0.75rem;
            opacity: 0.7;
            margin-bottom: 4px;
        }

        .progress-numbers {
            font-size: 1.1rem;
            font-weight: 700;
            letter-spacing: 1px;
        }

        .progress-bar-bg {
            position: absolute;
            bottom: 0;
            left: 0;
            height: 4px;
            background: rgba(255, 255, 255, 0.1);
            width: 100%;
            border-bottom-left-radius: 24px;
            border-bottom-right-radius: 24px;
            overflow: hidden;
        }

        .progress-bar-fill {
            height: 100%;
            background: var(--success);
            width: 0%;
            transition: width 0.4s ease;
        }

        .reset-link {
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.5);
            text-decoration: none;
            padding: 8px 12px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
        }
    </style>
</head>

<body>

    <div class="header">
        <h1>Hong Kong 2026 🇭🇰</h1>
        <p>確認清單 & 穿搭行程表</p>
    </div>

    <div class="outfit-section">
        <span class="section-label">OUTFIT PLAN</span>
        <div class="outfit-scroller">
            <div class="outfit-card">
                <span class="outfit-day">DAY 1 (1/21)</span>
                <span class="outfit-title">移動日 & 燒肉</span>
                <ul class="outfit-items">
                    <li>🧥 黑色皮衣</li>
                    <li>👕 白色 T (聚酯)</li>
                    <li>👖 灰色直筒褲</li>
                    <li>👞 黑色皮鞋 (身上)</li>
                </ul>
            </div>
            <div class="outfit-card">
                <span class="outfit-day">DAY 2 (1/22)</span>
                <span class="outfit-title">迪士尼樂園</span>
                <ul class="outfit-items">
                    <li>👕 針織毛衣 (灰)</li>
                    <li>🧥 白色外套</li>
                    <li>👖 白色直筒褲</li>
                    <li>👞 黑色皮鞋 (或換 AF1)</li>
                </ul>
            </div>
            <div class="outfit-card">
                <span class="outfit-day">DAY 3 (1/23)</span>
                <span class="outfit-title">長洲 & Bar</span>
                <ul class="outfit-items">
                    <li>👕 黑色 T (+內衣)</li>
                    <li>🧥 白色外套 + 黑皮衣</li>
                    <li>👖 棕色直筒褲</li>
                    <li>👟 Air Force 1</li>
                </ul>
            </div>
            <div class="outfit-card">
                <span class="outfit-day">DAY 4 (1/24)</span>
                <span class="outfit-title">回程</span>
                <ul class="outfit-items">
                    <li>🧥 海軍藍針織外套</li>
                    <li>👕 黑色 T</li>
                    <li>👖 白色褲子 + 皮帶</li>
                    <li>👟 Air Force 1</li>
                </ul>
            </div>
        </div>
    </div>

    <div class="container">

        <div class="list-group">
            <div class="group-header">
                <div class="group-icon">🎒</div>
                <div>
                    <div class="group-title">隨身手提</div>
                    <div class="group-desc">貴重、電池、畫作 (不可托運)</div>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">護照 & 身分證 <span class="tag tag-red">必備</span></span>
                    <span class="item-note">檢查效期，放包包夾層</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">港簽 / 台胞證</span>
                    <span class="item-note">紙本印了嗎？卡片帶了嗎？</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">噴漆畫 ×2 <span class="tag tag-yel">小心</span></span>
                    <span class="item-note">手提保護，上機放座位下或櫃頂</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">行動電源 <span class="tag tag-red">嚴禁托運</span></span>
                    <span class="item-note">只能放隨身包！</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">電動刮鬍刀 <span class="tag tag-red">含鋰電</span></span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">港幣 & 信用卡 (玫瑰)</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">AirPods & 手機 & 轉接頭</span>
                    <span class="item-note">轉接頭(英規)建議隨身</span>
                </div>
            </div>
        </div>

        <div class="list-group">
            <div class="group-header">
                <div class="group-icon">🧳</div>
                <div>
                    <div class="group-title">托運行李箱</div>
                    <div class="group-desc">液體 > 100ml、衣物、雜物</div>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">Air Force 1 (白)</span>
                    <span class="item-note">內塞襪子，包好放箱邊</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">所有換洗衣物 <span class="tag tag-blue">Day 2-4</span></span>
                    <span class="item-note">對照上方行程表檢查一次</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">內褲 / 襪子 × 3套</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">液體盥洗包 <span class="tag tag-yel">防漏</span></span>
                    <span class="item-note">隱眼液、食鹽水、洗面乳、香水</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">禮物：公仔×3、小熊</span>
                    <span class="item-note">用衣服包裹保護</span>
                </div>
            </div>

            <div class="item" onclick="toggleItem(this)">
                <div class="checkbox-custom"><svg viewBox="0 0 24 24">
                        <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z" />
                    </svg></div>
                <div class="item-content">
                    <span class="item-name">牙刷組 & 暖暖包 & 藥品</span>
                </div>
            </div>
        </div>

    </div>

    <div class="footer-nav">
        <div class="progress-info">
            <span class="progress-label">PACKING STATUS</span>
            <span class="progress-numbers"><span id="checked-count">0</span> / <span id="total-count">0</span></span>
        </div>
        <div onclick="resetAll()" class="reset-link">Reset</div>
        <div class="progress-bar-bg">
            <div class="progress-bar-fill" id="progress-fill"></div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const items = document.querySelectorAll('.item');
            document.getElementById('total-count').innerText = items.length;

            items.forEach((item, index) => {
                // 給每個項目唯一 ID
                item.dataset.id = index;
                // 讀取狀態 (使用 v3 避免舊緩存)
                if (localStorage.getItem('hk_pack_v3_' + index) === 'true') {
                    item.classList.add('checked');
                }
            });
            updateProgress();
        });

        function toggleItem(el) {
            el.classList.toggle('checked');
            const id = el.dataset.id;
            localStorage.setItem('hk_pack_v3_' + id, el.classList.contains('checked'));

            // 震動回饋 (手機端)
            if (navigator.vibrate) navigator.vibrate(10);

            updateProgress();
        }

        function updateProgress() {
            const total = document.querySelectorAll('.item').length;
            const checked = document.querySelectorAll('.item.checked').length;
            const percentage = (checked / total) * 100;

            document.getElementById('checked-count').innerText = checked;
            document.getElementById('progress-fill').style.width = percentage + '%';
        }

        function resetAll() {
            if (confirm('重置所有清單？')) {
                document.querySelectorAll('.item').forEach(item => {
                    item.classList.remove('checked');
                    localStorage.removeItem('hk_pack_v3_' + item.dataset.id);
                });
                updateProgress();
            }
        }
    </script>
</body>

</html>
