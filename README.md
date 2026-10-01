<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Битва королевств — план штурма</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Russo+One&family=PT+Sans:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px);
  padding-bottom:env(safe-area-inset-bottom,0px);
  --bg:#e7e9e4; --panel:#f6f7f3; --ink:#1d2320; --muted:#5c665f; --line:#c8ccc3;
  --mud:#b97b56; --mud-dark:#7b4e33; --stone:#8a8f8c;
  --us:#1f6f8b; --us-soft:#d3e7ee; --foe:#b3261e; --foe-soft:#f5d9d6;
  --ring:#1f6f8b55;
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#171b1a; --panel:#202624; --ink:#e6ebe7; --muted:#9aa59e; --line:#36403c;
    --mud:#8e5c3f; --mud-dark:#5a3826; --stone:#6c7370;
    --us:#58b4d1; --us-soft:#173540; --foe:#ef6b61; --foe-soft:#3d1c1a; --ring:#58b4d155;
  }
}
:root[data-theme="dark"]{
  --bg:#171b1a; --panel:#202624; --ink:#e6ebe7; --muted:#9aa59e; --line:#36403c;
  --mud:#8e5c3f; --mud-dark:#5a3826; --stone:#6c7370;
  --us:#58b4d1; --us-soft:#173540; --foe:#ef6b61; --foe-soft:#3d1c1a; --ring:#58b4d155;
}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*,*::before,*::after{box-sizing:inherit}
body{margin:0;background:var(--bg);color:var(--ink);font:17px/1.55 "PT Sans",system-ui,sans-serif}
main{max-width:1180px;margin:0 auto;padding:28px 18px 60px}
h1,h2,h3{font-family:"Russo One","PT Sans",system-ui,sans-serif;font-weight:400;line-height:1.15;margin:0}
h1{font-size:clamp(28px,4.5vw,46px);letter-spacing:.01em}
h2{font-size:24px;margin:44px 0 14px}
h3{font-size:18px;margin-bottom:6px}
p{max-width:72ch;margin:0 0 12px}
.lead{color:var(--muted);font-size:18px;margin-top:10px}
.score{display:flex;gap:28px;flex-wrap:wrap;margin:22px 0 6px;align-items:baseline}
.score b{font-family:"Russo One",sans-serif;font-size:34px}
.score .us b{color:var(--us)} .score .foe b{color:var(--foe)}
.score span{color:var(--muted)}

.mapwrap{display:grid;grid-template-columns:minmax(0,1fr) 300px;gap:20px;margin-top:24px}
@media (max-width:900px){.mapwrap{grid-template-columns:1fr}}
.map{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:10px;overflow-x:auto}
.map svg{display:block;width:100%;min-width:560px;height:auto}
.side{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:16px}
.toggles{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:14px}
.toggles label{display:flex;gap:6px;align-items:center;border:1px solid var(--line);border-radius:999px;padding:4px 12px;cursor:pointer;font-size:15px}
.toggles input{accent-color:var(--us)}
#info{min-height:150px;border-top:1px solid var(--line);padding-top:12px}
#info .who{font-family:"Russo One",sans-serif;font-size:22px}
#info .tag{display:inline-block;font-size:13px;padding:1px 8px;border-radius:6px;margin-left:6px;vertical-align:middle}
.tag.us{background:var(--us-soft);color:var(--us)} .tag.foe{background:var(--foe-soft);color:var(--foe)}
.legend{font-size:14px;color:var(--muted);margin-top:14px;display:grid;gap:6px}
.legend i{display:inline-block;width:14px;height:14px;border-radius:50%;vertical-align:-2px;margin-right:6px}

.alli{cursor:pointer}
.alli:focus{outline:none}
.alli:focus circle,.alli:hover circle{stroke-width:4}
.layer{transition:opacity .2s}
.hidden{opacity:0;pointer-events:none}
@media (prefers-reduced-motion:reduce){.layer{transition:none}}

.table-wrap{overflow-x:auto;background:var(--panel);border:1px solid var(--line);border-radius:14px}
table{border-collapse:collapse;width:100%;min-width:560px;font-size:16px}
th,td{text-align:left;padding:10px 14px;border-bottom:1px solid var(--line);vertical-align:top}
th{font-weight:700;color:var(--muted);font-size:14px}
tr:last-child td{border-bottom:0}
td.num{font-variant-numeric:tabular-nums;white-space:nowrap}
.bar{height:8px;border-radius:4px;background:var(--line);overflow:hidden;min-width:90px;margin-top:6px}
.bar span{display:block;height:100%}

