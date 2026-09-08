<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Payol Attendance</title>
</head>

<body>
  <h1>Payol Attendance</h1>
  <p>Employee Attendance System</p>

  <h2>Login</h2>

  <input id="employeeId" placeholder="Employee ID">
  <br><br>

  <input id="password" type="password" placeholder="Password">
  <br><br>

  <button onclick="login()">Login</button>

  <p id="message"></p>

  <script>
    const SUPABASE_URL = "https://nkbbcygtuaejcuquwhpi.supabase.co";
    const SUPABASE_KEY = "YAHAN_APNI_PUBLISHABLE_KEY_PASTE_KARO";

    async function login() {
      const employeeId = document.getElementById("employeeId").value.trim();
      const password = document.getElementById("password").value;

      if (!employeeId || !password) {
        document.getElementById("message").innerText =
          "Employee ID aur Password bhariye";
        return;
      }

      const response = await fetch(
        `${SUPABASE_URL}/rest/v1/employees?employee_id=eq.${encodeURIComponent(employeeId)}&password=eq.${encodeURIComponent(password)}&select=*`,
        {
          headers: {
            "apikey": SUPABASE_KEY,
            "Authorization": `Bearer ${SUPABASE_KEY}`
          }
        }
      );

      const data = await response.json();

      if (data.length > 0) {
        document.getElementById("message").innerText =
          "✅ Login Successful — " + data[0].name;
      } else {
        document.getElementById("message").innerText =
          "❌ Employee ID ya Password galat hai";
      }
    }
  </script>
</body>
</html>
