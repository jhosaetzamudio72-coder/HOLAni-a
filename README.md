<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Sorpresa Especial</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      font-family: Arial, sans-serif;
      color: white;
      text-align: center;
    }

    .pantalla {
      display: none;
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      background-image: url('hellokittyfondo.png');
      background-size: cover;
      background-position: center;
    }

    .activa {
      display: flex;
    }

    .mensaje {
      font-size: 22px;
      font-weight: bold;
      margin-bottom: 20px;
      text-shadow: 2px 2px 4px black;
      background: rgba(0,0,0,0.4);
      padding: 10px;
      border-radius: 10px;
    }

    .boton {
      padding: 12px 24px;
      background: #ff99cc;
      border: none;
      border-radius: 15px;
      cursor: pointer;
      font-size: 18px;
      font-weight: bold;
      color: white;
      box-shadow: 2px 2px 6px rgba(0,0,0,0.3);
    }

    .imagen-central {
      width: 250px;
      margin: 20px auto;
    }

    /* 🔹 Imágenes flotantes */
    .flotante {
      position: absolute;
      width: 90px;
      animation: flotar 8s linear infinite;
      cursor: pointer;
    }

    @keyframes flotar {
      from { transform: translateY(100vh) rotate(0deg); opacity: 1; }
      to   { transform: translateY(-120vh) rotate(360deg); opacity: 0.9; }
    }

    /* 🔹 Overlay para mensaje hermoso */
    #overlay {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.85);
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 1000;
    }

    #overlayMensaje {
      color: white;
      font-size: 26px;
      font-weight: bold;
      padding: 20px;
      border-radius: 15px;
      background: rgba(255, 153, 204, 0.8);
      box-shadow: 0 0 15px white;
      max-width: 80%;
      text-align: center;
    }

    #cerrar {
      margin-top: 20px;
      padding: 10px 20px;
      background: #ff3366;
      border: none;
      border-radius: 15px;
      color: white;
      font-size: 20px;
      cursor: pointer;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <!-- Pantalla 1 -->
  <div id="pantalla1" class="pantalla activa">
    <div class="mensaje">😉 Hola, niña: TE REGALO ESTE RAMO VIRTUAL CON TO MI CORAZONCITO 🫶🏻🤍.<br>
      Espero estés bien y quiero dejarte este último mensaje....</div>
    <img src="ilustracion-de-oso-lindo-en-estilo-de-arte-digital.png" alt="Oso tierno" class="imagen-central">
    <button class="boton" onclick="mostrarPantalla(2)">APRIETA SI ME QUIERES 💕</button>
  </div>

  <!-- Pantalla 2 -->
  <div id="pantalla2" class="pantalla">
    <div class="mensaje">😉 ERES TO' PARA MI , DISCULPA SI AMARME ES UN DOLOR DE CABEZA O PURO PROBLEMAS 🫤🫶🏻 <br>
      ❤️‍🩹 TE AMO MUCHO NO LO OLVIDES.</div>
    <img src="adorable-ilustracion-de-oso-en-estilo-de-arte-digital.png" alt="Oso romántico" class="imagen-central">
    <button class="boton" onclick="mostrarPantalla(3)">APRIETA SI ME QUIERES 💕</button>
  </div>

  <!-- Pantalla 3 -->
  <div id="pantalla3" class="pantalla">
    <div class="mensaje">
      💖 COMO QUISIERA VOLVER ESTAR CONTIGO PERO....................... 💖 <br><br>
      Hazle click a todas las imágenes que puedas.
    </div>
    <div id="imagenesExtra"></div>
  </div>

  <!-- Overlay con mensaje hermoso -->
  <div id="overlay">
    <div id="overlayMensaje">✨ Eres la razón más bonita por la que creo en el amor ✨</div>
    <button id="cerrar" onclick="cerrarOverlay()">Cerrar</button>
  </div>

  <script>
    // 🔹 Frases personalizadas (15)
    const frases = [
      "💯 Quiero que demos el 100% en esta relación, sin guardarnos nada.",
      "❌ Aquí no existen mentiras, solo la verdad que nos une.",
      "🤝 Quiero que no haya amistades que pongan en duda lo nuestro.",
      "🚫 Que no existan planes ocultos que traigan inseguridades.",
      "💔 Los ex son pasado, nosotros somos el presente y el futuro.",
      "💖 Prefiero la transparencia antes que cualquier mentira.",
      "🛡️ Dame la seguridad de que soy tu único camino.",
      "🌹 No quiero sombras, solo claridad en nuestro amor.",
      "🔥 Que no exista nadie que pueda romper lo que construimos.",
      "🫂 Si vamos a estar juntos, que sea con toda la confianza del mundo.",
      "✨ Sin engaños, sin juegos, solo un amor verdadero.",
      "📖 Que nuestra historia no tenga capítulos oscuros, solo sinceridad.",
      "🔒 Eres mía y yo soy tuyo, sin terceros que interfieran.",
      "🌙 Lo que quiero es simple: amor sincero, sin inseguridades.",
      "❤️ Estar contigo significa construir sin miedo, sin dudas, solo amor."
    ];

    function mostrarPantalla(num) {
      document.querySelectorAll('.pantalla').forEach(p => p.classList.remove('activa'));
      document.getElementById('pantalla' + num).classList.add('activa');

      if (num === 3) generarImagenesExtra();
    }

    function crearFlotante(src) {
      const img = document.createElement("img");
      img.src = src;
      img.className = "flotante";
      img.style.left = Math.random() * window.innerWidth + "px";
      img.style.animationDuration = (6 + Math.random() * 4) + "s";
      img.onclick = () => abrirOverlay(); // clic muestra mensaje hermoso
      document.body.appendChild(img);
      setTimeout(() => img.remove(), 10000);
    }

    function generarImagenesExtra() {
      let imagenes = [
        "HELLOKITTY1.png","HELLOKITTY2.png","HELLOKITTY3.png","HELLOKITTY4.png",
        "HELLOKITTY5.png","AMOR1.png","AMOR2.png","AMOR3.png","AMOR5.png",
        "AMOR6.png","AMOR7.png","AMOR8.png"
      ];
      setInterval(() => {
        let img = imagenes[Math.floor(Math.random() * imagenes.length)];
        crearFlotante(img);
      }, 500);
    }

    function abrirOverlay() {
      // Escoge una frase aleatoria
      const frase = frases[Math.floor(Math.random() * frases.length)];
      document.getElementById("overlayMensaje").innerText = frase;
      document.getElementById("overlay").style.display = "flex";
    }

    function cerrarOverlay() {
      document.getElementById("overlay").style.display = "none";
    }
  </script>

</body>
</html>