.fronts{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:14px}
.front{background:var(--panel);border:1px solid var(--line);border-left:6px solid var(--us);border-radius:10px;padding:14px 16px}
.front.hot{border-left-color:var(--foe)}
.front .ratio{font-family:"Russo One",sans-serif;font-size:26px}
.front ol{margin:8px 0 0;padding-left:20px}
.front li{margin-bottom:4px}
.front small{color:var(--muted)}

.phases{display:grid;gap:12px;counter-reset:ph}
.phase{display:grid;grid-template-columns:56px 1fr;gap:14px;background:var(--panel);border:1px solid var(--line);border-radius:10px;padding:14px 16px}
.phase::before{counter-increment:ph;content:counter(ph);font-family:"Russo One",sans-serif;font-size:34px;color:var(--us);line-height:1}
.rules{columns:2 300px;column-gap:28px;padding-left:20px}
.rules li{break-inside:avoid;margin-bottom:8px}
.note{font-size:15px;color:var(--muted);max-width:80ch}
.topbtns{position:fixed;right:14px;top:calc(env(safe-area-inset-top,0px) + 12px);display:flex;gap:8px;z-index:5}
button.theme{border:1px solid var(--line);background:var(--panel);color:var(--ink);border-radius:999px;padding:6px 12px;font:inherit;font-size:14px;cursor:pointer}
:focus-visible{outline:3px solid var(--us);outline-offset:2px}
</style>
</head>
<body>
<div class="topbtns"><button class="theme" id="langBtn" type="button" aria-label="Language">EN</button><button class="theme" id="themeBtn" type="button" data-i18n="theme">Тема</button></div>
<main>
  <h1 data-i18n="h1">Штурм замка C</h1>
  <p class="lead" data-i18n="lead">План атаки на грязь: кто куда встаёт, кто кого держит и в каком порядке берём башни.</p>
  <div class="score">
    <div class="us"><b>153</b> <span data-i18n="usPow">наша ударная сила, 10 альянсов</span></div>
    <div class="foe"><b>67</b> <span data-i18n="foePow">сила противника, 5 альянсов</span></div>
  </div>
  <p class="note" data-i18n="powNote">Сила считается условно: игрок с т10 = 5, т9 = 3, т8 = 1. Массу т7 и ниже не учитываем, но помним, что у слабых альянсов противника её много.</p>

  <div class="mapwrap">
    <div class="map">
      <svg viewBox="0 0 760 600" role="img" aria-label="Схема поля боя с расстановкой альянсов">
        <defs>
          <marker id="arrUs" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="var(--us)"/></marker>
          <marker id="arrFoe" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="var(--foe)"/></marker>
          <pattern id="mudTex" width="18" height="18" patternUnits="userSpaceOnUse"><circle cx="4" cy="5" r="1.4" fill="#000" opacity=".07"/><circle cx="13" cy="13" r="1" fill="#000" opacity=".07"/></pattern>
        </defs>

        <!-- mud -->
        <rect x="118" y="108" width="507" height="384" rx="6" fill="var(--mud)"/>
        <rect x="118" y="108" width="507" height="384" rx="6" fill="url(#mudTex)"/>
        <rect x="118" y="108" width="507" height="384" rx="6" fill="none" stroke="var(--ink)" stroke-width="2"/>
        <text x="128" y="128" font-size="13" fill="#fff" opacity=".8" font-family="PT Sans" data-i18n="mud">грязь — зона битвы</text>

        <!-- tower rings: inner = strongest -->
        <g id="lyrRings" class="layer" fill="none" stroke="var(--ring)" stroke-dasharray="5 5" stroke-width="1.5">
          <circle cx="296" cy="254" r="60"/><circle cx="296" cy="254" r="120"/>
          <circle cx="434" cy="254" r="60"/><circle cx="434" cy="254" r="120"/>
          <circle cx="296" cy="342" r="60"/><circle cx="296" cy="342" r="120"/>
          <circle cx="434" cy="342" r="60"/><circle cx="434" cy="342" r="120"/>
        </g>

        <!-- inner zone -->
        <rect x="285" y="243" width="160" height="110" rx="4" fill="var(--mud-dark)"/>
        <rect x="341" y="275" width="46" height="44" rx="3" fill="var(--stone)" stroke="#fff" stroke-width="1.5"/>
        <text x="364" y="303" text-anchor="middle" font-family="Russo One" font-size="18" fill="#fff">C</text>
        <g font-family="Russo One" font-size="13" fill="#fff" text-anchor="middle">
          <rect x="284" y="242" width="24" height="24" rx="3" fill="var(--stone)"/><text x="296" y="259">W</text>
          <rect x="422" y="242" width="24" height="24" rx="3" fill="var(--stone)"/><text x="434" y="259">N</text>
          <rect x="284" y="330" width="24" height="24" rx="3" fill="var(--stone)"/><text x="296" y="347">S</text>
          <rect x="422" y="330" width="24" height="24" rx="3" fill="var(--stone)"/><text x="434" y="347">E</text>
        </g>

        <!-- enemy -->
        <g id="lyrFoe" class="layer" font-family="Russo One" text-anchor="middle">
          <g class="alli" tabindex="0" data-id="NOT"><rect x="391" y="20" width="231" height="80" rx="18" fill="var(--foe-soft)" stroke="var(--foe)" stroke-width="2"/><text x="506" y="56" font-size="18" fill="var(--foe)">NOT</text><text x="506" y="78" font-size="12" font-family="PT Sans" fill="var(--muted)" data-i18n="sNOT">сила 2 · слабый</text></g>
          <g class="alli" tabindex="0" data-id="GgWp"><rect x="31" y="190" width="76" height="219" rx="18" fill="var(--foe-soft)" stroke="var(--foe)" stroke-width="3"/><text x="69" y="296" font-size="17" fill="var(--foe)">GgWp</text><text x="69" y="316" font-size="12" font-family="PT Sans" fill="var(--muted)" data-i18n="sGg">сила 22</text></g>
          <g class="alli" tabindex="0" data-id="NGoH"><rect x="631" y="298" width="90" height="190" rx="18" fill="var(--foe-soft)" stroke="var(--foe)" stroke-width="2"/><text x="676" y="392" font-size="17" fill="var(--foe)">NGoH</text><text x="676" y="412" font-size="12" font-family="PT Sans" fill="var(--muted)" data-i18n="sNG">сила 3</text></g>
          <g class="alli" tabindex="0" data-id="UNB"><rect x="119" y="498" width="232" height="67" rx="18" fill="var(--foe-soft)" stroke="var(--foe)" stroke-width="4"/><text x="235" y="529" font-size="19" fill="var(--foe)">UNB</text><text x="235" y="550" font-size="12" font-family="PT Sans" fill="var(--muted)" data-i18n="sUNB">сила 40 · главная угроза, т10</text></g>
          <g class="alli" tabindex="0" data-id="VRN"><rect x="375" y="498" width="245" height="67" rx="18" fill="var(--foe-soft)" stroke="var(--foe)" stroke-width="1.5"/><text x="497" y="529" font-size="18" fill="var(--foe)">VRN</text><text x="497" y="550" font-size="12" font-family="PT Sans" fill="var(--muted)" data-i18n="sVRN">сила 0 · только т7</text></g>
        </g>

        <!-- enemy pressure arrows -->
        <g id="lyrFoeArr" class="layer" stroke="var(--foe)" stroke-width="2.5" fill="none" opacity=".75">
          <path d="M235 498 L285 372" marker-end="url(#arrFoe)"/>
          <path d="M107 300 L270 262" marker-end="url(#arrFoe)"/>
          <path d="M107 360 L268 340" marker-end="url(#arrFoe)" stroke-dasharray="6 5"/>
        </g>

        <!-- our alliances -->
        <g id="lyrUs" class="layer" font-family="Russo One" text-anchor="middle">
          <!-- S front -->
          <g class="alli" tabindex="0" data-id="REG"><circle cx="252" cy="392" r="26" fill="var(--us)" stroke="var(--panel)" stroke-width="2"/><text x="252" y="397" font-size="13" fill="#fff">REG</text></g>
          <g class="alli" tabindex="0" data-id="IRON"><circle cx="318" cy="428" r="24" fill="var(--us)" stroke="var(--panel)" stroke-width="2"/><text x="318" y="433" font-size="12" fill="#fff">IRON</text></g>
          <g class="alli" tabindex="0" data-id="RPL"><circle cx="172" cy="452" r="15" fill="var(--us-soft)" stroke="var(--us)" stroke-width="2"/><text x="172" y="456" font-size="10" fill="var(--us)">RPL</text></g>
          <g class="alli" tabindex="0" data-id="Asp"><circle cx="545" cy="425" r="15" fill="var(--us-soft)" stroke="var(--us)" stroke-width="2"/><text x="545" y="429" font-size="10" fill="var(--us)">Asp</text></g>
          <!-- W front -->
          <g class="alli" tabindex="0" data-id="GOD"><circle cx="240" cy="226" r="24" fill="var(--us)" stroke="var(--panel)" stroke-width="2"/><text x="240" y="231" font-size="13" fill="#fff">GOD</text></g>
          <g class="alli" tabindex="0" data-id="SWA"><circle cx="190" cy="296" r="23" fill="var(--us)" stroke="var(--panel)" stroke-width="2"/><text x="190" y="301" font-size="13" fill="#fff">SWA</text></g>
          <g class="alli" tabindex="0" data-id="SHN"><circle cx="190" cy="150" r="15" fill="var(--us-soft)" stroke="var(--us)" stroke-width="2"/><text x="190" y="154" font-size="10" fill="var(--us)">SHN</text></g>
          <!-- N front -->
          <g class="alli" tabindex="0" data-id="POH"><circle cx="490" cy="212" r="20" fill="var(--us)" stroke="var(--panel)" stroke-width="2"/><text x="490" y="217" font-size="12" fill="#fff">POH</text></g>
          <g class="alli" tabindex="0" data-id="PHNX"><circle cx="420" cy="150" r="16" fill="var(--us-soft)" stroke="var(--us)" stroke-width="2"/><text x="420" y="154" font-size="9" fill="var(--us)">PHNX</text></g>
          <!-- E front -->
          <g class="alli" tabindex="0" data-id="KTK"><circle cx="492" cy="386" r="18" fill="var(--us)" stroke="var(--panel)" stroke-width="2"/><text x="492" y="390" font-size="11" fill="#fff">KTK</text></g>
        </g>

        <!-- our attack arrows -->
        <g id="lyrUsArr" class="layer" stroke="var(--us)" stroke-width="2.5" fill="none">
          <path d="M268 372 L289 356" marker-end="url(#arrUs)"/>
          <path d="M305 405 L299 360" marker-end="url(#arrUs)"/>
          <path d="M256 242 L282 256" marker-end="url(#arrUs)"/>
          <path d="M210 284 L280 262" marker-end="url(#arrUs)"/>
          <path d="M474 222 L448 248" marker-end="url(#arrUs)"/>
          <path d="M478 372 L450 352" marker-end="url(#arrUs)"/>
          <!-- castle hits -->
          <path d="M330 406 Q350 360 360 324" marker-end="url(#arrUs)" stroke-dasharray="4 5"/>
          <path d="M210 300 Q300 300 336 298" marker-end="url(#arrUs)" stroke-dasharray="4 5"/>
          <!-- reserve shift -->
          <path d="M532 414 Q520 400 510 398" marker-end="url(#arrUs)" stroke-width="2"/>
          <path d="M436 158 Q470 170 478 192" marker-end="url(#arrUs)" stroke-dasharray="2 4" stroke-width="2"/>
        </g>
      </svg>
    </div>

    <aside class="side">
      <div class="toggles" role="group" aria-label="Слои карты">
        <label><input type="checkbox" data-layer="lyrUs,lyrUsArr" checked> <span data-i18n="tUs">Наши</span></label>
        <label><input type="checkbox" data-layer="lyrFoe,lyrFoeArr" checked> <span data-i18n="tFoe">Противник</span></label>
        <label><input type="checkbox" data-layer="lyrRings" checked> <span data-i18n="tRings">Кольца</span></label>
      </div>
      <div id="info" aria-live="polite">
        <div class="who" data-i18n="pick">Нажми на альянс</div>
        <p class="note" data-i18n="pickNote">Покажу состав, силу и задачу в бою.</p>
      </div>
      <div class="legend">
        <div><i style="background:var(--us)"></i><span data-i18n="lg1">наш ударный альянс — первое кольцо</span></div>
        <div><i style="background:var(--us-soft);border:2px solid var(--us)"></i><span data-i18n="lg2">наша поддержка — внешнее кольцо</span></div>
        <div><i style="background:var(--foe-soft);border:2px solid var(--foe)"></i><span data-i18n="lg3">противник, толщина рамки = угроза</span></div>
        <div data-i18n="lg4">Сплошная стрелка — захват башни, пунктир — удары по замку, точки — переброска резерва.</div>
      </div>
    </aside>
  </div>

  <h2 data-i18n="hPow">Соотношение сил</h2>
  <div class="table-wrap">
    <table>
      <thead><tr><th data-i18n="thA">Альянс</th><th>т10</th><th>т9</th><th>т8</th><th data-i18n="thL">Ср. ур.</th><th data-i18n="thP">Сила</th></tr></thead>
      <tbody id="powerRows"></tbody>
    </table>
  </div>

  <h2 data-i18n="hFr">Фронты у башен</h2>
  <div class="fronts">
    <div class="front hot"><div data-i18n="fS">
      <h3>Башня S — против UNB</h3>
      <div class="ratio">81 : 40</div><small>перевес ×2, главный фронт</small>
      <ol>
        <li><b>REG</b> — первое кольцо, заходит в башню и держит гарнизон</li>
        <li><b>IRON</b> — второе кольцо, добивает отряды UNB, после стабилизации бьёт замок</li>
        <li><b>RPL</b> — внешнее кольцо, подкрепления в гарнизон и атаки по подходящим маршам</li>
      </ol></div>
    </div>
    <div class="front hot"><div data-i18n="fW">
      <h3>Башня W — против GgWp</h3>
      <div class="ratio">56 : 22</div><small>перевес ×2,5</small>
      <ol>
        <li><b>GOD</b> — первое кольцо, держит башню</li>
        <li><b>SWA</b> — второе кольцо, 28 т8: давит массой, отсекает GgWp от S</li>
        <li><b>SHN</b> — внешнее кольцо, подкрепления</li>
      </ol></div>
    </div>
    <div class="front"><div data-i18n="fN">
      <h3>Башня N — против NOT и части NGoH</h3>
      <div class="ratio">10 : ~4</div><small>быстрый захват</small>
      <ol>
        <li><b>POH</b> — первое кольцо, держит башню</li>
        <li><b>PHNX</b> — поддержка, доливает войска в гарнизон POH</li>
      </ol></div>
    </div>
    <div class="front"><div data-i18n="fE">
      <h3>Башня E — против VRN и части NGoH</h3>
      <div class="ratio">6 : ~2</div><small>быстрый захват, POH страхует</small>
      <ol>
        <li><b>KTK</b> — первое кольцо, заходит сразу на старте</li>
        <li><b>Asp</b> — второе кольцо, доливает гарнизон и встречает массу т7 от VRN</li>
      </ol></div>
    </div>
  </div>

  <h2 data-i18n="hPh">Порядок действий</h2>
  <div class="phases">
    <div class="phase"><div data-i18n="p1"><h3>Старт: заходим во все четыре башни одновременно</h3><p>N и E почти без сопротивления — это бесплатный урон каждые 15 секунд с первой минуты. Первыми в башни входят ударные альянсы первого кольца, не поддержка.</p></div></div>
    <div class="phase"><div data-i18n="p2"><h3>Удержание S и W</h3><p>UNB и GgWp будут выбивать нас. Второе кольцо (IRON, SWA) бьёт их отряды на подходе, поддержка постоянно доливает войска в гарнизон. Башня ни на секунду не должна оставаться пустой.</p></div></div>
    <div class="phase"><div data-i18n="p3"><h3>Удары по замку</h3><p>Как только у башни нет активной атаки, свободные марши IRON и SWA идут на замок и возвращаются. Сильные игроки REG остаются в гарнизоне S до конца.</p></div></div>
    <div class="phase"><div data-i18n="p4"><h3>Ротация и переброска</h3><p>Раненые выходят на лечение, их место сразу занимает следующий отряд. Если какая-то башня падает — её отбивает ближайший ударный альянс, поддержка с N и E подтягивается к S.</p></div></div>
  </div>

  <h2 data-i18n="hRu">Правила на бой</h2>
  <ul class="rules" data-i18n="rules">
    <li>У UNB есть игрок с т10 — не меняться с ним в лоб слабыми отрядами, на него идут только ралли REG и IRON.</li>
    <li>Разведка всех пяти альянсов противника перед стартом: проверить, кто реально пришёл и где стоят их т9.</li>
    <li>Поддержка стоит дальше от башен и под щитом, если он доступен: она нужна живой до конца боя.</li>
    <li>GgWp может развернуться на S — SWA следит за этим и перехватывает.</li>
    <li>VRN и NOT слабые по т8, но у них много т7. Если масса прёт на E или N — не геройствовать, звать резерв.</li>
    <li>Один ответственный за каждую башню в чате: он командует, когда доливать гарнизон.</li>
  </ul>
  </main>

