# firework<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>浪漫烟花秀</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{overflow:hidden;background:#000;height:100vh}
canvas{display:block}
.text{
  position:absolute;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  color:#fff;
  font-size:32px;
  font-family:"Microsoft Yahei",sans-serif;
  text-shadow:0 0 10px #ff6699,0 0 20px #ff3377;
  z-index:10;
  animation:fade 4s ease forwards;
  pointer-events:none;
}
@keyframes fade{
  0%{opacity:0}
  30%{opacity:1}
  80%{opacity:1}
  100%{opacity:0}
}
</style>
</head>
<body>
<div class="text">✨ 愿所有美好如约而至 ✨</div>
<canvas id="fireworks"></canvas>
<script>
const canvas = document.getElementById('fireworks');
const ctx = canvas.getContext('2d');
let W,H;
function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight}
resize();
window.addEventListener('resize',resize);

class Firework{
  constructor(x,y){
    this.x=x;this.y=y;
    this.vy=-8-Math.random()*4;
    this.vx=(Math.random()-0.5)*2;
    this.alpha=1;
    this.color=`hsl(${Math.random()*360},100%,65%)`;
    this.exploded=false;
  }
  update(){
    if(!this.exploded){
      this.x+=this.vx;
      this.y+=this.vy;
      this.vy+=0.12;
      if(this.vy>=0){
        this.exploded=true;
        createParticles(this.x,this.y,this.color);
      }
    }
  }
  draw(){
    ctx.beginPath();
    ctx.arc(this.x,this.y,2.5,0,Math.PI*2);
    ctx.fillStyle=this.color;
    ctx.fill();
  }
}
class Particle{
  constructor(x,y,color){
    this.x=x;this.y=y;
    this.speed=2+Math.random()*4;
    this.angle=Math.random()*Math.PI*2;
    this.vx=Math.cos(this.angle)*this.speed;
    this.vy=Math.sin(this.angle)*this.speed;
    this.alpha=1;
    this.color=color;
    this.decay=0.012+Math.random()*0.012;
  }
  update(){
    this.x+=this.vx;
    this.y+=this.vy;
    this.vy+=0.04;
    this.vx*=0.985;
    this.vy*=0.985;
    this.alpha-=this.decay;
  }
  draw(){
    ctx.globalAlpha=this.alpha;
    ctx.beginPath();
    ctx.arc(this.x,this.y,2,0,Math.PI*2);
    ctx.fillStyle=this.color;
    ctx.fill();
    ctx.globalAlpha=1;
  }
}
let fireworks=[];
let particles=[];
function createParticles(x,y,color){
  for(let i=0;i<100;i++){
    particles.push(new Particle(x,y,color));
  }
}
function loop(){
  ctx.fillStyle="rgba(0,0,0,0.18)";
  ctx.fillRect(0,0,W,H);
  for(let i=fireworks.length-1;i>=0;i--){
    fireworks[i].update();
    fireworks[i].draw();
    if(fireworks[i].exploded) fireworks.splice(i,1);
  }
  for(let i=particles.length-1;i>=0;i--){
    particles[i].update();
    particles[i].draw();
    if(particles[i].alpha<=0) particles.splice(i,1);
  }
  requestAnimationFrame(loop);
}
loop();
setInterval(()=>{
  fireworks.push(new Firework(W*(0.15+Math.random()*0.7),H));
},700);
canvas.addEventListener('click',e=>{
  fireworks.push(new Firework(e.clientX,e.clientY));
})
</script>
</body>
</html>