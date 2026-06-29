<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Lilyholic Chat</title>

  <!-- Firebase SDK (versión compatible con tu proyecto) -->
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

  <style>
    body {
      background: #111;
      color: #fff;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
    }

    h1 {
      text-align: center;
      margin-bottom: 10px;
    }

    #chat-container {
      width: 100%;
      max-width: 600px;
      margin: 0 auto;
      background: #222;
      padding: 20px;
      border-radius: 10px;
    }

    #messages {
      height: 300px;
      overflow-y: auto;
      background: #000;
      padding: 10px;
      border-radius: 5px;
      margin-bottom: 15px;
    }

    .msg {
      margin-bottom: 10px;
      padding: 8px;
      background: #333;
      border-radius: 5px;
    }

    #input-area {
      display: flex;
      gap: 10px;
    }

    input {
      flex: 1;
      padding: 10px;
      border-radius: 5px;
      border: none;
    }

    button {
      padding: 10px 15px;
      background: #4CAF50;
      border: none;
      border-radius: 5px;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background: #45a049;
    }
  </style>
</head>

<body>

  <h1>Bienvenidos a mi web</h1>
  <p style="text-align:center;">Aquí está mi chat funcionando con Firebase.</p>

  <div id="chat-container">
    <div id="messages"></div>

    <div id="input-area">
      <input type="text" id="messageInput" placeholder="Escribe un mensaje...">
      <button onclick="sendMessage()">Enviar</button>
    </div>
  </div>

  <script>
    const firebaseConfig = {
      apiKey: "AIzaSyBuruYnDWyG_7CDvs_nyfAD-iOkcaEwCaQ",
      authDomain: "lilyholic.firebaseapp.com",
      databaseURL: "https://lilyholic-default-rtdb.firebaseio.com",
      projectId: "lilyholic",
      storageBucket: "lilyholic.firebasestorage.app",
      messagingSenderId: "68491199560",
      appId: "1:68491199560:web:8dbf2ae48177e44d2f047d",
      measurementId: "G-384DPKGE8F"
    };

    firebase.initializeApp(firebaseConfig);
    const db = firebase.database();

    function sendMessage() {
      const input = document.getElementById("messageInput");
      const text = input.value.trim();
      if (text === "") return;

      db.ref("messages").push({ text });
      input.value = "";
    }

    function addMessageToScreen(text) {
      const messages = document.getElementById("messages");
      const div = document.createElement("div");
      div.className = "msg";
      div.textContent = text;
      messages.appendChild(div);
      messages.scrollTop = messages.scrollHeight;
    }

    db.ref("messages").on("child_added", snapshot => {
      addMessageToScreen(snapshot.val().text);
    });
  </script>

</body>
</html>