<script>
const D = {
  REG:{side:"us",t10:0,t9:6,t8:25,lvl:23,n:"—",role:"Башня S, первое кольцо. Главный кулак: держит гарнизон против UNB до конца боя.",roleEn:"Tower S, inner ring. Our main fist: holds the garrison against UNB until the end."},
  IRON:{side:"us",t10:0,t9:1,t8:32,lvl:23,n:99,role:"Башня S, второе кольцо. Бьёт марши UNB, в спокойные моменты — удары по замку. Игрок 30 ур. ведёт ралли.",roleEn:"Tower S, second ring. Hits UNB marches; during calm moments attacks the castle. The level-30 player leads rallies."},
  GOD:{side:"us",t10:0,t9:2,t8:20,lvl:22,n:100,role:"Башня W, первое кольцо. Держит башню против GgWp.",roleEn:"Tower W, inner ring. Holds the tower against GgWp."},
  SWA:{side:"us",t10:0,t9:0,t8:28,lvl:22,n:99,role:"Башня W, второе кольцо. Масса т8: давит GgWp и не даёт им уйти помогать UNB. Свободные марши — в замок.",roleEn:"Tower W, second ring. T8 mass: pushes GgWp and keeps them from helping UNB. Free marches go to the castle."},
  POH:{side:"us",t10:0,t9:0,t8:9,lvl:22,n:99,role:"Башня N, первое кольцо. Быстрый захват на старте.",roleEn:"Tower N, inner ring. Fast capture at the start."},
  KTK:{side:"us",t10:0,t9:0,t8:5,lvl:20,n:96,role:"Башня E, первое кольцо. Заходит сразу, против VRN почти без боя.",roleEn:"Tower E, inner ring. Goes in right away, almost no fight against VRN."},
  RPL:{side:"us",t10:0,t9:0,t8:3,lvl:21,n:92,role:"Поддержка S, внешнее кольцо. Доливает войска в гарнизон REG.",roleEn:"S support, outer ring. Tops up REG's garrison."},
  SHN:{side:"us",t10:0,t9:0,t8:2,lvl:21,n:94,role:"Поддержка W, внешнее кольцо. Доливает войска в гарнизон GOD.",roleEn:"W support, outer ring. Tops up GOD's garrison."},
  PHNX:{side:"us",t10:0,t9:0,t8:1,lvl:20,n:100,role:"Поддержка N. Доливает войска в гарнизон POH.",roleEn:"N support. Tops up POH's garrison."},
  Asp:{side:"us",t10:0,t9:0,t8:1,lvl:19,n:99,role:"Башня E, второе кольцо. Доливает гарнизон KTK и встречает массу т7 от VRN.",roleEn:"Tower E, second ring. Tops up KTK's garrison and meets VRN's T7 mass."},
  UNB:{side:"foe",t10:1,t9:2,t8:29,lvl:23,n:98,role:"Самый сильный противник, стоит у S. Против него REG + IRON.",roleEn:"Strongest enemy, positioned by S. REG + IRON go against them."},
  GgWp:{side:"foe",t10:0,t9:3,t8:13,lvl:22,n:100,role:"Второй по силе, у W. Может развернуться на помощь UNB к S.",roleEn:"Second strongest, by W. May turn to help UNB at S."},
  NOT:{side:"foe",t10:0,t9:0,t8:2,lvl:21,n:99,role:"Слабый, над N. Много т7 — опасен только массой.",roleEn:"Weak, above N. Lots of T7 — dangerous only by numbers."},
  NGoH:{side:"foe",t10:0,t9:0,t8:3,lvl:21,n:86,role:"Слабый, справа между N и E. Может метаться между двумя башнями.",roleEn:"Weak, on the right between N and E. May switch between the two towers."},
  VRN:{side:"foe",t10:0,t9:0,t8:0,lvl:20,n:98,role:"Без игроков выше 23 ур. Только масса т7 у башни E.",roleEn:"No players above level 23. Only a T7 mass near tower E."}
};
const pw = a => a.t10*5 + a.t9*3 + a.t8;
let lang="ru";
const info = document.getElementById("info");
let cur=null;
function show(id){
  const a = D[id]; if(!a) return; cur=id;
  const en=lang==="en";
  info.innerHTML = `<div class="who">${id}<span class="tag ${a.side}">${a.side==="us"?(en?"ours":"наши"):(en?"enemy":"противник")}</span></div>
  <p class="note">${en?"Players":"Игроков"}: ${a.n} · ${en?"avg. lvl":"ср. ур."} ~${a.lvl}<br>${en?"T10":"т10"}: ${a.t10} · ${en?"T9":"т9"}: ${a.t9} · ${en?"T8":"т8"}: ${a.t8} · ${en?"power":"сила"} <b>${pw(a)}</b></p><p>${en?a.roleEn:a.role}</p>`;
}
document.querySelectorAll(".alli").forEach(g=>{
  g.addEventListener("click",()=>show(g.dataset.id));
  g.addEventListener("keydown",e=>{if(e.key==="Enter"||e.key===" "){e.preventDefault();show(g.dataset.id)}});
});
document.querySelectorAll("[data-layer]").forEach(cb=>cb.addEventListener("change",()=>{
  cb.dataset.layer.split(",").forEach(id=>document.getElementById(id).classList.toggle("hidden",!cb.checked));
}));
const rows = Object.entries(D).sort((a,b)=>(a[1].side===b[1].side?pw(b[1])-pw(a[1]):a[1].side==="us"?-1:1));
const max = Math.max(...rows.map(r=>pw(r[1])));
document.getElementById("powerRows").innerHTML = rows.map(([id,a])=>`<tr>
<td><b style="color:var(--${a.side})">${id}</b></td><td class="num">${a.t10}</td><td class="num">${a.t9}</td><td class="num">${a.t8}</td><td class="num">~${a.lvl}</td>
<td class="num">${pw(a)}<div class="bar"><span style="width:${pw(a)/max*100}%;background:var(--${a.side})"></span></div></td></tr>`).join("");
const btn=document.getElementById("themeBtn");
btn.addEventListener("click",()=>{
  const r=document.documentElement;
  const dark = r.dataset.theme ? r.dataset.theme==="dark" : matchMedia("(prefers-color-scheme: dark)").matches;
  r.dataset.theme = dark ? "light" : "dark";
});

