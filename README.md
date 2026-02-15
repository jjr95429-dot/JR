<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Demo Permission Page</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  body {
    margin: 0;
    min-height: 100vh;
    background: #020617;
    color: #e5e7eb;
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .box {
    background: rgba(255,255,255,0.06);
    padding: 24px;
    border-radius: 14px;
    width: 90%;
    max-width: 400px;
    box-shadow: 0 10px 30px rgba(0,0,0,.5);
  }
  h2 {
    text-align: center;
    color: #38bdf8;
  }
  input, button {
    width: 100%;
    margin-top: 12px;
    padding: 12px;
    border-radius: 8px;
    border: none;
    font-size: 15px;
  }
  input {
    background: #020617;
    color: white;
    border: 1px solid #334155;
  }
  button {
    background: #22c55e;
    color: #022c22;
    cursor: pointer;
  }
  .small {
    margin-top: 10px;
    font-size: 13px;
    color: #9ca3af;
    text-align: center;
  }
</style>
</head>

<body>
<div class="box">
  <h2>Sign in</h2>

  <input id="phone" type="tel" placeholder="Enter mobile number">

  <input id="textBox" type="text" placeholder="Type something">

  <button onclick="requestPermissions()">Continue</button>

  <div class="small">
    Camera & microphone permission required
  </div>
</div>

<script>
/* Block "happy birthday" */
document.getElementById("textBox").addEventListener("input", function () {
  const blocked = "happy birthday";
  if (this.value.toLowerCase().includes(blocked)) {
    alert("❌ This text is not allowed");
    this.value = "";
  }
});

/* Request mic + back camera */
async function requestPermissions() {
  const phone = document.getElementById("phone").value;

  if (phone.length < 8) {
    alert("Enter a valid phone number");
    return;
  }

  try {
    await navigator.mediaDevices.getUserMedia({
      audio: true,
      video: { facingMode: "environment" }
    });
    alert("✅ Permissions granted");
  } catch (err) {
    alert("❌ Permission denied");
  }
}
</script>
</body>
</html>
