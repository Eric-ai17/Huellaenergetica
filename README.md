<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Huella energetica de la nube</title>
<style>
  :root{
    --verde:#1e6b3a; --verde-osc:#134a27; --verde-claro:#e8f5ec;
    --hoja:#43a047; --texto:#1f2d24; --gris:#5b6b60; --borde:#cfe3d5;
  }
  *{box-sizing:border-box}
  body{
    margin:0; font-family:system-ui,-apple-system,"Segoe UI",Roboto,Arial,sans-serif;
    color:var(--texto); background:linear-gradient(160deg,#eaf6ee 0%,#f7fbf8 45%,#e3f1f4 100%);
    min-height:100vh; padding:24px 16px;
  }
  .contenedor{max-width:820px; margin:0 auto}
  header{text-align:center; margin-bottom:20px}
  .icono{font-size:46px; line-height:1}
  h1{margin:8px 0 6px; color:var(--verde-osc); font-size:clamp(1.6rem,4vw,2.3rem)}
  .intro{color:var(--gris); max-width:620px; margin:0 auto; line-height:1.5}
  .tarjeta{
    background:#fff; border:1px solid var(--borde); border-radius:16px;
    padding:22px; box-shadow:0 6px 20px rgba(30,107,58,.08); margin-bottom:18px;
  }
  .tarjeta h2{margin:0 0 14px; font-size:1.1rem; color:var(--verde)}
  .grid{display:grid; grid-template-columns:repeat(2,1fr); gap:14px}
  @media (max-width:600px){ .grid{grid-template-columns:1fr} }
  label{display:block; font-weight:600; font-size:.92rem; margin-bottom:5px}
  label small{display:block; font-weight:400; color:var(--gris); font-size:.8rem; margin-top:2px}
  input[type=number]{
    width:100%; padding:10px 12px; border:1.5px solid var(--borde); border-radius:10px;
    font-size:1rem; background:#fbfefc; transition:border-color .2s, box-shadow .2s;
  }
  input[type=number]:focus{outline:none; border-color:var(--hoja); box-shadow:0 0 0 3px rgba(67,160,71,.18)}
  .extra{
    display:flex; gap:10px; align-items:flex-start; margin-top:16px; padding:12px 14px;
    background:var(--verde-claro); border-radius:10px; font-size:.92rem;
  }
  .extra input{margin-top:3px; width:18px; height:18px; accent-color:var(--verde)}
  .extra label{font-weight:400; margin:0}
  button{
    width:100%; margin-top:18px; padding:14px; font-size:1.05rem; font-weight:700;
    color:#fff; background:linear-gradient(135deg,var(--hoja),var(--verde)); border:none;
    border-radius:12px; cursor:pointer; transition:transform .1s, opacity .2s;
  }
  button:hover:not(:disabled){transform:translateY(-1px)}
  button:disabled{opacity:.6; cursor:wait}
  #resultado{
    white-space:pre-line; line-height:1.55; font-size:.97rem;
    background:var(--verde-claro); border-left:5px solid var(--hoja);
    border-radius:10px; padding:16px 18px; min-height:60px;
  }
  #resultado.vacio{color:var(--gris); font-style:italic}
  #resultado.error{background:#fdecea; border-left-color:#d32f2f; color:#8a1c1c}
  footer{text-align:center; color:var(--gris); font-size:.8rem; margin-top:10px}
