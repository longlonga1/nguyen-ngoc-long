<!-- index.html -->
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Đăng nhập - TTVIP</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body { background: #0f172a; color: white; }
    .box { max-width: 400px; margin: 80px auto; }
    .card { background: #1e293b; border: none; }
    .form-control { background: #334155; color: white; }
  </style>
</head>
<body>

<div class="box text-center">
  <h3>Tăng Tương Tác VIP</h3>
  <div class="card p-4">
    <input id="user" class="form-control mb-2" placeholder="Tên đăng nhập">
    <input id="pass" type="password" class="form-control mb-2" placeholder="Mật khẩu">
    <button class="btn btn-primary w-100" onclick="login()">Đăng nhập</button>
  </div>

  <div class="card p-4 mt-3 d-none" id="otpBox">
    <p>Mã OTP: <b id="otpShow"></b></p>
    <input id="otpInput" class="form-control mb-2" placeholder="Nhập mã OTP">
    <button class="btn btn-warning w-100" onclick="verifyOTP()">Xác minh</button>
  </div>
</div>

<script>
  const users = {
    admin: { pass: "123456", role: "admin" },
    user: { pass: "abc123", role: "user" }
  };
  let currentUser = "", currentRole = "", otpCode = "";

  function login() {
    const u = user.value.trim(), p = pass.value;
    if (!users[u] || users[u].pass !== p) return alert("Sai thông tin!");
    currentUser = u;
    currentRole = users[u].role;
    otpCode = Math.floor(100000 + Math.random() * 900000);
    otpShow.textContent = otpCode;
    document.getElementById("otpBox").classList.remove("d-none");
  }

  function verifyOTP() {
    if (otpInput.value == otpCode) {
      localStorage.setItem("loggedUser", currentUser);
      localStorage.setItem("role", currentRole);
      window.location.href = currentRole === "admin" ? "admin.html" : "home.html";
    } else {
      alert("Sai OTP!");
    }
  }
</script>

</body>
</html>
