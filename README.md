<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Company Checker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #e6f0ff;
      padding: 20px;
    }
    h1 {
      color: #0057b7;
      text-align: center;
    }
    .upload {
      margin-bottom: 20px;
      text-align: center;
    }
    .cliente {
      background-color: #ffffff;
      border-left: 5px solid #0057b7;
      padding: 15px;
      margin-bottom: 15px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .whatsapp-botao {
      background-color: #25D366;
      color: white;
      border: none;
      padding: 10px;
      border-radius: 5px;
      cursor: pointer;
    }
    .whatsapp-botao:hover {
      background-color: #1ebe5d;
    }
  </style>
</head>
<body>

  <h1>Company Checker</h1>

  <div class="upload">
    <input type="file" id="fileInput" accept=".csv" />
  </div>

  <div id="clientes"></div>

  <script>
    document.getElementById('fileInput').addEventListener('change', function(event) {
      const file = event.target.files[0];
      if (!file) return;

      const reader = new FileReader();
      reader.onload = function(e) {
        const lines = e.target.result.split('\n').slice(1);
        const container = document.getElementById('clientes');
        container.innerHTML = '';

        lines.forEach(line => {
          const [nome, telefone] = line.split(',');
          if (!nome || !telefone) return;

          const clienteDiv = document.createElement('div');
          clienteDiv.className = 'cliente';

          const info = document.createElement('div');
          info.innerHTML = <strong>${nome}</strong><br/>(${telefone});

          const link = document.createElement('a');
          link.href = https://wa.me/55${telefone.replace(/\D/g, '')};
          link.target = '_blank';

          const botao = document.createElement('button');
          botao.className = 'whatsapp-botao';
          botao.textContent = 'Conversar no WhatsApp';

          link.appendChild(botao);
          clienteDiv.appendChild(info);
          clienteDiv.appendChild(link);
          container.appendChild(clienteDiv);
        });
      };

      reader.readAsText(file);
    });
  </script>

</body>
</html>
