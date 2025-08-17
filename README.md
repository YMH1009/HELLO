
<head>
    <meta charset="UTF-8" />
    <title>健檢流程控制台</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            text-align: center;
            background: #f9f9f9;
        }

        h2,
        h3 {
            margin-bottom: 10px;
        }

        .option,
        .station {
            display: inline-block;
            margin: 8px;
        }

        .btn {
            width: 140px;
            height: 60px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            background-color: #ddd;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn.selected {
            background-color: #1E90FF;
            color: white;
        }

        .btn.done {
            background-color: #32CD32;
            color: white;
        }

        .hidden {
            display: none;
        }

        #addons {
            border: 1px solid #ccc;
            padding: 15px;
            margin: 15px auto;
            border-radius: 10px;
            background: white;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
            max-width: 800px;
        }

        #signature {
            border: 2px solid #000;
            width: 300px;
            height: 150px;
            margin: 10px auto;
            cursor: crosshair;
            background: white;
        }

        #signatureContainer {
            text-align: center;
            margin: 20px 0;
        }

        .signature-controls {
            margin: 10px 0;
        }

        .signature-controls button {
            margin: 5px;
            padding: 8px 15px;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .signature-controls button:hover {
            background: #0056b3;
        }

        #total {
            font-size: 18px;
            font-weight: bold;
            margin: 10px 0;
        }

        .package-section {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin: 10px 0;
        }

        .package-box {
            border: 1px solid #aaa;
            border-radius: 10px;
            padding: 10px;
            margin: 5px;
            width: 220px;
            background: #fdfdfd;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
        }

        .package-box h4 {
            margin: 5px 0;
        }

        .package-items {
            margin-top: 5px;
        }

        .package-items button {
            display: block;
            width: 120px;
            height: 40px;
            margin: 5px auto;
            font-size: 14px;
            border-radius: 8px;
            border: none;
            background-color: #eee;
            cursor: pointer;
        }

        .package-items button.selected {
            background-color: #1E90FF;
            color: white;
        }

        #selectedOptions button {
            margin: 5px;
        }

        .single-item {
            width: 160px;
            height: 50px;
            margin: 5px;
            font-size: 14px;
        }

        .single-item.selected {
            background-color: #FF6347;
            color: white;
        }

        .status-indicator {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #28a745;
            color: white;
            padding: 10px 15px;
            border-radius: 5px;
            font-size: 14px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        }

        #freeGifts {
            border: 2px solid #FF6B6B;
            border-radius: 10px;
            padding: 15px;
            margin: 20px auto;
            max-width: 800px;
            background: linear-gradient(135deg, #FFE5E5, #FFF0F0);
            box-shadow: 0 3px 10px rgba(255, 107, 107, 0.3);
        }

        #freeGifts h3 {
            color: #FF4757;
            margin-bottom: 15px;
            font-size: 20px;
        }

        .gift-item {
            width: 150px;
            height: 50px;
            margin: 5px;
            font-size: 13px;
            background-color: #FFB3BA;
            color: #333;
            border: 2px solid #FF8A95;
            transition: all 0.3s ease;
        }

        .gift-item:disabled {
            background-color: #F0F0F0;
            color: #999;
            cursor: not-allowed;
            border-color: #CCC;
        }

        .gift-item.selected {
            background-color: #FF4757;
            color: white;
            border-color: #FF3742;
            transform: scale(1.05);
        }

        .gift-item.auto-selected {
            background-color: #2ECC71;
            color: white;
            border-color: #27AE60;
        }

        .gift-info {
            font-size: 14px;
            color: #666;
            margin-bottom: 10px;
            font-style: italic;
        }
    </style>
</head>

