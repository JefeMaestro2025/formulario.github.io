<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Formulario de Servicio - Jefe Maestro</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    /* ------------------------------
       ESTILOS GENERALES
    ------------------------------ */
    :root {
      --bg-light: #f4f4f4;
      --bg-dark: #2c2c2c;
      --text-light: #333;
      --text-dark: #fe0000;
      --container-bg-light: #fff;
      --container-bg-dark: #3c3c3c;
      --border-color-light: #ccc;
      --border-color-dark: #666;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background-color: var(--bg-light);
      color: var(--text-light);
      transition: background-color 0.3s, color 0.3s;
    }
    body.dark-mode {
      background-color: var(--bg-dark);
      color: var(--text-dark);
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
      background-color: var(--container-bg-light);
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      transition: background-color 0.3s;
    }
    body.dark-mode .container {
      background-color: var(--container-bg-dark);
    }

    h1, h2, h3, h4 {
      margin-top: 0;
      margin-bottom: 10px;
    }

    label {
      display: block;
      margin-top: 10px;
      margin-bottom: 3px;
      font-weight: bold;
    }

    input[type="text"], input[type="email"], input[type="number"], textarea, select {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid var(--border-color-light);
      border-radius: 4px;
      transition: border-color 0.3s, background-color 0.3s, color 0.3s;
    }
    body.dark-mode input[type="text"],
    body.dark-mode input[type="email"],
    body.dark-mode input[type="number"],
    body.dark-mode textarea,
    body.dark-mode select {
      background-color: #555;
      border-color: var(--border-color-dark);
      color: #fff;
    }

    input[type="file"] {
      margin-top: 5px;
    }

    button {
      display: inline-block;
      padding: 10px 15px;
      margin-top: 10px;
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #218838;
    }

    .btn-secondary {
      background-color: #007bff;
    }
    .btn-secondary:hover {
      background-color: #0056b3;
    }

    .voice-btn {
      margin-left: 10px;
      background-color: #ff6b00;
    }
    .voice-btn:hover {
      background-color: #d45f00;
    }

    .toggle-theme-btn {
      float: right;
      margin-top: -10px;
    }

    .total-cost {
      margin-top: 20px;
      font-size: 18px;
      font-weight: bold;
      text-align: center;
    }

    .category-title {
      background-color: #dedede;
      padding: 10px;
      border-radius: 4px;
      margin: 30px 0 10px 0;
      transition: background-color 0.3s;
    }
    body.dark-mode .category-title {
      background-color: #444;
    }

    .checkbox-group {
      margin: 15px 0;
      padding: 15px;
      background: #f9f9f9;
      border-radius: 6px;
      transition: background-color 0.3s;
    }
    body.dark-mode .checkbox-group {
      background: #555;
    }

    .contact-info {
      margin-top: 20px;
      text-align: center;
      font-size: 14px;
    }

    /* Firma Digital */
    #signaturePad {
      border: 2px dashed var(--border-color-light);
      width: 100%;
      height: 200px;
      margin-top: 5px;
      cursor: crosshair;
      transition: border-color 0.3s;
    }
    body.dark-mode #signaturePad {
      border-color: var(--border-color-dark);
    }
    .signature-controls {
      text-align: center;
      margin-top: 5px;
    }

    /* Responsive */
    @media (max-width: 600px) {
      button {
        width: 100%;
        margin-top: 10px;
      }
      .voice-btn {
        margin-top: 5px;
        margin-left: 0;
      }
      .toggle-theme-btn {
        float: none;
        margin-top: 10px;
      }
    }
  </style>
</head>
<body>

