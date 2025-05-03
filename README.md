<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dublagem Automática</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0f172a;
      color: #fff;
      text-align: center;
      padding: 2rem;
    }
    h1 {
      color: #38bdf8;
      margin-bottom: 1rem;
    }
    p {
      margin-bottom: 2rem;
    }
    .upload-area {
      background: #1e293b;
      border: 2px dashed #38bdf8;
      padding: 2rem;
      border-radius: 1rem;
      max-width: 500px;
      margin: auto;
    }
    input[type="file"] {
      margin-top: 1rem;
    }
    button {
      background: #38bdf8;
      color: #0f172a;
      padding: 0.7rem 1.5rem;
      border: none;
      border-radius: 0.5rem;
      font-weight: bold;
      cursor: pointer;
      margin-top: 1rem;
    }
    button:hover {
      background: #0ea5e9;
    }
  </style>
</head>
<body>
  <h1>Dublagem Automática</h1>
  <p>Envie um vídeo curto e receba a versão dublada em português!</p>

  <div class="upload-area">
    <form action="/dublar" method="post" enctype="multipart/form-data">
      <label for="video">Escolha um vídeo (até 10 minutos):</label><br>
      <input type="file" name="video" id="video" accept="video/*" required><br>
      <button type="submit">Enviar e Dublar</button>
    </form>
  </div>
</body>
</html>
