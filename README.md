<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M & J Store</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        @keyframes textAnimation {
            0% { color: azure; }
            50% { color: aqua; }
            100% { color: azure; }
        }

        body {
            background-color: black;
            color: azure;
            text-align: center;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .text {
            animation: textAnimation 4s infinite ease-in-out;
            font-size: 24px;
        }

        .textt {
            font-size: 50px;
        }

        .hidden {
            display: none;
        }
    </style>
</head>

<body>

    <div class="container text-center">
        <!-- A imagem agora está na pasta "images" -->
        <img src="images/img.jpeg" alt="Logo da M & J Store" width="300">
        <h1 class="text">Seja bem-vindo à M & J Store</h1>

        <div class="mt-3">
            <!-- O vídeo agora está na pasta "videos" -->
            <video id="video" src="videos/WhatsApp Video 2025-02-12 at 12.56.24.mp4" controls></video>

            <select id="produto" class="form-select w-auto bg-dark text-light border-light mt-3" onchange="mostrarBotao()">
                <option selected disabled>Escolha um produto</option>
                <option value="Desenho coreano">Desenho coreano</option>
                <option value="Desenho brasileiro">Desenho brasileiro</option>
                <option value="Base para cubo mágico">Base para cubo mágico</option>
                <option value="Personagem com chapéu do Roblox">Personagem com chapéu do Roblox</option>
                <option value="Mangás">Mangás</option>
            </select>

            <button id="enviarWhatsApp" class="btn btn-success mt-3 hidden" onclick="enviarParaWhatsApp()">Enviar via WhatsApp</button>
        </div>

        <form id="uploadForm" enctype="multipart/form-data" class="mt-3">
            <input type="file" id="imagem" name="imagem" accept="image/*" class="form-control w-auto d-inline">
            <button type="button" class="btn btn-primary" onclick="enviarImagem()">Enviar Imagem</button>
        </form>
    </div>

    <script>
        function mostrarBotao() {
            document.getElementById("enviarWhatsApp").classList.remove("hidden");
        }

        function enviarParaWhatsApp() {
            let produtoSelecionado = document.getElementById("produto").value;
            let numeroDono = "+55 11 96749-6068"; // Substitua pelo número do WhatsApp com código do país (ex: +55XXXXXXXXXXX)
            let mensagem = `Olá! Gostaria de comprar o seguinte produto: ${produtoSelecionado}`;
            let url = `https://web.whatsapp.com/${numeroDono}?text=${encodeURIComponent(mensagem)}`;
            window.open(url, "_blank");
        }

        function enviarImagem() {
            let formData = new FormData();
            let imagem = document.getElementById("imagem").files[0];
            formData.append("imagem", imagem);

            fetch("http://localhost:5000/upload", {
                method: "POST",
                body: formData
            })
            .then(response => response.text())
            .then(data => alert(data))
            .catch(error => console.error("Erro:", error));
        }
    </script>

</body>
</html>