<div class="container">
  <!-- Botón para cambiar de modo claro/oscuro -->
  <button type="button" class="toggle-theme-btn" onclick="toggleTheme()">Modo Oscuro/Claro</button>

  <h1>Servicios - Jefe Maestro</h1>

  <form id="serviceForm">
    <h2>Datos del Cliente</h2>

    <!-- NOMBRE con voz -->
    <label for="nombre">Nombre:</label>
    <div style="display: flex; gap: 5px;">
      <input type="text" id="nombre" name="nombre" required>
      <button class="voice-btn" type="button" onclick="startVoice('nombre')">Voz</button>
    </div>

    <!-- TELÉFONO con voz -->
    <label for="telefono">Teléfono:</label>
    <div style="display: flex; gap: 5px;">
      <input type="text" id="telefono" name="telefono" required>
      <button class="voice-btn" type="button" onclick="startVoice('telefono')">Voz</button>
    </div>

    <label for="categoria">Categoría de Negocio/Empresa:</label>
    <input type="text" id="categoria" name="categoria" required>

    <label for="direccion">Dirección:</label>
    <input type="text" id="direccion" name="direccion" required>

    <label for="horarios">Horarios de Atención:</label>
    <input type="text" id="horarios" name="horarios" required>

    <!-- LOGO: Subir archivo/foto -->
    <label for="logoFile">Logotipo (subir o tomar foto):</label>
    <input type="file" id="logoFile" name="logoFile" accept="image/*" capture="environment" onchange="previewLogo(event)">

    <!-- Vista previa de imagen -->
    <div id="logoPreviewContainer" style="margin-top:10px; display:none;">
      <p><strong>Vista previa de Logotipo:</strong></p>
      <img id="logoPreview" alt="Vista previa" style="max-width:200px; border:1px solid #ccc; border-radius:4px;">
    </div>

    <!-- DESCRIPCIÓN -->
    <label for="descripcion">Descripción Breve del Negocio:</label>
    <textarea id="descripcion" name="descripcion" rows="3" required></textarea>

    <!-- Enlace personalizado -->
    <h3>Enlace Personalizado (mibotonera.com)</h3>
    <label for="aliasLink">Alias:</label>
    <input type="text" id="aliasLink" name="aliasLink" placeholder="ej: mi-negocio" oninput="generateLink()">
    <p>Tu enlace será: <strong id="generatedLink">https://www.mibotonera.com/</strong></p>

    <!-- LISTA DE SERVICIOS -->
    <h2>Selecciona los Servicios</h2>

    <!-- 1. Aparatos (Hardware) -->
    <div class="category-title"><strong>Aparatos (Hardware)</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="aparatos" value="Simcard configuración|20000" onchange="updateTotal()">Simcard configuración ($20.000 COP)</label>
      <label><input type="checkbox" name="aparatos" value="Celular configuración|35000" onchange="updateTotal()">Celular configuración ($35.000 COP)</label>
      <label><input type="checkbox" name="aparatos" value="Computadora configuración|45000" onchange="updateTotal()">Computadora configuración ($45.000 COP)</label>
      <label><input type="checkbox" name="aparatos" value="Cámaras instalación y configuración|35000" onchange="updateTotal()">Cámaras instalación ($35.000 c/punto)</label>
      <label><input type="checkbox" name="aparatos" value="Impresoras instalación y configuración|65000" onchange="updateTotal()">Impresoras instalación ($65.000 COP)</label>
      <label><input type="checkbox" name="aparatos" value="TODO_APARATOS|190000" onchange="updateTotal()">TODO POR $190.000 COP</label>
    </div>

    <!-- 2. Inducción -->
    <div class="category-title"><strong>Inducción</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="induccion" value="Seguridad|30000" onchange="updateTotal()">1 Seguridad ($30.000)</label>
      <label><input type="checkbox" name="induccion" value="Uso de las tecnologías|30000" onchange="updateTotal()">2 Uso de las tecnologías ($30.000)</label>
      <label><input type="checkbox" name="induccion" value="Estrategia personalizada|100000" onchange="updateTotal()">3 Estrategia personalizada ($100.000)</label>
      <label><input type="checkbox" name="induccion" value="Públicos Objetivos|100000" onchange="updateTotal()">4 Públicos Objetivos ($100.000)</label>
      <label><input type="checkbox" name="induccion" value="Gestión de contenido|100000" onchange="updateTotal()">5 Gestión de contenido ($100.000)</label>
      <label><input type="checkbox" name="induccion" value="SEO en Google|50000" onchange="updateTotal()">6 SEO en Google ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="Estrategia de Facebook|50000" onchange="updateTotal()">7 Estrategia de Facebook ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="Tendencias de Instagram|50000" onchange="updateTotal()">8 Tendencias de Instagram ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="Novedades de WhatsApp|50000" onchange="updateTotal()">9 Novedades de WhatsApp ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="Contenido de YouTube|50000" onchange="updateTotal()">10 Contenido de YouTube ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="TikTok|50000" onchange="updateTotal()">11 TikTok ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="LinkedIn|50000" onchange="updateTotal()">12 LinkedIn ($50.000)</label>
      <label><input type="checkbox" name="induccion" value="TODO_INDUCCION|250000" onchange="updateTotal()">TODO POR $250.000</label>
    </div>

    <!-- 3. Correo Electrónico -->
    <div class="category-title"><strong>Correo Electrónico</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="correo" value="Creación de correo electrónico|20000" onchange="updateTotal()">Creación de correo electrónico ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Pie de página o firma|50000" onchange="updateTotal()">Pie de página o firma ($50.000)</label>
      <label><input type="checkbox" name="correo" value="Icono Animado|30000" onchange="updateTotal()">Icono Animado ($30.000)</label>
      <label><input type="checkbox" name="correo" value="Cici IA|20000" onchange="updateTotal()">Cici IA ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Repositorio de Google Drive|30000" onchange="updateTotal()">Repositorio de Google Drive ($30.000)</label>
      <label><input type="checkbox" name="correo" value="Selection Reader (Text to Speech)|30000" onchange="updateTotal()">Selection Reader TTS ($30.000)</label>
      <label><input type="checkbox" name="correo" value="Adblock Plus|20000" onchange="updateTotal()">Adblock Plus ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario de Google mi Negocio|120000" onchange="updateTotal()">Usuario de Google mi Negocio ($120.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario de LinkedIn|30000" onchange="updateTotal()">Usuario de LinkedIn ($30.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario TikTok|20000" onchange="updateTotal()">Usuario TikTok ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario Canal de YouTube|30000" onchange="updateTotal()">Usuario Canal de YouTube ($30.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario de Gwen IA|50000" onchange="updateTotal()">Usuario de Gwen IA ($50.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario Freepik|20000" onchange="updateTotal()">Usuario Freepik ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario Flexclip|20000" onchange="updateTotal()">Usuario Flexclip ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Usuario Renderforest|50000" onchange="updateTotal()">Usuario Renderforest ($50.000)</label>
      <label><input type="checkbox" name="correo" value="Servidor|20000" onchange="updateTotal()">Servidor ($20.000)</label>
      <label><input type="checkbox" name="correo" value="Documentos de Google|20000" onchange="updateTotal()">Documentos de Google ($20.000)</label>
      <label><input type="checkbox" name="correo" value="TODO_CORREO|450000" onchange="updateTotal()">TODO POR $450.000</label>
    </div>

    <!-- 4. Servicios en PC -->
    <div class="category-title"><strong>Servicios en PC</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="pc" value="Mantenimiento Preventivo|50000" onchange="updateTotal()">Mantenimiento Preventivo ($50.000)</label>
      <label><input type="checkbox" name="pc" value="Configuración de usuarios|20000" onchange="updateTotal()">Configuración de usuarios ($20.000)</label>
      <label><input type="checkbox" name="pc" value="Correcta Instalación|20000" onchange="updateTotal()">Correcta Instalación ($20.000)</label>
      <label><input type="checkbox" name="pc" value="Optimización|30000" onchange="updateTotal()">Optimización ($30.000)</label>
      <label><input type="checkbox" name="pc" value="Breve Inducción|30000" onchange="updateTotal()">Breve Inducción ($30.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación photoshop|50000" onchange="updateTotal()">Instalación Photoshop ($50.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Tinytask|30000" onchange="updateTotal()">Instalación Tinytask ($30.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Text to Audio|30000" onchange="updateTotal()">Instalación Text to Audio ($30.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Google Drive|20000" onchange="updateTotal()">Instalación Google Drive ($20.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Audacity|30000" onchange="updateTotal()">Instalación Audacity ($30.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Click Champ|50000" onchange="updateTotal()">Instalación Click Champ ($50.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Visual studio Code|50000" onchange="updateTotal()">Instalación Visual Studio Code ($50.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Corel Draw|50000" onchange="updateTotal()">Instalación Corel Draw ($50.000)</label>
      <label><input type="checkbox" name="pc" value="Instalación Illustrator AI|50000" onchange="updateTotal()">Instalación Illustrator AI ($50.000)</label>
      <label><input type="checkbox" name="pc" value="Ollama IA|120000" onchange="updateTotal()">Ollama IA ($120.000)</label>
      <label><input type="checkbox" name="pc" value="Servidor PC|100000" onchange="updateTotal()">Servidor ($100.000)</label>
      <label><input type="checkbox" name="pc" value="TODO_PC|400000" onchange="updateTotal()">TODO POR $400.000</label>
    </div>

    <!-- 5. Servicios en Móvil -->
    <div class="category-title"><strong>Servicios en Móvil</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="movil" value="Optimización movil|20000" onchange="updateTotal()">Optimización ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Correcta Instalación de las app requeridas|20000" onchange="updateTotal()">Instalación de apps ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Inducción de IA|20000" onchange="updateTotal()">Inducción de IA ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Identificador de llamadas|20000" onchange="updateTotal()">Identificador de llamadas ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Inducción de seguridad|20000" onchange="updateTotal()">Inducción de seguridad ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Seguridad en dos pasos|50000" onchange="updateTotal()">Seguridad en dos pasos ($50.000)</label>
      <label><input type="checkbox" name="movil" value="Usuario de Google mi Negocio movil|120000" onchange="updateTotal()">Usuario Google mi Negocio ($120.000)</label>
      <label><input type="checkbox" name="movil" value="Usuario de Linkedin movil|20000" onchange="updateTotal()">Usuario de Linkedin ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Usuario Tik Tok movil|20000" onchange="updateTotal()">Usuario Tik Tok ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Usuario Canal de Youtube movil|20000" onchange="updateTotal()">Usuario Canal de Youtube ($20.000)</label>
      <label><input type="checkbox" name="movil" value="Usuario de Gwen IA movil|40000" onchange="updateTotal()">Usuario de Gwen IA ($40.000)</label>
      <label><input type="checkbox" name="movil" value="Usuario Renderforest movil|30000" onchange="updateTotal()">Usuario Renderforest ($30.000)</label>
      <label><input type="checkbox" name="movil" value="Documentos de Google movil|20000" onchange="updateTotal()">Documentos de Google ($20.000)</label>
      <label><input type="checkbox" name="movil" value="TODO_MOVIL|300000" onchange="updateTotal()">TODO POR $300.000</label>
    </div>

    <!-- 6. Herramientas de Gestión de Contenido -->
    <div class="category-title"><strong>Herramientas de Gestión de Contenido</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="herramientas" value="Videobold|50000" onchange="updateTotal()">Videobold ($50.000)</label>
      <label><input type="checkbox" name="herramientas" value="Flexclip|50000" onchange="updateTotal()">Flexclip ($50.000)</label>
      <label><input type="checkbox" name="herramientas" value="Freepik|50000" onchange="updateTotal()">Freepik ($50.000)</label>
      <label><input type="checkbox" name="herramientas" value="Canva|40000" onchange="updateTotal()">Canva ($40.000)</label>
      <label><input type="checkbox" name="herramientas" value="Qwen IA|40000" onchange="updateTotal()">Qwen IA ($40.000)</label>
      <label><input type="checkbox" name="herramientas" value="Tinytask|30000" onchange="updateTotal()">Tinytask ($30.000)</label>
      <label><input type="checkbox" name="herramientas" value="RenderForest|40000" onchange="updateTotal()">RenderForest ($40.000)</label>
      <label><input type="checkbox" name="herramientas" value="Remove BG|20000" onchange="updateTotal()">Remove BG ($20.000)</label>
      <label><input type="checkbox" name="herramientas" value="Logo IA|50000" onchange="updateTotal()">Logo IA ($50.000)</label>
      <label><input type="checkbox" name="herramientas" value="Capcut|50000" onchange="updateTotal()">Capcut ($50.000)</label>
      <label><input type="checkbox" name="herramientas" value="PowerDirector|50000" onchange="updateTotal()">PowerDirector ($50.000)</label>
      <label>
        <input type="checkbox" name="herramientas" value="TODO_HERRAMIENTAS|350000" onchange="updateTotal()">
        TODO POR $350.000
      </label>
    </div>

    <!-- 7. Piezas Gráficas Necesarias -->
    <div class="category-title"><strong>Piezas Gráficas Necesarias</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="piezas" value="Logotipo principal|50000" onchange="updateTotal()">Logotipo principal ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Derivaciones del logo|30000" onchange="updateTotal()">Derivaciones del logo ($30.000)</label>
      <label><input type="checkbox" name="piezas" value="Animación de logotipo #1|50000" onchange="updateTotal()">Animación logotipo #1 ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Animación de logotipo #2|50000" onchange="updateTotal()">Animación logotipo #2 ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Animación de logotipo #3|50000" onchange="updateTotal()">Animación logotipo #3 ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Banner de portada para Facebook|50000" onchange="updateTotal()">Banner Facebook ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Banner de portada para WhatsApp|50000" onchange="updateTotal()">Banner WhatsApp ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="6 Iconos Para Historias destacadas instagram|50000" onchange="updateTotal()">6 Iconos historias ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Feed de instagram en 9 piezas|100000" onchange="updateTotal()">Feed de instagram (9) ($100.000)</label>
      <label><input type="checkbox" name="piezas" value="3 imágenes para postear en Facebook|60000" onchange="updateTotal()">3 imágenes Facebook ($60.000)</label>
      <label><input type="checkbox" name="piezas" value="1 video de paneo del negocio|120000" onchange="updateTotal()">1 video de paneo ($120.000)</label>
      <label><input type="checkbox" name="piezas" value="3 piezas gráficas para reels|60000" onchange="updateTotal()">3 gráficas reels ($60.000)</label>
      <label><input type="checkbox" name="piezas" value="imágenes de productos 30|240000" onchange="updateTotal()">30 imágenes productos ($240.000)</label>
      <label><input type="checkbox" name="piezas" value="diseño de sitio web|250000" onchange="updateTotal()">Diseño de sitio web ($250.000)</label>
      <label><input type="checkbox" name="piezas" value="Diseño para catálogo|150000" onchange="updateTotal()">Catálogo o servicios ($150.000)</label>
      <label><input type="checkbox" name="piezas" value="Diseño QR|20000" onchange="updateTotal()">Diseño QR ($20.000)</label>
      <label><input type="checkbox" name="piezas" value="Diseño tarjeta de presentación con QR|50000" onchange="updateTotal()">Tarjeta presentación QR ($50.000)</label>
      <label><input type="checkbox" name="piezas" value="Diseño 6 stickers con QR|40000" onchange="updateTotal()">6 stickers QR ($40.000)</label>
      <label><input type="checkbox" name="piezas" value="Animación gif logo|30000" onchange="updateTotal()">Animación gif logo ($30.000)</label>
      <label>
        <input type="checkbox" name="piezas" value="TODO_PIEZAS|750000" onchange="updateTotal()">
        TODO POR $750.000
      </label>
    </div>

    <!-- 8. Contexto del negocio o empresa -->
    <div class="category-title"><strong>Contexto del negocio o empresa</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="contexto" value="Descripción larga del negocio|30000" onchange="updateTotal()">Descripción larga ($30.000)</label>
      <label><input type="checkbox" name="contexto" value="Descripción corta del negocio|20000" onchange="updateTotal()">Descripción corta ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Información sobre productos y servicio|20000" onchange="updateTotal()">Info productos/servicios ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Misión|40000" onchange="updateTotal()">Misión ($40.000)</label>
      <label><input type="checkbox" name="contexto" value="Visión|20000" onchange="updateTotal()">Visión ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Fundamentos|20000" onchange="updateTotal()">Fundamentos ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Principios|20000" onchange="updateTotal()">Principios ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Valores|20000" onchange="updateTotal()">Valores ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Llamado a la acción|30000" onchange="updateTotal()">Llamado a la acción ($30.000)</label>
      <label><input type="checkbox" name="contexto" value="información técnica del negocio|20000" onchange="updateTotal()">Info técnica negocio ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Links de redes sociales|20000" onchange="updateTotal()">Links de redes/plataformas ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="Información de medios de pago|20000" onchange="updateTotal()">Medios de pago ($20.000)</label>
      <label><input type="checkbox" name="contexto" value="información de opciones de contacto|20000" onchange="updateTotal()">Opciones de contacto ($20.000)</label>
      <label>
        <input type="checkbox" name="contexto" value="TODO_CONTEXTO|350000" onchange="updateTotal()">
        TODO POR $350.000
      </label>
    </div>

    <!-- 9. Configuración de Google -->
    <div class="category-title"><strong>Configuración de Google</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="google" value="Palabra clave principal|20000" onchange="updateTotal()">Palabra clave principal ($20.000)</label>
      <label><input type="checkbox" name="google" value="10 palabras clave para la búsqueda|20000" onchange="updateTotal()">10 palabras clave ($20.000)</label>
      <label><input type="checkbox" name="google" value="instalación de logotipo google|20000" onchange="updateTotal()">Instalación logotipo ($20.000)</label>
      <label><input type="checkbox" name="google" value="instalación de portada google|20000" onchange="updateTotal()">Instalación portada ($20.000)</label>
      <label><input type="checkbox" name="google" value="Instalar el contenido de marca|20000" onchange="updateTotal()">Instalar contenido marca ($20.000)</label>
      <label><input type="checkbox" name="google" value="Poner información técnica del negocio|20000" onchange="updateTotal()">Info técnica ($20.000)</label>
      <label><input type="checkbox" name="google" value="Enlazar redes sociales google|20000" onchange="updateTotal()">Enlazar redes sociales ($20.000)</label>
      <label><input type="checkbox" name="google" value="Entregar enlace para calificaciones|20000" onchange="updateTotal()">Enlace reseñas ($20.000)</label>
      <label><input type="checkbox" name="google" value="Poner descripción google|20000" onchange="updateTotal()">Poner descripción ($20.000)</label>
      <label><input type="checkbox" name="google" value="Enlazar sitio web google|20000" onchange="updateTotal()">Enlazar sitio web ($20.000)</label>
      <label><input type="checkbox" name="google" value="Entregar Propiedad digital de google|20000" onchange="updateTotal()">Propiedad digital ($20.000)</label>
      <label><input type="checkbox" name="google" value="Breve inducción google|20000" onchange="updateTotal()">Breve inducción ($20.000)</label>
      <label>
        <input type="checkbox" name="google" value="TODO_GOOGLE|120000" onchange="updateTotal()">
        TODO POR $120.000
      </label>
    </div>

    <!-- 10. Configuración de WhatsApp -->
    <div class="category-title"><strong>Configuración de WhatsApp</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="whatsapp" value="Hacer copia de seguridad|20000" onchange="updateTotal()">Copia de seguridad ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Hacer catálogo de productos|220000" onchange="updateTotal()">Catálogo de productos ($220.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Hace canal de novedades|120000" onchange="updateTotal()">Canal de novedades ($120.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner información técnica|20000" onchange="updateTotal()">Info técnica ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner logo|20000" onchange="updateTotal()">Poner logo ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner portada|20000" onchange="updateTotal()">Poner portada ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner descripción|20000" onchange="updateTotal()">Poner descripción ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner Mensaje de bienvenida|20000" onchange="updateTotal()">Mensaje bienvenida ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner respuestas rápidas|20000" onchange="updateTotal()">Respuestas rápidas ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner sitio web|20000" onchange="updateTotal()">Poner sitio web ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner mensaje en ausencia|20000" onchange="updateTotal()">Mensaje ausencia ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Poner contenido en el canal|20000" onchange="updateTotal()">Contenido en canal ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Enlazar Facebook|20000" onchange="updateTotal()">Enlazar Facebook ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Enlazar Instagram|20000" onchange="updateTotal()">Enlazar Instagram ($20.000)</label>
      <label><input type="checkbox" name="whatsapp" value="Breve inducción whatsapp|20000" onchange="updateTotal()">Breve inducción ($20.000)</label>
      <label>
        <input type="checkbox" name="whatsapp" value="TODO_WHATSAPP|200000" onchange="updateTotal()">
        TODO POR $200.000
      </label>
    </div>

    <!-- 11. Redes Sociales -->
    <div class="category-title"><strong>Redes Sociales</strong></div>
    <div class="checkbox-group">
      <label><input type="checkbox" name="redes" value="Configuración Meta Business Suite|120000" onchange="updateTotal()">Meta Business Suite ($120.000)</label>
      <label><input type="checkbox" name="redes" value="Configuración de Facebook|120000" onchange="updateTotal()">Configuración de Facebook ($120.000)</label>
      <label><input type="checkbox" name="redes" value="Configuración de Instagram|120000" onchange="updateTotal()">Configuración de Instagram ($120.000)</label>
      <label><input type="checkbox" name="redes" value="Configuración de Tik Tok|120000" onchange="updateTotal()">Configuración de Tik Tok ($120.000)</label>
      <label><input type="checkbox" name="redes" value="Configuración de Linkedin|120000" onchange="updateTotal()">Configuración de Linkedin ($120.000)</label>
      <label><input type="checkbox" name="redes" value="Configuración de Youtube|120000" onchange="updateTotal()">Configuración de Youtube ($120.000)</label>
      <label>
        <input type="checkbox" name="redes" value="TODO_REDES|450000" onchange="updateTotal()">
        TODO POR $450.000
      </label>
    </div>

    <!-- FIRMA DIGITAL -->
    <h3>Firma Digital</h3>
    <p>Firme dentro del recuadro:</p>
    <canvas id="signaturePad"></canvas>
    <div class="signature-controls">
      <button type="button" class="btn-secondary" onclick="clearSignature()">Limpiar Firma</button>
    </div>

    <div class="total-cost" id="totalCost">Costo Total: $0 COP</div>
    <button type="button" onclick="submitForm()">Enviar Pedido por WhatsApp</button>
  </form>

  <div class="contact-info">
    <p>Para más información, contáctanos en WhatsApp: 
       <a href="https://wa.me/573234283797" target="_blank">+57 323 428 3797</a>
    </p>
  </div>
</div>

<script>
/* ==============================================
   1. TOGGLE MODO OSCURO / CLARO
   ============================================== */
function toggleTheme() {
  document.body.classList.toggle('dark-mode');
}

/* ==============================================
   2. RECONOCIMIENTO DE VOZ (Voz a Texto)
   ============================================== */
let recognition = null;
if ('webkitSpeechRecognition' in window) {
  recognition = new webkitSpeechRecognition();
} else if ('SpeechRecognition' in window) {
  recognition = new SpeechRecognition();
} else {
  console.warn("API de Reconocimiento de Voz no soportada en este navegador.");
}

function startVoice(inputId) {
  if (!recognition) {
    alert("Lo siento, tu navegador no soporta SpeechRecognition.");
    return;
  }

  recognition.lang = "es-ES";
  recognition.continuous = false;
  recognition.interimResults = false;

  recognition.onresult = function(event) {
    const text = event.results[0][0].transcript;
    document.getElementById(inputId).value = text;
  };
  recognition.onerror = function(e) {
    console.error("Error en reconocimiento de voz:", e.error);
    alert("Error en reconocimiento de voz: " + e.error);
  };

  recognition.start();
}

/* ==============================================
   3. PREVISUALIZACIÓN DE LOGO (IMAGEN)
   ============================================== */
let logoBase64 = ""; // Guardaremos la imagen en Base64

function previewLogo(event) {
  const file = event.target.files[0];
  if (!file) {
    document.getElementById('logoPreviewContainer').style.display = 'none';
    logoBase64 = "";
    return;
  }

  const reader = new FileReader();
  reader.onload = function(e) {
    document.getElementById('logoPreviewContainer').style.display = 'block';
    document.getElementById('logoPreview').src = e.target.result;
    // Guardamos en variable global
    logoBase64 = e.target.result; 
  };
  reader.readAsDataURL(file);
}

/* ==============================================
   4. GENERACIÓN DE ENLACE (mibotonera)
   ============================================== */
function generateLink() {
  const alias = document.getElementById('aliasLink').value.trim();
  const linkEl = document.getElementById('generatedLink');
  let baseUrl = "https://www.mibotonera.com/";
  linkEl.textContent = alias ? baseUrl + alias : baseUrl;
}

/* ==============================================
   5. FIRMA DIGITAL en CANVAS
   ============================================== */
const canvas = document.getElementById('signaturePad');
const ctx = canvas.getContext('2d');
let isDrawing = false;
let lastX = 0;
let lastY = 0;

function resizeCanvas() {
  canvas.width = canvas.offsetWidth;
  canvas.height = 200; // altura fija
}
window.addEventListener('resize', resizeCanvas);
resizeCanvas();

function getPos(e) {
  let rect = canvas.getBoundingClientRect();
  let x, y;
  if (e.touches && e.touches.length > 0) {
    x = e.touches[0].clientX - rect.left;
    y = e.touches[0].clientY - rect.top;
  } else {
    x = e.clientX - rect.left;
    y = e.clientY - rect.top;
  }
  return { x, y };
}

canvas.addEventListener('mousedown', e => {
  isDrawing = true;
  const pos = getPos(e);
  lastX = pos.x;
  lastY = pos.y;
});
canvas.addEventListener('mousemove', e => {
  if (!isDrawing) return;
  ctx.beginPath();
  ctx.moveTo(lastX, lastY);
  const pos = getPos(e);
  ctx.lineTo(pos.x, pos.y);
  ctx.strokeStyle = '#000';
  ctx.lineWidth = 2;
  ctx.stroke();
  lastX = pos.x;
  lastY = pos.y;
});
canvas.addEventListener('mouseup', () => isDrawing = false);
canvas.addEventListener('mouseleave', () => isDrawing = false);

// Soporte táctil
canvas.addEventListener('touchstart', e => {
  isDrawing = true;
  const pos = getPos(e);
  lastX = pos.x;
  lastY = pos.y;
});
canvas.addEventListener('touchmove', e => {
  if (!isDrawing) return;
  ctx.beginPath();
  ctx.moveTo(lastX, lastY);
  const pos = getPos(e);
  ctx.lineTo(pos.x, pos.y);
  ctx.strokeStyle = '#000';
  ctx.lineWidth = 2;
  ctx.stroke();
  lastX = pos.x;
  lastY = pos.y;
});
canvas.addEventListener('touchend', () => isDrawing = false);

function clearSignature() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
}

/* ==============================================
   6. CÁLCULO DE COSTO TOTAL
   ============================================== */
function updateTotal() {
  const form = document.getElementById('serviceForm');
  let totalCost = 0;

  const categories = [
    { name: 'aparatos',   todoValue: 'TODO_APARATOS',   todoCost: 190000 },
    { name: 'induccion',  todoValue: 'TODO_INDUCCION',  todoCost: 250000 },
    { name: 'correo',     todoValue: 'TODO_CORREO',     todoCost: 450000 },
    { name: 'pc',         todoValue: 'TODO_PC',         todoCost: 400000 },
    { name: 'movil',      todoValue: 'TODO_MOVIL',      todoCost: 300000 },
    { name: 'herramientas', todoValue: 'TODO_HERRAMIENTAS', todoCost: 350000 },
    { name: 'piezas',     todoValue: 'TODO_PIEZAS',     todoCost: 750000 },
    { name: 'contexto',   todoValue: 'TODO_CONTEXTO',   todoCost: 350000 },
    { name: 'google',     todoValue: 'TODO_GOOGLE',     todoCost: 120000 },
    { name: 'whatsapp',   todoValue: 'TODO_WHATSAPP',   todoCost: 200000 },
    { name: 'redes',      todoValue: 'TODO_REDES',      todoCost: 450000 }
  ];

  let allTodoSelected = true;

  categories.forEach(cat => {
    const checkboxes = form.querySelectorAll(`input[name="${cat.name}"]:checked`);
    let categoryCost = 0;
    let todoSelected = false;

    checkboxes.forEach(chk => {
      const [serviceName, price] = chk.value.split('|');
      if (serviceName === cat.todoValue) {
        todoSelected = true;
      }
    });

    if (todoSelected) {
      categoryCost = cat.todoCost;
    } else {
      allTodoSelected = false;
      checkboxes.forEach(chk => {
        const [serviceName, price] = chk.value.split('|');
        categoryCost += parseInt(price) || 0;
      });
    }
    totalCost += categoryCost;
  });

  // Si en TODAS las categorías se marcó "TODO"
  if (allTodoSelected && categories.length > 0) {
    totalCost = 2000000; // super descuento
  }

  document.getElementById('totalCost').textContent = `Costo Total: $${totalCost.toLocaleString()} COP`;
}

/* ==============================================
   7. ENVÍO DE FORMULARIO a WHATSAPP
   ============================================== */
function submitForm() {
  const form = document.getElementById('serviceForm');
  const formData = new FormData(form);

  // Construimos el mensaje
  let message = "Pedido desde formulario (Jefe Maestro):\n\n";

  // Datos del cliente
  const nombre = formData.get('nombre');
  const telefono = formData.get('telefono');
  const categoria = formData.get('categoria');
  const direccion = formData.get('direccion');
  const horarios = formData.get('horarios');
  const descripcion = formData.get('descripcion');
  const aliasLink = formData.get('aliasLink');

  message += `Nombre: ${nombre}\n`;
  message += `Teléfono: ${telefono}\n`;
  message += `Categoría: ${categoria}\n`;
  message += `Dirección: ${direccion}\n`;
  message += `Horarios: ${horarios}\n\n`;
  message += `Descripción Breve del Negocio: ${descripcion}\n\n`;

  // Enlace personalizado
  if (aliasLink) {
    message += `Enlace Personalizado: https://www.mibotonera.com/${aliasLink}\n\n`;
  }

  // Calculamos costos y listamos servicios
  let totalCost = 0;
  const categories = [
    { name: 'aparatos',   label: 'Aparatos (Hardware)',  todoValue: 'TODO_APARATOS',   todoCost: 190000 },
    { name: 'induccion',  label: 'Inducción',            todoValue: 'TODO_INDUCCION',  todoCost: 250000 },
    { name: 'correo',     label: 'Correo Electrónico',   todoValue: 'TODO_CORREO',     todoCost: 450000 },
    { name: 'pc',         label: 'Servicios en PC',      todoValue: 'TODO_PC',         todoCost: 400000 },
    { name: 'movil',      label: 'Servicios en Móvil',   todoValue: 'TODO_MOVIL',      todoCost: 300000 },
    { name: 'herramientas', label: 'Herramientas de Contenido', todoValue: 'TODO_HERRAMIENTAS', todoCost: 350000 },
    { name: 'piezas',     label: 'Piezas Gráficas',      todoValue: 'TODO_PIEZAS',     todoCost: 750000 },
    { name: 'contexto',   label: 'Contexto del negocio', todoValue: 'TODO_CONTEXTO',   todoCost: 350000 },
    { name: 'google',     label: 'Configuración de Google', todoValue: 'TODO_GOOGLE',  todoCost: 120000 },
    { name: 'whatsapp',   label: 'Configuración de WhatsApp', todoValue: 'TODO_WHATSAPP', todoCost: 200000 },
    { name: 'redes',      label: 'Redes Sociales',       todoValue: 'TODO_REDES',      todoCost: 450000 }
  ];

  let allTodoSelected = true;
  message += "Servicios Seleccionados:\n";

  categories.forEach(cat => {
    const selected = formData.getAll(cat.name);
    let categoryCost = 0;
    let todoSelected = false;
    message += `\n[${cat.label}]\n`;
    
    selected.forEach(val => {
      const [serviceName, price] = val.split('|');
      if (serviceName === cat.todoValue) {
        todoSelected = true;
      }
    });

    if (todoSelected) {
      message += `- TODO por $${cat.todoCost}\n`;
      categoryCost = cat.todoCost;
    } else {
      allTodoSelected = false;
      selected.forEach(val => {
        const [serviceName, price] = val.split('|');
        if (price) {
          categoryCost += parseInt(price) || 0;
          message += `- ${serviceName} ($${price})\n`;
        }
      });
    }
    totalCost += categoryCost;
  });

  if (allTodoSelected && categories.length > 0) {
    totalCost = 2000000;
  }
  message += `\nCosto Total: $${totalCost.toLocaleString()} COP\n\n`;

  // Imagen de Logo en Base64 (si existe)
  if (logoBase64) {
    // Advertimos que es un base64
    message += "Imagen Logo (Base64): \n" + logoBase64 + "\n\n";
  } else {
    message += "Sin imagen de logo adjuntada.\n\n";
  }

  // Firma digital en Base64
  const signatureDataUrl = canvas.toDataURL("image/png");
  // Verificamos si la firma está vacía (canvas en blanco)
  // Para un control básico, podríamos chequear cuántos píxeles no están en blanco,
  // pero aquí solo revisamos si es el "data:,"
  if (signatureDataUrl.length > 100) {
    message += "Firma Digital (Base64): \n" + signatureDataUrl + "\n\n";
  } else {
    message += "Sin Firma Digital.\n\n";
  }

  // Enviar a WhatsApp vía URL
  const whatsappUrl = `https://wa.me/573234283797?text=${encodeURIComponent(message)}`;

  // IMPORTANTE: si el mensaje es muy grande, es posible que la URL sea demasiado larga
  // y no se abra correctamente. Esto es una limitación de WhatsApp en enlace directo.
  
  window.open(whatsappUrl, '_blank');
}
</script>
</body>
</html>
