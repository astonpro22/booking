<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Appointment Form</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1e1e1e;
      color: white;
      padding: 30px;
    }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin-top: 8px;
      margin-bottom: 15px;
      border-radius: 5px;
      border: none;
    }
    button {
      background: #5865F2;
      color: white;
      font-size: 16px;
      cursor: pointer;
    }
    button:hover {
      background: #4752c4;
    }
  </style>
</head>
<body>

  <h2>Appointment Request</h2>

  <label>Discord Username:</label>
  <input id="username" type="text" placeholder="User#1234" required>

  <label>Reason for Appointment:</label>
  <textarea id="reason" placeholder="Explain your reason..." required></textarea>

  <label>Date:</label>
  <input id="date" type="date" required>

  <label>Time:</label>
  <input id="time" type="time" required>

  <button onclick="sendToDiscord()">Submit</button>

  <script>
    function sendToDiscord() {
      const webhookURL = "https://discord.com/api/webhooks/1455764490023993567/1a4UOaW_V1Pqss12VolaLFUIHKF8aHVtr9CscnoXuQRtxjWaqy832q7KxSmhmNvGgd-0";

      const username = document.getElementById("username").value;
      const reason = document.getElementById("reason").value;
      const date = document.getElementById("date").value;
      const time = document.getElementById("time").value;

      if (!username || !reason || !date || !time) {
        alert("Please fill out all fields.");
        return;
      }

      fetch(webhookURL, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          username: "Appointment Bot",
          embeds: [{
            title: "📅 New Appointment Request",
            color: 5793266,
            fields: [
              { name: "Discord Username", value: username, inline: false },
              { name: "Reason", value: reason, inline: false },
              { name: "Date", value: date, inline: true },
              { name: "Time", value: time, inline: true }
            ],
            footer: {
              text: "Sent from HTML Form"
            }
          }]
        })
      })
      .then(() => alert("Appointment sent successfully!"))
      .catch(err => {
        console.error(err);
        alert("Failed to send.");
      });
    }
  </script>

</body>
</html>
