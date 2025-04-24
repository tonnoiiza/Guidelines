<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>สร้างแนวทางหวย</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    body {
      font-family: 'Sarabun', sans-serif;
      background: #111;
      color: #fff;
      text-align: center;
      padding: 20px;
    }

    input, select, textarea {
      padding: 8px;
      width: 300px;
      font-size: 16px;
      margin-top: 5px;
    }

    button {
      margin-top: 15px;
      padding: 10px 20px;
      font-size: 18px;
      background: #00c853;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      color: white;
    }

    #preview-container {
      position: relative;
      width: 600px;
      height: 600px;
      margin: 20px auto;
      border: 2px solid #fff;
      background-color: #000;
    }

    #preview-image {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .overlay {
      position: absolute;
      width: 100%;
      text-align: center;
      color: white;
      font-weight: bold;
      text-shadow: 2px 2px 5px #000;
    }

	#lottery-header {
	  top: 30px;
	  font-size: 35px;
	}

    #lottery-header span {
      display: inline-block;
      background: white;
      color: #1e3a8a;
      padding: 6px 12px;
      border-radius: 28px;
      text-decoration: line-through;
      font-weight: 900;
    }

	#lottery-date {
 	 top: 110px;
 	 font-size: 30px;
	}

	#lottery-content {
 	 position: absolute;
	  top: 55%;
	  left: 50%;
	  transform: translate(-50%, -50%); /* จัดกลางแนวตั้ง-แนวนอน */
	  font-size: 40px;
	  line-height: 1.9;
	  padding: 0 30px;
	  text-align: center;
	  white-space: pre-line;
	}
    
    #lottery-content {
	max-height: 580px;
	overflow: hidden;
	}
  </style>
</head>
<body>

  <h2>ระบบสร้างแนวทางหวย</h2>

  <div>
    <label>อัปโหลดพื้นหลัง: </label><br>
    <input type="file" accept="image/*" onchange="loadImage(event)">
  </div>

  <div>
    <label>วันที่:</label><br>
    <input type="date" id="dateInput" onchange="updatePreview()">
  </div>

  <div>
    <label>ประเภทหวย:</label><br>
    <select id="lotterySelect" onchange="updatePreview()">
      <option value="ดาวโจนส์">ดาวโจนส์</option>
      <option value="หวยลาว">หวยลาว</option>
      <option value="หวยฮานอย">หวยฮานอย</option>
      <option value="หวยรัฐบาล">หวยรัฐบาล</option>
    </select>
  </div>

  <div>
    <label>ข้อความแนวทาง:</label><br>
    <textarea id="textInput" rows="8" placeholder="พิมพ์ตัวเลขหรือข้อความ..." oninput="updatePreview()"></textarea>
  </div>

  <button onclick="saveImage()">บันทึกรูป</button>

  <div id="preview-container">
    <img id="preview-image" src="" alt="preview">
    <div class="overlay" id="lottery-header"><span id="lottery-type">ดาวโจนส์</span></div>
    <div class="overlay" id="lottery-date">วันที่ 23 เม.ย. 2568</div>
    <div class="overlay" id="lottery-content">รูด 3 / 0
30 35 32 34
05 02 04 52
305 302 352 052
เน้นเลขวิน 305247
อาจารย์หมาน นำโชค</div>
  </div>

  <script>
    function loadImage(event) {
      const reader = new FileReader();
      reader.onload = function () {
        document.getElementById('preview-image').src = reader.result;
      };
      reader.readAsDataURL(event.target.files[0]);
    }

    function updatePreview() {
      const type = document.getElementById('lotterySelect').value;
      const dateInput = document.getElementById('dateInput').value;
      const text = document.getElementById('textInput').value;

      const dateObj = new Date(dateInput);
      const thaiMonths = ["มกราคม", "กุมภาพันธ์", "มีนาคม", "เมษายน", "พฤษภาคม", "มิถุนายน",
                          "กรกฎาคม", "สิงคมหา", "กันยายน", "ตุลาคม", "พฤศจิกายน", "ธันวาคม"];
      const dateStr = dateInput
        ? `วันที่ ${dateObj.getDate()} ${thaiMonths[dateObj.getMonth()]} ${dateObj.getFullYear() + 543}`
        : '';

      document.getElementById('lottery-type').innerText = type;
      document.getElementById('lottery-date').innerText = dateStr;
      document.getElementById('lottery-content').innerText = text;
    }

    function saveImage() {
      html2canvas(document.getElementById("preview-container")).then(canvas => {
        const link = document.createElement('a');
        link.download = 'แนวทางหวย.png';
        link.href = canvas.toDataURL();
        link.click();
      });
    }
  </script>

</body>
</html>
