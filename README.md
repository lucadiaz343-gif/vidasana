[nano-os (3).html](https://github.com/user-attachments/files/27133208/nano-os.3.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#0d0d0b">
<meta name="description" content="Nano OS · Dashboard personal de organización diaria">
<title>Nano OS</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@500;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,400&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0d0d0b;--s1:#141412;--s2:#1c1c19;--s3:#252521;
  --border:#2a2a26;--border2:#363630;
  --gold:#E4C04A;--gold2:#c9a83a;--gold-bg:rgba(228,192,74,.09);
  --text:#f0ede6;--muted:#7a7a72;--dim:#3a3a34;
  --ok:#5aaa58;--ok-bg:rgba(90,170,88,.1);
  --blue:#5B8EE0;--blue-bg:rgba(91,142,224,.1);
  --coral:#E07A5B;--coral-bg:rgba(224,122,91,.08);
  --r:12px;--rs:8px;
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;font-size:15px;line-height:1.5;padding-bottom:72px;min-height:100vh}
::-webkit-scrollbar{width:3px}::-webkit-scrollbar-thumb{background:var(--s3)}

/* NAV */
.nav{position:fixed;bottom:0;left:0;right:0;background:rgba(13,13,11,.96);backdrop-filter:blur(16px);border-top:1px solid var(--border);display:flex;z-index:100;padding-bottom:env(safe-area-inset-bottom)}
.nav-btn{flex:1;border:none;background:none;color:var(--muted);padding:10px 4px 12px;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;transition:color .2s;font-size:11px;font-weight:500;letter-spacing:.02em;font-family:'DM Sans',sans-serif}
.nav-btn svg{width:20px;height:20px;stroke-width:1.5;stroke:currentColor;fill:none}
.nav-btn.on{color:var(--gold)}

/* LAYOUT */
.page{display:none;max-width:560px;margin:0 auto;padding:24px 16px 16px}
.page.on{display:block}

/* TYPOGRAPHY */
.hdr{margin-bottom:22px}
.hdr-date{font-size:12px;color:var(--muted);letter-spacing:.04em;margin-bottom:4px;text-transform:lowercase}
.hdr-h1{font-family:'Syne',sans-serif;font-size:26px;font-weight:800;line-height:1.1;margin-bottom:8px}
.slabel{font-size:10px;font-weight:500;color:var(--muted);text-transform:uppercase;letter-spacing:.1em;margin:20px 0 10px}
.text-muted{color:var(--muted);font-size:13px}

/* BADGES */
.badge{display:inline-flex;align-items:center;font-size:11px;font-weight:500;padding:3px 10px;border-radius:20px;line-height:1.6}
.bg{background:var(--gold-bg);color:var(--gold);border:1px solid rgba(228,192,74,.2)}
.bb{background:var(--blue-bg);color:var(--blue)}
.bo{background:var(--ok-bg);color:var(--ok)}
.bd{background:var(--s2);color:var(--muted);border:1px solid var(--border)}

/* PROGRESS */
.prog-wrap{margin-bottom:18px}
.prog-bar{height:3px;background:var(--s3);border-radius:2px;overflow:hidden}
.prog-fill{height:100%;background:var(--gold);border-radius:2px;transition:width .4s ease}
.prog-info{display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-top:5px}

/* MOOD */
.mood-row{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:18px;align-items:center}
.mood-label{font-size:12px;color:var(--muted)}
.mood-chip{border:1px solid var(--border2);background:var(--s1);border-radius:20px;padding:5px 11px;font-size:12px;cursor:pointer;color:var(--muted);transition:all .15s;user-select:none}
.mood-chip.on{border-color:var(--gold2);background:var(--gold-bg);color:var(--gold)}

/* DECISION */
.decision{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:14px 16px;margin-bottom:18px}
.decision-q{font-size:13px;color:var(--muted);margin-bottom:10px}
.d-opts{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.dopt{border:1px solid var(--border2);background:var(--s2);border-radius:var(--rs);padding:10px 12px;cursor:pointer;text-align:left;font-size:13px;color:var(--text);transition:all .15s;line-height:1.4;font-family:'DM Sans',sans-serif;width:100%}
.dopt:hover{background:var(--s3)}
.dopt.on{border-color:var(--gold2);background:var(--gold-bg);color:var(--gold)}
.dopt-sub{font-size:11px;color:var(--muted);margin-top:2px;display:block}
.dopt.on .dopt-sub{color:var(--gold2)}
.d-tip{font-size:12px;color:var(--muted);margin-top:10px;padding-top:10px;border-top:1px solid var(--border);display:none;line-height:1.6}
.d-tip.on{display:block}

/* ── TIMELINE (fixed layout) ─────────────── */
.tl-sep{font-size:10px;color:var(--dim);text-transform:uppercase;letter-spacing:.08em;margin:18px 0 8px;padding-left:72px}
.tl-block{display:flex;align-items:flex-start;margin-bottom:7px}
.tl-hora{
  flex-shrink:0;width:52px;
  font-size:11px;color:var(--muted);
  text-align:right;padding-top:15px;
  font-variant-numeric:tabular-nums;
  padding-right:0;
}
.tl-stem{
  flex-shrink:0;width:20px;
  display:flex;flex-direction:column;
  align-items:center;
  padding-top:17px;
  position:relative;
}
.tl-stem::after{
  content:'';position:absolute;
  top:26px;bottom:-7px;
  left:50%;transform:translateX(-50%);
  width:1px;background:var(--border);
}
.tl-block:last-child .tl-stem::after{display:none}
.tl-bullet{
  width:9px;height:9px;border-radius:50%;
  background:var(--s3);border:1.5px solid var(--border2);
  z-index:1;transition:all .2s;flex-shrink:0;
}
.tl-card{
  flex:1;margin-left:10px;
  background:var(--s1);border:1px solid var(--border);
  border-radius:var(--r);padding:11px 42px 11px 14px;
  cursor:pointer;position:relative;transition:border-color .15s,background .15s;
}
.tl-card:hover{border-color:var(--border2)}
.tl-card.done{border-color:rgba(90,170,88,.35);background:var(--ok-bg)}
.tl-card.done .tl-bullet,.tl-bullet.done{background:var(--ok)!important;border-color:var(--ok)!important}
.tl-title{font-size:14px;font-weight:500;color:var(--text);display:flex;align-items:center;gap:7px;flex-wrap:wrap}
.tl-card.done .tl-title{color:var(--ok)}
.tl-sub{font-size:12px;color:var(--muted);margin-top:3px;line-height:1.5}
.tl-ck{
  position:absolute;right:12px;top:50%;transform:translateY(-50%);
  width:22px;height:22px;border-radius:50%;
  border:1.5px solid var(--border2);
  display:flex;align-items:center;justify-content:center;
  transition:all .2s;flex-shrink:0;
}
.tl-card.done .tl-ck{background:var(--ok);border-color:var(--ok)}

/* CARDS */
.card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:14px 16px}

