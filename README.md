<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cuaderno de Siniestros en vivo - Flota Aquaservice</title>
<style>
  :root{
    --navy:#0B2447;
    --navy-2:#132f5c;
    --blue:#00A6E7;
    --coral:#EB235A;
    --paper:#F6F4EF;
    --ink:#1A2233;
    --ink-soft:#5B6472;
    --line:#D8D3C7;
    --ok:#1E7145;
    --ok-bg:#E4F3EA;
    --bad:#B00020;
    --bad-bg:#FBE6EA;
    --warn-bg:#FFF3D6;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    background:var(--paper);
    color:var(--ink);
    font-family:"Inter","Segoe UI",system-ui,-apple-system,sans-serif;
    font-size:14px;
    line-height:1.45;
  }
  .headwrap{
    background:var(--navy);
    color:#fff;
    padding:22px 28px 20px;
    background-image:
      repeating-linear-gradient(90deg, rgba(255,255,255,0.035) 0 1px, transparent 1px 64px);
  }
  .headrow{
    display:flex;
    justify-content:space-between;
    align-items:flex-end;
    flex-wrap:wrap;
    gap:14px;
    max-width:1180px;
    margin:0 auto;
  }
  .brand-label{
    font-size:11px;
    letter-spacing:.04em;
    color:var(--blue);
    font-weight:600;
    margin-bottom:6px;
  }
  h1{
    font-family:"Archivo","Inter",sans-serif;
    font-weight:800;
    font-size:28px;
    margin:0;
    letter-spacing:-0.01em;
  }
  .sub{color:#B9C4D6;font-size:13px;margin-top:4px;}
  .mode-pill{
    display:flex;align-items:center;gap:8px;
    background:rgba(255,255,255,0.08);
    border:1px solid rgba(255,255,255,0.18);
    padding:8px 14px;border-radius:3px;font-size:12.5px;color:#DCE4EF;
  }
  .dot{width:7px;height:7px;border-radius:50%;background:#F2C94C;flex:none;}
  .dot.live{background:#3ECF6E;}
  .dot.error{background:var(--coral);}

  .stats{
    max-width:1180px;margin:-26px auto 0;padding:0 28px;
    display:grid;grid-template-columns:repeat(4,1fr);gap:1px;
    background:var(--line);border:1px solid var(--line);
  }
  .stat{background:#fff;padding:16px 18px;}
  .stat .num{font-family:"Archivo","Inter",sans-serif;font-weight:800;font-size:30px;color:var(--navy);line-height:1;}
  .stat .num.coral{color:var(--coral);}
  .stat .num.ok{color:var(--ok);}
  .stat .label{margin-top:6px;font-size:12px;color:var(--ink-soft);}

  .layout{
    max-width:1180px;margin:26px auto 60px;padding:0 28px;
    display:grid;grid-template-columns:340px 1fr;gap:24px;align-items:start;
  }
  @media (max-width:860px){.layout{grid-template-columns:1fr;}}

  .panel{background:#fff;border:1px solid var(--line);}
  .panel-head{padding:14px 18px;border-bottom:1px solid var(--line);display:flex;align-items:center;justify-content:space-between;}
  .panel-head h2{font-size:14px;margin:0;font-weight:700;color:var(--navy);}
  .panel-body{padding:16px 18px 18px;}

  label{display:block;font-size:11.5px;color:var(--ink-soft);margin:12px 0 4px;}
  label:first-child{margin-top:0;}
  input, select, textarea{
    width:100%;padding:8px 9px;border:1px solid var(--line);background:#FBFAF7;
    font-family:inherit;font-size:13.5px;color:var(--ink);border-radius:2px;
  }
  input:focus, select:focus, textarea:focus{outline:none;border-color:var(--blue);background:#fff;}
  textarea{resize:vertical;min-height:52px;}
  .row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}

  button.primary{
    margin-top:16px;width:100%;background:var(--navy);color:#fff;border:none;
    padding:11px;font-size:13.5px;font-weight:700;cursor:pointer;border-radius:2px;
  }
  button.primary:hover{background:var(--navy-2);}
  button.primary:disabled{background:#9AA3AF;cursor:not-allowed;}
  button.ghost{
    margin-top:8px;width:100%;background:transparent;color:var(--navy);
    border:1px solid var(--line);padding:8px;font-size:12.5px;font-weight:600;
    cursor:pointer;border-radius:2px;
  }

  .hint{margin-top:10px;font-size:11.5px;color:var(--ink-soft);border-left:2px solid var(--blue);padding-left:8px;}
  .hint.warn{border-left-color:var(--coral);color:var(--bad);}

  table{width:100%;border-collapse:collapse;font-size:12.8px;}
  th{text-align:left;font-size:11px;color:var(--ink-soft);font-weight:600;padding:9px 10px;border-bottom:1px solid var(--line);white-space:nowrap;}
  td{padding:9px 10px;border-bottom:1px solid var(--line);vertical-align:top;}
  tr:last-child td{border-bottom:none;}
  .badge{display:inline-block;padding:2px 7px;border-radius:2px;font-size:11px;font-weight:700;}
  .badge.ok{background:var(--ok-bg);color:var(--ok);}
  .badge.bad{background:var(--bad-bg);color:var(--bad);}
  .rowwarn{background:var(--warn-bg);}
  .empty{padding:34px 18px;text-align:center;color:var(--ink-soft);font-size:13px;}
  .deleg-bars{padding:16px 18px 4px;}
  .barline{display:flex;align-items:center;gap:10px;margin-bottom:10px;font-size:12.5px;}
  .barline .lbl{width:70px;flex:none;color:var(--ink-soft);}
  .barline .track{flex:1;background:#EFEDE6;height:16px;position:relative;}
  .barline .fill{height:100%;background:var(--blue);}
  .barline .fill.coral{background:var(--coral);}
  .barline .n{width:24px;text-align:right;font-weight:700;color:var(--navy);}
  .footer-note{max-width:1180px;margin:0 auto 40px;padding:0 28px;font-size:11.5px;color:var(--ink-soft);}
  ::placeholder{color:#9AA3AF;}
  .setup-banner{
    max-width:1180px;margin:0 auto;padding:14px 28px;background:var(--bad-bg);
    color:var(--bad);font-size:13px;border-bottom:1px solid var(--line);
  }
</style>
</head>
<body>

<div class="setup-banner" id="setup_banner" style="display:none;">
  Falta configurar la conexion: abre este archivo con un editor de texto, busca <code>SCRIPT_URL</code> al final del todo, y pega ahi la URL de tu Apps Script (termina en /exec).
</div>

<div class="headwrap">
  <div class="headrow">
    <div>
      <div class="brand-label">AQUASERVICE · CONTROL DE FLOTA</div>
      <h1>Cuaderno de Siniestros</h1>
      <div class="sub">Delegación 113 (Cádiz) y 126 (Chiclana) · en vivo con todo el equipo</div>
    </div>
    <div class="mode-pill"><span class="dot" id="live_dot"></span> <span id="live_text">Conectando...</span></div>
  </div>
</div>

<div class="stats" id="stats"></div>

<div class="layout">

  <div class="panel">
    <div class="panel-head"><h2>Registrar siniestro</h2></div>
    <div class="panel-body">
      <label>Tu nombre (jefe de equipo)</label>
      <input type="text" id="f_autor" placeholder="Ej: Jaime Castro">

      <label>Fecha y hora del siniestro</label>
      <input type="datetime-local" id="f_fecha">

      <div class="row2">
        <div>
          <label>Delegación</label>
          <select id="f_deleg">
            <option value="113">113 · Cádiz</option>
            <option value="126">126 · Chiclana</option>
          </select>
        </div>
        <div>
          <label>Matrícula</label>
          <input type="text" id="f_matricula" placeholder="1234 ABC">
        </div>
      </div>

      <label>Repartidor implicado</label>
      <input type="text" id="f_repartidor" placeholder="Nombre y apellidos">

      <label>Tipo de siniestro</label>
      <select id="f_tipo">
        <option>Choque</option>
        <option>Daño material</option>
        <option>Avería por mal uso</option>
        <option>Robo</option>
        <option>Otro</option>
      </select>

      <label>Descripción breve</label>
      <textarea id="f_desc" placeholder="Qué ha ocurrido, en pocas líneas"></textarea>

      <div class="row2">
        <div>
          <label>Parte amistoso/policial</label>
          <select id="f_parte"><option>No</option><option>Sí</option></select>
        </div>
        <div>
          <label>Fotos adjuntas</label>
          <select id="f_fotos"><option>No</option><option>Sí</option></select>
        </div>
      </div>

      <label>Estado del vehículo</label>
      <select id="f_estado">
        <option>Circula con normalidad</option>
        <option>Inmovilizado</option>
        <option>En taller</option>
      </select>

      <div class="row2">
        <div>
          <label>Correo enviado a Flota</label>
          <select id="f_enviado"><option>No</option><option>Sí</option></select>
        </div>
        <div>
          <label>Fecha/hora de envío</label>
          <input type="datetime-local" id="f_fechaenvio">
        </div>
      </div>

      <label>CC al responsable de delegación</label>
      <select id="f_cc"><option>No</option><option>Sí</option></select>

      <button class="primary" id="btn_add">Guardar y avisar a todos</button>
      <div class="hint" id="form_hint">Se calculan solos los días hasta el envío y si entra en el margen de 3 días.</div>
    </div>
  </div>

  <div>
    <div class="panel">
      <div class="panel-head">
        <h2>Registro de siniestros</h2>
        <span id="count_pill" style="font-size:11.5px;color:var(--ink-soft);"></span>
      </div>
      <div style="overflow-x:auto;">
        <table id="tbl">
          <thead>
            <tr>
              <th>Fecha</th><th>Deleg.</th><th>Matrícula</th><th>Repartidor</th>
              <th>Tipo</th><th>Correo</th><th>CC</th><th>Plazo</th><th>Estado veh.</th><th>Reportado por</th><th></th>
            </tr>
          </thead>
          <tbody id="tbody"></tbody>
        </table>
        <div class="empty" id="empty_msg">Todavía no hay siniestros registrados. Usa el formulario de la izquierda para añadir el primero.</div>
      </div>
    </div>

    <div class="panel" style="margin-top:20px;">
      <div class="panel-head"><h2>Siniestros por delegación</h2></div>
      <div class="deleg-bars" id="bars"></div>
    </div>
  </div>

</div>

<div class="footer-note" id="footer_note">
  Los datos se sincronizan automáticamente cada 20 segundos entre todos los que tengan este enlace abierto.
</div>

<script>
// ============================================================
// PEGA AQUI LA URL DE TU APPS SCRIPT (termina en /exec)
// ============================================================
const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbwRkULB0KB6FSvEImZ249M3eG7TMQEnDpKAHETYtx4MyBwwDOCd1DNrx10WUi1NeWvg/exec";
const POLL_MS = 20000;

let entries = [];
let liveOk = false;

function jsonp(url, params){
  return new Promise((resolve, reject)=>{
    const cbName = "cb_" + Date.now() + "_" + Math.floor(Math.random()*100000);
    const timeout = setTimeout(()=>{
      cleanup();
      reject(new Error("timeout"));
    }, 12000);
    function cleanup(){
      clearTimeout(timeout);
      delete window[cbName];
      if(script.parentNode) script.parentNode.removeChild(script);
    }
    window[cbName] = function(data){
      cleanup();
      resolve(data);
    };
    const qp = new URLSearchParams(Object.assign({}, params, {callback:cbName}));
    const script = document.createElement("script");
    script.src = url + "?" + qp.toString();
    script.onerror = ()=>{ cleanup(); reject(new Error("network")); };
    document.body.appendChild(script);
  });
}

function setLiveStatus(ok, msg){
  liveOk = ok;
  document.getElementById("live_dot").className = "dot " + (ok ? "live" : "error");
  document.getElementById("live_text").textContent = msg;
}

async function loadFromSheet(){
  if(SCRIPT_URL.indexOf("PEGA_AQUI") === 0){
    document.getElementById("setup_banner").style.display = "block";
    setLiveStatus(false, "Sin configurar");
    return;
  }
  try{
    const data = await jsonp(SCRIPT_URL, {});
    entries = data.rows || [];
    setLiveStatus(true, "En vivo · actualizado ahora");
    render();
  }catch(e){
    setLiveStatus(false, "Sin conexión, reintentando...");
  }
}

function fmtDate(iso){
  if(!iso) return "—";
  const d = new Date(iso);
  if(isNaN(d)) return iso;
  return d.toLocaleDateString("es-ES",{day:"2-digit",month:"2-digit",year:"2-digit"}) + " " +
         d.toLocaleTimeString("es-ES",{hour:"2-digit",minute:"2-digit"});
}

function computePlazo(e){
  if(e.enviado !== "Sí" || !e.fecha || !e.fechaenvio) return null;
  const dias = (new Date(e.fechaenvio) - new Date(e.fecha)) / 86400000;
  if(isNaN(dias)) return null;
  return { dias, enPlazo: dias <= 3 && dias >= 0 };
}

function render(){
  const total = entries.length;
  const enviados = entries.filter(e=>e.enviado==="Sí").length;
  const conCC = entries.filter(e=>e.enviado==="Sí" && e.cc==="Sí").length;
  const enPlazo = entries.filter(e=>{const p=computePlazo(e); return p && p.enPlazo;}).length;
  const pctOk = total ? Math.round((conCC/total)*100) : 0;

  document.getElementById("stats").innerHTML = `
    <div class="stat"><div class="num">${total}</div><div class="label">Siniestros registrados</div></div>
    <div class="stat"><div class="num">${enviados}</div><div class="label">Correos enviados a Flota</div></div>
    <div class="stat"><div class="num ${pctOk>=80?'ok':'coral'}">${pctOk}%</div><div class="label">Enviados con CC correcto</div></div>
    <div class="stat"><div class="num">${enPlazo}</div><div class="label">Enviados en plazo (≤3 días)</div></div>
  `;

  document.getElementById("count_pill").textContent = total ? `${total} registro${total>1?'s':''}` : "";

  const tbody = document.getElementById("tbody");
  const emptyMsg = document.getElementById("empty_msg");
  if(!total){
    tbody.innerHTML = "";
    emptyMsg.style.display = "block";
  }else{
    emptyMsg.style.display = "none";
    tbody.innerHTML = entries.slice().reverse().map(e=>{
      const p = computePlazo(e);
      const warn = e.enviado === "Sí" && e.cc !== "Sí";
      const plazoCell = e.enviado !== "Sí" ? "—" :
        (p ? `<span class="badge ${p.enPlazo?'ok':'bad'}">${p.enPlazo?'En plazo':'Fuera de plazo'}</span>` : "—");
      return `<tr class="${warn?'rowwarn':''}">
        <td>${fmtDate(e.fecha)}</td>
        <td>${e.deleg||"—"}</td>
        <td>${e.matricula||"—"}</td>
        <td>${e.repartidor||"—"}</td>
        <td>${e.tipo||"—"}</td>
        <td><span class="badge ${e.enviado==='Sí'?'ok':'bad'}">${e.enviado||"No"}</span></td>
        <td><span class="badge ${e.cc==='Sí'?'ok':'bad'}">${e.cc||"No"}</span></td>
        <td>${plazoCell}</td>
        <td>${e.estado||"—"}</td>
        <td>${e.autor||"—"}</td>
        <td><a href="#" data-row="${e._row}" class="del" style="color:var(--ink-soft);text-decoration:none;">✕</a></td>
      </tr>`;
    }).join("");
  }

  const c113 = entries.filter(e=>String(e.deleg)==="113").length;
  const c126 = entries.filter(e=>String(e.deleg)==="126").length;
  const max = Math.max(c113, c126, 1);
  document.getElementById("bars").innerHTML = `
    <div class="barline"><div class="lbl">113 · Cádiz</div><div class="track"><div class="fill" style="width:${(c113/max)*100}%"></div></div><div class="n">${c113}</div></div>
    <div class="barline"><div class="lbl">126 · Chiclana</div><div class="track"><div class="fill coral" style="width:${(c126/max)*100}%"></div></div><div class="n">${c126}</div></div>
  `;

  document.querySelectorAll(".del").forEach(a=>{
    a.addEventListener("click", async (ev)=>{
      ev.preventDefault();
      const rowNum = ev.target.getAttribute("data-row");
      if(!confirm("¿Borrar este siniestro para todo el equipo?")) return;
      try{
        await jsonp(SCRIPT_URL, {action:"delete", row: rowNum});
        await loadFromSheet();
      }catch(err){
        alert("No se pudo borrar, revisa la conexión.");
      }
    });
  });
}

document.getElementById("btn_add").addEventListener("click", async ()=>{
  const fecha = document.getElementById("f_fecha").value;
  if(!fecha){ document.getElementById("f_fecha").style.borderColor = "var(--bad)"; return; }
  if(SCRIPT_URL.indexOf("PEGA_AQUI") === 0){
    alert("Este cuaderno todavía no está conectado al backend en vivo. Configura SCRIPT_URL primero.");
    return;
  }

  const btn = document.getElementById("btn_add");
  btn.disabled = true;
  btn.textContent = "Guardando...";

  const entry = {
    autor: document.getElementById("f_autor").value.trim(),
    fecha,
    deleg: document.getElementById("f_deleg").value,
    matricula: document.getElementById("f_matricula").value.trim(),
    repartidor: document.getElementById("f_repartidor").value.trim(),
    tipo: document.getElementById("f_tipo").value,
    desc: document.getElementById("f_desc").value.trim(),
    parte: document.getElementById("f_parte").value,
    fotos: document.getElementById("f_fotos").value,
    estado: document.getElementById("f_estado").value,
    enviado: document.getElementById("f_enviado").value,
    fechaenvio: document.getElementById("f_fechaenvio").value,
    cc: document.getElementById("f_cc").value,
  };

  try{
    await jsonp(SCRIPT_URL, Object.assign({action:"add"}, entry));
    await loadFromSheet();
    ["f_matricula","f_repartidor","f_desc","f_fechaenvio"].forEach(id=>document.getElementById(id).value="");
    document.getElementById("f_fecha").style.borderColor = "";
  }catch(e){
    alert("No se pudo guardar. Revisa tu conexión a internet e inténtalo de nuevo.");
  }finally{
    btn.disabled = false;
    btn.textContent = "Guardar y avisar a todos";
  }
});

loadFromSheet();
setInterval(loadFromSheet, POLL_MS);
</script>

</body>
</html>
