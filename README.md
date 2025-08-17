<!DOCTYPE html>
<html lang="zh-Hant">

<head>
    <meta charset="UTF-8">
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
            border: 1px solid #000;
            width: 300px;
            height: 150px;
            margin: 10px auto;
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
    </style>
</head>

<body>

    <div id="page1">
        <h2>加選項目 (8選2)</h2>
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
                <button class="btn" id="opt6" onclick="toggleOption(this)">HRV</button>
            </div>
            <div class="option">
                <button class="btn" id="opt7" onclick="toggleOption(this)">眼底攝影</button>
            </div>
            <div class="option">
                <button class="btn" id="opt8" onclick="toggleOption(this)">動脈硬化</button>
            </div>
        </div>

        <div style="margin-top:20px;">
            <button class="btn" onclick="toggleAddons()">加做項目 / 簽名 / 長截圖</button>
        </div>

        <div id="addons" class="hidden">
            <h3>加做項目套餐</h3>
            <div id="top-packages" class="package-section">
                <!-- A套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgA" onclick="togglePackage('A')">A套餐</button>
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
                    <button class="btn" id="pkgB" onclick="togglePackage('B')">B套餐</button>
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
                    <button class="btn" id="pkgC" onclick="togglePackage('C')">C套餐</button>
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
                    <button class="btn" id="pkgD" onclick="togglePackage('D')">D套餐(男)</button>
                    <div class="package-items" id="itemsD">
                        <button data-price="800" class="pkg-item" data-pkg="D" id="pkgD1">鼻咽癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="D" id="pkgD2">鱗狀上皮細胞癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="D" id="pkgD3">肺腺癌 800元</button>
                        <button data-price="700" class="pkg-item" data-pkg="D" id="pkgD4">肺癌 700元</button>
                    </div>
                </div>
                <!-- E套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgE" onclick="togglePackage('E')">E套餐(女)</button>
                    <div class="package-items" id="itemsE">
                        <button data-price="800" class="pkg-item" data-pkg="E" id="pkgE1">鱗狀上皮細胞癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="E" id="pkgE2">肺腺癌 800元</button>
                        <button data-price="800" class="pkg-item" data-pkg="E" id="pkgE3">卵巢癌 800元</button>
                        <button data-price="700" class="pkg-item" data-pkg="E" id="pkgE4">肺癌 700元</button>
                    </div>
                </div>
                <!-- F套餐 -->
                <div class="package-box">
                    <button class="btn" id="pkgF" onclick="togglePackage('F')">F套餐</button>
                    <div class="package-items" id="itemsF">
                        <button data-price="900" class="pkg-item" data-pkg="F" id="pkgF1">腎上腺皮質素 900元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF2">睪固酮(男) 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF3">雌二醇(女) 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF4">黃體生成激素 600元</button>
                        <button data-price="600" class="pkg-item" data-pkg="F" id="pkgF5">濾泡刺激素 600元</button>
                    </div>
                </div>
            </div>

            <div id="total">總金額: 0 元</div>
            <canvas id="signature"></canvas>
            <br>
            <button class="btn" onclick="alert('長截圖功能尚未完成')">長截圖</button>
            <br>
            <br>
        </div>

        <button class="btn" onclick="confirmPage1()">OK</button>
    </div>

    <div id="page2" class="hidden">
        <h2>健檢關卡進度</h2>
        <div id="selectedOptions"></div>
        <div class="station">
            <button class="btn" id="heigh" onclick="markDone(this)">身高</button>
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
        <br>
        <button class="btn" onclick="goBack()">返回</button>
    </div>

    <script>
        let selected = [];
        let packageTotals = {
            A: 0,
            B: 0,
            C: 0,
            D: 0,
            E: 0,
            F: 0
        };

        function toggleOption(btn) {
            if (btn.classList.contains("selected")) {
                btn.classList.remove("selected");
                selected = selected.filter(x => x !== btn.textContent);
                localStorage.removeItem(btn.id);
            } else {
                if (selected.length >= 2) {
                    alert("最多選2個");
                    return;
                }
                btn.classList.add("selected");
                selected.push(btn.textContent);
                localStorage.setItem(btn.id, "selected");
            }
        }

        function toggleAddons() {
            document.getElementById("addons").classList.toggle("hidden");
        }

        function togglePackage(pkg) {
            let btn = document.getElementById("pkg" + pkg);
            const packagePrice = {
                A: 3000,
                B: 2200,
                C: 2500,
                D: 2000,
                E: 2000,
                F: 2000
            };
            if (pkg === "D") {
                document.getElementById("pkgE").classList.remove("selected");
                packageTotals["E"] = 0;
                localStorage.removeItem("pkgE");
            }
            if (pkg === "E") {
                document.getElementById("pkgD").classList.remove("selected");
                packageTotals["D"] = 0;
                localStorage.removeItem("pkgD");
            }
            btn.classList.toggle("selected");
            packageTotals[pkg] = btn.classList.contains("selected") ? packagePrice[pkg] : 0;
            if (btn.classList.contains("selected")) localStorage.setItem("pkg" + pkg, "selected");
            else localStorage.removeItem("pkg" + pkg);
            document.querySelectorAll("#items" + pkg + " .pkg-item").forEach(innerBtn => {
                if (btn.classList.contains("selected")) innerBtn.classList.add("selected");
                else innerBtn.classList.remove("selected");
            });
            updateTotal();
        }

        // 內部按鈕
        document.querySelectorAll(".pkg-item").forEach(btn => {
            btn.addEventListener("click", function () {
                let pkg = btn.dataset.pkg;
                if (!document.getElementById("pkg" + pkg).classList.contains("selected")) {
                    btn.classList.toggle("selected");
                    if (btn.classList.contains("selected")) localStorage.setItem(btn.id, "selected");
                    else localStorage.removeItem(btn.id);
                    updateTotal();
                }
            });
        });

        function updateTotal() {
            let sum = 0;
            for (let k in packageTotals) sum += packageTotals[k];
            document.querySelectorAll(".pkg-item.selected").forEach(btn => {
                let pkg = btn.dataset.pkg;
                if (!document.getElementById("pkg" + pkg).classList.contains("selected")) {
                    sum += parseInt(btn.dataset.price);
                }
            });
            document.getElementById("total").textContent = "總金額: " + sum + " 元";
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
            document.getElementById("page1").classList.add("hidden");
            document.getElementById("page2").classList.remove("hidden");
            localStorage.setItem("currentPage", "page2");
            renderSelectedOptions();
        }

        function renderSelectedOptions() {
            let box = document.getElementById("selectedOptions");
            box.innerHTML = "";
            selected.forEach(name => {
                let btn = document.createElement("button");
                btn.className = "btn";
                btn.textContent = name;
                btn.id = name;
                btn.onclick = function () {
                    markDone(btn);
                }
                box.appendChild(btn);
            });
            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                if (document.getElementById("pkg" + pkg).classList.contains("selected")) {
                    document.querySelectorAll("#items" + pkg + " .pkg-item").forEach(innerBtn => {
                        let btn = document.createElement("button");
                        btn.className = "btn";
                        btn.textContent = innerBtn.textContent;
                        btn.id = pkg + "-" + innerBtn.textContent;
                        btn.onclick = function () {
                            markDone(btn);
                        }
                        box.appendChild(btn);
                    });
                } else {
                    document.querySelectorAll("#items" + pkg + " .pkg-item.selected").forEach(innerBtn => {
                        let btn = document.createElement("button");
                        btn.className = "btn";
                        btn.textContent = innerBtn.textContent;
                        btn.id = pkg + "-" + innerBtn.textContent;
                        btn.onclick = function () {
                            markDone(btn);
                        }
                        box.appendChild(btn);
                    });
                }
            });
            document.querySelectorAll("#selectedOptions button").forEach(btn => {
                if (localStorage.getItem(btn.id) === "done") {
                    btn.classList.add("done");
                    if (!btn.textContent.includes("✅")) btn.textContent += " ✅";
                }
            });
        }

        function goBack() {
            let pw = prompt("請輸入驗證碼");
            if (pw && pw.toLowerCase() === "s2") {
                document.getElementById("page2").classList.add("hidden");
                document.getElementById("page1").classList.remove("hidden");
                localStorage.setItem("currentPage", "page1");
            }
        }

        function markDone(button) {
            let input = prompt("輸入 'ok' 標示完成，'xx' 取消完成");
            if (!input) return;
            input = input.toLowerCase();
            if (input === "ok") {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) button.textContent += " ✅";
                localStorage.setItem(button.id, "done");
            } else if (input === "xx") {
                button.classList.remove("done");
                button.textContent = button.textContent.replace(" ✅", "");
                localStorage.removeItem(button.id);
            } else alert("輸入錯誤，請重新操作！");
        }

        window.onload = function () {
            selected = [];
            for (let i = 1; i <= 8; i++) {
                let btn = document.getElementById("opt" + i);
                if (localStorage.getItem(btn.id) === "selected" && selected.length < 2) {
                    btn.classList.add("selected");
                    selected.push(btn.textContent);
                } else {
                    btn.classList.remove("selected");
                    localStorage.removeItem(btn.id);
                }
            }
            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                if (localStorage.getItem("pkg" + pkg) === "selected") togglePackage(pkg);
            });
            document.querySelectorAll(".pkg-item").forEach(btn => {
                if (localStorage.getItem(btn.id) === "selected") btn.classList.add("selected");
            });
            document.querySelectorAll(".station .btn").forEach(btn => {
                if (localStorage.getItem(btn.id) === "done") {
                    btn.classList.add("done");
                    if (!btn.textContent.includes("✅")) btn.textContent += " ✅";
                }
            });
            renderSelectedOptions();
            const currentPage = localStorage.getItem("currentPage") || "page1";
            document.getElementById("page1").classList.toggle("hidden", currentPage === "page2");
            document.getElementById("page2").classList.toggle("hidden", currentPage === "page1");
            updateTotal();
        };
    </script>

</body>

</html>