const EN={"theme": "Theme", "h1": "Assault on Castle C", "lead": "Attack plan for the mud: who stands where, who holds whom, and the order we take the towers.", "usPow": "our strike power, 10 alliances", "foePow": "enemy power, 5 alliances", "powNote": "Power is approximate: a T10 player = 5, T9 = 3, T8 = 1. T7 and below are not counted, but remember that the weak enemy alliances have a lot of them.", "mud": "mud — battle zone", "sNOT": "power 2 · weak", "sGg": "power 22", "sNG": "power 3", "sUNB": "power 40 · main threat, T10", "sVRN": "power 0 · T7 only", "tUs": "Ours", "tFoe": "Enemy", "tRings": "Rings", "pick": "Tap an alliance", "pickNote": "I will show its roster, power and battle task.", "lg1": "our strike alliance — inner ring", "lg2": "our support — outer ring", "lg3": "enemy, border thickness = threat", "lg4": "Solid arrow — tower capture, dashed — castle hits, dotted — reserve shift.", "hPow": "Balance of power", "thA": "Alliance", "thL": "Avg. lvl", "thP": "Power", "hFr": "Tower fronts", "hPh": "Order of actions", "hRu": "Battle rules", "fS": "<h3>Tower S — vs UNB</h3><div class=\"ratio\">81 : 40</div><small>2× advantage, main front</small><ol><li><b>REG</b> — inner ring, enters the tower and holds the garrison</li><li><b>IRON</b> — second ring, finishes off UNB squads, hits the castle once things are stable</li><li><b>RPL</b> — outer ring, reinforces the garrison and attacks incoming marches</li></ol>", "fW": "<h3>Tower W — vs GgWp</h3><div class=\"ratio\">56 : 22</div><small>2.5× advantage</small><ol><li><b>GOD</b> — inner ring, holds the tower</li><li><b>SWA</b> — second ring, 28 T8: pushes with numbers, cuts GgWp off from S</li><li><b>SHN</b> — outer ring, reinforcements</li></ol>", "fN": "<h3>Tower N — vs NOT and part of NGoH</h3><div class=\"ratio\">10 : ~4</div><small>fast capture</small><ol><li><b>POH</b> — inner ring, holds the tower</li><li><b>PHNX</b> — support, tops up POH's garrison</li></ol>", "fE": "<h3>Tower E — vs VRN and part of NGoH</h3><div class=\"ratio\">6 : ~2</div><small>fast capture, POH covers</small><ol><li><b>KTK</b> — inner ring, goes in right at the start</li><li><b>Asp</b> — second ring, tops up the garrison and meets VRN's T7 mass</li></ol>", "p1": "<h3>Start: enter all four towers at once</h3><p>N and E have almost no resistance — free damage every 15 seconds from the first minute. Inner-ring strike alliances enter the towers first, not the support.</p>", "p2": "<h3>Holding S and W</h3><p>UNB and GgWp will try to knock us out. The second ring (IRON, SWA) hits their squads on approach, support keeps topping up the garrison. A tower must never stay empty, not even for a second.</p>", "p3": "<h3>Castle hits</h3><p>Whenever a tower is not under active attack, free IRON and SWA marches go to the castle and return. REG's strong players stay in the S garrison until the end.</p>", "p4": "<h3>Rotation and shifting</h3><p>Wounded players leave to heal and the next squad takes their place immediately. If a tower falls, the nearest strike alliance retakes it, and support from N and E moves toward S.</p>", "rules": "<li>UNB has a T10 player — do not trade with him head-on using weak squads; only REG and IRON rallies go at him.</li><li>Scout all five enemy alliances before the start: check who actually showed up and where their T9s are.</li><li>Support stands farther from the towers and under a shield if available: it needs to stay alive until the end.</li><li>GgWp may turn toward S — SWA watches for it and intercepts.</li><li>VRN and NOT are weak in T8 but have lots of T7. If a mass pushes on E or N, don't play hero — call the reserve.</li><li>One person in charge of each tower in chat: they call when to top up the garrison.</li>"};
const RU={}; document.querySelectorAll("[data-i18n]").forEach(el=>{RU[el.dataset.i18n]=el.innerHTML});
const META={ru:{title:"Битва королевств — план штурма",map:"Схема поля боя с расстановкой альянсов",btn:"EN",btnLbl:"Switch to English"},
            en:{title:"Kingdom Battle — Assault Plan",map:"Battlefield map with alliance positions",btn:"RU",btnLbl:"Переключить на русский"}};
const langBtn=document.getElementById("langBtn");
function setLang(l){
  lang=l; const dict=l==="en"?EN:RU;
  document.querySelectorAll("[data-i18n]").forEach(el=>{const v=dict[el.dataset.i18n]; if(v!=null) el.innerHTML=v;});
  document.documentElement.lang=l; document.title=META[l].title;
  document.querySelector(".map svg").setAttribute("aria-label",META[l].map);
  langBtn.textContent=META[l].btn; langBtn.setAttribute("aria-label",META[l].btnLbl);
  if(cur) show(cur);
  try{localStorage.setItem("kvk-lang",l)}catch(e){}
}
langBtn.addEventListener("click",()=>setLang(lang==="ru"?"en":"ru"));
let saved=null; try{saved=localStorage.getItem("kvk-lang")}catch(e){}
if(saved==="en") setLang("en");
</script>
</body>
</html>