/* EXERCISE */
.ex-hero{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:18px;margin-bottom:8px}
.ex-hero-h{font-family:'Syne',sans-serif;font-size:19px;font-weight:700;margin-bottom:4px}
.ex-hero-s{font-size:13px;color:var(--muted)}
.ex-cta{display:block;width:100%;margin-top:14px;padding:12px;border-radius:var(--rs);border:none;font-size:14px;font-weight:500;cursor:pointer;transition:all .2s;text-align:center;font-family:'DM Sans',sans-serif}
.ex-cta-start{background:var(--gold);color:#0d0d0b}
.ex-cta-start:hover{background:var(--gold2)}
.ex-cta-done{background:var(--ok-bg);color:var(--ok);border:1px solid rgba(90,170,88,.3)}
.circuit{background:var(--s2);border:1px solid var(--border);border-radius:var(--rs);margin-bottom:7px;overflow:hidden}
.cir-hdr{padding:10px 14px;font-size:13px;font-weight:500;cursor:pointer;display:flex;justify-content:space-between;align-items:center;user-select:none;transition:background .15s}
.cir-hdr:hover{background:var(--s3)}
.cir-body{padding:0 14px 12px;display:none}
.cir-body.on{display:block}
.cir-ex{display:flex;align-items:center;gap:10px;padding:7px 0;border-bottom:1px solid var(--border);cursor:pointer}
.cir-ex:last-child{border-bottom:none}
.cir-ex.done span{text-decoration:line-through;color:var(--muted)}
.ex-chk{width:16px;height:16px;border-radius:4px;border:1px solid var(--border2);flex-shrink:0;display:flex;align-items:center;justify-content:center;transition:all .15s}
.cir-ex.done .ex-chk{background:var(--ok);border-color:var(--ok)}
.cir-ex span{font-size:13px;color:var(--text)}

/* HISTORY */
.streak-row{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:20px}
.streak-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:12px 14px;text-align:center}
.streak-n{font-family:'Syne',sans-serif;font-size:28px;font-weight:800;color:var(--gold);line-height:1}
.streak-l{font-size:11px;color:var(--muted);margin-top:4px}
.hist-labels{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;margin-bottom:4px}
.hist-labels span{font-size:9px;color:var(--dim);text-align:center}
.hist-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;margin-bottom:4px}
.h-dot{aspect-ratio:1;border-radius:4px;cursor:default;transition:opacity .2s}
.h-dot.hf{background:#5aaa58}
.h-dot.hy{background:#5B8EE0}
.h-dot.hd{background:var(--s3)}
.h-dot.he{background:var(--s2);border:1px solid var(--border)}
.week-row{display:grid;grid-template-columns:repeat(7,1fr);gap:6px}
.wd-col{display:flex;flex-direction:column;align-items:center;gap:5px}
.wd-name{font-size:10px;color:var(--muted)}
.wd-dot{width:36px;height:36px;border-radius:50%;border:1px solid var(--border);background:var(--s2);display:flex;align-items:center;justify-content:center;font-size:12px;cursor:pointer;transition:all .15s}
.wd-dot.today{border-color:var(--gold);color:var(--gold)}
.wd-dot.tf{background:var(--ok-bg);border-color:rgba(90,170,88,.4);color:var(--ok)}
.wd-dot.ty{background:var(--blue-bg);border-color:rgba(91,142,224,.4);color:var(--blue)}
.wd-dot.done-d{background:var(--ok);border-color:var(--ok);color:#fff}

/* COMIDAS */
.meal-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--r);padding:13px 16px;margin-bottom:8px;display:flex;align-items:center;gap:12px;cursor:pointer;transition:all .15s}
.meal-card:hover{border-color:var(--border2)}
.meal-card.done{border-color:rgba(90,170,88,.35);background:var(--ok-bg)}
.meal-card.done .meal-plato{color:var(--ok)}
.meal-e{font-size:22px;width:32px;text-align:center;flex-shrink:0}
.meal-info{flex:1}
.meal-tipo{font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;margin-bottom:2px}
.meal-plato{font-size:14px;font-weight:500;color:var(--text);line-height:1.3;transition:color .15s}
.meal-kcal{font-size:11px;color:var(--muted);margin-top:2px}
.meal-ck{width:22px;height:22px;border-radius:50%;border:1.5px solid var(--border2);display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all .2s}
.meal-card.done .meal-ck{background:var(--ok);border-color:var(--ok)}
.wm-item{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);margin-bottom:7px;overflow:hidden}
.wm-head{padding:10px 14px;display:flex;justify-content:space-between;align-items:center;cursor:pointer;user-select:none;transition:background .15s}
.wm-head:hover{background:var(--s2)}
.wm-day-name{font-size:13px;font-weight:500}
.wm-preview{font-size:12px;color:var(--muted);max-width:200px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.wm-body{padding:0 14px 12px;display:none;border-top:1px solid var(--border)}
.wm-body.on{display:block}
.wm-row{display:flex;gap:8px;padding:7px 0;border-bottom:1px solid var(--border)}
.wm-row:last-child{border-bottom:none}
.wm-rl{font-size:11px;color:var(--muted);width:72px;flex-shrink:0;padding-top:2px}
.wm-rt{font-size:13px;color:var(--text);line-height:1.4}

/* SEMANA CALENDAR */
.sem-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:5px}
.sem-col{background:var(--s1);border:1px solid var(--border);border-radius:var(--rs);padding:8px 5px;display:flex;flex-direction:column;align-items:center;gap:5px;min-height:150px}
.sem-col.today{border-color:var(--gold2);background:var(--gold-bg)}
.sem-dn{font-size:10px;color:var(--muted);font-weight:500}
.sem-dd{font-size:17px;font-weight:700;font-family:'Syne',sans-serif;line-height:1}
.sem-col.today .sem-dd{color:var(--gold)}
.sem-ex{font-size:9px;padding:2px 5px;border-radius:4px;font-weight:500;text-align:center;width:100%}
.sem-ex.f{background:var(--ok-bg);color:var(--ok)}
.sem-ex.y{background:var(--blue-bg);color:var(--blue)}
.sem-ex.d{background:var(--s3);color:var(--dim)}
.sem-task{width:100%;display:flex;align-items:center;gap:4px;cursor:pointer;padding:2px 0}
.sem-dot{width:9px;height:9px;border-radius:2px;border:1px solid var(--border2);flex-shrink:0;transition:all .15s}
.sem-task.done .sem-dot{background:var(--ok);border-color:var(--ok)}
.sem-task span{font-size:9px;color:var(--muted);line-height:1.3}
.sem-task.done span{text-decoration:line-through;color:var(--dim)}

