<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>...</title>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600&display=swap" rel="stylesheet">

<style>
body {
    margin: 0;
    background: #0a0a0a;
    color: #f5f5f5;
    font-family: 'Playfair Display', serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
    overflow: hidden;
}

.container {
    max-width: 90%;
}

.text {
    font-size: 26px;
    opacity: 0;
    transition: opacity 2s ease;
}

.name {
    font-size: 40px;
    letter-spacing: 12px;
    margin-top: 20px;
    opacity: 0;
}

.sub {
    font-size: 20px;
    margin-top: 10px;
    opacity: 0;
}

.final {
    font-size: 28px;
    margin-top: 20px;
    opacity: 0;
}

button {
    margin-top: 40px;
    padding: 10px 25px;
    background: transparent;
    border: 1px solid #888;
    color: #ccc;
    cursor: pointer;
    font-size: 16px;
    transition: 0.3s;
}

button:hover {
    color: white;
    border-color: white;
}
</style>
</head>

<body>

<div class="container">
    <div id="text" class="text"></div>
    <div id="name" class="name"></div>
    <div id="sub" class="sub"></div>
    <div id="final" class="final"></div>
    <button onclick="next()">Continuar</button>
</div>

<!-- Música -->
<audio id="music" autoplay loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_5f1c4f6f4c.mp3?filename=piano-moment-9835.mp3" type="audio/mpeg">
</audio>

<script>
const steps = [
"No era mi intención escribirte…",
"Pero tampoco podía quedarme callado.",
"No es para incomodarte.",
"Ni para pedirte nada.",
"Solo quería que supieras algo…"
];

let i = 0;

function showText(content) {
    const el = document.getElementById("text");
    el.style.opacity = 0;
    setTimeout(() => {
        el.innerText = content;
        el.style.opacity = 1;
    }, 500);
}

function typeName(name) {
    const el = document.getElementById("name");
    el.innerText = "";
    el.style.opacity = 1;
    let index = 0;

    let interval = setInterval(() => {
        el.innerText += name[index] + " ";
        index++;
        if(index >= name.length){
            clearInterval(interval);
            setTimeout(() => {
                document.getElementById("sub").innerText = "Leo…";
                document.getElementById("sub").style.opacity = 1;
            }, 800);
        }
    }, 300);
}

function showFinal() {
    document.getElementById("text").style.opacity = 0;
    document.getElementById("name").style.opacity = 0;
    document.getElementById("sub").style.opacity = 0;

    setTimeout(() => {
        const final = document.getElementById("final");
        final.innerHTML = "Tú eres una de ellas.<br><br>Te extraño.<br><br>Y siempre vas a ser mi gran amor.";
        final.style.opacity = 1;
        document.querySelector("button").style.display = "none";
    }, 1000);
}

function next() {
    if(i < steps.length){
        showText(steps[i]);
        i++;
    } 
    else if(i === steps.length){
        document.getElementById("text").style.opacity = 0;
        setTimeout(() => {
            typeName("ANNYE");
        }, 800);
        i++;
    } 
    else {
        showFinal();
    }
}

// iniciar
window.onload = () => {
    showText(steps[0]);
    i = 1;

    // activar audio (por restricciones móviles)
    document.body.addEventListener('click', () => {
        document.getElementById("music").play();
    });
};
</script>

</body>
</html>
