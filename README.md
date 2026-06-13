<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>Biodata 3D | Nama Arrafah</title>
  <!-- Font & Icon -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    body {
      margin: 0;
      overflow: hidden;
      font-family: 'Poppins', sans-serif;
      background: radial-gradient(circle at center, #0a0f1e 0%, #020408 100%);
      height: 100vh;
      width: 100vw;
      perspective: 1200px;
      color: white;
    }

    /* Canvas latar 3D (bintang & partikel) */
    #bgCanvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
    }

    /* Menu Navigasi 3D */
    .menu-3d {
      position: fixed;
      top: 30px;
      left: 50%;
      transform: translateX(-50%) rotateX(5deg);
      z-index: 100;
      background: rgba(20, 30, 50, 0.65);
      backdrop-filter: blur(18px);
      border-radius: 60px;
      padding: 12px 30px;
      box-shadow: 0 25px 45px rgba(0,0,0,0.7), 0 0 20px rgba(0, 180, 255, 0.4);
      border: 1px solid rgba(255,255,255,0.25);
      display: flex;
      gap: 35px;
      transform-style: preserve-3d;
      animation: floatMenu 4s ease-in-out infinite;
    }

    @keyframes floatMenu {
      0% { transform: translateX(-50%) rotateX(5deg) translateY(0px); }
      50% { transform: translateX(-50%) rotateX(5deg) translateY(-8px); }
      100% { transform: translateX(-50%) rotateX(5deg) translateY(0px); }
    }

    .menu-item {
      text-decoration: none;
      color: #ccddf9;
      font-weight: 600;
      font-size: 1.2rem;
      letter-spacing: 1.5px;
      padding: 8px 16px;
      border-radius: 30px;
      transition: 0.3s;
      text-shadow: 0 2px 5px black;
      display: flex;
      align-items: center;
      gap: 6px;
      transform: translateZ(5px);
      background: rgba(255,255,255,0.05);
      border: 1px solid transparent;
    }

    .menu-item i {
      font-size: 1.1rem;
      color: #7ec8ff;
    }

    .menu-item:hover {
      background: rgba(255, 255, 255, 0.15);
      border-color: rgba(255,255,255,0.5);
      color: white;
      transform: translateZ(15px) scale(1.05);
      box-shadow: 0 10px 20px rgba(0,160,255,0.5);
    }

    /* Kartu Biodata 3D */
    .card-3d-container {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 10;
      width: 90%;
      max-width: 600px;
      transform-style: preserve-3d;
      animation: rotateCardSlow 20s infinite alternate ease-in-out;
    }

    @keyframes rotateCardSlow {
      0% { transform: translate(-50%, -50%) rotateY(5deg) rotateX(3deg); }
      100% { transform: translate(-50%, -50%) rotateY(-8deg) rotateX(-2deg); }
    }

    .card {
      background: rgba(18, 25, 45, 0.7);
      backdrop-filter: blur(25px);
      border-radius: 50px;
      padding: 35px 30px;
      box-shadow: 0 50px 80px rgba(0, 0, 0, 0.8), 0 0 60px rgba(0, 180, 255, 0.4), inset 0 0 25px rgba(255,255,255,0.2);
      border: 2px solid rgba(255, 255, 255, 0.25);
      transform-style: preserve-3d;
      transition: 0.2s;
      text-align: center;
      color: #f0f4ff;
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
    }

    .card:hover {
      box-shadow: 0 60px 90px rgba(0, 180, 255, 0.6), 0 0 70px #0066cc;
    }

    /* Foto profil 3D */
    .avatar-3d {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      background: linear-gradient(135deg, #1e3b70, #0b1a33);
      border: 4px solid rgba(255, 255, 255, 0.5);
      box-shadow: 0 25px 40px rgba(0,0,0,0.7), 0 0 35px #3f8ef0;
      margin-bottom: 20px;
      transform: translateZ(40px);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 5rem;
      color: white;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" fill="white"><circle cx="50" cy="40" r="20" fill="%23b3d9ff"/><circle cx="50" cy="85" r="28" fill="%23b3d9ff"/></svg>');
      background-size: cover;
      background-position: center;
      position: relative;
    }

    .avatar-3d i {
      font-size: 5.5rem;
      color: #eef7ff;
      filter: drop-shadow(0 8px 10px black);
    }

    .name-glow {
      font-size: 2.7rem;
      font-weight: 700;
      margin: 10px 0 5px;
      text-transform: uppercase;
      letter-spacing: 3px;
      background: linear-gradient(to right, #aad0ff, #ffffff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 0 20px #0066ff;
      transform: translateZ(35px);
    }

    .detail-grid {
      width: 100%;
      margin: 15px 0 10px;
      display: flex;
      flex-direction: column;
      gap: 16px;
      transform: translateZ(25px);
    }

    .info-row {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
      background: rgba(255, 255, 255, 0.08);
      backdrop-filter: blur(12px);
      padding: 12px 20px;
      border-radius: 40px;
      border: 1px solid rgba(255,255,255,0.25);
      box-shadow: 0 10px 20px rgba(0,0,0,0.4);
      transition: 0.2s;
    }

    .info-row i {
      font-size: 1.4rem;
      color: #7bc8ff;
      width: 30px;
      text-shadow: 0 0 10px blue;
    }

    .info-row span {
      font-weight: 500;
      font-size: 1.1rem;
      letter-spacing: 0.5px;
    }

    .hobi-tags {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 12px;
      margin-top: 8px;
      transform: translateZ(20px);
    }

    .tag {
      background: rgba(0, 180, 255, 0.2);
      border: 1px solid rgba(255,255,255,0.4);
      border-radius: 30px;
      padding: 8px 18px;
      font-weight: 500;
      backdrop-filter: blur(10px);
      display: flex;
      align-items: center;
      gap: 6px;
      box-shadow: 0 8px 15px rgba(0,0,0,0.5);
      transition: 0.3s;
    }

    .tag i {
      color: #ffd966;
    }

    .tag:hover {
      background: #1e4b8f;
      transform: translateY(-5px) scale(1.05);
      border-color: white;
    }

    .school-badge {
      margin-top: 15px;
      background: #122b44;
      padding: 10px 22px;
      border-radius: 30px;
      font-weight: 600;
      font-size: 1rem;
      display: flex;
      align-items: center;
      gap: 8px;
      border: 1px solid gold;
      box-shadow: 0 0 20px gold;
      transform: translateZ(30px);
    }

    /* Responsive */
    @media (max-width: 600px) {
      .menu-3d {
        gap: 12px;
        padding: 10px 18px;
      }
      .menu-item {
        font-size: 0.9rem;
        padding: 6px 10px;
      }
      .card {
        padding: 25px 15px;
      }
    }
  </style>
</head>
<body>
  <!-- Background 3D bergerak -->
  <canvas id="bgCanvas"></canvas>

  <!-- Menu Navigasi -->
  <div class="menu-3d">
    <a href="#" class="menu-item"><i class="fas fa-home"></i> Beranda</a>
    <a href="#" class="menu-item"><i class="fas fa-user"></i> Profil</a>
    <a href="#" class="menu-item"><i class="fas fa-star"></i> Prestasi</a>
    <a href="#" class="menu-item"><i class="fas fa-envelope"></i> Kontak</a>
  </div>

  <!-- Kartu Biodata 3D -->
  <div class="card-3d-container">
    <div class="card">
      <div class="avatar-3d">
        <i class="fas fa-user-graduate"></i>
      </div>
      <div class="name-glow">Nama Arrafah</div>
      
      <div class="detail-grid">
        <div class="info-row">
          <i class="fas fa-calendar-alt"></i>
          <span><strong>Lahir:</strong> 06 Oktober 2009</span>
        </div>
        <div class="info-row">
          <i class="fas fa-bullseye"></i>
          <span><strong>Cita-cita:</strong> Dokter</span>
        </div>
        <div class="info-row">
          <i class="fas fa-school"></i>
          <span><strong>Sekolah:</strong> SMAN 2 Jakarta</span>
        </div>
      </div>

      <div style="margin-top: 5px; font-weight: 600; letter-spacing: 1px;">✨ Hobi ✨</div>
      <div class="hobi-tags">
        <div class="tag"><i class="fas fa-swimmer"></i> Berenang</div>
        <div class="tag"><i class="fas fa-book-open"></i> Membaca</div>
        <div class="tag"><i class="fas fa-running"></i> Lari</div>
      </div>

      <div class="school-badge">
        <i class="fas fa-graduation-cap"></i> SMAN 2 Jakarta
      </div>
      <div style="margin-top: 12px; font-size: 0.8rem; opacity: 0.8; transform: translateZ(15px);">
        <i class="fas fa-stethoscope" style="margin-right: 6px;"></i> Future Doctor
      </div>
    </div>
  </div>

  <script>
    (function() {
      const canvas = document.getElementById('bgCanvas');
      const ctx = canvas.getContext('2d');
      let width, height;
      
      // Partikel dan bintang
      let particles = [];
      
      function resizeCanvas() {
        width = window.innerWidth;
        height = window.innerHeight;
        canvas.width = width;
        canvas.height = height;
        initParticles();
      }
      
      function initParticles() {
        particles = [];
        const particleCount = Math.floor((width * height) / 9000);
        for (let i = 0; i < particleCount; i++) {
          particles.push({
            x: Math.random() * width,
            y: Math.random() * height,
            z: Math.random() * 800 + 200, // kedalaman
            radius: Math.random() * 2.5 + 0.8,
            speed: Math.random() * 0.4 + 0.15,
            color: `rgba(255, 255, 255, ${Math.random() * 0.7 + 0.3})`,
            twinkle: Math.random() * 0.05
          });
        }
      }
      
      function drawBackground() {
        ctx.clearRect(0, 0, width, height);
        
        // Gradasi dasar
        const gradient = ctx.createLinearGradient(0, 0, width, height);
        gradient.addColorStop(0, '#030b1a');
        gradient.addColorStop(0.5, '#0a1830');
        gradient.addColorStop(1, '#020610');
        ctx.fillStyle = gradient;
        ctx.fillRect(0, 0, width, height);
        
        // Partikel bergerak (efek 3D dengan kedalaman)
        particles.forEach(p => {
          // Gerakan lambat berdasarkan kedalaman (z)
          p.y -= p.speed * (p.z / 500);
          if (p.y < -10) {
            p.y = height + 10;
            p.x = Math.random() * width;
          }
          
          // Twinkle effect
          let alpha = 0.5 + Math.sin(Date.now() * 0.002 + p.x) * 0.2;
          const size = p.radius * (p.z / 500);
          
          ctx.beginPath();
          ctx.arc(p.x, p.y, size, 0, Math.PI * 2);
          ctx.fillStyle = `rgba(180, 210, 255, ${alpha + 0.3})`;
          ctx.fill();
          
          // Glow tambahan
          ctx.beginPath();
          ctx.arc(p.x, p.y, size * 1.8, 0, Math.PI*2);
          ctx.fillStyle = `rgba(100, 180, 255, 0.08)`;
          ctx.fill();
        });
        
        // Bintang besar berkedip
        for (let i = 0; i < 8; i++) {
          const bx = (i * 130 + 50) % width;
          const by = (i * 90 + 30) % height;
          const flicker = 0.4 + Math.sin(Date.now() * 0.005 + i) * 0.3;
          ctx.beginPath();
          ctx.arc(bx, by, 2.2, 0, 2*Math.PI);
          ctx.fillStyle = `rgba(255, 255, 200, ${flicker})`;
          ctx.fill();
          ctx.shadowColor = 'white';
          ctx.shadowBlur = 8;
          ctx.fill();
          ctx.shadowBlur = 0;
        }
        
        requestAnimationFrame(drawBackground);
      }
      
      window.addEventListener('resize', resizeCanvas);
      resizeCanvas();
      drawBackground();
      
      // Interaksi gerakan mouse untuk efek 3D tambahan (opsional)
      document.addEventListener('mousemove', (e) => {
        const cardContainer = document.querySelector('.card-3d-container');
        if (!cardContainer) return;
        const xAxis = (window.innerWidth / 2 - e.clientX) / 45;
        const yAxis = (window.innerHeight / 2 - e.clientY) / 45;
        cardContainer.style.transform = `translate(-50%, -50%) rotateY(${xAxis}deg) rotateX(${yAxis}deg)`;
      });
      
      // Kembalikan animasi saat mouse meninggalkan area
      document.addEventListener('mouseleave', () => {
        const cardContainer = document.querySelector('.card-3d-container');
        if (cardContainer) {
          cardContainer.style.transform = 'translate(-50%, -50%) rotateY(5deg) rotateX(3deg)';
        }
      });
    })();
  </script>
</body>
</html>
