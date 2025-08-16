
<head>
    <meta charset="UTF-8">
    <title>健檢流程控制台</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }

        .station {
            display: inline-block;
            margin: 15px;
        }

        .btn {
            width: 120px;
            height: 120px;
            font-size: 18px;
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
    </style>
</head>

<body>

    <h2>健檢關卡進度</h2>

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

    <script>
        // 預設的關卡 ID 清單
        const stations = ["blood", "fat", "xray", "exam", "dr", "heigh"];

        // 載入時讀取 localStorage 狀態
        window.onload = function () {
            stations.forEach(id => {
                let status = localStorage.getItem(id);
                if (status === "done") {
                    let btn = document.getElementById(id);
                    btn.classList.add("done");
                    if (!btn.textContent.includes("✅")) {
                        btn.textContent += " ✅";
                    }
                }
            });
        };

        // 按下按鈕時的邏輯
        function markDone(button) {
            let input = prompt("請由操作人員輸入完成驗證");
            if (input && (input.toLowerCase() === "done" || input === "完成")) {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) {
                    button.textContent += " ✅";
                }
                localStorage.setItem(button.id, "done"); // 記錄狀態
            } else {
                alert("輸入錯誤，請重新操作！");
            }
        }
        // 按下按鈕時的邏輯
        function markDone(button) {
            let input = prompt("請由操作人員輸入完成驗證");
            if (!input) return;
            input = input.toLowerCase();
            if (input === "done" || input === "完成") {
                button.classList.add("done");
                if (!button.textContent.includes("✅")) {
                    button.textContent += " ✅";
                }
                localStorage.setItem(button.id, "done"); // 記錄狀態 
            } else if (input === "reset") {
                button.classList.remove("done");
                button.textContent = button.textContent.replace(" ✅", "");
                localStorage.removeItem(button.id); // 移除狀態 
            } else {
                alert("輸入錯誤，請重新操作！");
            }
        }
    </script>
    <h3>勿自行操作</h3>
</body>

</html>
