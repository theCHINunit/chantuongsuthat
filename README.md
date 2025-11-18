# chantuongsuthat
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bạn đã biết được sự thật chưa</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-image: url('Tosca Modern Creative Web Development Presentation.png');
      background-size: cover;
      background-repeat: no-repeat;
      background-position: center;
      color: white;
      text-align: center;
      padding-top: 100px;
    }
    .container {
      background-color: rgba(0, 0, 0, 0.6);
      margin: 0 auto;
      padding: 30px;
      border-radius: 20px;
      width: 80%;
      max-width: 600px;
    }
    input, button {
      padding: 10px;
      margin: 10px;
      border-radius: 10px;
      border: none;
      font-size: 16px;
    }
    button {
      background-color: crimson;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background-color: darkred;
    }
    .hidden {
      display: none;
    }
    p.msg {
      font-weight: bold;
      margin-top: 8px;
      color: #ffdd57;
    }
    p.msg.wrong { color: #ff6b6b; }
    p.msg.ok { color: #9be564; }
    label { display: block; text-align: left; margin-left: 20%; }
    p.note { font-size: 14px; color: #ffd966; margin-bottom: 10px; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Bạn đã biết được sự thật chưa</h1>
    <p class="lead">Hãy trả lời từng mục theo thứ tự.</p>

    <!-- Mục 1 -->
    <div id="muc1">
      <h2>Mục 1: Điền tên hung thủ</h2>
      <input type="text" id="hungThu" placeholder="Nhập tên...">
      <button onclick="kiemTraHungThu()">Xác nhận</button>
      <p id="ketQua1" class="msg"></p>
    </div>

    <!-- Mục 2 -->
    <div id="muc2" class="hidden">
      <h2>Mục 2: Tình tiết giúp bạn tìm ra sự thật</h2>
      <p class="note">Bạn có thể chọn nhiều hơn 1 đáp án đúng.</p>
      <form id="formTinhTiet">
        <label><input type="checkbox" value="1"> Lời khai của bà Hân</label>
        <label><input type="checkbox" value="2"> Chiết xuất camera</label>
        <label><input type="checkbox" value="3"> Lời khai của Mạnh</label>
        <label><input type="checkbox" value="4"> Lời khai của bà Lan</label>
        <label><input type="checkbox" value="5"> Khám nghiệm tử thi</label>
        <label><input type="checkbox" value="6"> Lời khai của ông Hải</label>
        <label><input type="checkbox" value="7"> Lời khai của ông Nhân</label>
        <label><input type="checkbox" value="8"> Lời khai của ông Công</label>
        <label><input type="checkbox" value="9"> Vật chứng</label>
      </form>
      <button onclick="kiemTraTinhTiet()">Xác nhận</button>
      <p id="ketQua2" class="msg"></p>
    </div>

    <!-- Mục 3 -->
    <div id="muc3" class="hidden">
      <h2>Mục 3: Chân tướng</h2>
      <a href="https://docs.google.com/document/d/1r9ZSYgqvA0Fp_bFw47HmLhms1p3VuiYxmTSjKdEk-Es/edit?hl=vi&tab=t.0" target="_blank">Xem sự thật tại đây</a>
    </div>
  </div>

  <script>
    function normalizeVietnamese(str){
      if(!str) return '';
      try{ str = str.normalize('NFD'); }catch(e){}
      str = str.replace(/\p{M}/gu, '');
      str = str.replace(/[^\p{L}\p{N}\s]/gu, '');
      str = str.replace(/\s+/g, ' ').trim().toLowerCase();
      return str;
    }

    function isValidName(input){
      const s = normalizeVietnamese(input);
      const variants = ['nguyen dinh hai','dinh hai','hai'];
      return variants.some(v => s.includes(v));
    }

    function kiemTraHungThu() {
      const input = document.getElementById('hungThu').value;
      const ketQua1 = document.getElementById('ketQua1');

      if(isValidName(input)){
        ketQua1.textContent = 'Đúng rồi!';
        ketQua1.className = 'msg ok';
        document.getElementById('muc2').classList.remove('hidden');
      } else {
        ketQua1.textContent = 'Ôi có lẽ bạn đã phán đoán sai rồi';
        ketQua1.className = 'msg wrong';
        document.getElementById('muc2').classList.add('hidden');
        document.getElementById('muc3').classList.add('hidden');
        document.getElementById('ketQua2').textContent = '';
      }
    }

    function arraysEqual(a, b){
      if(a.length !== b.length) return false;
      const sa = a.slice().sort();
      const sb = b.slice().sort();
      return sa.every((v,i) => v === sb[i]);
    }

    function kiemTraTinhTiet(){
      const checked = Array.from(document.querySelectorAll('#formTinhTiet input:checked')).map(cb => cb.value);
      const ketQua2 = document.getElementById('ketQua2');
      const correct = ['1','2']; // Lời khai của bà Hân và Chiết xuất camera

      if(arraysEqual(checked, correct)){
        ketQua2.textContent = 'Đúng rồi!';
        ketQua2.className = 'msg ok';
        document.getElementById('muc3').classList.remove('hidden');
      } else {
        ketQua2.textContent = 'Ôi có lẽ bạn đã phán đoán sai rồi';
        ketQua2.className = 'msg wrong';
        document.getElementById('muc3').classList.add('hidden');
      }
    }
  </script>
</body>
</html>