<body>
    <div class="status-indicator" id="statusIndicator">已選擇: 0/2</div>

    <div id="page1">
        <h2>加選項目 (9選2)</h2>
        <div id="options">
            <div class="option">
                <button class="btn" id="opt1" onclick="toggleOption(this)">腹部超音波</button>
            </div>
            <div class="option">
                <button class="btn" id="opt2" onclick="toggleOption(this)">婦科超音波</button>
            </div>
            <div class="option">
                <button class="btn" id="opt3" onclick="toggleOption(this)">頸動脈超音波</button>
            </div>
            <div class="option">
                <button class="btn" id="opt4" onclick="toggleOption(this)">甲狀腺超音波</button>
            </div>
            <div class="option">
                <button class="btn" id="opt5" onclick="toggleOption(this)">攝護腺超音波</button>
            </div>
            <div class="option">
                <button class="btn" id="opt6" onclick="toggleOption(this)">乳房超音波</button>
            </div>
            <div class="option">
                <button class="btn" id="opt7" onclick="toggleOption(this)">HRV</button>
            </div>
            <div class="option">
                <button class="btn" id="opt8" onclick="toggleOption(this)">眼底攝影</button>
            </div>
            <div class="option">
                <button class="btn" id="opt9" onclick="toggleOption(this)">動脈硬化</button>
            </div>
        </div>

        <div style="margin-top:20px;">
            <button class="btn" onclick="toggleAddons()">加做項目</button>
        </div>

        <div id="addons" class="hidden">
            <h3>加做項目套餐</h3>
            <div id="top-packages" class="package-section">
                <!-- A套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgA" onclick="togglePackage('A')">A套餐 優惠價3000元</button>
                    <div class="package-items" id="itemsA">
                        <button data-price="900" class="pkg-item" data-pkg="A" id="pkgA1">同半胱胺酸 900元</button>
                        <button data-price="900" class="pkg-item" data-pkg="A" id="pkgA2">高敏感C反應蛋白 900元</button>
                        <button data-price="800" class="pkg-item" data-pkg="A" id="pkgA3">心肌旋轉蛋白 800元</button>
                        <button data-price="1600" class="pkg-item" data-pkg="A" id="pkgA4">B型利納肽前驅物 1600元</button>
                        <button data-price="1200" class="pkg-item" data-pkg="A" data-single="true" id="pkgA5">頸動脈超音波 1200元</button>
                        <button data-price="1200" class="pkg-item" data-pkg="A" data-single="true" id="pkgA6">眼底攝影 1200元</button>
                    </div>
                </div>
                <!-- B套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgB" onclick="togglePackage('B')">B套餐 優惠價2200元</button>
                    <div class="package-items" id="itemsB">
                        <button data-price="900" class="pkg-item" data-pkg="B" id="pkgB1">甲狀腺功能 900元</button>
                        <button data-price="800" class="pkg-item" data-pkg="B" id="pkgB2">自體免疫疾病檢查 800元</button>
                        <button data-price="500" class="pkg-item" data-pkg="B" id="pkgB3">電解質檢查 500元</button>
                        <button data-price="600" class="pkg-item" data-pkg="B" id="pkgB4">B肝抗原抗體 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="B" id="pkgB5">C肝檢查 600元</button>
                        <button data-price="800" class="pkg-item" data-pkg="B" id="pkgB6">胰島素 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="B" id="pkgB7">維生素D 800元</button>
                    </div>
                </div>
                <!-- C套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgC" onclick="togglePackage('C')">C套餐 優惠價2500元</button>
                    <div class="package-items" id="itemsC">
                        <button data-price="500" class="pkg-item" data-pkg="C" id="pkgC1">解肢酶 500元</button>
                        <button data-price="800" class="pkg-item" data-pkg="C" id="pkgC2">胃癌 800元</button>
                        <button data-price="700" class="pkg-item" data-pkg="C" id="pkgC3">胰臟癌 700元</button>
                        <button data-price="1200" class="pkg-item" data-pkg="C" id="pkgC4">C13 1200元</button>
                    </div>
                </div>
            </div>

            <div id="bottom-packages" class="package-section">
                <!-- D套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgD" onclick="togglePackage('D')">D套餐(男) 優惠價2000元</button>
                    <div class="package-items" id="itemsD">
                        <button data-price="800" class="pkg-item" data-pkg="D" id="pkgD1">鼻咽癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="D" id="pkgD2">鱗狀上皮細胞癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="D" id="pkgD3">肺腺癌 800元</button>
                        <button data-price="700" class="pkg-item" data-pkg="D" id="pkgD4">肺癌 700元</button>
                    </div>
                </div>
                <!-- E套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgE" onclick="togglePackage('E')">E套餐(女) 優惠價2000元</button>
                    <div class="package-items" id="itemsE">
                        <button data-price="800" class="pkg-item" data-pkg="E" id="pkgE1">鱗狀上皮細胞癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="E" id="pkgE2">肺腺癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="E" id="pkgE3">卵巢癌 800元</button>
                        <button data-price="700" class="pkg-item" data-pkg="E" id="pkgE4">肺癌 700元</button>
                    </div>
                </div>
                <!-- F套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgF" onclick="togglePackage('F')">F套餐 優惠價2000元</button>
                    <div class="package-items" id="itemsF">
                        <button data-price="900" class="pkg-item" data-pkg="F" id="pkgF1">腎上腺皮質素 900元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF2">睪固酮(男) 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF3">雌二醇(女) 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF4">黃體生成激素 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF5">濾泡刺激素 600元</button>
                    </div>
                </div>
            </div>

            <div style="margin: 20px 0;">
                <h3>單項加做項目</h3>
                <div class="package-section">
                    <button data-price="1200" class="single-item btn" id="singleHRV">HRV 1200元</button>
                    <button data-price="600" class="single-item btn" id="singleAbdominal">腹部超音波 600元</button>
                    <button data-price="600" class="single-item btn" id="singleThyroid">甲狀腺超音波 600元</button>
                    <button data-price="600" class="single-item btn" id="singleProstate">攝護腺超音波 600元</button>
                    <button data-price="800" class="single-item btn" id="singleBreast">乳房超音波 800元</button>
                    <button data-price="600" class="single-item btn" id="singleGynecology">婦科超音波 600元</button>
                    <button data-price="2500" class="single-item btn" id="singleE66">E66 2500元</button>
                    <button data-price="4800" class="single-item btn" id="singleE110">E110 4800元</button>
                </div>
            </div>

            <div id="total">總金額: 0 元</div>

            <div id="freeGifts">
                <h3>🎁 免費贈送項目</h3>
                <div class="gift-info">
                    滿7500元可選擇1項超音波檢查 | 滿9000元自動加贈IGE免疫球蛋白
                </div>
                <div class="package-section">
                    <button class="gift-item btn" id="giftAbdominal" onclick="selectGift(this)" disabled>腹部超音波</button>
                    <button class="gift-item btn" id="giftGynecology" onclick="selectGift(this)" disabled>婦科超音波</button>
                    <button class="gift-item btn" id="giftBreast" onclick="selectGift(this)" disabled>乳房超音波</button>
                    <button class="gift-item btn" id="giftThyroid" onclick="selectGift(this)" disabled>甲狀腺超音波</button>
                    <button class="gift-item btn" id="giftCarotid" onclick="selectGift(this)" disabled>頸動脈超音波</button>
                    <button class="gift-item btn" id="giftProstate" onclick="selectGift(this)" disabled>攝護腺超音波</button>
                    <button class="gift-item btn" id="giftIGE" onclick="selectGift(this)" disabled>IGE免疫球蛋白</button>
                </div>
            </div>

            <div id="signatureContainer">
                <h4>請在下方簽名：</h4>
                <canvas id="signature" width="300" height="150"></canvas>
                <div class="signature-controls">
                    <button onclick="clearSignature()">清除簽名</button>
                </div>
            </div>

            <button class="btn" onclick="takeScreenshot()">長截圖</button>
            <br />
            <br />
        </div>

        <button class="btn" onclick="confirmPage1()">OK</button>
    </div>

    <div id="page2" class="hidden">
        <h2>健檢關卡進度</h2>
        <div id="selectedOptions"></div>
        <div class="station">
            <button class="btn" id="height" onclick="markDone(this)">身高</button>
        </div>
        <div class="station">
            <button class="btn" id="fat" onclick="markDone(this)">體脂</button>
        </div>
        <div class="station">
            <button class="btn" id="blood" onclick="markDone(this)">抽血</button>
        </div>
        <div class="station">
            <button class="btn" id="dr" onclick="markDone(this)">理學檢查</button>
        </div>
        <div class="station">
            <button class="btn" id="xray" onclick="markDone(this)">X光</button>
        </div>
        <br />
        <button class="btn" onclick="goBack()">返回</button>
    </div>

    <script>
        // 統一使用一套變數系統來管理狀態
        let selected = [];
        let selectedButtons = {};
        let packageTotals = {
            A: 0,
            B: 0,
            C: 0,
            D: 0,
            E: 0,
            F: 0
        };
        let selectedGift = null;
        let currentPage = 1;
        let addonsVisible = false;

        // 签名相关变量
        let isDrawing = false;
        let canvas, ctx;

        // URL參數處理函數
        function updateURL() {
            const state = {
                page: currentPage,
                selected: selected.join(','),
                selectedButtons: Object.keys(selectedButtons).join(','),
                packages: Object.keys(packageTotals).filter(k => packageTotals[k] > 0).join(','),
                pkgItems: [],
                singleItems: [],
                gift: selectedGift,
                addons: addonsVisible ? '1' : '0',
                done: []
            };

            // 收集套餐內選中的項目
            document.querySelectorAll(".pkg-item.selected").forEach(btn => {
                state.pkgItems.push(btn.id);
            });

            // 收集單項選中的項目
            document.querySelectorAll(".single-item.selected").forEach(btn => {
                state.singleItems.push(btn.id);
            });

            // 收集完成狀態的按鈕（包含第二頁的關卡按鈕和動態生成的按鈕）
            document.querySelectorAll(".btn.done").forEach(btn => {
                state.done.push(btn.id);
            });

            // 特別處理第二頁動態生成的按鈕
            if (currentPage === 2) {
                document.querySelectorAll("#selectedOptions .btn.done").forEach(btn => {
                    state.done.push('dynamic-' + btn.id);
                });
            }

            const params = new URLSearchParams();
            Object.keys(state).forEach(key => {
                if (Array.isArray(state[key])) {
                    if (state[key].length > 0) {
                        params.set(key, state[key].join(','));
                    }
                } else if (state[key] !== null && state[key] !== '' && state[key] !== 0) {
                    params.set(key, state[key]);
                }
            });

            const newURL = window.location.pathname + '?' + params.toString();
            window.history.replaceState({}, '', newURL);
        }

        function loadFromURL() {
            const params = new URLSearchParams(window.location.search);

            // 恢復當前頁面
            currentPage = parseInt(params.get('page')) || 1;

            // 恢復基本選項
            const selectedItems = params.get('selected');
            if (selectedItems) {
                selected = selectedItems.split(',').filter(s => s);
            }

            const selectedBtns = params.get('selectedButtons');
            if (selectedBtns) {
                selectedBtns.split(',').forEach(btnId => {
                    if (btnId) {
                        selectedButtons[btnId] = true;
                        const btn = document.getElementById(btnId);
                        if (btn) btn.classList.add('selected');
                    }
                });
            }

            // 恢復套餐選擇
            const packages = params.get('packages');
            if (packages) {
                packages.split(',').forEach(pkg => {
                    if (pkg) {
                        packageTotals[pkg] = getPackagePrice(pkg);
                        const btn = document.getElementById('pkg' + pkg);
                        if (btn) btn.classList.add('selected');
                    }
                });
            }

            // 恢復套餐內項目
            const pkgItems = params.get('pkgItems');
            if (pkgItems) {
                pkgItems.split(',').forEach(itemId => {
                    if (itemId) {
                        const btn = document.getElementById(itemId);
                        if (btn) btn.classList.add('selected');
                    }
                });
            }

            // 恢復單項選擇
            const singleItems = params.get('singleItems');
            if (singleItems) {
                singleItems.split(',').forEach(itemId => {
                    if (itemId) {
                        const btn = document.getElementById(itemId);
                        if (btn) btn.classList.add('selected');
                    }
                });
            }

            // 恢復贈品選擇
            selectedGift = params.get('gift');
            if (selectedGift) {
                const giftBtn = document.getElementById(selectedGift);
                if (giftBtn) giftBtn.classList.add('selected');
            }

            // 恢復addons顯示狀態
            addonsVisible = params.get('addons') === '1';
            if (addonsVisible) {
                document.getElementById('addons').classList.remove('hidden');
            }

            // 恢復完成狀態
            const doneItems = params.get('done');
            if (doneItems) {
                doneItems.split(',').forEach(btnId => {
                    if (btnId) {
                        // 處理動態按鈕的完成狀態
                        if (btnId.startsWith('dynamic-')) {
                            const actualId = btnId.replace('dynamic-', '');
                            // 這些狀態會在renderSelectedOptions中處理
                            return;
                        }

                        const btn = document.getElementById(btnId);
                        if (btn) {
                            btn.classList.add('done');
                            if (!btn.textContent.includes('✅')) {
                                btn.textContent += ' ✅';
                            }
                        }
                    }
                });
            }

            // 切換到正確的頁面
            if (currentPage === 2) {
                document.getElementById('page1').classList.add('hidden');
                document.getElementById('page2').classList.remove('hidden');
                renderSelectedOptions();

                // 恢復動態生成按鈕的完成狀態
                if (doneItems) {
                    setTimeout(() => {
                        doneItems.split(',').forEach(btnId => {
                            if (btnId.startsWith('dynamic-')) {
                                const actualId = btnId.replace('dynamic-', '');
                                const btn = document.getElementById(actualId);
                                if (btn) {
                                    btn.classList.add('done');
                                    if (!btn.textContent.includes('✅')) {
                                        btn.textContent += ' ✅';
                                    }
                                }
                            }
                        });
                    }, 100);
                }
            }

            updateStatusIndicator();
            updateTotal();
        }

        // 初始化签名画布
        function initSignature() {
            canvas = document.getElementById('signature');
            ctx = canvas.getContext('2d');

            ctx.strokeStyle = '#000000';
            ctx.lineWidth = 2;
            ctx.lineCap = 'round';

            // 鼠标事件
            canvas.addEventListener('mousedown', startDrawing);
            canvas.addEventListener('mousemove', draw);
            canvas.addEventListener('mouseup', stopDrawing);
            canvas.addEventListener('mouseout', stopDrawing);

            // 触摸事件（移动设备）
            canvas.addEventListener('touchstart', handleTouch);
            canvas.addEventListener('touchmove', handleTouch);
            canvas.addEventListener('touchend', stopDrawing);
        }

        function startDrawing(e) {
            isDrawing = true;
            const rect = canvas.getBoundingClientRect();
            ctx.beginPath();
            ctx.moveTo(e.clientX - rect.left, e.clientY - rect.top);
        }

        function draw(e) {
            if (!isDrawing) return;
            const rect = canvas.getBoundingClientRect();
            ctx.lineTo(e.clientX - rect.left, e.clientY - rect.top);
            ctx.stroke();
        }

        function stopDrawing() {
            if (isDrawing) {
                isDrawing = false;
                saveSignature();
            }
        }

        function handleTouch(e) {
            e.preventDefault();
            const touch = e.touches[0];
            const rect = canvas.getBoundingClientRect();

            if (e.type === 'touchstart') {
                isDrawing = true;
                ctx.beginPath();
                ctx.moveTo(touch.clientX - rect.left, touch.clientY - rect.top);
            } else if (e.type === 'touchmove' && isDrawing) {
                ctx.lineTo(touch.clientX - rect.left, touch.clientY - rect.top);
                ctx.stroke();
            }
        }

        function clearSignature() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        function saveSignature() {
            const signatureData = canvas.toDataURL();
        }

        function updateStatusIndicator() {
            const indicator = document.getElementById('statusIndicator');
            indicator.textContent = `已選擇: ${selected.length}/2`;
            indicator.style.backgroundColor = selected.length === 2 ? '#28a745' : '#ffc107';
        }

        // 新增贈品選擇功能
        function selectGift(btn) {
            if (btn.disabled) return;

            if (btn.id === 'giftIGE') {
                return;
            }

            // 清除其他超音波選擇（除了IGE）
            document.querySelectorAll('.gift-item:not(#giftIGE)').forEach(giftBtn => {
                giftBtn.classList.remove('selected');
            });

            // 選擇當前按鈕
            btn.classList.add('selected');
            selectedGift = btn.id;
            updateURL();
        }

        // 更新贈品可用狀態
        function updateGiftAvailability(totalAmount) {
            const ultrasoundGifts = ['giftAbdominal', 'giftGynecology', 'giftBreast', 'giftThyroid', 'giftCarotid',
                'giftProstate'
            ];
            const igeGift = document.getElementById('giftIGE');

            // 處理超音波贈品（滿7500元）
            ultrasoundGifts.forEach(giftId => {
                const giftBtn = document.getElementById(giftId);
                if (totalAmount >= 7500) {
                    giftBtn.disabled = false;
                    giftBtn.style.cursor = 'pointer';
                } else {
                    giftBtn.disabled = true;
                    giftBtn.classList.remove('selected');
                    giftBtn.style.cursor = 'not-allowed';
                }
            });

            // 處理IGE免疫球蛋白（滿9000元自動選擇）
            if (totalAmount >= 9000) {
                igeGift.disabled = false;
                igeGift.classList.add('auto-selected');
                igeGift.classList.remove('selected');
            } else {
                igeGift.disabled = true;
                igeGift.classList.remove('auto-selected', 'selected');
            }

            // 如果總金額降到7500以下，清除所有選擇
            if (totalAmount < 7500) {
                selectedGift = null;
            }
        }

        async function takeScreenshot() {
            try {
                const script = document.createElement('script');
                script.src = 'https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js';
                document.head.appendChild(script);

                script.onload = async function () {
                    try {
                        const loadingMsg = document.createElement('div');
                        loadingMsg.textContent = '正在生成截圖...';
                        loadingMsg.style.position = 'fixed';
                        loadingMsg.style.top = '50%';
                        loadingMsg.style.left = '50%';
                        loadingMsg.style.transform = 'translate(-50%, -50%)';
                        loadingMsg.style.background = '#007bff';
                        loadingMsg.style.color = 'white';
                        loadingMsg.style.padding = '20px';
                        loadingMsg.style.borderRadius = '10px';
                        loadingMsg.style.zIndex = '9999';
                        loadingMsg.style.fontSize = '18px';
                        document.body.appendChild(loadingMsg);

                        const screenshotCanvas = await html2canvas(document.body, {
                            useCORS: true,
                            allowTaint: true,
                            scale: 1,
                            backgroundColor: '#ffffff',
                            removeContainer: false,
                            foreignObjectRendering: true
                        });

                        document.body.removeChild(loadingMsg);

                        screenshotCanvas.toBlob(async function (blob) {
                            try {
                                if (navigator.clipboard && window.ClipboardItem) {
                                    await navigator.clipboard.write([
                                        new ClipboardItem({
                                            'image/png': blob
                                        })
                                    ]);
                                    alert('完整頁面截圖已複製到剪貼簿！\n可以直接貼到其他應用程式中使用。');
                                } else {
                                    throw new Error('剪貼簿API不可用');
                                }
                            } catch (err) {
                                console.error('複製到剪貼簿失敗:', err);
                                const url = URL.createObjectURL(blob);
                                const a = document.createElement('a');
                                a.href = url;
                                a.download = '健檢流程-' + new Date().toISOString().slice(0, 10) + '.png';
                                a.click();
                                URL.revokeObjectURL(url);
                                alert('完整頁面截圖已下載到本機！');
                            }
                        }, 'image/png', 1.0);
                    } catch (error) {
                        console.error('截圖失敗:', error);
                        alert('截圖功能出現問題，請嘗試以下備用方案：\n1. 使用瀏覽器列印功能（Ctrl+P）\n2. 使用瀏覽器開發者工具的裝置模擬功能截圖');
                    }
                };

                script.onerror = function () {
                    alert('截圖功能載入失敗，請檢查網路連線或使用瀏覽器列印功能（Ctrl+P）');
                };
            } catch (error) {
                console.error('截圖功能初始化失敗:', error);
                alert('截圖功能暫不可用，建議使用瀏覽器列印功能（Ctrl+P）儲存頁面');
            }
        }

        function toggleOption(btn) {
            if (btn.classList.contains("selected")) {
                btn.classList.remove("selected");
                selected = selected.filter(x => x !== btn.textContent);
                delete selectedButtons[btn.id];
            } else {
                if (selected.length >= 2) {
                    alert("最多選2個");
                    return;
                }
                btn.classList.add("selected");
                selected.push(btn.textContent);
                selectedButtons[btn.id] = true;
            }
            updateStatusIndicator();
            updateURL();
        }

        function toggleAddons() {
            document.getElementById("addons").classList.toggle("hidden");
            addonsVisible = !document.getElementById("addons").classList.contains("hidden");
            updateURL();
        }

        function getPackagePrice(pkg) {
            const packagePrice = {
                A: 3000,
                B: 2200,
                C: 2500,
                D: 2000,
                E: 2000,
                F: 2000
            };
            return packagePrice[pkg];
        }

        function clearPackage(pkg) {
            // 清除指定套餐的所有狀態
            const pkgBtn = document.getElementById("pkg" + pkg);
            pkgBtn.classList.remove("selected");
            packageTotals[pkg] = 0;

            // 清除該套餐所有內部項目
            document.querySelectorAll("#items" + pkg + " .pkg-item").forEach(innerBtn => {
                innerBtn.classList.remove("selected");
            });
        }

        function togglePackage(pkg) {
            let btn = document.getElementById("pkg" + pkg);

            // D和E套餐互斥 - 先處理互斥邏輯
            if (pkg === "D") {
                clearPackage("E");
            }
            if (pkg === "E") {
                clearPackage("D");
            }

            // 切換當前套餐狀態
            btn.classList.toggle("selected");
            packageTotals[pkg] = btn.classList.contains("selected") ? getPackagePrice(pkg) : 0;

            // 處理當前套餐的子項目
            document.querySelectorAll("#items" + pkg + " .pkg-item").forEach(innerBtn => {
                if (btn.classList.contains("selected")) {
                    innerBtn.classList.add("selected");
                } else {
                    innerBtn.classList.remove("selected");
                }
            });

            updateTotal();
            updateURL();
        }

        document.querySelectorAll(".pkg-item").forEach(btn => {
            btn.addEventListener("click", function () {
                let pkg = btn.dataset.pkg;
                if (!document.getElementById("pkg" + pkg).classList.contains("selected")) {
                    // D和E套餐內部項目互斥邏輯 - 無論是否已選中，都要清除對方套餐
                    if (pkg === "D") {
                        clearPackage("E");
                    }
                    if (pkg === "E") {
                        clearPackage("D");
                    }

                    btn.classList.toggle("selected");
                    updateTotal();
                    updateURL();
                }
            });
        });

        // 單項加做項目點擊事件
        document.querySelectorAll(".single-item").forEach(btn => {
            btn.addEventListener("click", function () {
                btn.classList.toggle("selected");
                updateTotal();
                updateURL();
            });
        });

        function updateTotal() {
            let sum = 0;

            // 檢查選中的套餐
            let selectedPackages = [];
            for (let k in packageTotals) {
                if (packageTotals[k] > 0) {
                    selectedPackages.push(k);
                }
            }

            // 檢查優惠組合規則（按優惠力度排序）
            let comboApplied = false;
            let comboDescription = "";

            // 規則4: A+B+C+D或E+F = 10000
            if (selectedPackages.includes('A') && selectedPackages.includes('B') && selectedPackages.includes('C') &&
                ((selectedPackages.includes('D') || selectedPackages.includes('E')) && selectedPackages.includes('F'))) {
                sum = 10000;
                comboApplied = true;
                comboDescription = " (套餐A+B+C+D/E+F優惠組合)";
            }
            // 規則2: A+B+C+D = 9000
            else if (selectedPackages.includes('A') && selectedPackages.includes('B') &&
                selectedPackages.includes('C') && selectedPackages.includes('D')) {
                sum = 9000;
                comboApplied = true;
                comboDescription = " (套餐A+B+C+D優惠組合)";
            }
            // 規則3: A+B+C+E = 9000
            else if (selectedPackages.includes('A') && selectedPackages.includes('B') &&
                selectedPackages.includes('C') && selectedPackages.includes('E')) {
                sum = 9000;
                comboApplied = true;
                comboDescription = " (套餐A+B+C+E優惠組合)";
            }
            // 規則1: A+B+C = 7500
            else if (selectedPackages.includes('A') && selectedPackages.includes('B') &&
                selectedPackages.includes('C')) {
                sum = 7500;
                comboApplied = true;
                comboDescription = " (套餐A+B+C優惠組合)";
            }
            // 沒有符合優惠組合，使用原始價格計算
            else {
                for (let k in packageTotals) sum += packageTotals[k];
            }

            // 計算套餐內個別選項的價格（只有在沒有套餐組合優惠時才計算）
            if (!comboApplied) {
                document.querySelectorAll(".pkg-item.selected").forEach(btn => {
                    let pkg = btn.dataset.pkg;
                    if (!document.getElementById("pkg" + pkg).classList.contains("selected")) {
                        sum += parseInt(btn.dataset.price);
                    }
                });
            } else {
                // 如果有套餐組合優惠，仍需要計算非套餐內的個別選項
                document.querySelectorAll(".pkg-item.selected").forEach(btn => {
                    let pkg = btn.dataset.pkg;
                    if (!document.getElementById("pkg" + pkg).classList.contains("selected")) {
                        sum += parseInt(btn.dataset.price);
                    }
                });
            }

            // 計算單項加做項目的價格
            document.querySelectorAll(".single-item.selected").forEach(btn => {
                sum += parseInt(btn.dataset.price);
            });

            document.getElementById("total").textContent = "總金額: " + sum + " 元" + comboDescription;

            // 更新贈品可用性
            updateGiftAvailability(sum);
        }

        function confirmPage1() {
            let pwd = prompt("請輸入驗證碼");
            if (!pwd || pwd.toLowerCase() !== "s1") {
                alert("驗證失敗");
                return;
            }
            if (selected.length !== 2) {
                alert("請選2個項目");
                return;
            }

            currentPage = 2;
            document.getElementById("page1").classList.add("hidden");
            document.getElementById("page2").classList.remove("hidden");
            renderSelectedOptions();
            updateURL();
        }

        function renderSelectedOptions() {
            let box = document.getElementById("selectedOptions");
            box.innerHTML = "";

            // 獲取當前完成狀態以便恢復
            const params = new URLSearchParams(window.location.search);
            const doneItems = params.get('done') ? params.get('done').split(',') : [];

            selected.forEach(name => {
                let btn = document.createElement("button");
                btn.className = "btn";
                btn.textContent = name;
                btn.id = name;
                btn.onclick = function () {
                    markDone(btn);
                }

                // 恢復完成狀態
                if (doneItems.includes('dynamic-' + name) || doneItems.includes(name)) {
                    btn.classList.add('done');
                    if (!btn.textContent.includes('✅')) {
                        btn.textContent += ' ✅';
                    }
                }

                box.appendChild(btn);
            });

            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                document.querySelectorAll("#items" + pkg + " .pkg-item").forEach(innerBtn => {
                    if (innerBtn.classList.contains("selected")) {
                        let btn = document.createElement("button");
                        btn.className = "btn";
                        btn.textContent = innerBtn.textContent;
                        btn.id = pkg + "-" + innerBtn.textContent;
                        btn.onclick = function () {
                            markDone(btn);
                        }

                        // 恢復完成狀態
                        const btnIdentifier = pkg + "-" + innerBtn.textContent;
                        if (doneItems.includes('dynamic-' + btnIdentifier) || doneItems.includes(
                                btnIdentifier)) {
                            btn.classList.add('done');
                            if (!btn.textContent.includes('✅')) {
                                btn.textContent += ' ✅';
                            }
                        }

                        box.appendChild(btn);
                    }
                });
            });

            // 新增單項加做項目到第二頁
            document.querySelectorAll(".single-item.selected").forEach(singleBtn => {
                let btn = document.createElement("button");
                btn.className = "btn";
                btn.textContent = singleBtn.textContent;
                btn.id = "single-" + singleBtn.textContent;
                btn.onclick = function () {
                    markDone(btn);
                }

                // 恢復完成狀態
                const btnIdentifier = "single-" + singleBtn.textContent;
                if (doneItems.includes('dynamic-' + btnIdentifier) || doneItems.includes(btnIdentifier)) {
                    btn.classList.add('done');
                    if (!btn.textContent.includes('✅')) {
                        btn.textContent += ' ✅';
                    }
                }

                box.appendChild(btn);
            });

            // 新增贈送項目到第二頁
            if (selectedGift) {
                let giftBtn = document.getElementById(selectedGift);
                let btn = document.createElement("button");
                btn.className = "btn";
                btn.textContent = "🎁 " + giftBtn.textContent;
                btn.id = "gift-" + selectedGift;
                btn.onclick = function () {
                    markDone(btn);
                }

                // 恢復完成狀態
                const btnIdentifier = "gift-" + selectedGift;
                if (doneItems.includes('dynamic-' + btnIdentifier) || doneItems.includes(btnIdentifier)) {
                    btn.classList.add('done');
                    if (!btn.textContent.includes('✅')) {
                        btn.textContent += ' ✅';
                    }
                }

                box.appendChild(btn);
            }

            // 如果IGE被自動選擇
            const igeGift = document.getElementById('giftIGE');
            if (igeGift.classList.contains('auto-selected')) {
                let btn = document.createElement("button");
                btn.className = "btn";
                btn.textContent = "🎁 " + igeGift.textContent;
                btn.id = "gift-giftIGE";
                btn.onclick = function () {
                    markDone(btn);
                }

                // 恢復完成狀態
                const btnIdentifier = "gift-giftIGE";
                if (doneItems.includes('dynamic-' + btnIdentifier) || doneItems.includes(btnIdentifier)) {
                    btn.classList.add('done');
                    if (!btn.textContent.includes('✅')) {
                        btn.textContent += ' ✅';
                    }
                }

                box.appendChild(btn);
            }
        }

        function goBack() {
            let pw = prompt("請輸入驗證碼");
            if (pw && pw.toLowerCase() === "s2") {
                currentPage = 1;
                document.getElementById("page2").classList.add("hidden");
                document.getElementById("page1").classList.remove("hidden");
                updateURL();
            }
        }

        function markDone(button) {
            let input = prompt("輸入 'ok' 標示完成，'xx' 取消完成");
            if (!input) return;

            input = input.toLowerCase();
            if (input === "ok") {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) button.textContent += " ✅";
            } else if (input === "xx") {
                button.classList.remove("done");
                button.textContent = button.textContent.replace(" ✅", "");
            } else {
                alert("輸入錯誤，請重新操作！");
            }
            updateURL();
        }

        // 頁面載入時初始化
        window.onload = function () {
            initSignature();
            loadFromURL(); // 從URL恢復狀態
            updateStatusIndicator();
            updateTotal();
        }
    </script>

</body>