/* MISC */
.nota{width:100%;background:var(--s2);border:1px solid var(--border);border-radius:var(--rs);padding:12px;font-size:13px;color:var(--text);resize:none;outline:none;line-height:1.6;font-family:'DM Sans',sans-serif}
.nota::placeholder{color:var(--dim)}
.nota:focus{border-color:var(--border2)}
.divider{height:1px;background:var(--border);margin:20px 0}
.svgck{pointer-events:none}
</style>
</head>
<body>

<nav class="nav">
  <button class="nav-btn on" id="nav-hoy" onclick="go('hoy')">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M4.93 19.07l1.41-1.41M17.66 6.34l1.41-1.41"/></svg>
    Hoy
  </button>
  <button class="nav-btn" id="nav-ejercicio" onclick="go('ejercicio')">
    <svg viewBox="0 0 24 24"><path d="M6.5 6.5h11M6.5 17.5h11M12 2v3M12 19v3M4.22 4.22l2.12 2.12M17.66 17.66l2.12 2.12M2 12h3M19 12h3M4.22 19.78l2.12-2.12M17.66 6.34l2.12-2.12"/></svg>
    Ejercicio
  </button>
  <button class="nav-btn" id="nav-comidas" onclick="go('comidas')">
    <svg viewBox="0 0 24 24"><path d="M3 11l19-9-9 19-2-8-8-2z"/></svg>
    Comidas
  </button>
  <button class="nav-btn" id="nav-semana" onclick="go('semana')">
    <svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
    Semana
  </button>
</nav>

<!-- HOY -->
<div class="page on" id="sec-hoy">
  <div class="hdr">
    <div class="hdr-date" id="hdr-date"></div>
    <div class="hdr-h1" id="hdr-saludo">Buenos días, Nano</div>
    <div id="hdr-badge"></div>
  </div>

  <div class="mood-row">
    <span class="mood-label">Hoy estoy:</span>
    <button class="mood-chip" onclick="toggleMood(this)">😴 cansado</button>
    <button class="mood-chip" onclick="toggleMood(this)">😤 estresado</button>
    <button class="mood-chip" onclick="toggleMood(this)">😐 neutro</button>
    <button class="mood-chip" onclick="toggleMood(this)">🙂 bien</button>
    <button class="mood-chip" onclick="toggleMood(this)">⚡ enfocado</button>
  </div>

  <div class="prog-wrap">
    <div class="prog-bar"><div class="prog-fill" id="prog-fill" style="width:0%"></div></div>
    <div class="prog-info"><span id="prog-txt">0 completados</span><span id="prog-pct">0%</span></div>
  </div>

  <div class="decision" id="comida-box">
    <div class="decision-q">🍽️ ¿Dónde comés al mediodía?</div>
    <div class="d-opts">
      <button class="dopt" id="dopt-t" onclick="pickComida('trabajo')">🏢 En el trabajo<span class="dopt-sub">Traés vianda o comprás</span></button>
      <button class="dopt" id="dopt-c" onclick="pickComida('casa')">🏠 En casa a las 15:30<span class="dopt-sub">Cocinás al llegar</span></button>
    </div>
    <div class="d-tip" id="d-tip"></div>
  </div>

  <div id="timeline-wrap"></div>

  <div class="divider"></div>
  <div class="slabel">Nota del día</div>
  <textarea class="nota" id="nota-dia" rows="3" placeholder="Pendientes, ideas, recordatorios..."></textarea>
