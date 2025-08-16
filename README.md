

<head>
    <meta charset="UTF-8">
    <title>健檢流程控制台</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 40px;
        }

        h2 {
            margin-bottom: 20px;
        }

        .hidden {
            display: none;
        }

        .station {
            display: inline-block;
            margin: 15px;
        }

        .btn {
            width: 140px;
            height: 120px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            background-color: lightgray;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn.done {
            background-color: lightgreen;
            color: white;
        }

        .option {
            display: inline-block;
            margin: 10px;
        }

        label {
            font-size: 18px;
            cursor: pointer;
        }

        #okBtn,
        #backBtn {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
        }
    </style>
</head>

<body>

    <!-- 第一頁：選擇 8 選 2 -->
    <div id="page1">
        <h2>請選擇 8 選 2 項目</h2>
        <div class="option">
            <label>
                <input type="checkbox" value="腹部超音波"> 腹部超音波</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="婦科超音波"> 婦科超音波</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="頸動脈超音波"> 頸動脈超音波</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="甲狀腺超音波"> 甲狀腺超音波</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="攝護腺超音波"> 攝護腺超音波</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="HRV"> HRV</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="眼底攝影"> 眼底攝影</label>
        </div>
        <div class="option">
            <label>
                <input type="checkbox" value="動脈硬化"> 動脈硬化</label>
        </div>
        <br>
        <br>
        <button id="okBtn" onclick="confirmSelection()">OK</button>
    </div>

    <!-- 第二頁：流程控制台 -->
    <div id="page2" class="hidden">
        <h2>健檢流程進度</h2>

        <!-- 特殊選的 2 個項目會在 JS 插入 -->
        <div id="special-items"></div>

        <!-- 原本流程 -->
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
        <!-- 返回選擇頁 -->
        <button id="backBtn" onclick="goBack()">返回選擇頁</button>

        <h3>請勿自行操作</h3>
    </div>

    <script>
        // 限制只能勾選 2 個
        const checkboxes = document.querySelectorAll('#page1 input[type="checkbox"]');
        checkboxes.forEach(cb => {
            cb.addEventListener("change", function () {
                const checked = document.querySelectorAll('#page1 input[type="checkbox"]:checked');
                if (checked.length >= 2) {
                    checkboxes.forEach(box => {
                        if (!box.checked) box.disabled = true;
                    });
                } else {
                    checkboxes.forEach(box => box.disabled = false);
                }
            });
        });

        // 確認選擇並切換到第二頁
        function confirmSelection() {
            const checked = Array.from(document.querySelectorAll('#page1 input[type="checkbox"]:checked'))
                .map(c => c.value);

            if (checked.length !== 2) {
                alert("請務必選擇 2 個項目！");
                return;
            }

            let password = prompt("請輸入驗證字串以確認");
            if (!password || password.toLowerCase() !== "s1") {
                alert("驗證錯誤，請重新操作！");
                return;
            }

            localStorage.setItem("selectedSpecialItems", JSON.stringify(checked));
            showPage2();
        }

        // 顯示第二頁內容
        function showPage2() {
            document.getElementById("page1").classList.add("hidden");
            document.getElementById("page2").classList.remove("hidden");

            const specialDiv = document.getElementById("special-items");
            specialDiv.innerHTML = "";

            const selected = JSON.parse(localStorage.getItem("selectedSpecialItems")) || [];
            selected.forEach((item, index) => {
                const id = "special" + index;
                const btn = document.createElement("button");
                btn.className = "btn";
                btn.id = id;
                btn.textContent = item;
                btn.onclick = function () {
                    markDone(btn);
                };

                const div = document.createElement("div");
                div.className = "station";
                div.appendChild(btn);
                specialDiv.appendChild(div);

                if (localStorage.getItem(id) === "done") {
                    btn.classList.add("done");
                    if (!btn.textContent.includes("✅")) btn.textContent += " ✅";
                }
            });

            ["heigh", "fat", "blood", "dr", "xray"].forEach(id => {
                let status = localStorage.getItem(id);
                if (status === "done") {
                    let btn = document.getElementById(id);
                    btn.classList.add("done");
                    if (!btn.textContent.includes("✅")) btn.textContent += " ✅";
                }
            });
        }

        // 按鈕完成邏輯
        function markDone(button) {
            let input = prompt("請由操作人員輸入完成驗證");
            if (!input) return;
            input = input.toLowerCase();
            if (input === "oo") {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) button.textContent += " ✅";
                localStorage.setItem(button.id, "done");
            } else if (input === "xx") {
                button.classList.remove("done");
                button.textContent = button.textContent.replace(" ✅", "");
                localStorage.removeItem(button.id);
            } else {
                alert("輸入錯誤，請重新操作！");
            }
        }

        // 返回選擇頁（保留進度）
        function goBack() {
            alert("請找諮詢人員處理");
            let pw = prompt("輸入驗證字串以返回");
            if (pw && pw.toLowerCase() === "s2") {
                localStorage.removeItem("selectedSpecialItems");

                // 取消勾選 + 解鎖
                checkboxes.forEach(cb => {
                    cb.checked = false;
                    cb.disabled = false;
                });

                document.getElementById("page2").classList.add("hidden");
                document.getElementById("page1").classList.remove("hidden");
            } else {
                alert("驗證錯誤，無法返回");
            }
        }

        window.onload = function () {
            const selected = JSON.parse(localStorage.getItem("selectedSpecialItems"));
            if (selected && selected.length === 2) {
                showPage2();
            }
        }
    </script>
</body>
