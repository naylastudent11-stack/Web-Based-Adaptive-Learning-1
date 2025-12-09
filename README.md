# Web-Based-Adaptive-Learning-1[p3.html](https://github.com/user-attachments/files/24050253/p3.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Adaptive Learning — SMA 11 Wajo (Prototype)</title>
  <link rel="icon" href="data:;base64,iVBORw0KGgo=" />
  <style>
    /* --- Basic design system --- */
    :root{
      --bg:#0f1724; --card:#0b1220; --accent:#3b82f6; --muted:#94a3b8; --glass: rgba(255,255,255,0.03);
      --radius:14px; --gap:16px; --maxw:1200px;
      --font-sans: system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:var(--font-sans);background:linear-gradient(180deg,#071029 0%, #071827 100%);color:#e6eef8;line-height:1.45}
    .wrap{max-width:var(--maxw);margin:28px auto;padding:20px}
    header{display:flex;gap:12px;align-items:center;justify-content:space-between}
    .brand{display:flex;gap:12px;align-items:center}
    .logo{width:52px;height:52px;border-radius:12px;background:linear-gradient(135deg,var(--accent),#60a5fa);display:flex;align-items:center;justify-content:center;font-weight:700}
    h1{font-size:18px;margin:0}
    p.lead{margin:0;color:var(--muted);font-size:13px}

    /* layout */
    .grid{display:grid;grid-template-columns:300px 1fr;gap:18px;margin-top:20px}
    nav.card, .main.card{background:var(--card);padding:16px;border-radius:12px;box-shadow:0 6px 22px rgba(2,6,23,0.6)}
    nav.card{height:calc(100vh - 120px);overflow:auto}
    .nav-item{display:flex;align-items:center;gap:12px;padding:10px;border-radius:10px;margin-bottom:8px;cursor:pointer}
    .nav-item:hover{background:var(--glass)}
    .nav-item .ico{width:34px;height:34px;border-radius:8px;background:rgba(255,255,255,0.03);display:flex;align-items:center;justify-content:center}

    /* dashboard actions */
    .actions{display:flex;flex-direction:column;gap:10px}
    .btn{background:linear-gradient(90deg,var(--accent),#60a5fa);border:none;padding:10px 12px;border-radius:10px;color:#04243a;font-weight:600;cursor:pointer}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.04);color:var(--muted)}

    /* module cards */
    .modules{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
    .module{background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);padding:12px;border-radius:12px}
    .module h3{margin:4px 0 8px}
    .module p{font-size:13px;color:var(--muted)}

    /* content area */
    .panel{background:linear-gradient(180deg,rgba(255,255,255,0.01),transparent);padding:16px;border-radius:12px;margin-top:12px}
    .hidden{display:none}

    /* small helpers */
    .row{display:flex;gap:12px;align-items:center}
    .badge{background:rgba(255,255,255,0.04);padding:6px 8px;border-radius:999px;font-size:12px}
    code{background:rgba(255,255,255,0.02);padding:4px;border-radius:6px}

    /* responsive */
    @media (max-width:900px){
      .grid{grid-template-columns:1fr;}
      nav.card{height:auto}
    }

    /* simple flipbook simulation */
    .flipbook{background:#071627;border-radius:10px;padding:12px;min-height:200px}
    .flipbook .page{background:linear-gradient(180deg,#0f1724,#07122a);padding:12px;border-radius:8px}

    footer{margin-top:18px;color:var(--muted);font-size:13px;text-align:center}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="brand">
        <div class="logo">A</div>
        <div>
          <h1>Adaptive Learning — SMA 11 Wajo</h1>
          <p class="lead">Domain: <code>adaptika.sma11wajo.sch.id</code> · Prototype dashboard</p>
        </div>
      </div>
      <div class="row">
        <div class="badge">Guru: Pak/Ibu</div>
        <button class="btn" id="logoutBtn">Keluar</button>
      </div>
    </header>

    <div class="grid">
      <nav class="card" aria-label="sidebar">
        <div class="row" style="justify-content:space-between;align-items:center;margin-bottom:12px">
          <strong>Kontrol Guru</strong>
          <small style="color:var(--muted);font-size:12px">v0.9</small>
        </div>

        <div class="actions">
          <label class="btn" for="fileInput">Unggah Materi Baru</label>
          <input id="fileInput" type="file" accept=".doc,.docx,application/pdf,application/vnd.ms-powerpoint,application/vnd.openxmlformats-officedocument.presentationml.presentation" style="display:none">

          <button class="btn ghost" id="classesBtn">Daftar Kelas Saya</button>
          <button class="btn ghost" id="progressBtn">Pantau Progres Siswa</button>
          <button class="btn ghost" id="manualBtn">Ganti Format Manual</button>
        </div>

        <hr style="border:none;border-top:1px solid rgba(255,255,255,0.03);margin:12px 0">

        <div>
          <div class="nav-item" data-target="visual">
            <div class="ico">V</div>
            <div>
              <div style="font-weight:700">Modul Visual</div>
              <div style="font-size:12px;color:var(--muted)">Landing page & video animasi</div>
            </div>
          </div>

          <div class="nav-item" data-target="aural">
            <div class="ico">A</div>
            <div>
              <div style="font-weight:700">Modul Aural</div>
              <div style="font-size:12px;color:var(--muted)">Audio naratif otomatis</div>
            </div>
          </div>

          <div class="nav-item" data-target="readwrite">
            <div class="ico">R</div>
            <div>
              <div style="font-weight:700">Modul Read/Write</div>
              <div style="font-size:12px;color:var(--muted)">Perpustakaan digital</div>
            </div>
          </div>

          <div class="nav-item" data-target="kinestetik">
            <div class="ico">K</div>
            <div>
              <div style="font-weight:700">Modul Kinestetik</div>
              <div style="font-size:12px;color:var(--muted)">Permainan edukasi</div>
            </div>
          </div>
        </div>

        <hr style="border:none;border-top:1px solid rgba(255,255,255,0.03);margin:12px 0">
        <small style="color:var(--muted)">Ikon besar, tipografi jelas — dirancang agar mudah dipakai tanpa pelatihan</small>
      </nav>

      <main class="main card">
        <section id="home">
          <div style="display:flex;justify-content:space-between;align-items:center;gap:12px">
            <div>
              <h2 style="margin:0 0 6px">Dashboard Utama</h2>
              <div style="color:var(--muted);font-size:13px">Akses cepat ke empat modul penyajian materi dan manajemen kelas</div>
            </div>
            <div style="text-align:right">
              <div style="font-weight:700">Pantau Progres Siswa</div>
              <div style="color:var(--muted);font-size:13px">Grafik perkembangan real-time (demo)</div>
            </div>
          </div>

          <div class="modules" style="margin-top:14px">
            <div class="module">
              <h3>Visual — Landing Page Interaktif</h3>
              <p>Desain responsif, Gamma-like landing, kontras warna, tipografi jelas.</p>
              <div style="margin-top:8px"><button class="btn" onclick="openModule('visual')">Buka Modul</button></div>
            </div>

            <div class="module">
              <h3>Aural — Audio Naratif</h3>
              <p>Audio otomatis dengan intonasi & tempo yang dapat disesuaikan.</p>
              <div style="margin-top:8px"><button class="btn" onclick="openModule('aural')">Buka Modul</button></div>
            </div>

            <div class="module">
              <h3>Read/Write — Flipbook</h3>
              <p>FlipHTML5-like flipbook interaktif & anotasi digital.</p>
              <div style="margin-top:8px"><button class="btn" onclick="openModule('readwrite')">Buka Modul</button></div>
            </div>

            <div class="module">
              <h3>Kinestetik — Game</h3>
              <p>Permainan edukasi berbasis Phaser.js (skeleton game included).</p>
              <div style="margin-top:8px"><button class="btn" onclick="openModule('kinestetik')">Buka Modul</button></div>
            </div>
          </div>

          <div class="panel">
            <strong>Info unggahan</strong>
            <p id="uploadInfo" style="color:var(--muted);font-size:13px">Tidak ada file diunggah.</p>
          </div>
        </section>

        <!-- VISUAL MODULE -->
        <section id="visual" class="hidden">
          <div class="row" style="justify-content:space-between;align-items:center">
            <div>
              <h2>Modul Visual</h2>
              <p class="lead">Landing page interaktif & video animasi (contoh: Goa Nipon)</p>
            </div>
            <div><button class="btn ghost" onclick="openModule('home')">Kembali</button></div>
          </div>

          <div class="panel">
            <h3>Contoh Landing Page</h3>
            <div style="padding:12px;background:rgba(255,255,255,0.02);border-radius:8px">
              <h4 style="margin:6px 0">Sejarah Goa Nipon — Ringkasan</h4>
              <p style="color:var(--muted)">Halaman pengantar singkat yang memuat konteks dan tujuan pembelajaran. Desain responsif dan mudah dipindai.</p>
            </div>

            <h3 style="margin-top:12px">Video Animasi (Contoh)</h3>
            <div style="display:flex;gap:12px;flex-wrap:wrap">
              <div style="flex:1;min-width:280px">
                <video id="sampleVideo" controls style="width:100%;border-radius:8px;background:#000">
                  <source src="" />
                  <!-- demo: tidak ada source — ganti dengan file video produksi Anda -->
                  Browser Anda tidak mendukung tag video.
                </video>
                <p style="color:var(--muted);font-size:13px;margin-top:6px">Video animasi 3 menit biasanya ideal untuk topik sejarah singkat.</p>
              </div>

              <div style="width:260px">
                <div style="background:rgba(255,255,255,0.02);padding:10px;border-radius:8px">
                  <strong>Kontrol Animasi</strong>
                  <p style="color:var(--muted);font-size:13px;margin:6px 0">Atur karakter, latar, teks, dan narasi menggunakan tools produksi lalu unggah MP4 ke sini.</p>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- AURAL MODULE -->
        <section id="aural" class="hidden">
          <div class="row" style="justify-content:space-between;align-items:center">
            <div>
              <h2>Modul Aural</h2>
              <p class="lead">Audio naratif otomatis (Web Speech API demo)</p>
            </div>
            <div><button class="btn ghost" onclick="openModule('home')">Kembali</button></div>
          </div>

          <div class="panel">
            <label for="audioText">Teks untuk diubah menjadi narasi (contoh singkat):</label>
            <textarea id="audioText" rows="4" style="width:100%;margin-top:8px;padding:10px;border-radius:8px;background:#051226;color:inherit;border:1px solid rgba(255,255,255,0.03)">Goa Nipon adalah situs bersejarah yang digunakan sebagai bunker pada masa pendudukan. Pelajari struktur dan kisahnya melalui peta visual dan narasi singkat ini.</textarea>
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="speakBtn">Mainkan Narasi</button>
              <button class="btn ghost" id="stopBtn">Hentikan</button>
              <div style="flex:1;text-align:right;color:var(--muted)" id="voicesInfo">Voices: —</div>
            </div>
          </div>
        </section>

        <!-- READ/WRITE MODULE -->
        <section id="readwrite" class="hidden">
          <div class="row" style="justify-content:space-between;align-items:center">
            <div>
              <h2>Modul Read/Write</h2>
              <p class="lead">Perpustakaan digital & flipbook (simulasi flipbook)</p>
            </div>
            <div><button class="btn ghost" onclick="openModule('home')">Kembali</button></div>
          </div>

          <div class="panel">
            <div class="flipbook">
              <div class="page">
                <h4>Flipbook — Halaman 1</h4>
                <p style="color:var(--muted)">Ini adalah contoh konversi dokumen menjadi flipbook. Di implementasi nyata gunakan FlipHTML5 atau layanan serupa untuk fitur anotasi.</p>
              </div>
            </div>
            <div style="margin-top:10px;display:flex;gap:8px">
              <button class="btn" onclick="annotate()">Anotasi (demo)</button>
              <button class="btn ghost" onclick="openPdf()">Buka PDF (contoh)</button>
            </div>
          </div>
        </section>

        <!-- KINESTETIK MODULE -->
        <section id="kinestetik" class="hidden">
          <div class="row" style="justify-content:space-between;align-items:center">
            <div>
              <h2>Modul Kinestetik</h2>
              <p class="lead">Game edukasi (Phaser.js skeleton). Tiga mini-games: Number Rescue, Cell Defense, Word Builder.</p>
            </div>
            <div><button class="btn ghost" onclick="openModule('home')">Kembali</button></div>
          </div>

          <div class="panel">
            <div id="gameArea" style="min-height:320px;background:linear-gradient(180deg,#051123,#021226);border-radius:8px;padding:12px;color:var(--muted);display:flex;align-items:center;justify-content:center">Memuat game demo...</div>
            <div style="margin-top:10px;display:flex;gap:8px">
              <button class="btn" onclick="startPhaserDemo()">Mulai Demo Game</button>
              <button class="btn ghost" onclick="stopPhaserDemo()">Hentikan</button>
            </div>
          </div>
        </section>

        <footer>Prototype ini menyajikan struktur front-end dan simulasi fitur. Untuk produksi: sambungkan ke backend (unggah file, konversi dokumen, penyimpanan, auth, database siswa, & layanan TTS/Video hosting).</footer>
      </main>
    </div>

  </div>

  <script src="https://cdn.jsdelivr.net/npm/phaser@3.60.0/dist/phaser.min.js"></script>
  <script>
    // --- Module navigation ---
    function openModule(id){
      document.querySelectorAll('main section').forEach(s=>s.classList.add('hidden'));
      document.getElementById(id).classList.remove('hidden');
      window.scrollTo({top:0,behavior:'smooth'});
    }

    document.querySelectorAll('.nav-item').forEach(it=>{
      it.addEventListener('click',()=>openModule(it.dataset.target));
    });

    document.getElementById('logoutBtn').addEventListener('click',()=>alert('Menutup sesi (demo).'))

    // --- Upload simulation & "convert to 4 formats" demo ---
    const fileInput = document.getElementById('fileInput');
    const uploadInfo = document.getElementById('uploadInfo');
    fileInput.addEventListener('change',async(e)=>{
      const f = e.target.files[0];
      if(!f) return;
      uploadInfo.textContent = `Mengunggah: ${f.name} — ukuran ${Math.round(f.size/1024)} KB`;

      // Simulasi proses konversi (tidak melakukan konversi nyata di frontend)
      uploadInfo.textContent += ' · Mengonversi ke format Visual/Aural/ReadWrite/Kinestetik...';
      await new Promise(r=>setTimeout(r,900));
      uploadInfo.textContent = `File ${f.name} berhasil diunggah. Versi: Visual (landing), Aural (TTS-ready), Read/Write (flipbook), Kinestetik (exercise JSON).`;
    });

    // --- Web Speech API TTS demo ---
    let synth = window.speechSynthesis;
    const speakBtn = document.getElementById('speakBtn');
    const stopBtn = document.getElementById('stopBtn');
    const audioText = document.getElementById('audioText');
    const voicesInfo = document.getElementById('voicesInfo');

    function populateVoices(){
      const voices = synth.getVoices();
      voicesInfo.textContent = `Voices: ${voices.length}`;
    }
    populateVoices();
    if (speechSynthesis.onvoiceschanged !== undefined) speechSynthesis.onvoiceschanged = populateVoices;

    speakBtn.addEventListener('click',()=>{
      if(!synth) return alert('TTS tidak tersedia pada browser Anda.');
      synth.cancel();
      const ut = new SpeechSynthesisUtterance(audioText.value);
      ut.lang = 'id-ID';
      ut.rate = 1; ut.pitch = 1;
      synth.speak(ut);
    });
    stopBtn.addEventListener('click',()=>synth.cancel());

    // --- Read/Write demo actions ---
    function annotate(){
      alert('Demo anotasi: fitur anotasi digital perlu backend / editor JS (contoh: PDF.js + annotator library).');
    }
    function openPdf(){
      alert('Buka PDF contoh: di produksi, tampilkan dengan PDF.js atau embed FlipHTML5.');
    }

    // --- Phaser demo: simple scene that acts as placeholder for Number Rescue ---
    let phaserGame = null;
    function startPhaserDemo(){
      if(phaserGame) return;
      const cfg = {
        type: Phaser.AUTO,
        width: 800, height: 320,
        parent: 'gameArea',
        backgroundColor: '#021122',
        scene: {
          preload: function(){
            this.load.image('ball','https://labs.phaser.io/assets/sprites/pangball.png');
          },
          create: function(){
            this.add.text(16,16,'Number Rescue — Demo (klik layar untuk menambah angka)',{font:'16px Arial',fill:'#fff'});
            this.score = 0;
            this.scoreText = this.add.text(16,44,'Score: 0',{font:'14px Arial',fill:'#fff'});

            this.input.on('pointerdown',()=>{
              const x = Phaser.Math.Between(50,750);
              const y = Phaser.Math.Between(80,280);
              const s = this.add.image(x,y,'ball').setScale(0.4).setInteractive();
              s.on('pointerdown',()=>{ s.destroy(); this.score+=1; this.scoreText.setText('Score: '+this.score);});
            });
          }
        },
        scale: {mode: Phaser.Scale.FIT,autoCenter:Phaser.Scale.CENTER_BOTH}
      };
      phaserGame = new Phaser.Game(cfg);
      document.getElementById('gameArea').innerHTML = '';
    }
    function stopPhaserDemo(){
      if(!phaserGame) return alert('Game belum berjalan');
      phaserGame.destroy(true);
      phaserGame = null;
      document.getElementById('gameArea').textContent = 'Game demo dihentikan.';
    }

    // --- Simple openModule to show home on load ---
    openModule('home');

    // --- Extra: show teacher classes & progress (demo modal) ---
    document.getElementById('classesBtn').addEventListener('click',()=>{
      alert('Daftar Kelas:\n- XI IPA 1\n- XI IPS 2\n(Prototype: hubungkan ke SSO & DB sekolah)');
    });
    document.getElementById('progressBtn').addEventListener('click',()=>{
      alert('Pantau progres:\n- Rata-rata kelas: 78%\n- 5 siswa di bawah KKM\n(Prototype: gunakan charting & real-time socket untuk data nyata)');
    });

    // --- Manual format change (demo) ---
    document.getElementById('manualBtn').addEventListener('click',()=>{
      const choice = prompt('Ganti tampilan ke: visual / aural / readwrite / kinestetik');
      if(choice) openModule(choice.trim());
    });
  </script>
</body>
</html>

</body>
</html>
