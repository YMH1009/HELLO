
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

        /* A套餐二選一項目特殊樣式 */

        .package-items button.exclusive-option {
            border: 2px solid #FF6B35;
            position: relative;
        }

        .package-items button.exclusive-option.selected {
            background-color: #FF6B35;
            color: white;
            border-color: #FF6B35;
        }

        .package-items button.exclusive-option:not(.selected) {
            background-color: #FFE5D9;
            color: #FF6B35;
        }

        /* 全局互斥項目樣式（9選2中的頸動脈超音波與眼底攝影） */

        .btn.exclusive-global {
            border: 2px solid #9C27B0;
            position: relative;
        }

        .btn.exclusive-global.selected {
            background-color: #9C27B0;
            color: white;
            border-color: #9C27B0;
        }

        .btn.exclusive-global:not(.selected) {
            background-color: #F3E5F5;
            color: #9C27B0;
        }

        /* 贈品中的頸動脈超音波特殊樣式 */

        .gift-item#giftCarotid {
            border-color: #9C27B0;
        }

        .gift-item#giftCarotid.selected {
            background-color: #9C27B0;
            border-color: #7B1FA2;
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

        .additional-items {
            border: 2px solid #FF8C00;
            border-radius: 15px;
            padding: 20px;
            margin: 20px auto;
            max-width: 900px;
            background: linear-gradient(135deg, #FFF8DC, #FFFACD);
            box-shadow: 0 4px 15px rgba(255, 140, 0, 0.2);
        }

        .additional-items h3 {
            color: #FF6600;
            margin-bottom: 15px;
            font-size: 18px;
            text-align: center;
            border-bottom: 2px solid #FF8C00;
            padding-bottom: 8px;
        }

        .basic-checkup {
            border: 2px solid #4682B4;
            border-radius: 15px;
            padding: 20px;
            margin: 20px auto;
            max-width: 900px;
            background: linear-gradient(135deg, #E6F3FF, #F0F8FF);
            box-shadow: 0 4px 15px rgba(70, 130, 180, 0.2);
        }

        .basic-checkup h3 {
            color: #4682B4;
            margin-bottom: 15px;
            font-size: 18px;
            text-align: center;
            border-bottom: 2px solid #4682B4;
            padding-bottom: 8px;
        }

        .selected-options {
            border: 2px solid #32CD32;
            border-radius: 15px;
            padding: 20px;
            margin: 20px auto;
            max-width: 900px;
            background: linear-gradient(135deg, #F0FFF0, #F5FFFA);
            box-shadow: 0 4px 15px rgba(50, 205, 50, 0.2);
        }

        .selected-options h3 {
            color: #228B22;
            margin-bottom: 15px;
            font-size: 18px;
            text-align: center;
            border-bottom: 2px solid #32CD32;
            padding-bottom: 8px;
        }

        /* A套餐提示區域 */

        .exclusive-hint {
            background: #FFF3E0;
            border: 1px solid #FF9800;
            border-radius: 5px;
            padding: 8px;
            margin: 10px 0;
            font-size: 12px;
            color: #E65100;
        }
    </style>
</head>

<body>
    <div class="status-indicator" id="statusIndicator">已選擇: 0/2</div>

    <div id="page1">
        <h2>公費項目 (9選2)</h2>

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
                <button class="btn" id="opt9" onclick="toggleOption(this)">ABI</button>
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
                        <button data-price="1200" class="pkg-item exclusive-option" data-pkg="A" data-single="true" id="pkgA5">頸動脈超音波 1200元</button>
                        <button data-price="1200" class="pkg-item exclusive-option" data-pkg="A" data-single="true" id="pkgA6">眼底攝影 1200元</button>
                    </div>
                    <div class="exclusive-hint">
                        💡 頸動脈超音波與眼底攝影二選一
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
                        <button data-price="500" class="pkg-item" data-pkg="C" id="pkgC1">解脂酶 500元</button>
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

        <!-- 9選2的基本項目區塊 -->
        <div class="selected-options">
            <h3>🔹 公費項目 (9選2)</h3>
            <div id="selectedOptions"></div>
        </div>

        <!-- 基本檢查關卡區塊 (移到上方) -->
        <div class="basic-checkup">
            <h3>🏥 基本檢查關卡</h3>
            <div class="station">
                <button class="btn" id="height" onclick="markDone(this)">身高</button>
            </div>
            <div class="station">
                <button class="btn" id="weightFat" onclick="markDone(this)">體重體脂</button>
            </div>
            <div class="station">
                <button class="btn" id="boneDensity" onclick="markDone(this)">骨質密度</button>
            </div>
            <div class="station">
                <button class="btn" id="waistHearing" onclick="markDone(this)">腰圍聽力</button>
            </div>
            <div class="station">
                <button class="btn" id="vision" onclick="markDone(this)">視力</button>
            </div>
            <div class="station">
                <button class="btn" id="eyePressure" onclick="markDone(this)">眼壓</button>
            </div>
            <div class="station">
                <button class="btn" id="bloodPressure" onclick="markDone(this)">血壓</button>
            </div>
            <div class="station">
                <button class="btn" id="blood" onclick="markDone(this)">抽血</button>
            </div>
            <div class="station">
                <button class="btn" id="ecg" onclick="markDone(this)">心電圖</button>
            </div>
            <div class="station">
                <button class="btn" id="doctor" onclick="markDone(this)">醫師</button>
            </div>
            <div class="station">
                <button class="btn" id="urine" onclick="markDone(this)">尿液</button>
            </div>
            <div class="station">
                <button class="btn" id="xray" onclick="markDone(this)">X光</button>
            </div>
        </div>

        <!-- 加做項目區塊 (移到下方) -->
        <div class="additional-items">
            <h3>🔸 加做項目</h3>
            <div id="additionalItems"></div>
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

        // 需要在第二頁顯示的項目列表
        const allowedItems = [
            '頸動脈超音波',
            '眼底攝影',
            'C13',
            'HRV',
            '腹部超音波',
            '甲狀腺超音波',
            '攝護腺超音波',
            '乳房超音波',
            '婦科超音波',
            'E66',
            'E110'
        ];

        // 移除文字中的價格部分，只保留名稱
        function extractItemName(text) {
            // 移除價格（如 " 900元", " 1200元"等）
            return text.replace(/\s+\d+元$/, '').trim();
        }

        // 檢查項目是否在允許列表中
        function isAllowedItem(itemText) {
            const itemName = extractItemName(itemText);
            return allowedItems.includes(itemName);
        }

        // 處理A套餐中頸動脈超音波與眼底攝影的互斥邏輯
        function handlePackageAExclusive(clickedBtn) {
            const pkgA5 = document.getElementById("pkgA5"); // 頸動脈超音波
            const pkgA6 = document.getElementById("pkgA6"); // 眼底攝影

            if (clickedBtn.id === "pkgA5") {
                // 點擊頸動脈超音波
                pkgA5.classList.add("selected");
                pkgA6.classList.remove("selected");
            } else if (clickedBtn.id === "pkgA6") {
                // 點擊眼底攝影
                pkgA6.classList.add("selected");
                pkgA5.classList.remove("selected");
            }
        }

        // 處理非套餐中頸動脈超音波與眼底攝影的全局互斥邏輯
        function handleCarotidEyeExclusive() {
            // 檢查所有可能的頸動脈超音波和眼底攝影選項
            const carotidOptions = [{
                    id: 'opt3',
                    text: '頸動脈超音波'
                }, // 9選2中的選項
                {
                    id: 'pkgA5',
                    text: '頸動脈超音波'
                }, // A套餐中的選項
                {
                    id: 'giftCarotid',
                    text: '頸動脈超音波'
                } // 贈品中的選項
            ];

            const eyeOptions = [{
                    id: 'opt8',
                    text: '眼底攝影'
                }, // 9選2中的選項
                {
                    id: 'pkgA6',
                    text: '眼底攝影'
                }, // A套餐中的選項
                {
                    id: 'giftEye',
                    text: '眼底攝影'
                } // 贈品中的選項（如果有的話）
            ];

            let selectedCarotid = null;
            let selectedEye = null;

            // 找出目前選中的頸動脈超音波和眼底攝影
            carotidOptions.forEach(option => {
                const btn = document.getElementById(option.id);
                if (btn && btn.classList.contains('selected')) {
                    selectedCarotid = option;
                }
            });

            eyeOptions.forEach(option => {
                const btn = document.getElementById(option.id);
                if (btn && btn.classList.contains('selected')) {
                    selectedEye = option;
                }
            });

            // 如果同時選中了頸動脈超音波和眼底攝影，則保留最後選擇的那個
            if (selectedCarotid && selectedEye) {
                // 這裡需要知道最後點擊的是哪個，由調用方決定
                return {
                    carotidOptions,
                    eyeOptions,
                    selectedCarotid,
                    selectedEye
                };
            }

            return null;
        }

        // 取消頸動脈超音波的所有選擇
        function clearAllCarotidSelections() {
            const carotidSelectors = ['#opt3', '#pkgA5', '#giftCarotid'];
            carotidSelectors.forEach(selector => {
                const btn = document.querySelector(selector);
                if (btn && btn.classList.contains('selected')) {
                    btn.classList.remove('selected');

                    // 特別處理9選2的選項
                    if (selector === '#opt3') {
                        selected = selected.filter(x => x !== '頸動脈超音波');
                        delete selectedButtons['opt3'];
                    }

                    // 特別處理贈品選擇
                    if (selector === '#giftCarotid' && selectedGift === 'giftCarotid') {
                        selectedGift = null;
                    }
                }
            });
        }

        // 取消眼底攝影的所有選擇
        function clearAllEyeSelections() {
            const eyeSelectors = ['#opt8', '#pkgA6'];
            eyeSelectors.forEach(selector => {
                const btn = document.querySelector(selector);
                if (btn && btn.classList.contains('selected')) {
                    btn.classList.remove('selected');

                    // 特別處理9選2的選項
                    if (selector === '#opt8') {
                        selected = selected.filter(x => x !== '眼底攝影');
                        delete selectedButtons['opt8'];
                    }
                }
            });
        }

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

                        // A套餐特殊處理：確保頸動脈超音波與眼底攝影的互斥狀態
                        if (pkg === 'A') {
                            // 先設定所有A套餐項目為選中
                            document.querySelectorAll("#itemsA .pkg-item").forEach(innerBtn => {
                                innerBtn.classList.add("selected");
                            });
                            // 然後根據URL參數決定頸動脈超音波與眼底攝影的狀態
                            // 預設選擇頸動脈超音波
                            const pkgItems = params.get('pkgItems');
                            if (pkgItems && pkgItems.includes('pkgA6')) {
                                // 如果URL中有眼底攝影，則選眼底攝影
                                document.getElementById("pkgA5").classList.remove("selected");
                                document.getElementById("pkgA6").classList.add("selected");
                            } else {
                                // 否則預設選頸動脈超音波
                                document.getElementById("pkgA5").classList.add("selected");
                                document.getElementById("pkgA6").classList.remove("selected");
                            }
                        }
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

            const isCarotid = btn.textContent.includes('頸動脈超音波');

            // 處理頸動脈超音波贈品的互斥邏輯
            if (isCarotid) {
                clearAllEyeSelections(); // 取消所有眼底攝影選擇
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
            const isCarotid = btn.textContent.includes('頸動脈超音波');
            const isEye = btn.textContent.includes('眼底攝影');

            if (btn.classList.contains("selected")) {
                btn.classList.remove("selected");
                selected = selected.filter(x => x !== btn.textContent);
                delete selectedButtons[btn.id];
            } else {
                if (selected.length >= 2) {
                    alert("最多選2個");
                    return;
                }

                // 處理頸動脈超音波與眼底攝影的互斥邏輯
                if (isCarotid) {
                    clearAllEyeSelections(); // 取消所有眼底攝影選擇
                } else if (isEye) {
                    clearAllCarotidSelections(); // 取消所有頸動脈超音波選擇
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

                    // A套餐特殊處理：預設選擇頸動脈超音波，取消眼底攝影
                    if (pkg === "A") {
                        if (innerBtn.id === "pkgA5") { // 頸動脈超音波
                            innerBtn.classList.add("selected");
                        } else if (innerBtn.id === "pkgA6") { // 眼底攝影
                            innerBtn.classList.remove("selected");
                        }
                    }
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
                const isCarotid = btn.textContent.includes('頸動脈超音波');
                const isEye = btn.textContent.includes('眼底攝影');

                if (!document.getElementById("pkg" + pkg).classList.contains("selected")) {
                    // D和E套餐內部項目互斥邏輯 - 無論是否已選中，都要清除對方套餐
                    if (pkg === "D") {
                        clearPackage("E");
                    }
                    if (pkg === "E") {
                        clearPackage("D");
                    }

                    // 處理非套餐狀態下的頸動脈超音波與眼底攝影互斥
                    if (isCarotid) {
                        clearAllEyeSelections(); // 取消所有眼底攝影選擇
                    } else if (isEye) {
                        clearAllCarotidSelections(); // 取消所有頸動脈超音波選擇
                    }

                    btn.classList.toggle("selected");
                    updateTotal();
                    updateURL();
                } else {
                    // A套餐特殊處理：頸動脈超音波與眼底攝影二選一
                    if (pkg === "A" && (btn.id === "pkgA5" || btn.id === "pkgA6")) {
                        handlePackageAExclusive(btn);
                        updateTotal();
                        updateURL();
                        return;
                    }

                    // 其他套餐項目的正常切換邏輯
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
            let pwd = prompt("請由諮詢人員輸入驗證碼");
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
            let selectedBox = document.getElementById("selectedOptions");
            let additionalBox = document.getElementById("additionalItems");
            selectedBox.innerHTML = "";
            additionalBox.innerHTML = "";

            // 獲取當前完成狀態以便恢復
            const params = new URLSearchParams(window.location.search);
            const doneItems = params.get('done') ? params.get('done').split(',') : [];

            // 只渲染9選2的基本項目到selectedOptions
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

                selectedBox.appendChild(btn);
            });

            // 檢查是否有加做項目需要顯示
            let hasAdditionalItems = false;

            // 套餐項目放入additionalItems（只有允許的項目）
            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                document.querySelectorAll("#items" + pkg + " .pkg-item").forEach(innerBtn => {
                    if (innerBtn.classList.contains("selected")) {
                        const itemText = innerBtn.textContent;
                        // 只有在允許列表中的項目才會顯示在第二頁
                        if (isAllowedItem(itemText)) {
                            hasAdditionalItems = true;
                            let btn = document.createElement("button");
                            btn.className = "btn";
                            btn.textContent = extractItemName(itemText); // 移除價格，只顯示名稱
                            btn.id = pkg + "-" + extractItemName(itemText);
                            btn.onclick = function () {
                                markDone(btn);
                            }

                            // 恢復完成狀態
                            const btnIdentifier = pkg + "-" + extractItemName(itemText);
                            if (doneItems.includes('dynamic-' + btnIdentifier) || doneItems.includes(
                                    btnIdentifier)) {
                                btn.classList.add('done');
                                if (!btn.textContent.includes('✅')) {
                                    btn.textContent += ' ✅';
                                }
                            }

                            additionalBox.appendChild(btn);
                        }
                    }
                });
            });

            // 單項加做項目放入additionalItems（只有允許的項目）
            document.querySelectorAll(".single-item.selected").forEach(singleBtn => {
                const itemText = singleBtn.textContent;
                // 只有在允許列表中的項目才會顯示在第二頁
                if (isAllowedItem(itemText)) {
                    hasAdditionalItems = true;
                    let btn = document.createElement("button");
                    btn.className = "btn";
                    btn.textContent = extractItemName(itemText); // 移除價格，只顯示名稱
                    btn.id = "single-" + extractItemName(itemText);
                    btn.onclick = function () {
                        markDone(btn);
                    }

                    // 恢復完成狀態
                    const btnIdentifier = "single-" + extractItemName(itemText);
                    if (doneItems.includes('dynamic-' + btnIdentifier) || doneItems.includes(btnIdentifier)) {
                        btn.classList.add('done');
                        if (!btn.textContent.includes('✅')) {
                            btn.textContent += ' ✅';
                        }
                    }

                    additionalBox.appendChild(btn);
                }
            });

            // 贈送項目放入additionalItems（只有允許的項目）
            if (selectedGift) {
                let giftBtn = document.getElementById(selectedGift);
                const giftText = giftBtn.textContent;
                // 只有在允許列表中的項目才會顯示在第二頁
                if (isAllowedItem(giftText)) {
                    hasAdditionalItems = true;
                    let btn = document.createElement("button");
                    btn.className = "btn";
                    btn.textContent = "🎁 " + extractItemName(giftText); // 移除價格，只顯示名稱
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

                    additionalBox.appendChild(btn);
                }
            }

            // IGE贈品放入additionalItems（IGE不在允許列表中，所以不會顯示）
            const igeGift = document.getElementById('giftIGE');
            if (igeGift.classList.contains('auto-selected')) {
                const igeText = igeGift.textContent;
                // IGE不在允許列表中，所以不會顯示在第二頁
                if (isAllowedItem(igeText)) {
                    hasAdditionalItems = true;
                    let btn = document.createElement("button");
                    btn.className = "btn";
                    btn.textContent = "🎁 " + extractItemName(igeText);
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

                    additionalBox.appendChild(btn);
                }
            }

            // 如果沒有加做項目，隱藏加做項目區塊
            const additionalBlock = document.querySelector('.additional-items');
            if (!hasAdditionalItems) {
                additionalBlock.style.display = 'none';
            } else {
                additionalBlock.style.display = 'block';
            }
        }

        function goBack() {
            let pw = prompt("請由諮詢人員輸入驗證碼");
            if (pw && pw.toLowerCase() === "s2") {
                currentPage = 1;
                document.getElementById("page2").classList.add("hidden");
                document.getElementById("page1").classList.remove("hidden");
                updateURL();
            }
        }

        function markDone(button) {
            let input = prompt("請由操作人員確認");
            if (!input) return;

            input = input.toLowerCase();
            if (input === "v") {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) button.textContent += " ✅";
            } else if (input === "x") {
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

