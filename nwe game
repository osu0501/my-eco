<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>지구 리부트 | Earth Reboot</title>
  <style>
    :root{
      --bg:#f5f7f2;
      --text:#26332a;
      --accent:#4caf50;
      --panel: rgba(255,255,255,0.95);
    }
    *{box-sizing:border-box;margin:0;padding:0;font-family:Inter, Pretendard, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;}
    html,body{height:100%;}
    body{
      background:var(--bg);
      color:var(--text);
      -webkit-tap-highlight-color: transparent;
    }

    .stage{
      width:100%;
      height:100vh;
      display:flex;
      flex-direction:column;
      align-items:center;
      justify-content:center;
      position:relative;
      overflow:hidden;
      padding:1.6rem;
    }
    .hidden{display:none;}
    .topbar{
      position:fixed; top:12px; left:12px; right:12px;
      display:flex; justify-content:space-between; align-items:center;
      z-index:2000; gap:12px;
    }
    .title{
      background:var(--panel);
      padding:.6rem 1rem; border-radius:12px; font-weight:700;
      box-shadow:0 6px 18px rgba(0,0,0,0.06);
    }
    .scoreBox{
      background:var(--panel); padding:.5rem 0.9rem; border-radius:12px; font-weight:600;
      box-shadow:0 6px 18px rgba(0,0,0,0.06);
    }

    h1{font-size:1.6rem; margin-bottom:.6rem;}
    p{max-width:860px; text-align:center; line-height:1.6; margin-bottom:1rem; background:var(--panel); padding:0.9rem 1rem; border-radius:12px;}

    button.btn{
      background:var(--accent); color:white; border:none; padding:.72rem 1rem; border-radius:999px; font-weight:700;
      box-shadow:0 8px 18px rgba(76,175,80,0.18); cursor:pointer;
    }
    button.btn.secondary{background:#9aaea1;}
    button.btn:active{transform:translateY(2px);}

    footer{position:fixed;left:0;right:0;bottom:0;padding:10px 12px;text-align:center;background:rgba(232,240,228,0.9);font-size:.85rem;color:#516652;}

    .character{ position:absolute; bottom:8%; left:6%; width:120px; height:120px; z-index:1500; background:var(--panel); border-radius:14px; display:flex; align-items:center; justify-content:center; box-shadow:0 8px 20px rgba(0,0,0,0.12); padding:8px; }
    .dialog{ position:absolute; bottom:8%; right:6%; z-index:1500; background:var(--panel); padding:12px 14px; border-radius:14px; max-width:46%; box-shadow:0 8px 20px rgba(0,0,0,0.12); font-weight:600; }

    /* backgrounds by stage */
    #stage0{background:linear-gradient(180deg,#eef7f0,#f5f7f2);}
    #stage1{background:linear-gradient(180deg,#cfdcd0,#eef7f0);}
    #stage2{background:linear-gradient(180deg,#e8f8ff,#eef7f0);}
    #stage3{background:linear-gradient(180deg,#f0f9f2,#eef7f0);}
    #stage4{background:linear-gradient(180deg,#dbf3ff,#eef7f0);}
    #stage5{background:linear-gradient(180deg,#fff7e6,#f9f6ed);}
    #stage6{background:linear-gradient(180deg,#fff6f6,#fbf8f7);}
    #stage7{background:linear-gradient(180deg,#e8fbef,#f5fff5);}

    .obj{ position:absolute; touch-action:none; user-select:none; cursor:pointer; transition:transform .18s ease, opacity .25s ease; }
    .cloud{width:110px;height:66px;background:linear-gradient(#fff,#f2f2f2); border-radius:40px; box-shadow:0 8px 18px rgba(0,0,0,0.08); display:flex; align-items:center; justify-content:center; font-weight:700; color:#6b6b6b;}
    .trash{width:56px;height:56px;background:#fff;border-radius:10px;border:2px solid rgba(0,0,0,0.06);display:flex;align-items:center;justify-content:center;font-weight:800;color:#7b7b7b;}
    .seed{width:46px;height:46px;border-radius:8px;background:#fff;border:2px dashed rgba(0,0,0,0.06);display:flex;align-items:center;justify-content:center;font-weight:700;}
    .plastic{width:48px;height:48px;border-radius:8px;background:#fff;border:2px solid rgba(0,0,0,0.06);display:flex;align-items:center;justify-content:center;font-weight:700;}
    .building{width:90px;height:120px;background:linear-gradient(#e6e6e6,#cfcfcf);border-radius:8px;display:flex;flex-direction:column;gap:6px;padding:8px;align-items:center;justify-content:flex-end;}
    .window{width:20px;height:16px;background:#1f1f1f;border-radius:2px;transition:background .25s ease;}
    .window.on{background:gold;}
    .vehicle{width:84px;height:48px;background:#fff;border-radius:8px;border:2px solid rgba(0,0,0,0.06);display:flex;align-items:center;justify-content:center;font-weight:700;}
    .butterfly{position:absolute;width:46px;height:46px;background:url('https://cdn-icons-png.flaticon.com/512/616/616408.png') center/cover no-repeat; transform-origin:center;}

    @media (max-width:520px){
      .dialog{max-width:75%; bottom:6%; right:4%;}
      .character{left:4%; width:100px; height:100px;}
    }
  </style>
</head>
<body>

  <div class="topbar">
    <div class="title">🌍 지구 리부트</div>
    <div class="scoreBox">환경 지수: <span id="ecoScore">0</span></div>
  </div>

  <section id="stage0" class="stage">
    <h1>시작하기</h1>
    <p>AI와 함께 지구를 되살리는 7단계 미션입니다. 각 스테이지에서 배경의 오브젝트를 직접 터치하거나 드래그해 상호작용하세요.</p>
    <div style="display:flex;gap:12px;">
      <button class="btn" id="startBtn">시작하기</button>
      <button class="btn secondary" id="howBtn">플레이 방법</button>
    </div>
  </section>

  <section id="stage1" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog1">AI 가디언: 도시의 회색 구름을 직접 밀어보세요.</div>
    <h1>Stage 1 — 공기 정화</h1>
    <p>구름(먼지)을 스와이프하거나 터치하여 제거하면 하늘이 맑아집니다.</p>
    <div id="cloudLayer" style="width:100%;height:60%;position:absolute;top:6%;left:0;pointer-events:none;"></div>
  </section>

  <section id="stage2" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog2">AI 가디언: 거리의 쓰레기를 하나씩 눌러 치워주세요.</div>
    <h1>Stage 2 — 거리 청소</h1>
    <p>바닥에 나타나는 쓰레기를 터치하면 사라집니다.</p>
    <div id="trashLayer" style="width:100%;height:60%;position:absolute;bottom:12%;left:0;"></div>
  </section>

  <section id="stage3" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog3">AI 가디언: 빈 땅을 탭하면 묘목이 자랍니다. 여러 번 심어 숲을 만들어보세요.</div>
    <h1>Stage 3 — 묘목 심기</h1>
    <p>땅을 탭(혹은 클릭)하면 묘목이 심어져 자랍니다.</p>
    <div id="ground" style="width:100%;height:60%;position:absolute;bottom:6%;left:0;"></div>
  </section>

  <section id="stage4" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog4">AI 가디언: 떠다니는 플라스틱을 눌러 바다를 깨끗하게 해주세요.</div>
    <h1>Stage 4 — 바다 정화</h1>
    <p>물 위의 플라스틱을 눌러 제거하면 물 색이 맑아집니다.</p>
    <div id="seaLayer" style="width:100%;height:60%;position:absolute;top:8%;left:0;"></div>
  </section>

  <section id="stage5" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog5">AI 가디언: 켜진 조명을 꺼서 에너지를 절약하세요.</div>
    <h1>Stage 5 — 에너지 절약</h1>
    <p>건물의 창문을 눌러 불을 끄면 에너지 점수가 올라갑니다.</p>
    <div id="buildingLayer" style="width:100%;height:60%;position:absolute;bottom:4%;left:0;"></div>
  </section>

  <section id="stage6" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog6">AI 가디언: 자동차를 눌러 자전거로 바꿔보세요.</div>
    <h1>Stage 6 — 탄소 절감 생활</h1>
    <p>도로의 자동차를 눌러 자전거로 바꾸면 탄소 배출이 줄어듭니다.</p>
    <div id="roadLayer" style="width:100%;height:60%;position:absolute;bottom:6%;left:0;"></div>
  </section>

  <section id="stage7" class="stage hidden">
    <div class="character"><img src="https://cdn-icons-png.flaticon.com/512/3093/3093402.png" alt="guardian" style="width:100%;height:100%;object-fit:contain;border-radius:8px;"></div>
    <div class="dialog" id="dialog7">AI 가디언: 화면을 스와이프하거나 탭해서 나비를 풀어주세요. 지구가 회복됩니다.</div>
    <h1>Stage 7 — 숲의 회복 (엔딩)</h1>
    <p>대시나 탭으로 나비를 생성해 숲을 활기차게 만드세요. 충분히 만들면 엔딩이 나타납니다.</p>
    <div id="forestLayer" style="width:100%;height:70%;position:absolute;bottom:0;left:0;"></div>
  </section>

  <footer>© 2025 김보아 — 지구 리부트 (Earth Reboot) 모든 창작의 지적소유권은 김보아에게 있습니다.</footer>

<script>
  // 상태
  let stageIndex = 0; // 0..7
  let ecoScore = 0;
  const MAX_STAGE = 7;
  const inited = {}; // init flags per stage

  const $score = id => document.getElementById(id);
  const updateScoreUI = ()=> { $score('ecoScore').textContent = ecoScore; };

  function showStage(index){
    // hide all
    for(let i=0;i<=MAX_STAGE;i++){
      const s = document.getElementById('stage'+i);
      if(s) s.classList.add('hidden');
    }
    const active = document.getElementById('stage'+index);
    if(active) active.classList.remove('hidden');
    stageIndex = index;
  }

  // 안전한 nextStage: 초기화 호출 관리
  function nextStage(){
    const next = stageIndex + 1;
    if(next > MAX_STAGE){
      showEnding();
      return;
    }
    showStage(next);
    // init only once
    if(!inited[next]){
      inited[next] = true;
      const fn = {
        1: initStage1,
        2: initStage2,
        3: initStage3,
        4: initStage4,
        5: initStage5,
        6: initStage6,
        7: initStage7
      }[next];
      if(fn) fn();
    }
  }

  function advanceAfterDelay(ms=900){ setTimeout(nextStage, ms); }

  // 유틸
  function rand(min,max){ return Math.floor(Math.random()*(max-min+1))+min; }
  function createObj(className, xPct, yPct, html){
    const el = document.createElement('div');
    el.className = 'obj ' + className;
    el.style.left = xPct + '%';
    el.style.top = yPct + '%';
    el.style.transform = 'translate(-50%,-50%)';
    el.innerHTML = html || '';
    return el;
  }

  // 시작 버튼
  document.getElementById('startBtn').addEventListener('click', ()=>{
    showStage(1);
    if(!inited[1]) { inited[1]=true; initStage1(); }
  });
  document.getElementById('howBtn').addEventListener('click', ()=> {
    alert('오브젝트를 터치/스와이프/클릭하여 상호작용하세요. 각 행동이 환경 지수를 올립니다.');
  });

  updateScoreUI();

  /* ---------------- Stage 1: clouds ---------------- */
  function initStage1(){
    const layer = document.getElementById('cloudLayer');
    layer.innerHTML = '';
    layer.style.pointerEvents = 'auto';
    const clouds = [];
    for(let i=0;i<5;i++){
      const x = rand(12,88), y = rand(6,36);
      const c = createObj('cloud', x, y, '먼지');
      c.classList.add('cloud');
      layer.appendChild(c);
      clouds.push(c);

      const remove = ()=> {
        if(!c.parentNode) return;
        c.style.opacity = 0;
        c.style.transform += ' scale(.85)';
        setTimeout(()=> c.parentNode && c.parentNode.removeChild(c), 260);
        ecoScore += 8; updateScoreUI();
        document.getElementById('dialog1').textContent = 'AI 가디언: 공기가 조금 맑아졌어요!';
        if(layer.querySelectorAll('.cloud').length === 0) advanceAfterDelay();
      };

      c.addEventListener('click', remove);
      // touch swipe detection
      let startX = null;
      c.addEventListener('touchstart', (e)=> { startX = e.touches[0].clientX; }, {passive:true});
      c.addEventListener('touchend', (e)=> {
        if(startX === null) return;
        const endX = (e.changedTouches && e.changedTouches[0])? e.changedTouches[0].clientX : null;
        if(endX && Math.abs(endX - startX) > 25) remove();
        startX = null;
      }, {passive:true});
    }
  }

  /* ---------------- Stage 2: trash ---------------- */
  function initStage2(){
    const layer = document.getElementById('trashLayer');
    layer.innerHTML = '';
    layer.style.pointerEvents = 'auto';
    const count = 7;
    for(let i=0;i<count;i++){
      const x = rand(6,94), y = rand(52,86);
      const t = createObj('trash', x, y, '🗑️');
      t.classList.add('trash');
      layer.appendChild(t);
      t.addEventListener('click', ()=> {
        if(!t.parentNode) return;
        t.style.opacity = 0; t.style.transform += ' scale(.7) rotate(-12deg)';
        setTimeout(()=> t.parentNode && t.parentNode.removeChild(t), 240);
        ecoScore += 6; updateScoreUI();
        document.getElementById('dialog2').textContent = 'AI 가디언: 깨끗해졌어요!';
        if(layer.querySelectorAll('.trash').length === 0) advanceAfterDelay();
      });
      t.addEventListener('touchstart', ()=> t.dispatchEvent(new Event('click')), {passive:true});
    }
  }

  /* ---------------- Stage 3: plant ---------------- */
  function initStage3(){
    const ground = document.getElementById('ground');
    ground.innerHTML = '';
    ground.style.pointerEvents = 'auto';
    let planted = 0;
    const handler = (e)=>{
      // compute position
      const rect = ground.getBoundingClientRect();
      let xPct, yPct;
      if(e && e.clientX){
        xPct = ((e.clientX - rect.left)/rect.width)*100;
        yPct = ((e.clientY - rect.top)/rect.height)*100;
      } else if(e && e.touches){
        xPct = ((e.touches[0].clientX - rect.left)/rect.width)*100;
        yPct = ((e.touches[0].clientY - rect.top)/rect.height)*100;
      } else {
        xPct = rand(10,90); yPct = rand(58,90);
      }
      const seed = createObj('seed', xPct, yPct, '🌱');
      seed.classList.add('seed');
      ground.appendChild(seed);
      // animate
      seed.animate([{transform:'translate(-50%,-50%) scale(.6)', opacity:.6},{transform:'translate(-50%,-50%) scale(1.05)', opacity:1}], {duration:600, easing:'ease-out'});
      planted++; ecoScore += 7; updateScoreUI();
      document.getElementById('dialog3').textContent = `AI 가디언: 묘목이 심어졌어요! (${planted}/5)`;
      if(planted >= 5){
        setTimeout(()=> {
          ground.querySelectorAll('.seed').forEach(s=> { s.innerHTML='🌳'; s.style.width='64px'; s.style.height='64px'; });
          ground.removeEventListener('click', handler);
          ground.removeEventListener('touchstart', handler);
          advanceAfterDelay();
        }, 700);
      }
    };
    ground.addEventListener('click', handler);
    ground.addEventListener('touchstart', handler, {passive:false});
  }

  /* ---------------- Stage 4: sea cleanup ---------------- */
  function initStage4(){
    const sea = document.getElementById('seaLayer');
    sea.innerHTML = '';
    sea.style.pointerEvents = 'auto';
    for(let i=0;i<8;i++){
      const x = rand(6,94), y = rand(10,72);
      const p = createObj('plastic', x, y, '🧴');
      p.classList.add('plastic');
      sea.appendChild(p);
      p.addEventListener('click', ()=> {
        if(!p.parentNode) return;
        p.style.opacity = 0; p.style.transform += ' translateY(-20px) scale(.85)';
        setTimeout(()=> p.parentNode && p.parentNode.removeChild(p),240);
        ecoScore += 6; updateScoreUI();
        document.getElementById('dialog4').textContent = 'AI 가디언: 쓰레기를 치웠어요!';
        if(sea.querySelectorAll('.plastic').length === 0) advanceAfterDelay();
      });
      p.addEventListener('touchstart', ()=> p.dispatchEvent(new Event('click')), {passive:true});
      // drifting (light)
      (function drift(el){
        let t=0, amp = rand(6,14), speed = rand(3000,6000), dir = Math.random()>0.5?1:-1;
        function step(){
          t+=16;
          const dx = Math.sin(t/speed*Math.PI*2)*amp*dir;
          el.style.transform = `translate(calc(-50% + ${dx}px), -50%)`;
          if(el.parentNode) requestAnimationFrame(step);
        }
        requestAnimationFrame(step);
      })(p);
    }
  }

  /* ---------------- Stage 5: lights off ---------------- */
  function initStage5(){
    const layer = document.getElementById('buildingLayer');
    layer.innerHTML = '';
    layer.style.pointerEvents = 'auto';
    const cols = 5;
    for(let i=0;i<cols;i++){
      const leftPct = 10 + i*18;
      const b = createObj('building', leftPct, 52, '');
      b.classList.add('building');
      for(let w=0;w<3;w++){
        const win = document.createElement('div');
        win.className='window on';
        b.appendChild(win);
      }
      layer.appendChild(b);
      b.addEventListener('click', ()=>{
        const wins = b.querySelectorAll('.window');
        wins.forEach(win=>win.classList.toggle('on'));
        const offCount = [...wins].filter(x=>!x.classList.contains('on')).length;
        if(offCount >= 2){ ecoScore += 5; updateScoreUI(); document.getElementById('dialog5').textContent='AI 가디언: 에너지 절약 성공!'; }
        else document.getElementById('dialog5').textContent='AI 가디언: 조금 더 꺼볼까요?';
        const totalOff = [...document.querySelectorAll('.window')].filter(x=>!x.classList.contains('on')).length;
        const total = document.querySelectorAll('.window').length;
        if(total>0 && totalOff >= Math.floor(total*0.5)) advanceAfterDelay();
      });
    }
  }

  /* ---------------- Stage 6: cars -> bikes ---------------- */
  function initStage6(){
    const layer = document.getElementById('roadLayer');
    layer.innerHTML = '';
    layer.style.pointerEvents = 'auto';
    for(let i=0;i<6;i++){
      const x = 8 + i*14;
      const y = rand(62,78);
      const v = createObj('vehicle', x, y, '🚗');
      v.classList.add('vehicle');
      layer.appendChild(v);
      v.addEventListener('click', ()=>{
        if(v.dataset.transformed === '1') return;
        v.dataset.transformed = '1';
        v.innerHTML = '🚲';
        v.style.background = 'linear-gradient(#eaffea,#ffffff)';
        ecoScore += 7; updateScoreUI();
        document.getElementById('dialog6').textContent = 'AI 가디언: 탄소 배출이 줄었습니다!';
        const bikes = [...document.querySelectorAll('.vehicle')].filter(x=>x.innerText.includes('🚲')).length;
        if(bikes >= 4) advanceAfterDelay();
      });
      v.addEventListener('touchstart', ()=> v.dispatchEvent(new Event('click')), {passive:true});
    }
  }

  /* ---------------- Stage 7: butterflies ---------------- */
  function initStage7(){
    const layer = document.getElementById('forestLayer');
    layer.innerHTML = '';
    layer.style.pointerEvents = 'auto';
    let butterflies = 0;
    const target = 10;
    function spawn(xPct,yPct){
      const b = createObj('butterfly', xPct, yPct, '');
      b.classList.add('butterfly');
      b.style.pointerEvents = 'none';
      layer.appendChild(b);
      butterflies++; ecoScore += 3; updateScoreUI();
      // floating motion
      const startLeft = (xPct/100)*layer.clientWidth;
      const startTop = (yPct/100)*layer.clientHeight;
      let t=0, angle=Math.random()*Math.PI*2, speed=0.8+Math.random()*1.4;
      function fly(){ t+=0.02*speed; if(!b.parentNode) return; b.style.left = ((startLeft + Math.sin(t*2+angle)*40)/layer.clientWidth*100)+'%'; b.style.top = ((startTop + Math.cos(t*3+angle)*24)/layer.clientHeight*100)+'%'; b.style.transform = `translate(-50%,-50%) rotate(${Math.sin(t)*20}deg)`; requestAnimationFrame(fly); }
      requestAnimationFrame(fly);
      if(butterflies >= target){
        document.getElementById('dialog7').textContent = 'AI 가디언: 숲이 되살아났습니다! 엔딩으로 이동합니다.';
        advanceAfterDelay(1200);
      }
    }
    // click/touch spawn
    const onClick = (e)=> {
      const rect = layer.getBoundingClientRect();
      const cx = (e.clientX !== undefined) ? e.clientX : (e.touches && e.touches[0] ? e.touches[0].clientX : null);
      const cy = (e.clientY !== undefined) ? e.clientY : (e.touches && e.touches[0] ? e.touches[0].clientY : null);
      if(cx===null || cy===null) return;
      const xPct = ((cx - rect.left)/rect.width)*100;
      const yPct = ((cy - rect.top)/rect.height)*100;
      spawn(xPct,yPct);
    };
    layer.addEventListener('click', onClick);
    layer.addEventListener('touchstart', onClick, {passive:true});
  }

  /* ---------------- Ending ---------------- */
  function showEnding(){
    showStage(7);
    // remove any previous ending overlay
    const prev = document.getElementById('endingBlock'); if(prev) prev.remove();
    const container = document.getElementById('stage7');
    const ending = document.createElement('div');
    ending.id = 'endingBlock';
    ending.style.position='absolute';
    ending.style.left='50%';
    ending.style.top='18%';
    ending.style.transform='translateX(-50%)';
    ending.style.background='rgba(255,255,255,0.98)';
    ending.style.padding='20px 22px';
    ending.style.borderRadius='14px';
    ending.style.boxShadow='0 12px 30px rgba(0,0,0,0.12)';
    ending.style.textAlign='center';
    ending.style.zIndex='4000';
    let msg='';
    if(ecoScore >= 120) msg = '🌿 지구가 완전히 회복되었습니다! 당신의 선택이 큰 변화를 만들었어요.';
    else if(ecoScore >= 80) msg = '⚖️ 지구는 회복 중입니다. 꾸준한 노력이 필요합니다.';
    else msg = '☁️ 지구는 아직 아픕니다. 다시 시도해보세요!';
    ending.innerHTML = `<h2 style="margin:0 0 8px 0">${msg}</h2><p style="margin:0 0 12px 0">최종 환경 지수: <strong>${ecoScore}</strong></p><div><button id="restartBtn" class="btn">다시하기</button></div>`;
    container.appendChild(ending);
    document.getElementById('restartBtn').addEventListener('click', ()=> location.reload());
  }

  // preload guardian image
  (function(){ const img = new Image(); img.src='https://cdn-icons-png.flaticon.com/512/3093/3093402.png'; })();

  // keyboard helpers for desktop testing
  window.addEventListener('keydown',(e)=>{ if(e.key==='ArrowRight') nextStage(); if(e.key==='r') location.reload(); });
</script>
</body>
</html>
