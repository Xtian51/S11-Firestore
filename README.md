<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Semana 11B — Firebase · Android Studio + Kotlin</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Nunito:wght@300;600;800;900&family=Crimson+Pro:ital,wght@0,400;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0f0f0f;
    --surface: #171717;
    --surface2: #1f1f1f;
    --border: #2a2a2a;
    --border2: #333;
    --accent: #ff6b2b;
    --accent2: #ffc107;
    --accent3: #4caf50;
    --accent4: #2196f3;
    --text: #f5f5f5;
    --text-dim: #aaa;
    --text-muted: #555;
    --kotlin: #b08fff;
    --xml: #fb923c;
    --gradle: #4caf50;
    --firebase: #ff6b2b;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: 'Crimson Pro', serif; font-size: 17px; line-height: 1.75; }

  /* ── HERO ── */
  .hero {
    padding: 56px 48px 48px;
    background: var(--bg);
    border-bottom: 1px solid var(--border2);
    position: relative;
    overflow: hidden;
  }
  .hero-bg-text {
    position: absolute;
    right: -30px; top: -20px;
    font-family: 'Nunito', sans-serif;
    font-size: 180px;
    font-weight: 900;
    line-height: 1;
    color: rgba(255,107,43,0.04);
    user-select: none;
    pointer-events: none;
  }
  .week-tag {
    display: inline-flex; align-items: center; gap: 8px;
    border: 1px solid rgba(255,107,43,0.35);
    background: rgba(255,107,43,0.08);
    color: #ffa07a;
    font-family: 'JetBrains Mono', monospace; font-size: 10px; font-weight: 700;
    letter-spacing: 0.14em; text-transform: uppercase;
    padding: 5px 14px; border-radius: 20px; margin-bottom: 20px; width: fit-content;
  }
  .hero h1 { font-family: 'Nunito', sans-serif; font-size: clamp(2.6rem, 6.5vw, 4.4rem); font-weight: 900; color: #fff; line-height: 1.0; margin-bottom: 8px; }
  .hero h1 span { color: var(--accent); }
  .hero-sub { color: #666; font-size: 1rem; max-width: 600px; margin-bottom: 32px; font-family: 'Crimson Pro', serif; }
  .meta-strip { display: flex; flex-wrap: wrap; gap: 20px; border-top: 1px solid var(--border); padding-top: 22px; }
  .meta-chip { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--text-muted); display: flex; align-items: center; gap: 6px; }
  .meta-chip strong { color: #888; font-weight: 600; }

  .container { max-width: 980px; margin: 0 auto; padding: 0 28px 100px; }

  /* ── VS BANNER ── */
  .vs-banner {
    background: var(--surface);
    border: 1px solid var(--border2);
    border-left: 4px solid var(--accent);
    border-radius: 8px;
    padding: 16px 20px;
    margin: 40px 0 0;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.85rem;
  }
  .vs-banner strong { color: var(--accent); }
  .vs-banner p { margin: 0; color: var(--text-dim); font-family: 'Crimson Pro', serif; }

  /* ── CLASE HEADER ── */
  .clase-header { margin: 56px 0 26px; display: flex; align-items: center; gap: 16px; }
  .clase-badge { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; background: var(--accent); color: #fff; padding: 5px 14px; border-radius: 3px; white-space: nowrap; flex-shrink: 0; }
  .clase-title { font-family: 'Nunito', sans-serif; font-size: 1.7rem; font-weight: 800; color: var(--text); line-height: 1.15; }
  .clase-title span { color: var(--accent); }
  .clase-line { flex: 1; height: 1px; background: var(--border); }

  /* ── OBJETIVO ── */
  .objetivo { background: rgba(76,175,80,0.07); border: 1px solid rgba(76,175,80,0.2); border-left: 4px solid var(--accent3); border-radius: 6px; padding: 14px 20px; margin-bottom: 26px; font-size: 0.9rem; }
  .objetivo strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--accent3); display: block; margin-bottom: 5px; }
  .objetivo p { margin: 0; color: var(--text-dim); font-family: 'Crimson Pro', serif; }

  /* ── SECTION ── */
  .section { margin-bottom: 36px; }
  .section-title { font-family: 'Nunito', sans-serif; font-size: 0.88rem; font-weight: 800; color: var(--text); margin-bottom: 14px; display: flex; align-items: center; gap: 10px; text-transform: uppercase; letter-spacing: 0.07em; }
  .section-title .tag { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; padding: 2px 8px; border-radius: 3px; }
  .section-title .tag.kotlin  { background: rgba(176,143,255,0.2); color: var(--kotlin); border: 1px solid rgba(176,143,255,0.3); }
  .section-title .tag.xml     { background: rgba(251,146,60,0.2);  color: var(--xml);    border: 1px solid rgba(251,146,60,0.3); }
  .section-title .tag.gradle  { background: rgba(76,175,80,0.2);   color: var(--gradle); border: 1px solid rgba(76,175,80,0.3); }
  .section-title .tag.concept { background: rgba(255,107,43,0.2);  color: #ffa07a;       border: 1px solid rgba(255,107,43,0.3); }
  .section-title .tag.config  { background: rgba(33,150,243,0.2);  color: #90caf9;       border: 1px solid rgba(33,150,243,0.3); }

  p { margin-bottom: 12px; color: var(--text-dim); font-size: 0.93rem; font-family: 'Crimson Pro', serif; }

  /* ── COMPARE TABLE ── */
  .compare { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin: 18px 0; }
  @media(max-width:600px){ .compare { grid-template-columns: 1fr; } }
  .compare-card { border-radius: 8px; padding: 16px; border: 1px solid var(--border); }
  .compare-card.local { background: rgba(33,150,243,0.06); border-color: rgba(33,150,243,0.2); }
  .compare-card.cloud { background: rgba(255,107,43,0.06); border-color: rgba(255,107,43,0.2); }
  .compare-card .label { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; margin-bottom: 8px; display: block; }
  .compare-card.local .label { color: #90caf9; }
  .compare-card.cloud .label { color: #ffa07a; }
  .compare-card h4 { font-family: 'Nunito', sans-serif; font-weight: 700; font-size: 0.9rem; margin-bottom: 6px; }
  .compare-card ul { list-style: none; padding: 0; font-size: 0.82rem; color: var(--text-dim); font-family: 'Crimson Pro', serif; }
  .compare-card ul li { padding: 2px 0; }
  .compare-card ul li::before { content: '→ '; color: var(--text-muted); }

  /* ── STEPS CONFIG ── */
  .config-steps { display: flex; flex-direction: column; gap: 0; margin: 18px 0; border: 1px solid var(--border2); border-radius: 8px; overflow: hidden; }
  .config-step { display: flex; gap: 16px; padding: 16px; align-items: flex-start; border-bottom: 1px solid var(--border); }
  .config-step:last-child { border-bottom: none; }
  .step-num { min-width: 28px; height: 28px; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 12px; font-weight: 700; border-radius: 4px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
  .step-content h4 { font-family: 'Nunito', sans-serif; font-weight: 700; font-size: 0.9rem; margin-bottom: 4px; }
  .step-content p { font-size: 0.84rem; margin: 0; }

  /* ── CODE BLOCK ── */
  .code-block { background: #0a0a0a; border: 1px solid var(--border2); border-radius: 8px; overflow: hidden; margin: 16px 0; font-size: 0.84rem; }
  .code-header { display: flex; align-items: center; justify-content: space-between; padding: 9px 16px; background: var(--surface2); border-bottom: 1px solid var(--border); }
  .code-lang { font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase; padding: 2px 9px; border-radius: 3px; }
  .lang-kotlin  { background: rgba(176,143,255,0.15); color: var(--kotlin);  border: 1px solid rgba(176,143,255,0.3); }
  .lang-xml     { background: rgba(251,146,60,0.15);  color: var(--xml);     border: 1px solid rgba(251,146,60,0.3); }
  .lang-gradle  { background: rgba(76,175,80,0.15);   color: var(--gradle);  border: 1px solid rgba(76,175,80,0.3); }
  .code-filename { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: var(--text-muted); }
  .code-body { padding: 18px 20px; overflow-x: auto; }
  pre { font-family: 'JetBrains Mono', monospace; line-height: 1.65; white-space: pre; color: #ccc; background: transparent; }
  .kw  { color: #c792ea; } .fn  { color: #82aaff; } .str { color: #c3e88d; }
  .cm  { color: #3a3a3a; font-style: italic; } .num { color: #f78c6c; }
  .cls { color: #ffcb6b; } .op  { color: #89ddff; } .tag { color: #e06c75; }
  .attr{ color: #c3e88d; } .val { color: #f78c6c; } .an  { color: #89ddff; }

  /* ── ALERT ── */
  .alert { border-radius: 6px; padding: 13px 17px; margin: 14px 0; font-size: 0.87rem; display: flex; gap: 12px; align-items: flex-start; }
  .alert-orange { background: rgba(255,107,43,0.07);  border: 1px solid rgba(255,107,43,0.25); }
  .alert-green  { background: rgba(76,175,80,0.07);   border: 1px solid rgba(76,175,80,0.2); }
  .alert-yellow { background: rgba(255,193,7,0.07);   border: 1px solid rgba(255,193,7,0.2); }
  .alert-blue   { background: rgba(33,150,243,0.07);  border: 1px solid rgba(33,150,243,0.2); }
  .alert-icon   { font-size: 1.1rem; flex-shrink: 0; margin-top: 1px; }
  .alert p      { margin: 0; color: var(--text-dim); font-family: 'Crimson Pro', serif; }

  /* ── DIVIDER ── */
  .divider { margin: 56px 0 0; border: none; border-top: 1px solid var(--border2); position: relative; }
  .divider::after { content: 'CLASE 02'; position: absolute; top: -10px; left: 50%; transform: translateX(-50%); background: var(--bg); padding: 0 14px; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; color: var(--text-muted); }

  /* ── TAREA ── */
  .tarea { background: var(--surface); border: 1px solid var(--border2); border-top: 4px solid var(--accent); border-radius: 10px; padding: 34px; margin-top: 56px; }
  .tarea-badge { display: inline-block; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 9px; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; padding: 4px 12px; border-radius: 3px; margin-bottom: 14px; }
  .tarea h2 { font-family: 'Nunito', sans-serif; font-size: 1.8rem; font-weight: 900; color: var(--text); margin-bottom: 10px; }
  .tarea-desc { color: var(--text-dim); margin-bottom: 22px; font-size: 0.93rem; font-family: 'Crimson Pro', serif; }
  .reqs { display: flex; flex-direction: column; gap: 10px; margin-bottom: 22px; }
  .req { display: flex; gap: 12px; align-items: flex-start; font-size: 0.89rem; color: var(--text-dim); font-family: 'Crimson Pro', serif; }
  .req-num { min-width: 22px; height: 22px; background: var(--accent); color: #fff; font-family: 'JetBrains Mono', monospace; font-size: 10px; font-weight: 700; border-radius: 3px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }
  .req-num.star { background: var(--accent3); }
  .entrega { background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; padding: 13px 17px; font-size: 0.84rem; }
  .entrega strong { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--accent2); text-transform: uppercase; letter-spacing: 0.12em; display: block; margin-bottom: 4px; }
  .entrega p { color: var(--text-muted); margin: 0; font-family: 'Crimson Pro', serif; }

  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: var(--surface); }
  ::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }
</style>
</head>
<body>

<div class="hero">
  <div class="hero-bg-text">FIREBASE</div>
  <div class="week-tag">📅 Semana 11 de 16 · Opción B</div>
  <h1>Firebase<br><span>Firestore</span></h1>
  <p class="hero-sub">Conecta tu app a una base de datos en la nube en tiempo real. Los datos se sincronizan automáticamente entre dispositivos sin servidores propios.</p>
  <div class="meta-strip">
    <div class="meta-chip">Clases <strong>2 × 2 hrs</strong></div>
    <div class="meta-chip">Lenguaje <strong>Kotlin</strong></div>
    <div class="meta-chip">Layout <strong>ConstraintLayout</strong></div>
    <div class="meta-chip">Prereq <strong>Semana 10 — ViewModel + LiveData</strong></div>
  </div>
</div>

<div class="container">

  <div class="vs-banner">
    <strong>Opción B vs Opción A:</strong>
    <p>Room guarda datos localmente en el dispositivo. Firebase Firestore los guarda en la nube, permite sincronización entre usuarios en tiempo real y funciona como backend sin necesidad de un servidor propio.</p>
  </div>

  <!-- ══════════════ CLASE 1 ══════════════ -->
  <div class="clase-header">
    <span class="clase-badge">Clase 01</span>
    <div class="clase-title">Configuración y <span>primeras operaciones</span></div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Conectar el proyecto Android a Firebase, configurar Firestore y realizar las operaciones básicas: agregar, leer y eliminar documentos.</p>
  </div>

  <!-- Local vs Cloud -->
  <div class="section">
    <div class="section-title"><span class="tag concept">CONCEPTO</span> Room vs Firebase Firestore</div>
    <div class="compare">
      <div class="compare-card local">
        <span class="label">Room (Opción A)</span>
        <h4>Base de datos local</h4>
        <ul>
          <li>Datos solo en el dispositivo</li>
          <li>Sin internet requerido</li>
          <li>Más rápido, sin latencia</li>
          <li>No comparte datos entre usuarios</li>
          <li>Se pierde si se desinstala la app</li>
        </ul>
      </div>
      <div class="compare-card cloud">
        <span class="label">Firebase (Opción B)</span>
        <h4>Base de datos en la nube</h4>
        <ul>
          <li>Datos en servidores de Google</li>
          <li>Sincronización en tiempo real</li>
          <li>Compartido entre usuarios</li>
          <li>Persiste aunque se desinstale</li>
          <li>Requiere conexión a internet</li>
        </ul>
      </div>
    </div>
  </div>

  <!-- Configuración paso a paso -->
  <div class="section">
    <div class="section-title"><span class="tag config">CONFIGURACIÓN</span> Conectar Firebase al proyecto</div>
    <div class="config-steps">
      <div class="config-step">
        <div class="step-num">1</div>
        <div class="step-content">
          <h4>Crear proyecto en Firebase Console</h4>
          <p>Ir a <code>console.firebase.google.com</code> → Crear proyecto → Agregar app Android → Registrar con el package name del proyecto.</p>
        </div>
      </div>
      <div class="config-step">
        <div class="step-num">2</div>
        <div class="step-content">
          <h4>Descargar google-services.json</h4>
          <p>Descargar el archivo y colocarlo en la carpeta <code>app/</code> del proyecto (mismo nivel que <code>build.gradle</code> del módulo).</p>
        </div>
      </div>
      <div class="config-step">
        <div class="step-num">3</div>
        <div class="step-content">
          <h4>Agregar plugin y dependencias en Gradle</h4>
          <p>Modificar los dos archivos <code>build.gradle</code> como se muestra en los Códigos 1 y 2.</p>
        </div>
      </div>
      <div class="config-step">
        <div class="step-num">4</div>
        <div class="step-content">
          <h4>Habilitar Firestore en la consola</h4>
          <p>En Firebase Console → Firestore Database → Crear base de datos → Modo de prueba (reglas abiertas para desarrollo).</p>
        </div>
      </div>
    </div>
    <div class="alert alert-yellow">
      <span class="alert-icon">⚠️</span>
      <p><strong>Modo de prueba:</strong> Las reglas de seguridad abiertas permiten leer y escribir sin autenticación durante 30 días. Suficiente para el curso. En producción real se configuran reglas estrictas junto con Firebase Auth.</p>
    </div>
  </div>

  <!-- Código 1: build.gradle proyecto raíz -->
  <div class="section">
    <div class="section-title"><span class="tag gradle">GRADLE</span> Código 1 — build.gradle.kts (Project)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-gradle">Gradle · Kotlin DSL</span>
        <span class="code-filename">build.gradle.kts (Project raíz)</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">plugins</span> {
    id(<span class="str">"com.android.application"</span>) version <span class="str">"8.3.0"</span> apply <span class="kw">false</span>
    id(<span class="str">"org.jetbrains.kotlin.android"</span>) version <span class="str">"1.9.0"</span> apply <span class="kw">false</span>
    <span class="cm">// Plugin de Google Services — necesario para firebase</span>
    id(<span class="str">"com.google.gms.google-services"</span>) version <span class="str">"4.4.1"</span> apply <span class="kw">false</span>
}</pre></div>
    </div>
  </div>

  <!-- Código 2: build.gradle módulo -->
  <div class="section">
    <div class="section-title"><span class="tag gradle">GRADLE</span> Código 2 — build.gradle.kts (Module)</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-gradle">Gradle · Kotlin DSL</span>
        <span class="code-filename">build.gradle.kts (Module: app)</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">plugins</span> {
    id(<span class="str">"com.android.application"</span>)
    id(<span class="str">"org.jetbrains.kotlin.android"</span>)
    <span class="cm">// Aplicar el plugin en el módulo</span>
    id(<span class="str">"com.google.gms.google-services"</span>)
}

<span class="fn">dependencies</span> {
    <span class="cm">// Firebase BoM — gestiona versiones compatibles automáticamente</span>
    <span class="fn">implementation</span>(<span class="fn">platform</span>(<span class="str">"com.google.firebase:firebase-bom:33.1.0"</span>))

    <span class="cm">// Firestore con soporte para Kotlin coroutines</span>
    <span class="fn">implementation</span>(<span class="str">"com.google.firebase:firebase-firestore-ktx"</span>)

    <span class="cm">// ViewModel + LiveData (de Semana 10)</span>
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.lifecycle:lifecycle-livedata-ktx:2.7.0"</span>)
    <span class="fn">implementation</span>(<span class="str">"androidx.activity:activity-ktx:1.9.0"</span>)
}</pre></div>
    </div>
    <div class="alert alert-blue">
      <span class="alert-icon">💡</span>
      <p><strong>Firebase BoM (Bill of Materials):</strong> Al declarar la plataforma BoM no se especifican versiones individuales de cada librería Firebase — el BoM garantiza que todas sean compatibles entre sí.</p>
    </div>
  </div>

  <!-- Código 3: Nota.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 3 — Nota.kt (modelo de datos)</div>
    <p>En Firestore los datos se guardan como documentos JSON. La data class debe tener un constructor vacío y propiedades con valores por defecto para que Firestore pueda deserializarla automáticamente.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">Nota.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">data class</span> <span class="cls">Nota</span>(
    <span class="kw">val</span> id:        <span class="cls">String</span>  = <span class="str">""</span>,    <span class="cm">// ID del documento en Firestore</span>
    <span class="kw">val</span> titulo:    <span class="cls">String</span>  = <span class="str">""</span>,
    <span class="kw">val</span> contenido: <span class="cls">String</span>  = <span class="str">""</span>,
    <span class="kw">val</span> fechaMs:   <span class="cls">Long</span>    = <span class="num">0L</span>
) {
    <span class="cm">// Constructor vacío requerido por Firestore para deserializar</span>
    <span class="kw">constructor</span>() : <span class="kw">this</span>(<span class="str">""</span>, <span class="str">""</span>, <span class="str">""</span>, <span class="num">0L</span>)
}</pre></div>
    </div>
  </div>

  <!-- Código 4: NotaRepository.kt con Firestore -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 4 — NotaRepository.kt</div>
    <p>El Repository encapsula toda la lógica de Firestore. El ViewModel solo llama métodos del Repository sin conocer los detalles de Firebase.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaRepository.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.lifecycle.MutableLiveData
<span class="kw">import</span> com.google.firebase.firestore.ktx.firestore
<span class="kw">import</span> com.google.firebase.firestore.ktx.toObject
<span class="kw">import</span> com.google.firebase.ktx.Firebase

<span class="kw">class</span> <span class="cls">NotaRepository</span> {

    <span class="cm">// Referencia a la colección "notas" en Firestore</span>
    <span class="kw">private val</span> coleccion = <span class="cls">Firebase</span>.firestore.<span class="fn">collection</span>(<span class="str">"notas"</span>)

    <span class="kw">private val</span> _notas = <span class="cls">MutableLiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;&gt;(<span class="fn">emptyList</span>())
    <span class="kw">val</span> notas: <span class="cls">LiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;&gt; = _notas

    <span class="kw">private val</span> _error = <span class="cls">MutableLiveData</span>&lt;<span class="cls">String</span>?&gt;()
    <span class="kw">val</span> error: <span class="cls">LiveData</span>&lt;<span class="cls">String</span>?&gt; = _error

    <span class="kw">init</span> {
        <span class="cm">// addSnapshotListener: se ejecuta cada vez que los datos cambian en la nube</span>
        coleccion
            .<span class="fn">orderBy</span>(<span class="str">"fechaMs"</span>, com.google.firebase.firestore.<span class="cls">Query</span>.<span class="cls">Direction</span>.DESCENDING)
            .<span class="fn">addSnapshotListener</span> { snapshot, exception <span class="op">-&gt;</span>
                <span class="kw">if</span> (exception != <span class="kw">null</span>) {
                    _error.value = exception.message
                    <span class="kw">return</span><span class="an">@addSnapshotListener</span>
                }
                <span class="kw">val</span> lista = snapshot?.documents<span class="op">?.</span><span class="fn">mapNotNull</span> { doc <span class="op">-&gt;</span>
                    doc.<span class="fn">toObject</span>&lt;<span class="cls">Nota</span>&gt;()<span class="op">?.</span><span class="fn">copy</span>(id = doc.id)
                } <span class="op">?:</span> <span class="fn">emptyList</span>()
                _notas.value = lista
            }
    }

    <span class="kw">fun</span> <span class="fn">insertar</span>(nota: <span class="cls">Nota</span>) {
        <span class="kw">val</span> datos = <span class="fn">hashMapOf</span>(
            <span class="str">"titulo"</span>    to nota.titulo,
            <span class="str">"contenido"</span> to nota.contenido,
            <span class="str">"fechaMs"</span>   to <span class="cls">System</span>.<span class="fn">currentTimeMillis</span>()
        )
        coleccion.<span class="fn">add</span>(datos)
            .<span class="fn">addOnFailureListener</span> { e <span class="op">-&gt;</span> _error.value = e.message }
    }

    <span class="kw">fun</span> <span class="fn">actualizar</span>(nota: <span class="cls">Nota</span>) {
        <span class="kw">val</span> datos = <span class="fn">mapOf</span>(
            <span class="str">"titulo"</span>    to nota.titulo,
            <span class="str">"contenido"</span> to nota.contenido
        )
        coleccion.<span class="fn">document</span>(nota.id).<span class="fn">update</span>(datos)
            .<span class="fn">addOnFailureListener</span> { e <span class="op">-&gt;</span> _error.value = e.message }
    }

    <span class="kw">fun</span> <span class="fn">eliminar</span>(nota: <span class="cls">Nota</span>) {
        coleccion.<span class="fn">document</span>(nota.id).<span class="fn">delete</span>()
            .<span class="fn">addOnFailureListener</span> { e <span class="op">-&gt;</span> _error.value = e.message }
    }
}</pre></div>
    </div>
    <div class="alert alert-orange">
      <span class="alert-icon">💡</span>
      <p><strong>addSnapshotListener:</strong> A diferencia de Room donde LiveData se actualiza solo, en Firestore se registra un listener que recibe automáticamente los cambios en tiempo real — incluyendo cambios hechos desde otro dispositivo o directamente desde la consola de Firebase.</p>
    </div>
  </div>

  <!-- Código 5: NotaViewModel.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 5 — NotaViewModel.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaViewModel.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.lifecycle.LiveData
<span class="kw">import</span> androidx.lifecycle.ViewModel

<span class="kw">class</span> <span class="cls">NotaViewModel</span> : <span class="cls">ViewModel</span>() {

    <span class="cm">// ViewModel simple (no AndroidViewModel) — Firebase no necesita contexto</span>
    <span class="kw">private val</span> repository = <span class="cls">NotaRepository</span>()

    <span class="kw">val</span> notas: <span class="cls">LiveData</span>&lt;<span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;&gt; = repository.notas
    <span class="kw">val</span> error: <span class="cls">LiveData</span>&lt;<span class="cls">String</span>?&gt;       = repository.error

    <span class="kw">fun</span> <span class="fn">insertar</span>(titulo: <span class="cls">String</span>, contenido: <span class="cls">String</span>) {
        <span class="kw">if</span> (titulo.<span class="fn">isBlank</span>()) <span class="kw">return</span>
        repository.<span class="fn">insertar</span>(<span class="cls">Nota</span>(titulo = titulo, contenido = contenido))
    }

    <span class="kw">fun</span> <span class="fn">actualizar</span>(nota: <span class="cls">Nota</span>) = repository.<span class="fn">actualizar</span>(nota)

    <span class="kw">fun</span> <span class="fn">eliminar</span>(nota: <span class="cls">Nota</span>) = repository.<span class="fn">eliminar</span>(nota)
}</pre></div>
    </div>
  </div>

  <!-- Código 6: AndroidManifest -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 6 — AndroidManifest.xml</div>
    <p>Firebase requiere permiso de internet en el Manifest.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">AndroidManifest.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;manifest</span> <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span><span class="tag">&gt;</span>

    <span class="cm">&lt;!-- Permiso de internet obligatorio para Firebase --&gt;</span>
    <span class="tag">&lt;uses-permission</span> <span class="attr">android:name</span>=<span class="val">"android.permission.INTERNET"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;application</span>
        <span class="attr">android:allowBackup</span>=<span class="val">"true"</span>
        <span class="attr">android:theme</span>=<span class="val">"@style/Theme.AppCompat.Light.DarkActionBar"</span><span class="tag">&gt;</span>

        <span class="tag">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".NotasActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"true"</span><span class="tag">&gt;</span>
            <span class="tag">&lt;intent-filter&gt;</span>
                <span class="tag">&lt;action</span> <span class="attr">android:name</span>=<span class="val">"android.intent.action.MAIN"</span> <span class="tag">/&gt;</span>
                <span class="tag">&lt;category</span> <span class="attr">android:name</span>=<span class="val">"android.intent.category.LAUNCHER"</span> <span class="tag">/&gt;</span>
            <span class="tag">&lt;/intent-filter&gt;</span>
        <span class="tag">&lt;/activity&gt;</span>

        <span class="tag">&lt;activity</span>
            <span class="attr">android:name</span>=<span class="val">".EditarNotaActivity"</span>
            <span class="attr">android:exported</span>=<span class="val">"false"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;/application&gt;</span>
<span class="tag">&lt;/manifest&gt;</span></pre></div>
    </div>
  </div>

  <!-- ══════════════ CLASE 2 ══════════════ -->
  <hr class="divider">

  <div class="clase-header" style="margin-top:56px">
    <span class="clase-badge">Clase 02</span>
    <div class="clase-title">UI completa y <span>tiempo real</span></div>
    <div class="clase-line"></div>
  </div>

  <div class="objetivo">
    <strong>🎯 Objetivo</strong>
    <p>Construir la UI con RecyclerView y la Activity de edición. Demostrar la sincronización en tiempo real abriendo la consola de Firebase en paralelo con el emulador.</p>
  </div>

  <!-- Código 7: activity_notas.xml -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 7 — activity_notas.xml</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_notas.xml</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="tag">&lt;?xml</span> <span class="attr">version</span>=<span class="val">"1.0"</span> <span class="attr">encoding</span>=<span class="val">"utf-8"</span><span class="tag">?&gt;</span>
<span class="tag">&lt;androidx.constraintlayout.widget.ConstraintLayout</span>
    <span class="attr">xmlns:android</span>=<span class="val">"http://schemas.android.com/apk/res/android"</span>
    <span class="attr">xmlns:app</span>=<span class="val">"http://schemas.android.com/apk/res-auto"</span>
    <span class="attr">android:layout_width</span>=<span class="val">"match_parent"</span>
    <span class="attr">android:layout_height</span>=<span class="val">"match_parent"</span><span class="tag">&gt;</span>

    <span class="tag">&lt;TextView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/tvEstadoConexion"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:textSize</span>=<span class="val">"12sp"</span>
        <span class="attr">android:textColor</span>=<span class="val">"#888"</span>
        <span class="attr">android:text</span>=<span class="val">"🔄 Sincronizando..."</span>
        <span class="attr">app:layout_constraintTop_toTopOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;androidx.recyclerview.widget.RecyclerView</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/recyclerNotas"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"0dp"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"0dp"</span>
        <span class="attr">android:padding</span>=<span class="val">"8dp"</span>
        <span class="attr">android:clipToPadding</span>=<span class="val">"false"</span>
        <span class="attr">app:layout_constraintTop_toBottomOf</span>=<span class="val">"@id/tvEstadoConexion"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintStart_toStartOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

    <span class="tag">&lt;com.google.android.material.floatingactionbutton.FloatingActionButton</span>
        <span class="attr">android:id</span>=<span class="val">"@+id/fabNuevaNota"</span>
        <span class="attr">android:layout_width</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_height</span>=<span class="val">"wrap_content"</span>
        <span class="attr">android:layout_margin</span>=<span class="val">"24dp"</span>
        <span class="attr">android:src</span>=<span class="val">"@android:drawable/ic_input_add"</span>
        <span class="attr">android:contentDescription</span>=<span class="val">"Nueva nota"</span>
        <span class="attr">app:layout_constraintBottom_toBottomOf</span>=<span class="val">"parent"</span>
        <span class="attr">app:layout_constraintEnd_toEndOf</span>=<span class="val">"parent"</span> <span class="tag">/&gt;</span>

<span class="tag">&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 8: item_nota.xml — igual que Room, reutilizable -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 8 — item_nota.xml</div>
    <p>El layout del ítem es idéntico al de la Opción A (Room). El adapter también es casi igual — la única diferencia es que el id ahora es un <code>String</code> en lugar de un <code>Int</code>.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/item_nota.xml — igual al de la Opción A</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="cm">&lt;!-- Mismo layout que en Room: tvTituloNota, tvContenidoNota, btnEliminarNota --&gt;
&lt;!-- Ver Código 9 de la Opción A para el XML completo --&gt;</span></pre></div>
    </div>
  </div>

  <!-- Código 9: NotaAdapter.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 9 — NotaAdapter.kt</div>
    <p>Igual al de la Opción A pero el id de <code>Nota</code> ahora es <code>String</code> — no hay que cambiar nada más en el adapter.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotaAdapter.kt — igual estructura que Opción A</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="cm">// Misma estructura que el NotaAdapter de la Opción A.
// Cambio: el tipo del id en Nota es String en lugar de Int.
// El adapter en sí no necesita modificaciones por ese cambio.</span>

<span class="kw">class</span> <span class="cls">NotaAdapter</span>(
    <span class="kw">private var</span> notas: <span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt; = <span class="fn">emptyList</span>(),
    <span class="kw">private val</span> onClick:    (<span class="cls">Nota</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>,
    <span class="kw">private val</span> onEliminar: (<span class="cls">Nota</span>) <span class="op">-&gt;</span> <span class="cls">Unit</span>
) : <span class="cls">RecyclerView</span>.<span class="cls">Adapter</span>&lt;<span class="cls">NotaAdapter</span>.<span class="cls">NotaViewHolder</span>&gt;() {
    <span class="cm">// ... implementación idéntica al Código 10 de la Opción A ...</span>

    <span class="kw">fun</span> <span class="fn">actualizarLista</span>(nuevas: <span class="cls">List</span>&lt;<span class="cls">Nota</span>&gt;) {
        notas = nuevas
        <span class="fn">notifyDataSetChanged</span>()
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 10: NotasActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 10 — NotasActivity.kt</div>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">NotasActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.content.Intent
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.TextView
<span class="kw">import</span> android.widget.Toast
<span class="kw">import</span> androidx.activity.result.contract.ActivityResultContracts
<span class="kw">import</span> androidx.activity.viewModels
<span class="kw">import</span> androidx.recyclerview.widget.LinearLayoutManager
<span class="kw">import</span> androidx.recyclerview.widget.RecyclerView
<span class="kw">import</span> com.google.android.material.floatingactionbutton.FloatingActionButton

<span class="kw">class</span> <span class="cls">NotasActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">private val</span> viewModel: <span class="cls">NotaViewModel</span> <span class="kw">by</span> <span class="fn">viewModels</span>()

    <span class="kw">private val</span> editarLauncher = <span class="fn">registerForActivityResult</span>(
        <span class="cls">ActivityResultContracts</span>.<span class="cls">StartActivityForResult</span>()
    ) { result <span class="op">-&gt;</span>
        <span class="kw">if</span> (result.resultCode == <span class="cls">RESULT_OK</span>) {
            <span class="kw">val</span> titulo    = result.data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"TITULO"</span>)    <span class="op">?:</span> <span class="kw">return</span><span class="an">@registerForActivityResult</span>
            <span class="kw">val</span> contenido = result.data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"CONTENIDO"</span>) <span class="op">?:</span> <span class="str">""</span>
            <span class="kw">val</span> id        = result.data<span class="op">?.</span><span class="fn">getStringExtra</span>(<span class="str">"ID"</span>) <span class="op">?:</span> <span class="str">""</span>

            <span class="kw">if</span> (id.<span class="fn">isEmpty</span>()) {
                viewModel.<span class="fn">insertar</span>(titulo, contenido)
            } <span class="kw">else</span> {
                viewModel.<span class="fn">actualizar</span>(<span class="cls">Nota</span>(id = id, titulo = titulo, contenido = contenido))
            }
        }
    }

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_notas)

        <span class="kw">val</span> tvEstado = <span class="fn">findViewById</span>&lt;<span class="cls">TextView</span>&gt;(<span class="cls">R</span>.id.tvEstadoConexion)

        <span class="kw">val</span> adapter = <span class="cls">NotaAdapter</span>(
            onClick    = { nota <span class="op">-&gt;</span> <span class="fn">abrirEditor</span>(nota) },
            onEliminar = { nota <span class="op">-&gt;</span> viewModel.<span class="fn">eliminar</span>(nota) }
        )

        <span class="fn">findViewById</span>&lt;<span class="cls">RecyclerView</span>&gt;(<span class="cls">R</span>.id.recyclerNotas).<span class="fn">apply</span> {
            layoutManager = <span class="cls">LinearLayoutManager</span>(<span class="kw">this</span><span class="an">@NotasActivity</span>)
            this.adapter  = adapter
        }

        <span class="cm">// Observer: la lista se actualiza automáticamente cuando Firestore cambia</span>
        viewModel.notas.<span class="fn">observe</span>(<span class="kw">this</span>) { lista <span class="op">-&gt;</span>
            adapter.<span class="fn">actualizarLista</span>(lista)
            tvEstado.text = <span class="str">"☁️ ${lista.size} notas sincronizadas"</span>
        }

        <span class="cm">// Observer de errores</span>
        viewModel.error.<span class="fn">observe</span>(<span class="kw">this</span>) { mensaje <span class="op">-&gt;</span>
            mensaje<span class="op">?.</span><span class="fn">let</span> {
                <span class="cls">Toast</span>.<span class="fn">makeText</span>(<span class="kw">this</span>, <span class="str">"Error: $it"</span>, <span class="cls">Toast</span>.LENGTH_LONG).<span class="fn">show</span>()
            }
        }

        <span class="fn">findViewById</span>&lt;<span class="cls">FloatingActionButton</span>&gt;(<span class="cls">R</span>.id.fabNuevaNota).<span class="fn">setOnClickListener</span> {
            <span class="fn">abrirEditor</span>(<span class="kw">null</span>)
        }
    }

    <span class="kw">private fun</span> <span class="fn">abrirEditor</span>(nota: <span class="cls">Nota</span>?) {
        <span class="kw">val</span> intent = <span class="cls">Intent</span>(<span class="kw">this</span>, <span class="cls">EditarNotaActivity</span>::<span class="kw">class</span>.java)
        nota<span class="op">?.</span><span class="fn">let</span> {
            intent.<span class="fn">putExtra</span>(<span class="str">"ID"</span>,        it.id)
            intent.<span class="fn">putExtra</span>(<span class="str">"TITULO"</span>,    it.titulo)
            intent.<span class="fn">putExtra</span>(<span class="str">"CONTENIDO"</span>, it.contenido)
        }
        editarLauncher.<span class="fn">launch</span>(intent)
    }
}</pre></div>
    </div>
  </div>

  <!-- Código 11: activity_editar_nota.xml + EditarNotaActivity.kt -->
  <div class="section">
    <div class="section-title"><span class="tag xml">XML</span> Código 11 — activity_editar_nota.xml</div>
    <p>Idéntico al de la Opción A. Consultar el Código 12 de la Opción A para el XML completo.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-xml">XML</span>
        <span class="code-filename">res/layout/activity_editar_nota.xml — igual al de la Opción A</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="cm">&lt;!-- Mismo layout: etTituloNota, etContenidoNota, btnGuardarNota --&gt;
&lt;!-- Ver Código 12 de la Opción A para el XML completo --&gt;</span></pre></div>
    </div>
  </div>

  <div class="section">
    <div class="section-title"><span class="tag kotlin">Kotlin</span> Código 12 — EditarNotaActivity.kt</div>
    <p>La única diferencia con la Opción A es que el ID del Intent es <code>String</code> en lugar de <code>Int</code>.</p>
    <div class="code-block">
      <div class="code-header">
        <span class="code-lang lang-kotlin">Kotlin</span>
        <span class="code-filename">EditarNotaActivity.kt</span>
      </div>
      <div class="code-body"><pre style="background:transparent"><span class="kw">import</span> androidx.appcompat.app.AppCompatActivity
<span class="kw">import</span> android.app.Activity
<span class="kw">import</span> android.os.Bundle
<span class="kw">import</span> android.widget.Button
<span class="kw">import</span> android.widget.EditText

<span class="kw">class</span> <span class="cls">EditarNotaActivity</span> : <span class="cls">AppCompatActivity</span>() {

    <span class="kw">override fun</span> <span class="fn">onCreate</span>(savedInstanceState: <span class="cls">Bundle</span>?) {
        <span class="kw">super</span>.<span class="fn">onCreate</span>(savedInstanceState)
        <span class="fn">setContentView</span>(<span class="cls">R</span>.layout.activity_editar_nota)

        <span class="kw">val</span> etTitulo    = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etTituloNota)
        <span class="kw">val</span> etContenido = <span class="fn">findViewById</span>&lt;<span class="cls">EditText</span>&gt;(<span class="cls">R</span>.id.etContenidoNota)
        <span class="kw">val</span> btnGuardar  = <span class="fn">findViewById</span>&lt;<span class="cls">Button</span>&gt;(<span class="cls">R</span>.id.btnGuardarNota)

        <span class="cm">// ID es String en Firebase (a diferencia del Int de Room)</span>
        <span class="kw">val</span> idExistente = intent.<span class="fn">getStringExtra</span>(<span class="str">"ID"</span>) <span class="op">?:</span> <span class="str">""</span>
        intent.<span class="fn">getStringExtra</span>(<span class="str">"TITULO"</span>)<span class="op">?.</span><span class="fn">let</span> { etTitulo.<span class="fn">setText</span>(it) }
        intent.<span class="fn">getStringExtra</span>(<span class="str">"CONTENIDO"</span>)<span class="op">?.</span><span class="fn">let</span> { etContenido.<span class="fn">setText</span>(it) }

        btnGuardar.<span class="fn">setOnClickListener</span> {
            <span class="kw">val</span> titulo = etTitulo.text.toString().<span class="fn">trim</span>()
            <span class="kw">if</span> (titulo.<span class="fn">isEmpty</span>()) {
                etTitulo.error = <span class="str">"El título no puede estar vacío"</span>
                <span class="kw">return</span><span class="an">@setOnClickListener</span>
            }
            <span class="kw">val</span> resultado = android.content.<span class="cls">Intent</span>()
            resultado.<span class="fn">putExtra</span>(<span class="str">"TITULO"</span>,    titulo)
            resultado.<span class="fn">putExtra</span>(<span class="str">"CONTENIDO"</span>, etContenido.text.toString())
            resultado.<span class="fn">putExtra</span>(<span class="str">"ID"</span>,        idExistente)  <span class="cm">// String, no Int</span>
            <span class="fn">setResult</span>(<span class="cls">Activity</span>.RESULT_OK, resultado)
            <span class="fn">finish</span>()
        }
    }
}</pre></div>
    </div>
    <div class="alert alert-green">
      <span class="alert-icon">🔥</span>
      <p><strong>Demo impactante para clase:</strong> Abrir la Firebase Console en el navegador mientras corre el emulador. Agregar un documento directamente desde la consola y ver cómo aparece instantáneamente en la app sin recargar. Eso es tiempo real.</p>
    </div>
  </div>

  <!-- TAREA -->
  <div class="tarea">
    <div class="tarea-badge">📝 Práctica — Tarea</div>
    <h2>App: Lista de Deseos Compartida</h2>
    <p class="tarea-desc">Construye una app de lista de deseos que almacene datos en Firebase Firestore, visible y editable en tiempo real desde múltiples dispositivos.</p>
    <div class="reqs">
      <div class="req"><div class="req-num">1</div><div>Conectar el proyecto a Firebase y configurar Firestore. Crear la colección <strong>"deseos"</strong> con documentos que tengan los campos: titulo, descripcion, precio (Number) y obtenido (Boolean).</div></div>
      <div class="req"><div class="req-num">2</div><div>Implementar el patrón <strong>Repository → ViewModel → Activity</strong> con <code>addSnapshotListener</code> para escuchar cambios en tiempo real.</div></div>
      <div class="req"><div class="req-num">3</div><div>La UI muestra un <strong>RecyclerView</strong> con los ítems y un FAB para agregar. Los ítems marcados como "obtenidos" deben mostrarse con un estilo visual diferente (tachado o diferente color).</div></div>
      <div class="req"><div class="req-num">4</div><div>Al hacer clic en un ítem navegar a una Activity de edición que permita modificar todos los campos y guardar los cambios en Firestore con <code>document(id).update(...)</code>.</div></div>
      <div class="req"><div class="req-num">5</div><div>Manejar y mostrar los errores de Firestore con un <code>Toast</code> — usar el LiveData de error del Repository.</div></div>
      <div class="req"><div class="req-num star">⭐</div><div><strong>Punto extra:</strong> Agregar un <strong>filtro</strong> con dos botones: "Todos" y "Pendientes". Usar una segunda query de Firestore (<code>.whereEqualTo("obtenido", false)</code>) para el filtro de pendientes.</div></div>
    </div>
    <div class="entrega">
      <strong>📦 Entrega</strong>
      <p>Captura de la app Y de la consola de Firebase mostrando los documentos.</p>
    </div>
  </div>

</div>
</body>
</html>
