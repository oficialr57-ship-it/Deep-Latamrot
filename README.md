# Deep-Latamrot
Pagina de Latamrots
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Deep Latamrot System</title>

<style>
body{
    margin:0;
    font-family:Arial, Helvetica, sans-serif;
    background:#0a0a0a;
    color:#00ffcc;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    background:#111;
    padding:40px;
    border-radius:15px;
    box-shadow:0 0 25px #00ffcc;
    width:350px;
    text-align:center;
}

input{
    width:100%;
    padding:10px;
    margin:10px 0;
    background:#000;
    border:2px solid #00ffcc;
    color:#00ffcc;
    border-radius:8px;
    outline:none;
}

button{
    padding:10px 20px;
    background:#00ffcc;
    border:none;
    border-radius:8px;
    cursor:pointer;
    font-weight:bold;
    transition:0.3s;
}

button:hover{
    background:#00ffaa;
    box-shadow:0 0 15px #00ffcc;
}

.hidden{
    display:none;
}

h1{
    text-shadow:0 0 10px #00ffcc;
}
</style>
</head>
<body>

<div class="container" id="registerBox">
    <h1>Deep Latamrot</h1>
    <p>Ingresa tu Nombre de Usuario</p>
    <input type="text" id="username" maxlength="15" placeholder="Max 15 caracteres">
    <button onclick="register()">Continuar</button>
</div>

<div class="container hidden" id="verifyBox">
    <h1>Verificación</h1>
    <input type="text" id="verifyUser" placeholder="Repite tu usuario">
    <input type="text" id="accessCode" placeholder="Access Code">
    <button onclick="verify()">Continuar</button>
</div>

<div class="container hidden" id="mainPage">
    <h1 id="welcomeText"></h1>
    <hr>
    <p><strong>System Information</strong></p>
    <p id="userInfo"></p>
    <p id="dateInfo"></p>
    <p>Status : Normal</p>
    <hr>
    <p>—————-</p>
    <p>Proximamente más.</p>
</div>

<script>
function register(){
    const username = document.getElementById("username").value.trim();

    if(username === ""){
        alert("Debes ingresar un nombre.");
        return;
    }

    localStorage.setItem("tempUser", username);
    document.getElementById("registerBox").classList.add("hidden");
    document.getElementById("verifyBox").classList.remove("hidden");
}

function verify(){
    const verifyUser = document.getElementById("verifyUser").value.trim();
    const accessCode = document.getElementById("accessCode").value.trim();
    const savedUser = localStorage.getItem("tempUser");

    if(verifyUser !== savedUser){
        alert("El usuario no coincide.");
        return;
    }

    if(accessCode !== "Latam"){
        alert("Access Code incorrecto.");
        return;
    }

    const date = new Date().toLocaleString();
    localStorage.setItem("registeredUser", savedUser);
    localStorage.setItem("registerDate", date);
    localStorage.removeItem("tempUser");

    loadMain();
}

function loadMain(){
    const user = localStorage.getItem("registeredUser");
    const date = localStorage.getItem("registerDate");

    if(!user){
        return;
    }

    document.getElementById("registerBox").classList.add("hidden");
    document.getElementById("verifyBox").classList.add("hidden");
    document.getElementById("mainPage").classList.remove("hidden");

    document.getElementById("welcomeText").innerText = "Welcome, " + user;
    document.getElementById("userInfo").innerText = "User : " + user;
    document.getElementById("dateInfo").innerText = "Inicio de sesión : " + date;
}

window.onload = function(){
    const user = localStorage.getItem("registeredUser");

    if(user){
        document.getElementById("registerBox").classList.add("hidden");
        document.getElementById("verifyBox").classList.remove("hidden");
        document.getElementById("verifyUser").value = user;
    }
}
</script>

</body>
</html>