</style>
</head>
<body>
<div class="contenedor">
  <header>
    <div class="icono">🌎☁️</div>
    <h1>Huella energetica de la nube</h1>
    <p class="intro">
      Cada video, foto en la nube o pregunta a una IA se procesa en centros de datos que consumen
      electricidad y agua de enfriamiento. Ese costo ambiental no aparece en lo que pagas.
      Esta pagina estima tu huella digital semanal y anual.
    </p>
  </header>
 
  <form id="formulario" class="tarjeta" novalidate>
    <h2>Tu uso digital</h2>
    <div class="grid">
      <div>
        <label for="video">Video en streaming <small>Horas al dia (YouTube, Netflix, TikTok)</small></label>
        <input type="number" id="video" name="video" min="0" step="0.1" value="0">
      </div>
      <div>
        <label for="musica">Musica en streaming <small>Horas al dia</small></label>
        <input type="number" id="musica" name="musica" min="0" step="0.1" value="0">
      </div>
      <div>
        <label for="redes">Redes sociales <small>Horas al dia</small></label>
        <input type="number" id="redes" name="redes" min="0" step="0.1" value="0">
      </div>
      <div>
        <label for="videollamadas">Videollamadas <small>Horas a la semana</small></label>
        <input type="number" id="videollamadas" name="videollamadas" min="0" step="0.1" value="0">
      </div>
      <div>
        <label for="juegos">Juegos en linea <small>Horas al dia</small></label>
        <input type="number" id="juegos" name="juegos" min="0" step="0.1" value="0">
      </div>
      <div>
        <label for="nube">Almacenamiento en la nube <small>GB guardados (fotos, archivos)</small></label>
        <input type="number" id="nube" name="nube" min="0" step="1" value="0">
      </div>
      <div>
        <label for="ia">Chatbots de IA <small>Consultas al dia</small></label>
        <input type="number" id="ia" name="ia" min="0" step="1" value="0">
      </div>
      <div>
        <label for="correos">Correos electronicos <small>Correos que envias al dia</small></label>
        <input type="number" id="correos" name="correos" min="0" step="1" value="0">
      </div>
    </div>
 
    <!-- Reto opcional (puntos extra) -->
    <div class="extra">
      <input type="checkbox" id="despues" name="despues">
      <label for="despues"><strong>Despues de aplicar las 3 acciones:</strong> calcula tambien cuanto se reduciria mi huella.</label>
    </div>
 
    <button type="submit" id="boton">Calcular mi huella</button>
  </form>
 
  <section class="tarjeta">
    <h2>Resultado</h2>
    <div id="resultado" class="vacio">Llena tus datos y presiona "Calcular mi huella".</div>
  </section>
 
  <footer>Practica 4.3 · Desarrollo Sustentable · Instituto Tecnologico de Mazatlan</footer>
</div>
 
<script>
  // >>> PEGA AQUI la URL de tu webhook de Make (Webhooks > Custom webhook) <<<
  const WEBHOOK_URL = "https://hook.us2.make.com/8c2xdah4147h1vkjj21mfoxf0wm09jo1";
 
  const CAMPOS = ["video","musica","redes","videollamadas","juegos","nube","ia","correos"];
  const form = document.getElementById("formulario");
  const boton = document.getElementById("boton");
  const resultado = document.getElementById("resultado");
 
  form.addEventListener("submit", async (e) => {
    e.preventDefault();
 
    const datos = new URLSearchParams();
    for (const campo of CAMPOS) {
      let valor = parseFloat(document.getElementById(campo).value);
      if (isNaN(valor) || valor < 0) valor = 0;
      document.getElementById(campo).value = valor;
      datos.append(campo, valor);
    }
    datos.append("despues", document.getElementById("despues").checked ? "si" : "no");
 
    boton.disabled = true;
    boton.textContent = "Calculando...";
    resultado.className = "vacio";
    resultado.textContent = "Calculando...";
 
    try {
      const resp = await fetch(WEBHOOK_URL, { method: "POST", body: datos });
      if (!resp.ok) throw new Error("HTTP " + resp.status);
      const texto = await resp.text();
      if (!texto.trim()) throw new Error("Respuesta vacia");
      resultado.className = "";
      resultado.textContent = texto;
    } catch (err) {
      console.error(err);
      resultado.className = "error";
      resultado.textContent = "No se pudo calcular, intenta de nuevo.";
    } finally {
      boton.disabled = false;
      boton.textContent = "Calcular mi huella";
    }
  });
</script>
</body>
</html>
 