</div>

<!-- EJERCICIO -->
<div class="page" id="sec-ejercicio">
  <div class="hdr">
    <div class="hdr-date" id="ex-fecha"></div>
    <div class="hdr-h1" id="ex-h1">Ejercicio</div>
    <div class="text-muted" id="ex-sub"></div>
  </div>
  <div class="streak-row" id="streaks"></div>
  <div class="slabel">Esta semana</div>
  <div class="week-row" id="week-row"></div>
  <div class="divider"></div>
  <div id="rutina-container"></div>
  <div class="divider"></div>
  <div class="slabel">Historial · últimas 4 semanas</div>
  <div class="hist-labels"><span>L</span><span>M</span><span>X</span><span>J</span><span>V</span><span>S</span><span>D</span></div>
  <div class="hist-grid" id="hist-grid"></div>
  <div style="display:flex;gap:12px;margin-top:8px">
    <span style="font-size:11px;color:var(--muted)"><span style="display:inline-block;width:10px;height:10px;background:#5aaa58;border-radius:2px;margin-right:4px"></span>Fuerza</span>
    <span style="font-size:11px;color:var(--muted)"><span style="display:inline-block;width:10px;height:10px;background:#5B8EE0;border-radius:2px;margin-right:4px"></span>Yoga</span>
    <span style="font-size:11px;color:var(--muted)"><span style="display:inline-block;width:10px;height:10px;background:var(--s3);border-radius:2px;margin-right:4px"></span>Descanso</span>
  </div>
</div>

<!-- COMIDAS -->
<div class="page" id="sec-comidas">
  <div class="hdr">
    <div class="hdr-date" id="com-fecha"></div>
    <div class="hdr-h1">Lo que comés hoy</div>
    <div class="text-muted">Nutritivo · rico · sin complicaciones</div>
  </div>
  <div id="today-meals"></div>
  <div class="divider"></div>
  <div class="slabel">Plan semanal</div>
  <div id="week-meals"></div>
</div>

<!-- SEMANA -->
<div class="page" id="sec-semana">
  <div class="hdr">
    <div class="hdr-date" id="sem-fecha"></div>
    <div class="hdr-h1">Esta semana</div>
  </div>
  <div class="sem-grid" id="sem-grid"></div>
  <div class="divider"></div>
  <div class="slabel">Nota semanal</div>
  <textarea class="nota" id="nota-sem" rows="3" placeholder="Objetivos de la semana, compromisos..."></textarea>
</div>

<script>
// ── CONSTANTS ────────────────────────────────────────────────────────────────
const DN=['Dom','Lun','Mar','Mié','Jue','Vie','Sáb'];
const DL=['Domingo','Lunes','Martes','Miércoles','Jueves','Viernes','Sábado'];
const MN=['enero','febrero','marzo','abril','mayo','junio','julio','agosto','septiembre','octubre','noviembre','diciembre'];

// Exercise type: 0=Sun,1=Mon,2=Tue,3=Wed,4=Thu,5=Fri,6=Sat
const EX={'0':'d','1':'f','2':'y','3':'f','4':'y','5':'f','6':'y'};
const EL={f:'Fuerza 💪',y:'Yoga 🧘',d:'Descanso 🌿'};

const BLOQUES=[
  {id:'despertar',h:'7:50',e:'☀️',t:'Despertar',s:'20 min para arrancar bien · agua · sin mirar el celu'},
  {id:'bici',h:'8:10',e:'🚴',t:'Salida en bici al trabajo',s:'Ya eso son ~30 min de movimiento diario · es parte del entrenamiento'},
  {id:'trabajo',h:'9:00',e:'🏢',t:'Trabajo',s:'Definí la tarea más importante antes de arrancar',tipo:'trabajo'},
  {id:'almuerzo',h:'12:00',e:'🍱',t:'Almuerzo',s:'',dyn:'almuerzo'},
  {id:'vuelta',h:'15:30',e:'🏠',t:'Vuelta a casa en bici',s:'Otro tramo de movimiento · llegás activo y con la cabeza despejada'},
  {id:'ejercicio',h:'16:00',e:'🏋️',t:'',s:'Mirá la pestaña Ejercicio para la rutina completa',dyn:'ejercicio'},
  {id:'perros',h:'17:00',e:'🐕',t:'Pasear los perros',s:'30 min · afuera, luz natural · el mejor reset entre ejercicio y freelance'},
  {id:'freelance',h:'17:30',e:'🎨',t:'Bloque freelance · 3h',s:'Corner Talk, nano.ds, clientes — foco sin interrupciones',tipo:'freelance'},
  {id:'casa',h:'20:30',e:'🧹',t:'Ordenar casa · 20 min',s:'Tareas pequeñas diarias, no dejarlo todo para el finde'},
  {id:'cena',h:'21:00',e:'🥘',t:'Cena liviana',s:'',dyn:'cena'},
  {id:'lectura',h:'21:30',e:'📖',t:'Lectura o recreativo',s:'Leer, música, serie · tiempo para vos, sin culpa'},
  {id:'cierre',h:'22:30',e:'✍️',t:'Cierre del día',s:'1 cosa que salió bien · 1 cosa que mejorar · pantallas off a las 23h'},
];

