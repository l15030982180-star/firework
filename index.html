<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>烟花</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            overflow: hidden;
            background-color: #000;
        }
        canvas {
            display: block;
        }
        #musicBtn {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 9999;
            background: rgba(0,0,0,0.55);
            color: #fff;
            border: 1px solid rgba(255,255,255,0.3);
            padding: 10px 18px;
            border-radius: 25px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <canvas id="fireworksCanvas"></canvas>

    <button id="musicBtn">🎵 点击开启音乐</button>
    <audio id="bgm" loop preload="auto">
        <source src="bgm.mp3" type="audio/mpeg">
    

<script>
const canvas = document.getElementById('fireworksCanvas');
const ctx = canvas.getContext('2d');
let w, h;
function resize(){
    w = canvas.width = window.innerWidth;
    h = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

let particles = [];
class Particle{
    constructor(x,y,color){
        this.x = x;
        this.y = y;
        this.color = color;
        this.vx = (Math.random()-0.5)*6;
        this.vy = (Math.random()-0.5)*6;
        this.alpha = 1;
        this.decay = Math.random()*0.015+0.008;
    }
    update(){
        this.x += this.vx;
        this.y += this.vy;
        this.vy += 0.03;
        this.alpha -= this.decay;
    }
    draw(){
        ctx.globalAlpha = this.alpha;
        ctx.fillStyle = this.color;
        ctx.beginPath();
        ctx.arc(this.x,this.y,2,0,Math.PI*2);
        ctx.fill();
    }
}

function createFirework(){
    const x = Math.random()*w;
    const y = Math.random()*h*0.5;
    const color = `hsl(${Math.random()*360},100%,60%)`;
    for(let i=0;i<80;i++){
        particles.push(new Particle(x,y,color));
    }
}

function animate(){
    ctx.fillStyle = 'rgba(0,0,0,0.18)';
    ctx.fillRect(0,0,w,h);
    for(let i=particles.length-1;i>=0;i--){
        const p = particles[i];
        p.update();
        p.draw();
        if(p.alpha <= 0) particles.splice(i,1);
    }
    ctx.globalAlpha = 1;
    requestAnimationFrame(animate);
}
animate();
setInterval(createFirework, 900);

// 修复版音乐控制，适配微信
const bgm = document.getElementById('bgm');
const musicBtn = document.getElementById('musicBtn');
let musicPlay = false;

bgm.load(); // 强制预加载音频

musicBtn.onclick = async function(){
    try{
        if(!musicPlay){
            await bgm.play();
            musicBtn.innerText = "🎵 暂停音乐";
            musicPlay = true;
        }else{
            bgm.pause();
            musicBtn.innerText = "🎵 点击开启音乐";
            musicPlay = false;
        }
    }catch(err){
        alert("音频加载失败！请确认仓库根目录已经上传 bgm.mp3");
        console.log(err);
    }
}
</script>
</body>
</html>
