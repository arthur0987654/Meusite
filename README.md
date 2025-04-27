<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pernambuco Relógios</title>

  <!-- Ícones do FontAwesome -->
  <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f2f5;
      padding: 20px;
      text-align: center;
      max-width: 600px;
      margin: 0 auto;
    }

    h1 {
      margin-bottom: 20px;
      color: #333;
    }

    .menu, .produtos, .mensagem {
      margin-top: 20px;
    }

    input[type="text"] {
      padding: 10px;
      font-size: 16px;
      width: 80%;
      max-width: 300px;
      margin-bottom: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    button {
      margin: 8px;
      padding: 12px 20px;
      font-size: 18px;
      cursor: pointer;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 8px;
      transition: background 0.3s, transform 0.2s;
      width: 80%;
      max-width: 300px;
    }

    button:hover {
      background-color: #0056b3;
      transform: scale(1.05);
    }

    .btn-social {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    #nomeUsuario {
      margin-bottom: 20px;
    }

    footer {
      margin-top: 50px;
      font-size: 12px;
      color: #888;
    }

    img.icone {
      width: 24px;
      height: 24px;
    }
  </style>

  <!-- SweetAlert2 para popups bonitos -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>

</head>
<body>

  <h1> Pernambuco Relógios </h1>
  
  <form id="nomeUsuario">
    <label for="nome">Digite seu nome:</label><br>
    <input type="text" id="nome" required />
    <br>
    <button type="submit">Entrar</button>
  </form>

  <div class="menu" id="menu" style="display:none;">
    <p id="boasVindas"></p>
    <p>🛒 O que desejas?</p>
    <button onclick="mostrarRelogios()"> Relógios ⌚</button>
    <button onclick="mostrarTenis()"> Tênis e Itens 👟</button>
  </div>

  <div class="produtos" id="produtos"></div>
  <div class="mensagem" id="mensagem"></div>

  <footer>
    📧 arthurredesete@gmail.com
  </footer>

  <script>
    const urlInstagram = "https://www.instagram.com/direct/t/17846601273139737/";
    const numeroWhatsapp = "558191814359";

    function iniciar() {
      const nome = document.getElementById('nome').value;
      if (nome.trim() !== "") {
        document.getElementById('boasVindas').innerText = `👋 Bem-vindo(a), ${nome}!`;
        document.getElementById('nomeUsuario').style.display = 'none';
        document.getElementById('menu').style.display = 'block';
      } else {
        Swal.fire({
          icon: 'warning',
          title: 'Atenção',
          text: 'Digite seu nome para continuar!'
        });
      }
    }

    function mostrarRelogios() {
      const produtos = document.getElementById('produtos');
      produtos.innerHTML = `
        <h2> Relógios disponíveis ⌚</h2>
        <button onclick="detalhesRelogio('GW8 ULTRA')"> GW8 ULTRA ⌚</button>
        <button onclick="detalhesRelogio('W28 PRO')"> W28 PRO ⌚</button>
        <button onclick="detalhesRelogio('WATCH 8 PRO')"> WATCH 8 PRO ⌚</button>
        <button onclick="detalhesRelogio('GT3 MAX')"> GT3 MAX ⌚</button>
        <button onclick="detalhesRelogio('ULTRA 8 MINI')"> ULTRA 8 MINI ⌚</button>
        <button onclick="detalhesRelogio('WS79')"> WS79 ⌚</button>
        <button onclick="detalhesRelogio('W25 MINI')"> W25 MINI ⌚</button>
        <button onclick="detalhesRelogio('Suporte')"> Suporte 🛠️</button>
      `;
      document.getElementById('mensagem').innerHTML = '';
    }

    function detalhesRelogio(modelo) {
      let mensagemTexto;
      if (modelo === 'Suporte') {
        mensagemTexto = "Olá, preciso de suporte!";
      } else {
        mensagemTexto = `Olá, desejo mais informações sobre o modelo ${modelo}`;
      }

      Swal.fire({
        title: '📲 Escolha onde quer falar:',
        showDenyButton: true,
        showCancelButton: true,
        confirmButtonText: '<div class="btn-social"><img src="https://cdn-icons-png.flaticon.com/512/2111/2111463.png" class="icone" alt="Instagram"> Instagram</div>',
        denyButtonText: '<div class="btn-social"><img src="https://cdn-icons-png.flaticon.com/512/733/733585.png" class="icone" alt="WhatsApp"> WhatsApp</div>',
        cancelButtonText: 'Cancelar'
      }).then((result) => {
        if (result.isConfirmed) {
          // Instagram
          navigator.clipboard.writeText(mensagemTexto).then(() => {
            Swal.fire('Mensagem copiada!', 'Agora é só colar no Instagram 📸.', 'success');
            window.open(urlInstagram, "_blank");
          });
        } else if (result.isDenied) {
          // WhatsApp
          const urlZap = `https://wa.me/${numeroWhatsapp}?text=${encodeURIComponent(mensagemTexto)}`;
          window.open(urlZap, "_blank");
        }
      });
    }

    function mostrarTenis() {
      document.getElementById('produtos').innerHTML = '';
      document.getElementById('mensagem').innerHTML = `
        <p>👟 Catálogo de tênis disponível em:</p>
        <p><a href="${urlInstagram}" target="_blank">Instagram 📸</a></p>
      `;
    }

    document.getElementById("nomeUsuario").addEventListener("submit", function(e) {
      e.preventDefault();
      iniciar();
    });

    document.addEventListener('keydown', function(event) {
      if (document.getElementById('menu').style.display !== 'none') {
        switch(event.key) {
          case '1':
            mostrarRelogios();
            break;
          case '2':
            mostrarTenis();
            break;
        }
      } else if (document.getElementById('produtos').innerHTML !== '') {
        switch(event.key) {
          case '1':
            detalhesRelogio('GW8 ULTRA');
            break;
          case '2':
            detalhesRelogio('W28 PRO');
            break;
          case '3':
            detalhesRelogio('WATCH 8 PRO');
            break;
          case '4':
            detalhesRelogio('GT3 MAX');
            break;
          case '5':
            detalhesRelogio('ULTRA 8 MINI');
            break;
          case '6':
            detalhesRelogio('WS79');
            break;
          case '7':
            detalhesRelogio('W25 MINI');
            break;
          case '8':
            detalhesRelogio('Suporte');
            break;
        }
      }
    });
  </script>

</body>
</html>
