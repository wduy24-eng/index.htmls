<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Duyviphehe1</title>
  <style>
    html,body{
      height:100%;margin:0;
      font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;
      background:#000;color:#fff;
      display:flex;align-items:center;justify-content:center;
    }
    .card{width:min(680px,92vw);background:#111;border-radius:20px;padding:24px;text-align:center}
    input,button{padding:12px 16px;font-size:16px;border-radius:10px;border:none}
    input{width:70%;background:#222;color:#fff;border:1px solid #333}
    button{background:#00e5ff;color:#000;font-weight:600;cursor:pointer;margin-top:12px}
    .hide{display:none!important}
    video{width:100%;height:auto;display:block;background:#000}
  </style>
</head>
<body>
  <main class="card">
    <section id="step1">
      <h2>👋 Tên của bạn là gì?</h2>
      <input id="nameInput" type="text" placeholder="Nhập tên..." maxlength="40" /><br>
      <button id="toStep2">Gửi</button>
    </section>

    <section id="step2" class="hide">
      <h2>Giới tính của bạn là gì?</h2>
      <button id="pickMale">Nam</button>
      <button id="pickFemale">Nữ</button>
    </section>

    <section id="step3" class="hide">
      <video id="theVideo" controls preload="metadata"></video>
    </section>
  </main>

  <script>
    const $ = id => document.getElementById(id);
    const step1 = $('step1'), step2 = $('step2'), step3 = $('step3');
    const nameInput = $('nameInput'), toStep2 = $('toStep2');
    const pickMale = $('pickMale'), pickFemale = $('pickFemale');
    const theVideo = $('theVideo');

    const VIDEO_URL = 'video.mp4';

    function show(s){[step1,step2,step3].forEach(x=>x.classList.add('hide'));s.classList.remove('hide');}

    toStep2.onclick = () => {
      const name = (nameInput.value||'').trim();
      if(!name){alert('Vui lòng nhập tên!');return;}
      show(step2);
    };

    async function enterFullscreen(el){
      try{
        if(el.requestFullscreen) await el.requestFullscreen();
        else if(el.webkitRequestFullscreen) await el.webkitRequestFullscreen();
        else if(el.msRequestFullscreen) await el.msRequestFullscreen();
        else if(el.webkitEnterFullscreen) el.webkitEnterFullscreen(); // iPhone
      }catch(e){console.warn(e);}
    }

    async function playVideo(){
      show(step3);
      theVideo.src = VIDEO_URL;
      theVideo.load();
      await enterFullscreen(theVideo);
      try{await theVideo.play();}catch(e){console.warn('autoplay bị chặn',e);}
    }

    pickMale.onclick = playVideo;
    pickFemale.onclick = playVideo;
  </script>
</body>
</html>
