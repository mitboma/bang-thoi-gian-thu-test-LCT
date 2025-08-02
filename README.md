# bang-thoi-gian-thu-test-LCT
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Bảng thời gian đợt</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 40px;
    }
    input {
      padding: 5px;
      font-size: 16px;
    }
    button {
      padding: 5px 10px;
      font-size: 16px;
      margin-left: 10px;
    }
    pre {
      background: #f6f8fa;
      padding: 20px;
      border-radius: 5px;
      white-space: pre-wrap;
      font-family: monospace;
    }
  </style>
</head>
<body>

  <h2>Bảng thời gian các đợt</h2>
  <label>Thời gian bắt đầu đợt 1 (hh:mm):</label>
  <input type="time" id="startTime" value="07:45">
  <button onclick="generateTable()">Tạo bảng</button>

  <h3>Kết quả dạng markdown:</h3>
  <pre id="output"></pre>

  <script>
    function pad(num) {
      return num.toString().padStart(2, '0');
    }

    function generateTable() {
      const inputTime = document.getElementById("startTime").value;
      if (!inputTime) return;

      const [hourStr, minStr] = inputTime.split(":");
      let hour = parseInt(hourStr);
      let minute = parseInt(minStr);

      let result = "| Đợt | Start  | End    |\n";
      result += "|-----|--------|--------|\n";

      for (let i = 0; i <= 8; i++) {
        let wave = (1 + i * 0.5).toFixed(1);

        let startMinutes = hour * 60 + minute + i * 5;
        let endMinutes = startMinutes + 20;

        let startH = Math.floor(startMinutes / 60);
        let startM = startMinutes % 60;

        let endH = Math.floor(endMinutes / 60);
        let endM = endMinutes % 60;

        let startStr = `${pad(startH)}:${pad(startM)}`;
        let endStr = `${pad(endH)}:${pad(endM)}`;

        result += `| ${wave} | ${startStr}  | ${endStr}  |\n`;
      }

      document.getElementById("output").textContent = result;
    }
  </script>

</body>
</html>