const TL_SEPS={despertar:'Mañana',trabajo:'Trabajo · 9:00 → 15:00',vuelta:'Tarde en casa',cena:'Noche'};

const RUTINAS={
  f:{
    t:'Fuerza en casa · 45 min',s:'Circuito de cuerpo entero · Lun / Mié / Vie',
    c:[
      {n:'☀️ Calentamiento · 5 min',e:['Trote en el lugar — 2 min','Rotación de cadera y hombros — 1 min','Movilidad articular suave — 1 min','Sentadillas sin peso — 1 min']},
      {n:'💪 Tren superior · 3 series × 45s',e:['Flexiones completas','Flexiones cerradas (tríceps)','Superman (espalda baja)','Plancha frontal']},
      {n:'🦵 Tren inferior · 3 series × 45s',e:['Sentadillas con salto','Estocadas alternadas','Puente de glúteos con pausa arriba','Sentadilla sumo con pausa']},
      {n:'🧠 Core · 2 series × 45s',e:['Crunches bicicleta','Plancha lateral — cada lado','Mountain climbers','Dead bug']},
      {n:'🔥 Cardio final · 5 min',e:['Burpees: 30s trabajo / 30s descanso × 5 rondas']},
      {n:'🌬️ Enfriamiento · 5 min',e:['Isquiotibiales — 30s c/lado','Apertura de cadera — 1 min','Estiramiento de pecho','Respiración abdominal — 2 min']},
    ]
  },
  y:{
    t:'Yoga & Movilidad · 30 min',s:'Flujo para flexibilidad y energía · Mar / Jue / Sáb',
    c:[
      {n:'🙏 Saludo al sol · 10 min',e:['5 rondas de Surya Namaskar A','Sincronizá el movimiento con la respiración']},
      {n:'🧍 Secuencia en pie · 10 min',e:['Guerrero I — 5 respiraciones c/lado','Guerrero II — 5 respiraciones c/lado','Triángulo extendido — 5 resp. c/lado','Perro boca abajo ↔ boca arriba (3 veces)']},
      {n:'🌿 Suelo y restaurativo · 10 min',e:['Paloma — 2 min c/lado','Torsión supina — 1 min c/lado','Postura del niño — 2 min','Savasana — 3 min']},
    ]
  },
  d:{
    t:'Descanso activo · Domingo',s:'El cuerpo se construye en el descanso',
    c:[{n:'🌳 Suave y opcional',e:['Caminata de 20–30 min al aire libre','Estiramientos suaves 10 min','Respirar, relajar, desconectar — sin culpa']}]
  }
};

const MEALS={
  1:{desayuno:{tag:'🥑',p:'Tostadas integrales con palta y huevo revuelto',k:420},almuerzo:{tag:'🍗',p:'Arroz integral con pollo a la plancha y ensalada verde',k:580},merienda:{tag:'🍓',p:'Yogur griego con fruta y granola',k:280},cena:{tag:'🍳',p:'Omelette de 3 huevos con verduras salteadas',k:380}},
  2:{desayuno:{tag:'🍌',p:'Avena con banana, miel y canela + café',k:390},almuerzo:{tag:'🫘',p:'Lentejas guisadas con zanahoria y papas',k:540},merienda:{tag:'🍎',p:'Manzana + mantequilla de maní',k:220},cena:{tag:'🥦',p:'Pollo al horno con batata y brócoli',k:490}},
  3:{desayuno:{tag:'🫐',p:'Yogur griego con frutas del bosque y semillas',k:360},almuerzo:{tag:'🍝',p:'Fideos integrales con atún, tomates cherry y albahaca',k:560},merienda:{tag:'🍊',p:'Nueces + naranja',k:240},cena:{tag:'🍔',p:'Hamburguesa casera de pollo + ensalada coleslaw',k:460}},
  4:{desayuno:{tag:'🥞',p:'Panqueques de avena y banana (sin azúcar) + café',k:410},almuerzo:{tag:'🥗',p:'Ensalada de garbanzos, quinoa, pepino y queso feta',k:520},merienda:{tag:'🍅',p:'Tostada con queso fresco y tomate',k:200},cena:{tag:'🥢',p:'Wok de vegetales con pollo y arroz jazmín',k:480}},
  5:{desayuno:{tag:'🍓',p:'Tostadas con ricota y mermelada + fruta',k:380},almuerzo:{tag:'🥩',p:'Milanesa al horno con puré de calabaza y ensalada',k:620},merienda:{tag:'🥤',p:'Smoothie: banana + leche + avena + cacao',k:340},cena:{tag:'🍕',p:'Pizza casera integral con mozzarella y vegetales',k:500}},
  6:{desayuno:{tag:'🍳',p:'Huevos revueltos con tostadas y jugo natural',k:440},almuerzo:{tag:'🔥',p:'Asado liviano — cortes magros, ensalada, poco pan',k:650},merienda:{tag:'🧉',p:'Mate + 1–2 facturas (¡merecido!)',k:300},cena:{tag:'🍲',p:'Sopa casera de vegetales y fideos',k:350}},
  0:{desayuno:{tag:'🥞',p:'Pancakes integrales con miel y fruta',k:460},almuerzo:{tag:'🍝',p:'Pasta con salsa casera y albóndigas magras',k:600},merienda:{tag:'🥜',p:'Tostadas con mantequilla de maní y banana',k:310},cena:{tag:'🥪',p:'Sándwich de pavo con lechuga, tomate y mostaza',k:380}},
};

