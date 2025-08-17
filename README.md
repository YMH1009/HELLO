
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

        .package-items label {
            display: block;
            text-align: left;
            margin: 2px 0;
        }

        .price-label {
            font-size: 12px;
            color: #555;
            margin-left: 5px;
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
                <button class="btn" onclick="toggleOption(this)">腹部超音波</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">婦科超音波</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">頸動脈超音波</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">甲狀腺超音波</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">攝護腺超音波</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">HRV</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">眼底攝影</button>
            </div>
            <div class="option">
                <button class="btn" onclick="toggleOption(this)">動脈硬化</button>
            </div>
        </div>

        <div style="margin-top:20px;">
            <button class="btn" onclick="toggleAddons()">加做項目 / 簽名 / 長截圖</button>
        </div>

        <div id="addons" class="hidden">
            <h3>加做項目套餐</h3>
            <div id="top-packages" class="package-section">
                <div class="package-box">
                    <button class="btn" id="pkgA" onclick="togglePackage('A')">A套餐</button>
                    <div class="package-items" id="itemsA">
                        <label>
                            <input type="checkbox" data-price="900" class="manual">同半胱胺酸
                            <span class="price-label">900元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="900" class="manual">高敏感C反應蛋白
                            <span class="price-label">900元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">心肌旋轉蛋白
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="1600" class="manual">B型利納肽前驅物
                            <span class="price-label">1600元</span>
                        </label>
                        <label>
                            <input type="checkbox" name="Aselect" data-price="1200" class="manual">頸動脈超音波
                            <span class="price-label">1200元</span>
                        </label>
                        <label>
                            <input type="checkbox" name="Aselect" data-price="1200" class="manual">眼底攝影
                            <span class="price-label">1200元</span>
                        </label>
                    </div>
                </div>
                <div class="package-box">
                    <button class="btn" id="pkgB" onclick="togglePackage('B')">B套餐</button>
                    <div class="package-items" id="itemsB">
                        <label>
                            <input type="checkbox" data-price="900" class="manual">甲狀腺功能
                            <span class="price-label">900元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">自體免疫疾病檢查
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="500" class="manual">電解質檢查
                            <span class="price-label">500元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="600" class="manual">B肝抗原抗體
                            <span class="price-label">600元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="600" class="manual">C肝檢查
                            <span class="price-label">600元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">胰島素
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">維生素D
                            <span class="price-label">800元</span>
                        </label>
                    </div>
                </div>
                <div class="package-box">
                    <button class="btn" id="pkgC" onclick="togglePackage('C')">C套餐</button>
                    <div class="package-items" id="itemsC">
                        <label>
                            <input type="checkbox" data-price="500" class="manual">解肢酶
                            <span class="price-label">500元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">胃癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="700" class="manual">胰臟癌
                            <span class="price-label">700元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="1200" class="manual">C13
                            <span class="price-label">1200元</span>
                        </label>
                    </div>
                </div>
            </div>

            <div id="bottom-packages" class="package-section">
                <div class="package-box">
                    <button class="btn" id="pkgD" onclick="togglePackage('D')">D套餐(男)</button>
                    <div class="package-items" id="itemsD">
                        <label>
                            <input type="checkbox" data-price="800" class="manual">鼻咽癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">鱗狀上皮細胞癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">肺腺癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="700" class="manual">肺癌
                            <span class="price-label">700元</span>
                        </label>
                    </div>
                </div>
                <div class="package-box">
                    <button class="btn" id="pkgE" onclick="togglePackage('E')">E套餐(女)</button>
                    <div class="package-items" id="itemsE">
                        <label>
                            <input type="checkbox" data-price="800" class="manual">鱗狀上皮細胞癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">肺腺癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="800" class="manual">卵巢癌
                            <span class="price-label">800元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="700" class="manual">肺癌
                            <span class="price-label">700元</span>
                        </label>
                    </div>
                </div>
                <div class="package-box">
                    <button class="btn" id="pkgF" onclick="togglePackage('F')">F套餐</button>
                    <div class="package-items" id="itemsF">
                        <label>
                            <input type="checkbox" data-price="900" class="manual">腎上腺皮質素
                            <span class="price-label">900元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="600" class="manual">睪固酮(男)
                            <span class="price-label">600元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="600" class="manual">雌二醇(女)
                            <span class="price-label">600元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="600" class="manual">黃體生成激素
                            <span class="price-label">600元</span>
                        </label>
                        <label>
                            <input type="checkbox" data-price="600" class="manual">濾泡刺激素
                            <span class="price-label">600元</span>
                        </label>
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
            } else {
                if (selected.length >= 2) {
                    alert("最多選2個");
                    return;
                }
                btn.classList.add("selected");
                selected.push(btn.textContent);
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
            }
            if (pkg === "E") {
                document.getElementById("pkgD").classList.remove("selected");
                packageTotals["D"] = 0;
            }

            btn.classList.toggle("selected");
            packageTotals[pkg] = btn.classList.contains("selected") ? packagePrice[pkg] : 0;

            let inputs = document.querySelectorAll("#items" + pkg + " input");
            if (pkg === "A" && btn.classList.contains("selected")) {
                let twoOptions = document.querySelectorAll("#itemsA input[name='Aselect']");
                twoOptions.forEach(x => x.checked = false);
                let randIndex = Math.floor(Math.random() * twoOptions.length);
                twoOptions[randIndex].checked = true;
                inputs.forEach(inp => {
                    if (inp.name !== "Aselect") inp.checked = true;
                });
            } else {
                inputs.forEach(inp => inp.checked = btn.classList.contains("selected"));
            }

            updateTotal();
        }

        document.querySelectorAll("#itemsA input[name='Aselect']").forEach(r => {
            r.addEventListener("click", function () {
                if (this.checked) {
                    if (this.dataset.waschecked === "true") {
                        this.checked = false;
                        this.dataset.waschecked = "false";
                    } else {
                        document.querySelectorAll("#itemsA input[name='Aselect']").forEach(x => {
                            x.checked = false;
                            x.dataset.waschecked = "false";
                        });
                        this.checked = true;
                        this.dataset.waschecked = "true";
                    }
                } else this.dataset.waschecked = "false";
                updateTotal();
            });
        });

        document.querySelectorAll(".manual").forEach(input => {
            input.addEventListener("change", updateTotal);
        });

        function updateTotal() {
            let sum = 0;
            for (let key in packageTotals) sum += packageTotals[key];
            document.querySelectorAll(".manual:checked").forEach(inp => {
                if (!inp.closest(".package-box").querySelector("button").classList.contains("selected"))
                    sum += parseInt(inp.dataset.price);
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
                };
                box.appendChild(btn);
            });

            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                if (document.getElementById("pkg" + pkg).classList.contains("selected")) {
                    document.getElementById("items" + pkg).querySelectorAll("input").forEach(inp => {
                        let btn = document.createElement("button");
                        btn.className = "btn";
                        btn.textContent = inp.parentNode.textContent.replace(/\d+元$/, "");
                        btn.id = pkg + "-" + inp.parentNode.textContent;
                        btn.onclick = function () {
                            markDone(btn);
                        };
                        box.appendChild(btn);
                    });
                }
            });

            // 回存 localStorage 已做狀態
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
            }
        }

        function markDone(button) {
            let input = prompt("輸入 'ook' 標示完成，'xx' 取消完成");
            if (!input) return;
            input = input.toLowerCase();
            if (input === "ook") {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) button.textContent += " ✅";
                localStorage.setItem(button.id, "done");
            } else if (input === "xx") {
                button.classList.remove("done");
                button.textContent = button.textContent.replace(" ✅", "");
                localStorage.removeItem(button.id);
            } else alert("輸入錯誤，請重新操作！");
        }

        // 預載 localStorage 狀態
        window.onload = function () {
            ["heigh", "fat", "blood", "dr", "xray"].forEach(id => {
                let status = localStorage.getItem(id);
                if (status === "done") {
                    let btn = document.getElementById(id);
                    btn.classList.add("done");
                    if (!btn.textContent.includes("✅")) btn.textContent += " ✅";
                }
            });

            // 恢復先前選的加選項目按鈕
            document.querySelectorAll("#options .btn").forEach(btn => {
                if (localStorage.getItem("option-" + btn.textContent) === "selected") {
                    btn.classList.add("selected");
                    selected.push(btn.textContent);
                }
            });

            // 恢復套餐選擇
            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                if (localStorage.getItem("pkg-" + pkg) === "selected") {
                    document.getElementById("pkg" + pkg).classList.add("selected");
                    togglePackage(pkg); // 重新計算總金額
                }
            });
            updateTotal();
        }

        // 保存選項到 localStorage
        window.addEventListener("beforeunload", () => {
            document.querySelectorAll("#options .btn").forEach(btn => {
                localStorage.setItem("option-" + btn.textContent, btn.classList.contains("selected") ?
                    "selected" : "");
            });
            ["A", "B", "C", "D", "E", "F"].forEach(pkg => {
                localStorage.setItem("pkg-" + pkg, document.getElementById("pkg" + pkg).classList.contains(
                    "selected") ? "selected" : "");
            });
        });
    </script>
</body>