// ── UTILS ────────────────────────────────────────────────────────────────────
const today=new Date();
const dk=d=>`${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
const todayK=dk(today);

function getMonday(d=today){
  const r=new Date(d);const wd=r.getDay();
  r.setDate(r.getDate()-(wd===0?6:wd-1));return r;
}

const LS={
  get:(k,def)=>{try{const v=localStorage.getItem(k);return v!==null?JSON.parse(v):def;}catch{return def;}},
  set:(k,v)=>{try{localStorage.setItem(k,JSON.stringify(v));}catch{}}
};

// ── STATE ────────────────────────────────────────────────────────────────────
const S={
  blocks: LS.get('nb_'+todayK,{}),
  exDone: LS.get('ne_done',{}),
  exItems: LS.get('nei_'+todayK,{}),
  meals:  LS.get('nm_'+todayK,{}),
  comida: LS.get('nc_'+todayK,null),
  mood:   LS.get('nmo_'+todayK,[]),
  notaDia:LS.get('nnd_'+todayK,''),
  notaSem:LS.get('nns_'+dk(getMonday()),''),
  semT:   LS.get('nst_'+dk(getMonday()),{}),
};
const save=()=>{
  LS.set('nb_'+todayK,S.blocks);
  LS.set('ne_done',S.exDone);
  LS.set('nei_'+todayK,S.exItems);
  LS.set('nm_'+todayK,S.meals);
  LS.set('nc_'+todayK,S.comida);
  LS.set('nmo_'+todayK,S.mood);
  LS.set('nnd_'+todayK,S.notaDia);
  LS.set('nns_'+dk(getMonday()),S.notaSem);
  LS.set('nst_'+dk(getMonday()),S.semT);
};

// ── NAVIGATION ───────────────────────────────────────────────────────────────
const INITS={ejercicio:false,comidas:false,semana:false};
function go(p){
  document.querySelectorAll('.page').forEach(x=>x.classList.remove('on'));
  document.querySelectorAll('.nav-btn').forEach(x=>x.classList.remove('on'));
  document.getElementById('sec-'+p).classList.add('on');
  document.getElementById('nav-'+p).classList.add('on');
  if(!INITS[p]&&p!=='hoy'){
    INITS[p]=true;
    if(p==='ejercicio')initEjercicio();
    if(p==='comidas')initComidas();
    if(p==='semana')initSemana();
  }
}

// ── HOY ──────────────────────────────────────────────────────────────────────
function initHoy(){
  const dow=today.getDay();
  document.getElementById('hdr-date').textContent=`${DL[dow].toLowerCase()} · ${today.getDate()} de ${MN[today.getMonth()]}`;
  const h=today.getHours();
  document.getElementById('hdr-saludo').textContent=(h<12?'Buenos días':h<20?'Buenas tardes':'Buenas noches')+', Nano';
  const et=EX[dow];
  document.getElementById('hdr-badge').innerHTML=`<span class="badge ${et==='f'?'bg':et==='y'?'bb':'bd'}">${EL[et]}</span>`;

  // restore mood
  S.mood.forEach(m=>{
    document.querySelectorAll('.mood-chip').forEach(c=>{if(c.textContent.trim()===m)c.classList.add('on');});
  });

  renderComida();
  renderTimeline();
  updateProg();
  const nd=document.getElementById('nota-dia');
  nd.value=S.notaDia;
  nd.oninput=e=>{S.notaDia=e.target.value;save();};
}

function toggleMood(btn){
  btn.classList.toggle('on');
  S.mood=Array.from(document.querySelectorAll('.mood-chip.on')).map(b=>b.textContent.trim());
  save();
}

function pickComida(t){
  S.comida=t;save();renderComida();renderTimeline();
}

function renderComida(){
  const c=S.comida;
  document.getElementById('dopt-t').className='dopt'+(c==='trabajo'?' on':'');
  document.getElementById('dopt-c').className='dopt'+(c==='casa'?' on':'');
  const tip=document.getElementById('d-tip');
  if(c==='trabajo'){
    tip.textContent='✓ Armá la vianda la noche anterior: arroz o pasta integral + proteína + verduras. Rápido de cocinar, nutritivo, sin depender de lo que haya cerca.';
    tip.classList.add('on');
  } else if(c==='casa'){
    tip.textContent='✓ Al llegar (~15:30h), cocinás algo rápido en 20 min antes del ejercicio. Así hacés el bloque completo: comer → moverse → freelance.';
    tip.classList.add('on');
  } else {
    tip.classList.remove('on');
  }
}

function renderTimeline(){
  const dow=today.getDay();
  const m=MEALS[dow]||MEALS[1];
  const et=EX[dow];
  const wrap=document.getElementById('timeline-wrap');
  wrap.innerHTML='';

  BLOQUES.forEach(b=>{
    if(TL_SEPS[b.id]){
      const sep=document.createElement('div');
      sep.className='tl-sep';sep.textContent=TL_SEPS[b.id];
      wrap.appendChild(sep);
    }

    let titulo=b.t,sub=b.s;
    if(b.dyn==='ejercicio'){titulo=RUTINAS[et].t;}
    if(b.dyn==='almuerzo'){
      if(S.comida==='casa') sub='🏠 Hoy cocinás al llegar a casa (~15:30)';
      else sub=(m.almuerzo.tag+' '+m.almuerzo.p);
    }
    if(b.dyn==='cena') sub=m.cena.tag+' '+m.cena.p;

    const done=!!S.blocks[b.id];
    const row=document.createElement('div');row.className='tl-block';
    row.innerHTML=`
      <div class="tl-hora">${b.h}</div>
      <div class="tl-stem">
        <div class="tl-bullet${done?' done':''}" id="blt-${b.id}"></div>
      </div>
      <div class="tl-card${done?' done':''}" id="tc-${b.id}" onclick="toggleBlock('${b.id}')">
        <div class="tl-title">${b.e} ${titulo}${b.tipo?`<span class="badge ${b.tipo==='trabajo'?'bo':'bg'}">${b.tipo}</span>`:''}</div>
        ${sub?`<div class="tl-sub">${sub}</div>`:''}
        <div class="tl-ck">${done?ckSVG():''}</div>
      </div>`;
    wrap.appendChild(row);
  });
}

function ckSVG(){return '<svg class="svgck" width="12" height="12" viewBox="0 0 12 12" fill="none"><polyline points="2,6 5,9 10,3" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>';}

function toggleBlock(id){
  S.blocks[id]=!S.blocks[id];save();
  const done=S.blocks[id];
  const card=document.getElementById('tc-'+id);
  const blt=document.getElementById('blt-'+id);
  if(card){card.classList.toggle('done',done);card.querySelector('.tl-ck').innerHTML=done?ckSVG():'';}
  if(blt){blt.classList.toggle('done',done);}
  updateProg();
}

function updateProg(){
  const done=Object.values(S.blocks).filter(Boolean).length;
  const total=BLOQUES.length;
  const pct=Math.round(done/total*100);
  document.getElementById('prog-fill').style.width=pct+'%';
  document.getElementById('prog-txt').textContent=`${done} de ${total} completados`;
  document.getElementById('prog-pct').textContent=pct+'%';
}

// ── EJERCICIO ────────────────────────────────────────────────────────────────
function initEjercicio(){
  const dow=today.getDay();
  const et=EX[dow];
  const r=RUTINAS[et];
  document.getElementById('ex-fecha').textContent=`${DL[dow].toLowerCase()} · ${today.getDate()} de ${MN[today.getMonth()]}`;
  document.getElementById('ex-h1').textContent=r.t;
  document.getElementById('ex-sub').textContent=r.s;

  // Streaks
  let total=0,semana=0,racha=0;
  Object.values(S.exDone).forEach(v=>{if(v)total++;});
  const mon=getMonday();
  for(let i=0;i<7;i++){const d=new Date(mon);d.setDate(mon.getDate()+i);if(S.exDone[dk(d)])semana++;}
  let cur=new Date(today);
  for(let i=0;i<60;i++){
    const k=dk(cur);const t=EX[cur.getDay()];
    if(t==='d'){cur.setDate(cur.getDate()-1);continue;}
    if(!S.exDone[k])break;
    racha++;cur.setDate(cur.getDate()-1);
  }
  document.getElementById('streaks').innerHTML=[
    ['<span style="color:var(--gold)">'+total+'</span>','sesiones totales'],
    ['<span style="color:var(--gold)">'+semana+'</span>','esta semana'],
    ['<span style="color:var(--gold)">'+racha+'</span>','racha actual'],
  ].map(([n,l])=>`<div class="streak-card"><div class="streak-n">${n}</div><div class="streak-l">${l}</div></div>`).join('');

  // Week row
  const wr=document.getElementById('week-row');wr.innerHTML='';
  for(let i=0;i<7;i++){
    const d=new Date(mon);d.setDate(mon.getDate()+i);
    const et2=EX[d.getDay()];const done=!!S.exDone[dk(d)];const isT=dk(d)===todayK;
    const col=document.createElement('div');col.className='wd-col';
    col.innerHTML=`<div class="wd-name">${DN[d.getDay()]}</div>
      <div class="wd-dot${isT?' today':''}${done?' done-d':et2==='f'?' tf':et2==='y'?' ty':''}" onclick="toggleExDay('${dk(d)}')">${done?'✓':et2==='f'?'F':et2==='y'?'Y':'—'}</div>`;
    wr.appendChild(col);
  }

  // Today's routine
  const rc=document.getElementById('rutina-container');
  const done=!!S.exDone[todayK];
  rc.innerHTML=`<div class="slabel">Rutina de hoy</div>
    <div class="ex-hero">
      <div class="ex-hero-h">${r.t}</div>
      <div class="ex-hero-s">${r.s}</div>
      <button class="ex-cta ${done?'ex-cta-done':'ex-cta-start'}" onclick="toggleExToday()">
        ${done?'✓ Sesión completada — clic para desmarcar':'Marcar sesión como completada'}
      </button>
    </div>
    ${r.c.map((c,ci)=>`
      <div class="circuit">
        <div class="cir-hdr" onclick="toggleCir(${ci})"><span>${c.n}</span><span style="color:var(--muted);font-size:11px" id="cir-arrow-${ci}">▾</span></div>
        <div class="cir-body" id="cir-${ci}">
          ${c.e.map((ej,ei)=>{
            const k=`${ci}_${ei}`;const d=!!S.exItems[k];
            return `<div class="cir-ex${d?' done':''}" id="cex-${k}" onclick="toggleExItem('${k}')">
              <div class="ex-chk">${d?'<svg width="10" height="10" viewBox="0 0 10 10" fill="none"><polyline points="1.5,5 4,7.5 8.5,2.5" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>':''}</div>
              <span>${ej}</span>
            </div>`;
          }).join('')}
        </div>
      </div>`).join('')}`;

  // History
  const hg=document.getElementById('hist-grid');hg.innerHTML='';
  for(let i=27;i>=0;i--){
    const d=new Date(today);d.setDate(today.getDate()-i);
    const et2=EX[d.getDay()];const done=!!S.exDone[dk(d)];
    const dot=document.createElement('div');dot.className='h-dot';
    dot.className+=' '+(done?(et2==='y'?'hy':'hf'):et2==='d'?'hd':'he');
    dot.title=`${DN[d.getDay()]} ${d.getDate()}/${d.getMonth()+1} ${done?'✓':EL[et2]}`;
    hg.appendChild(dot);
  }
}

function toggleExToday(){S.exDone[todayK]=!S.exDone[todayK];save();INITS.ejercicio=false;initEjercicio();}
function toggleExDay(k){S.exDone[k]=!S.exDone[k];save();INITS.ejercicio=false;initEjercicio();}
function toggleExItem(key){
  S.exItems[key]=!S.exItems[key];save();
  const row=document.getElementById('cex-'+key);if(!row)return;
  row.classList.toggle('done',S.exItems[key]);
  row.querySelector('.ex-chk').innerHTML=S.exItems[key]?'<svg width="10" height="10" viewBox="0 0 10 10" fill="none"><polyline points="1.5,5 4,7.5 8.5,2.5" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>':'';
}
function toggleCir(ci){
  const b=document.getElementById('cir-'+ci);b.classList.toggle('on');
}

// ── COMIDAS ──────────────────────────────────────────────────────────────────
function initComidas(){
  const dow=today.getDay();
  document.getElementById('com-fecha').textContent=`${DL[dow].toLowerCase()} · ${today.getDate()} de ${MN[today.getMonth()]}`;
  const m=MEALS[dow]||MEALS[1];
  const ord=['desayuno','almuerzo','merienda','cena'];
  const labs={desayuno:'Desayuno · 8:00h',almuerzo:'Almuerzo · 12:00h',merienda:'Merienda · 17:30h',cena:'Cena · 21:00h'};
  document.getElementById('today-meals').innerHTML=ord.map(t=>{
    const x=m[t];const done=!!S.meals[t];
    return `<div class="meal-card${done?' done':''}" id="mc-${t}" onclick="toggleMeal('${t}')">
      <div class="meal-e">${x.tag}</div>
      <div class="meal-info">
        <div class="meal-tipo">${labs[t]}</div>
        <div class="meal-plato">${x.p}</div>
        <div class="meal-kcal">~${x.k} kcal</div>
      </div>
      <div class="meal-ck">${done?ckSVG():''}</div>
    </div>`;
  }).join('');

  const ord2=[1,2,3,4,5,6,0];
  const dnames=['Lunes','Martes','Miércoles','Jueves','Viernes','Sábado','Domingo'];
  document.getElementById('week-meals').innerHTML=ord2.map((d,i)=>{
    const mx=MEALS[d];const isT=d===dow;
    return `<div class="wm-item">
      <div class="wm-head" onclick="document.getElementById('wm${d}').classList.toggle('on')">
        <div class="wm-day-name">${isT?'⬤ ':''}<strong>${dnames[i]}</strong></div>
        <div class="wm-preview">${mx.desayuno.p}</div>
      </div>
      <div class="wm-body${isT?' on':''}" id="wm${d}">
        ${[['Desayuno',mx.desayuno],['Almuerzo',mx.almuerzo],['Merienda',mx.merienda],['Cena',mx.cena]].map(([l,x])=>`
          <div class="wm-row"><div class="wm-rl">${l}</div><div class="wm-rt">${x.tag} ${x.p} <span style="color:var(--muted);font-size:11px">~${x.k}kcal</span></div></div>`).join('')}
      </div>
    </div>`;
  }).join('');
}

function toggleMeal(t){
  S.meals[t]=!S.meals[t];save();
  const c=document.getElementById('mc-'+t);if(!c)return;
  c.classList.toggle('done',S.meals[t]);
  c.querySelector('.meal-ck').innerHTML=S.meals[t]?ckSVG():'';
}

// ── SEMANA ────────────────────────────────────────────────────────────────────
function initSemana(){
  const dow=today.getDay();
  const mon=getMonday();
  document.getElementById('sem-fecha').textContent=`semana del ${mon.getDate()} de ${MN[mon.getMonth()]}`;
  const TASKS=['Trabajo','Ejercicio','Freelance'];
  const grid=document.getElementById('sem-grid');grid.innerHTML='';
  for(let i=0;i<7;i++){
    const d=new Date(mon);d.setDate(mon.getDate()+i);
    const et=EX[d.getDay()];const isT=dk(d)===todayK;
    const col=document.createElement('div');col.className='sem-col'+(isT?' today':'');
    const tasks=TASKS.map(t=>{
      const k=`${dk(d)}_${t}`;const done=!!S.semT[k];
      return `<div class="sem-task${done?' done':''}" onclick="toggleSemTask('${k}',this)"><div class="sem-dot"></div><span>${t}</span></div>`;
    }).join('');
    col.innerHTML=`<div class="sem-dn">${DN[d.getDay()]}</div>
      <div class="sem-dd">${d.getDate()}</div>
      <div class="sem-ex ${et}">${et==='f'?'💪':et==='y'?'🧘':'🌿'}</div>
      <div style="height:1px;width:100%;background:var(--border);margin:2px 0"></div>
      ${tasks}`;
    grid.appendChild(col);
  }
  const ns=document.getElementById('nota-sem');
  ns.value=S.notaSem;
  ns.oninput=e=>{S.notaSem=e.target.value;save();};
}

function toggleSemTask(k,row){
  S.semT[k]=!S.semT[k];save();
  row.classList.toggle('done',S.semT[k]);
}

// ── START ────────────────────────────────────────────────────────────────────
initHoy();
</script>
</body>
</html>
