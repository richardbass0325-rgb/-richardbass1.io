<!DOCTYPE html><html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover"><title>Blackwood: Last Shift</title><meta name="color-scheme" content="dark">
<style>
:root{--bg:#040506;--fg:#d5ddd8;--ac:#e23b3b;--ok:#6fd49a;--pn:#0b100fe8;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media(prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#040506}}:root[data-theme="dark"]{--bg:#040506}
html,body{height:100%;margin:0;background:var(--bg);color:var(--fg);font:14px/1.45 ui-monospace,Menlo,Consolas,monospace;overflow:hidden}
canvas{position:fixed;inset:0;width:100%;height:100%}
.ov{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:radial-gradient(#13201bdd,#000f);z-index:5;overflow:auto}
.pn{background:var(--pn);border:1px solid #29403a;border-radius:4px;padding:24px 28px;max-width:580px;width:calc(100% - 32px);box-shadow:0 0 60px #000,inset 0 0 40px #0a1a14}
h1{margin:0;font-size:34px;letter-spacing:.22em;color:var(--ac);text-shadow:0 0 22px #b00;animation:fk 4s infinite}@keyframes fk{0%,92%,96%,100%{opacity:1}94%{opacity:.35}98%{opacity:.6}}
h2{margin:16px 0 4px;font-size:12px;letter-spacing:.2em;color:var(--ok)}p{margin:4px 0}small{color:#93a39b}
button,input{font:inherit;color:var(--fg);background:linear-gradient(#1a2a24,#101a16);border:1px solid #3e5a4e;border-radius:3px;padding:11px 18px;margin:5px 6px 5px 0;cursor:pointer;letter-spacing:.1em}
button:hover{border-color:var(--ok);box-shadow:0 0 14px #2a6;background:#1f3a30}button.big{width:100%;padding:15px;font-size:16px;margin:8px 0}input{cursor:text;width:120px;text-transform:uppercase}
.hud{position:fixed;z-index:3;pointer-events:none;text-shadow:0 0 6px #000}
#obj{left:14px;top:calc(12px + env(safe-area-inset-top,0px));background:#050909b0;border-left:3px solid var(--ok);padding:8px 12px;font-size:12px;min-width:210px}
#role{right:14px;top:calc(12px + env(safe-area-inset-top,0px));font-weight:700;letter-spacing:.2em;padding:6px 12px;background:#050909b0;border-right:3px solid var(--ac)}
#msg{left:0;right:0;top:20%;text-align:center;font-size:19px;color:#ffd27a;letter-spacing:.08em}#pr{left:0;right:0;bottom:24%;text-align:center;font-size:15px}
#abs{left:0;right:0;bottom:calc(14px + env(safe-area-inset-bottom,0px));display:flex;justify-content:center;gap:8px}
.ab{position:relative;border:1px solid #6a2a2a;background:#1a0b0bdd;padding:7px 10px;min-width:84px;text-align:center;font-size:11px;overflow:hidden}.ab i{position:absolute;left:0;bottom:0;height:3px;background:var(--ac)}.ab.cd{opacity:.5}
#xh{left:50%;top:50%;width:4px;height:4px;margin:-2px;background:#fff9;border-radius:50%}
#sb{left:50%;bottom:calc(14px + env(safe-area-inset-bottom,0px));width:160px;margin-left:-80px;height:5px;background:#0008}#sb i{display:block;height:100%;background:#8cd}
#vg{position:fixed;inset:0;pointer-events:none;z-index:2;background:radial-gradient(transparent 45%,#000d),repeating-linear-gradient(#0000 0 2px,#0003 2px 3px)}
select{font:inherit;color:var(--fg);background:#101a16;border:1px solid #3e5a4e;padding:7px;border-radius:3px;margin:3px 0;width:100%}select:disabled{opacity:.6}.scr{display:none}.cg{display:grid;grid-template-columns:1fr 1fr;gap:2px 10px}.cg label{font-size:11px;color:#93a39b}.row{display:flex;align-items:center;gap:6px;margin:3px 0}.row span{flex:1}button.sm{padding:5px 10px;margin:0;font-size:12px}
</style></head><body>
<div id="vg"></div><div class="hud" id="obj"></div><div class="hud" id="role"></div><div class="hud" id="msg"></div><div class="hud" id="pr"></div><div class="hud" id="xh"></div><div class="hud" id="sb"><i></i></div><div class="hud" id="abs"></div>
<div class="ov" id="menu"><div class="pn">
<h1>BLACKWOOD</h1><p><b>LAST SHIFT</b> <small>— the asylum never sleeps</small></p>
<div class="scr" id="s-user"><h2>CHOOSE YOUR USERNAME</h2><p><small>Other players and friends will see this name.</small></p><input id="un" maxlength="14" placeholder="username" style="width:100%;text-transform:none"><h2>YOUR STATE</h2><select id="us"></select><p id="ue" style="color:#e66"></p><button class="big" id="ub">CONTINUE</button></div>
<div class="scr" id="s-main"><p id="hi"></p><button class="big" id="bs">QUICK PLAY <small>· you + bots</small></button><button class="big" id="bc">CREATE LOBBY</button><button class="big" id="bj0">JOIN LOBBY</button><button class="big" id="bf">FRIENDS</button><p id="me"></p>
<h2>SURVIVORS</h2><p><small>Repair every generator (hold E), find the gate key, unlock the exit and escape.</small></p><h2>THE WARDEN</h2><p><small>[1] Dash · [2] Sense · [3] Seal Door · [4] Blackout · [5] Shriek. One random player or bot is the Warden each match.</small></p><p><small>WASD move · Shift sprint · E interact · click to capture the mouse</small></p><button id="bn" class="sm">CHANGE NAME / STATE</button></div>
<div class="scr" id="s-join"><h2>JOIN A LOBBY</h2><div class="row"><input id="code" maxlength="4" placeholder="CODE" style="width:90px"><button id="bj" style="margin:0">JOIN</button></div><p id="je" style="color:#e66"></p><h2 id="ph"></h2><div id="pl"></div><button class="back">BACK</button></div>
<div class="scr" id="s-fr"><h2>FRIENDS</h2><div class="row"><input id="fi" maxlength="14" placeholder="friend’s username" style="width:180px;text-transform:none"><button id="fa" style="margin:0">ADD FRIEND</button></div><div id="fl"></div><p><small>Friends show as online when they have the game open. If they are in a lobby, you can join them.</small></p><button class="back">BACK</button></div>
<div class="scr" id="s-lob"><h2>LOBBY CODE: <span id="lc" style="color:#ffd27a;letter-spacing:.3em;font-size:18px"></span></h2><div id="lp"></div><h2>SETTINGS <small id="lh"></small></h2><div class="cg"><label>Max players<select id="c-max"></select></label><label>Generator repair time<select id="c-rep"><option value="40">Quick (40s)</option><option value="60">Normal (60s)</option><option value="90">Long (90s)</option></select></label><label>Generators<select id="c-gen"><option>3</option><option>4</option><option>5</option></select></label><label>Bot skill<select id="c-dif"><option value="0">Easy</option><option value="1">Normal</option><option value="2">Hard</option></select></label><label>Visibility<select id="c-pub"><option value="1">Public (my state)</option><option value="0">Private (code / friends)</option></select></label></div><p><small>Empty slots are filled with bots when the host starts.</small></p><button class="big" id="bcr">CREATE LOBBY</button><button class="big" id="bg">START MATCH</button><button onclick="location.reload()">LEAVE</button></div>
</div></div>
<div class="ov" id="end" style="display:none"><div class="pn"><h1 id="et"></h1><p id="es"></p><button onclick="location.reload()">MAIN MENU</button></div></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
const $=i=>document.getElementById(i),rnd=Math.random;
const AB=[['Dash',14],['Sense',24],['Seal Door',18],['Blackout',40],['Shriek',28]];
const sc=new THREE.Scene();sc.background=new THREE.Color(0x030506);sc.fog=new THREE.FogExp2(0x040a0a,.08);
const cam=new THREE.PerspectiveCamera(75,innerWidth/innerHeight,.1,70);cam.rotation.order='YXZ';sc.add(cam);
const rd=new THREE.WebGLRenderer({antialias:true});rd.setSize(innerWidth,innerHeight);rd.setPixelRatio(Math.min(devicePixelRatio,1.5));document.body.prepend(rd.domElement);
addEventListener('resize',()=>{rd.setSize(innerWidth,innerHeight);cam.aspect=innerWidth/innerHeight;cam.updateProjectionMatrix()});
const amb=new THREE.AmbientLight(0x40545e,.55);sc.add(amb);
const fl=new THREE.SpotLight(0xfff0d8,2.4,26,.6,.5);fl.target.position.set(0,0,-1);cam.add(fl,fl.target);
function tex(f,rx,ry){const c=document.createElement('canvas');c.width=c.height=128;const g=c.getContext('2d');f(g);const t=new THREE.CanvasTexture(c);t.wrapS=t.wrapT=THREE.RepeatWrapping;t.repeat.set(rx,ry);return t}
const nz=(g,n,a)=>{for(let i=0;i<n;i++){g.fillStyle=`rgba(${rnd()<.5?0:255},${rnd()<.5?0:255},${rnd()<.5?0:255},${rnd()*a})`;g.fillRect(rnd()*128,rnd()*128,1+rnd()*2,1+rnd()*2)}};
const wt=tex(g=>{g.fillStyle='#59625e';g.fillRect(0,0,128,128);nz(g,1400,.12);for(let i=0;i<6;i++){const x=rnd()*128,l=g.createLinearGradient(0,0,0,128);l.addColorStop(0,'#0000');l.addColorStop(1,'#1a1208aa');g.fillStyle=l;g.fillRect(x,0,6+rnd()*12,128)}g.fillStyle='#2a2f2c';g.fillRect(0,112,128,16);g.fillStyle='#0004';g.fillRect(0,110,128,2)},1,1);
const ft=tex(g=>{g.fillStyle='#2a2e2c';g.fillRect(0,0,128,128);g.fillStyle='#222624';g.fillRect(0,0,64,64);g.fillRect(64,64,64,64);nz(g,1500,.1);g.strokeStyle='#0008';g.strokeRect(0,0,128,128)},30,30);
const ct=tex(g=>{g.fillStyle='#2d3231';g.fillRect(0,0,128,128);g.strokeStyle='#161a19';g.lineWidth=4;g.strokeRect(2,2,124,124);nz(g,600,.08)},15,15);
const mat=(c,e,t)=>new THREE.MeshStandardMaterial({color:c,roughness:.9,emissive:e||0,emissiveIntensity:e?1:0,map:t||null});
const G=[],W=[];
function bx(x,z,w,d,h,m,y){const o=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),m);o.position.set(x,y==null?h/2:y,z);sc.add(o);return o}
function seg(ax,c,a,b){if(b-a<.1)return;const t=.4,m=mat(0xffffff,0,wt.clone());m.map.needsUpdate=true;m.map.repeat.set((b-a)/3,1);if(ax=='x'){bx(c,(a+b)/2,t,b-a,3.6,m);W.push([c-t/2,c+t/2,a,b])}else{bx((a+b)/2,c,b-a,t,3.6,m);W.push([a,b,c-t/2,c+t/2])}}
function line(ax,c,a,b,gs){let s=a;for(const g of gs){seg(ax,c,s,g-1.5);G.push({x:ax=='x'?c:g,z:ax=='x'?g:c});s=g+1.5}seg(ax,c,s,b)}
const fm=new THREE.Mesh(new THREE.PlaneGeometry(60,60),mat(0xffffff,0,ft));fm.rotation.x=-Math.PI/2;sc.add(fm);
const cm=new THREE.Mesh(new THREE.PlaneGeometry(60,60),mat(0xffffff,0,ct));cm.rotation.x=Math.PI/2;cm.position.y=3.6;sc.add(cm);
[-30,30].forEach(c=>{line('x',c,-30,30,[]);line('z',c,-30,30,[])});
[-10,10].forEach(c=>{line('x',c,-30,30,[-20,0,20]);line('z',c,-30,30,[-20,0,20])});
const RC=[];for(const a of[-20,0,20])for(const b of[-20,0,20])RC.push([a,b]);
const lights=[];RC.forEach(([a,b],i)=>{const cr=mat(0x3d2e20),bd=mat(0x8a8f8c);bx(a+5.5,b+5.5,1.4,1.4,1.4,cr);W.push([a+4.8,a+6.2,b+4.8,b+6.2]);bx(a-6,b-4.5,.9,2,.5,bd);bx(a-6,b-4.5,.9,2,.2,mat(0xb9b3a4),.9);W.push([a-6.5,a-5.5,b-5.5,b-3.5]);
const pl=new THREE.PointLight(i%3==1?0xffd9a0:0xa8d0ff,.9,15);pl.position.set(a,3.2,b);sc.add(pl);lights.push(pl);bx(a,b,1.4,.6,.06,mat(0x222,0xd8e8ff),3.55);
const bl=new THREE.Mesh(new THREE.PlaneGeometry(2.2,1.6),new THREE.MeshBasicMaterial({color:0x2a0505,transparent:true,opacity:.7}));bl.rotation.x=-Math.PI/2;bl.position.set(a+2.5*(i%2?-1:1),.02,b+3);sc.add(bl)});
function col(p,r){for(const b of W){const cx=Math.max(b[0],Math.min(p.x,b[1])),cz=Math.max(b[2],Math.min(p.z,b[3])),dx=p.x-cx,dz=p.z-cz,d=Math.hypot(dx,dz);if(d<r){if(d>1e-4){p.x+=dx/d*(r-d);p.z+=dz/d*(r-d)}else p.x+=r}}}
const FS=RC.map(([a,b])=>[a-4.5,b+4.5]),NS=RC.map(([a,b])=>[a+4.5,b-4.5]),SP=FS.concat(NS);
const dp=new Float32Array(900);for(let i=0;i<900;i++)dp[i]=(rnd()-.5)*60;const dg=new THREE.BufferGeometry();dg.setAttribute('position',new THREE.BufferAttribute(dp,3));const dust=new THREE.Points(dg,new THREE.PointsMaterial({size:.05,color:0x9aa8a8,transparent:true,opacity:.5}));dust.position.y=1.8;sc.add(dust);
// gate
const hz=tex(g=>{g.fillStyle='#d9b200';g.fillRect(0,0,128,128);g.fillStyle='#161616';for(let x=-128;x<256;x+=32){g.beginPath();g.moveTo(x,128);g.lineTo(x+16,128);g.lineTo(x+144,0);g.lineTo(x+128,0);g.fill()}},1,1);
const sgn=(t,c)=>{const cv=document.createElement('canvas');cv.width=256;cv.height=96;const g=cv.getContext('2d');g.fillStyle='#050505';g.fillRect(0,0,256,96);g.strokeStyle=c;g.lineWidth=4;g.strokeRect(4,4,248,88);g.fillStyle=c;g.font='bold 54px monospace';g.textAlign='center';g.fillText(t,128,68);return new THREE.CanvasTexture(cv)};
const sR=sgn('LOCKED','#ff3b2a'),sG=sgn('EXIT','#40ff80'),steel=mat(0x3a3f44),GATE={x:0,z:29};
const gate=bx(0,29.6,6,3.4,.3,mat(0x23262a,0x120000)),gl=bx(0,29.3,.5,.5,.5,mat(0x300,0xff2200),3.7);for(let i=-2;i<=2;i++)bx(i*1.2,29.4,.14,.14,3.4,mat(0x6a7076,0x060000));
[-3.3,3.3].forEach(x=>{bx(x,29.4,.7,.7,3.6,steel);bx(x,29.05,.78,.1,3.6,mat(0xffffff,0,hz.clone()))});bx(0,29.3,7.3,.6,.5,mat(0xffffff,0,hz.clone()),3.35);
const sign=new THREE.Mesh(new THREE.PlaneGeometry(2.4,.9),new THREE.MeshBasicMaterial({map:sR}));sign.position.set(0,2.75,29.0);sc.add(sign);
function mkGen(x,z){const g=new THREE.Group();g.position.set(x,0,z);const A=(geo,m,px,py,pz)=>{const o=new THREE.Mesh(geo,m);o.position.set(px,py,pz);g.add(o);return o},B=(w,h,d)=>new THREE.BoxGeometry(w,h,d),C=(r,h,n)=>new THREE.CylinderGeometry(r,r,h,n||10);
A(B(1.7,.14,1.3),steel,0,.07,0);A(B(1.3,.85,.9),mat(0x3d5a3a),0,.6,0);A(B(1.34,.16,.94),mat(0xffffff,0,hz.clone()),0,1.1,0);
[.4,.1].forEach(px=>{A(C(.07,.8),steel,px,1.55,.2);A(C(.1,.1),mat(0x111),px,1.97,.2)});
const fan=new THREE.Group();fan.position.set(0,.6,.47);g.add(fan);fan.add(new THREE.Mesh(B(.5,.05,.02),mat(0x222)),new THREE.Mesh(B(.05,.5,.02),mat(0x222)));A(C(.3,.04,16),steel,0,.6,.45).rotation.x=Math.PI/2;
A(B(.4,.3,.12),mat(0x111418,0x0a2a30),-.4,.8,.5);A(C(.03,1.6),mat(0x111),.8,.8,.2).rotation.z=1.2;A(C(.03,1.6),mat(0x111),-.8,.6,-.3).rotation.z=-1.3;
const lamp=A(new THREE.SphereGeometry(.11,10,8),mat(0x300,0xff2200),.5,1.3,.4);
const bg=A(B(1.3,.1,.1),mat(0x111),0,2.35,0),bar=A(B(1.24,.06,.12),new THREE.MeshBasicMaterial({color:0xff3a22}),0,2.35,0);bar.scale.x=.01;
const beam=A(new THREE.CylinderGeometry(.12,.3,3,12,1,true),new THREE.MeshBasicMaterial({color:0xff3322,transparent:true,opacity:.14,blending:THREE.AdditiveBlending,depthWrite:false,side:2}),0,1.8,0);
const pl=new THREE.PointLight(0xff3322,.7,7);pl.position.set(0,1.8,.5);g.add(pl);sc.add(g);return{b:g,l:lamp,bar,fan:fan,beam,pl}}
function mkKey(x,z){const g=new THREE.Group(),au_=mat(0xe8c24a,0xa07800),A=(geo,px,py)=>{const o=new THREE.Mesh(geo,au_);o.position.set(px,py,0);g.add(o);return o};
A(new THREE.TorusGeometry(.15,.04,8,16),0,1.35);A(new THREE.BoxGeometry(.06,.5,.05),0,1.0);A(new THREE.BoxGeometry(.18,.06,.05),.1,.82);A(new THREE.BoxGeometry(.12,.06,.05),.08,.93);
const bm=new THREE.Mesh(new THREE.CylinderGeometry(.08,.35,3.2,10,1,true),new THREE.MeshBasicMaterial({color:0xffd24a,transparent:true,opacity:.16,blending:THREE.AdditiveBlending,depthWrite:false,side:2}));bm.position.y=1.6;g.add(bm);
const pl=new THREE.PointLight(0xffc840,1.1,8);pl.position.y=1.2;g.add(pl);g.position.set(x,0,z);sc.add(g);return g}
// state
let S=null,R=null,myId='me',L=[],role='s',st='a',carry=0,keys={},yaw=0,pit=0,px=0,pz=0,stam=100,mode='menu',md=0,tmr=0,pt=0,toastT=0,endT=0,gens=[],keyM=null,bots=[],blk=0,slow=0,dash=0,sense=0,cds=[0,0,0,0,0],rpT=0,lastA=0,bob=0;
const PM={},toast=t=>{$('msg').textContent=t;toastT=3.2};
let au;function beep(f,d,ty,v){try{au=au||new AudioContext();const o=au.createOscillator(),g=au.createGain();o.type=ty||'sawtooth';o.frequency.value=f;g.gain.value=v||.07;g.gain.exponentialRampToValueAtTime(.0001,au.currentTime+d);o.connect(g);g.connect(au.destination);o.start();o.stop(au.currentTime+d)}catch(e){}}
function rng(s){return()=>{s|=0;s=s+0x6D2B79F5|0;let t=Math.imul(s^s>>>15,1|s);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296}}
const PAL=[0x2b6a78,0x8a5a2a,0x4a7a3a,0x7a3a7a,0x8a7a2a];
function figure(mon,id){const g=new THREE.Group(),h=[...String(id)].reduce((a,c)=>a+c.charCodeAt(0),0),sk=mat(mon?0x1d1d22:0xc9b49b),cl=mat(mon?0x141016:PAL[h%5],mon?0x180000:0),dk=mat(0x1a1c1e),s=mon?1.25:1;
const add=(geo,m,x,y,z,p)=>{const o=new THREE.Mesh(geo,m);o.position.set(x*s,y*s,z*s);(p||g).add(o);return o};
const limb=(m,x,y,len,r)=>{const p=new THREE.Group();p.position.set(x*s,y*s,0);g.add(p);const o=new THREE.Mesh(new THREE.CylinderGeometry(r,r*.75,len,7),m);o.position.y=-len/2*s;o.scale.setScalar(s);p.add(o);return p};
add(new THREE.CylinderGeometry(.26,.3,mon?1.3:.85,10),cl,0,mon?1.1:1.2,0);add(new THREE.SphereGeometry(mon?.27:.2,10,8),sk,0,mon?1.95:1.75,0);
const la=limb(cl,-.36,mon?1.55:1.55,mon?1.3:.8,.07),ra=limb(cl,.36,mon?1.55:1.55,mon?1.3:.8,.07),ll=limb(mon?cl:dk,-.15,mon?.9:.85,mon?.9:.8,.1),rl=limb(mon?cl:dk,.15,mon?.9:.85,mon?.9:.8,.1);
if(mon){la.rotation.x=ra.rotation.x=-.5;[-.1,.1].forEach(x=>{add(new THREE.SphereGeometry(.045,6,6),new THREE.MeshBasicMaterial({color:0xff2200}),x,2,.22);add(new THREE.ConeGeometry(.06,.4,6),mat(0x0c0c0c),x*2.4,2.3,0)})}
else{add(new THREE.SphereGeometry(.215,10,6,0,6.3,0,1.5),mat(0x2a1c12),0,1.78,0);add(new THREE.BoxGeometry(.34,.5,.16),dk,0,1.25,-.24);add(new THREE.CylinderGeometry(.305,.305,.07,10),mat(0xdddddd,0x444444),0,1.0,0);
const fl2=add(new THREE.CylinderGeometry(.035,.035,.2,8),mat(0xfff0c0,0xfff0c0),.36,1.15,.15);fl2.rotation.x=Math.PI/2;
const gm=new THREE.ConeGeometry(.55,3,12,1,true);gm.translate(0,-1.5,0);const bm=new THREE.Mesh(gm,new THREE.MeshBasicMaterial({color:0xfff2cc,transparent:true,opacity:.07,blending:THREE.AdditiveBlending,depthWrite:false,side:2}));bm.rotation.x=-Math.PI/2;bm.position.set(.36,1.15,.25);g.add(bm);ra.rotation.x=-1.2;}
const mk=new THREE.Mesh(new THREE.SphereGeometry(.35,8,8),new THREE.MeshBasicMaterial({color:0xff2a2a,depthTest:false}));mk.position.y=1.3;mk.renderOrder=999;mk.visible=false;g.add(mk);
g.userData={mk,ll,rl,la,ra,mon};sc.add(g);return g}
// ---- match ----
function begin(seed,mon,nb){const r=rng(seed),pick=(a,n)=>{a=a.slice();const o=[];while(o.length<n)o.push(a.splice(r()*a.length|0,1)[0]);return o};
gens.forEach(g=>{sc.remove(g.b);sc.remove(g.l)});if(keyM)sc.remove(keyM);for(const k in PM){sc.remove(PM[k]);delete PM[k]}
const sp=pick(SP,cfg.gens+1);S={mon,gate:0,gk:0,end:0};
gens=sp.slice(0,cfg.gens).map(p=>Object.assign({p:0,x:p[0],z:p[1]},mkGen(p[0],p[1])));vis.fill(0);noise=null;pat=null;
keyM=mkKey(sp[cfg.gens][0],sp[cfg.gens][1]);S.kx=sp[cfg.gens][0];S.kz=sp[cfg.gens][1];
const cs=[[-20,-20],[20,-20],[-20,20],[20,20]],c=cs[r()*4|0];role=myId==mon?'m':'s';st='a';blk=slow=dash=sense=0;cds=[3,3,3,3,3];
if(role=='m'){px=c[0];pz=c[1]}else{px=(rnd()-.5)*6;pz=(rnd()-.5)*6}yaw=pit=0;
bots=[];if(!R||isHost)Array.from({length:nb||0},(_,i)=>'b'+(i+1)).forEach(id=>{const w=id==mon;bots.push({id,x:w?c[0]:(rnd()-.5)*8,z:w?c[1]:(rnd()-.5)*8,yaw:0,r:w?'m':'s',s:'a',t:0})});
mode='play';$('menu').style.display='none';$('end').style.display='none';$('role').textContent=role=='m'?'YOU ARE THE WARDEN':'SURVIVOR';$('role').style.color=role=='m'?'#f55':'#8cd';
$('abs').innerHTML=role=='m'?AB.map((a,i)=>`<div class="ab" id="ab${i}">[${i+1}] ${a[0]}<br><small id="cd${i}"></small><i id="cb${i}"></i></div>`).join(''):'';
$('sb').style.display=role=='m'?'none':'block';toast(role=='m'?'You are the Warden. Hunt them down.':'Repair the generators, find the key, escape.');beep(80,1.2)}
const done=()=>gens.filter(g=>g.p>=100).length;
const pb=(p,c)=>`<div style="height:5px;background:#1c2420;margin:2px 0 6px"><i style="display:block;height:100%;width:${p}%;background:${c};box-shadow:0 0 6px ${c}"></i></div>`;
function objHTML(){if(!S)return'';const d=done(),L=(ok,i,t)=>`<div style="color:${ok?'#6fd49a':'#d5ddd8'}">${i} ${t}${ok?' ✔':''}</div>`;
let h='<div style="letter-spacing:.25em;color:#6fd49a;font-size:11px;margin-bottom:5px">OBJECTIVES</div>'+L(d>=3,'⚙',`GENERATORS ${d}/3`);
gens.forEach((g,i)=>h+=`<div style="font-size:11px;color:#8fa59a">&nbsp;&nbsp;GEN ${i+1} · ${g.p>=100?'ONLINE':(g.p|0)+'%'}</div>`+pb(g.p,g.p>=100?'#6fd49a':g.p>0?'#e8b84a':'#e24a3a'));
h+=L(S.gk,'🗝','GATE KEY '+(S.gk?'RECOVERED':'MISSING'))+L(S.gate,'⛩','UNLOCK THE EXIT')+L(st=='e','🚪','ESCAPE');
return h+(role=='m'?'<div style="color:#f77;margin-top:6px">Stop them.</div>':'')}
// ---- net ----
const send=d=>R?R.emit('g',d):handle(d,{isMe:true,peer:'me'});
function kill(id){if(id==myId){if(role=='s'&&st=='a'){st='d';toast('The Warden caught you.');beep(55,1.2)}}else{const b=bots.find(x=>x.id==id);if(b)b.s='d'}}
function handle(d,m){if(d.t=='cfg'){if(R&&m.peer==hostId()&&!isHost){cfg=d.c;lobby()}return}if(d.t=='start'){if(R&&m.peer!=hostId())return;cfg=d.c;return begin(d.seed,d.mon,d.nb)}if(!S)return;switch(d.t){
case'rp':{const g=gens[d.i];if(!g||g.p>=100)break;noise={x:g.x,z:g.z,t:tmr};g.p=Math.min(100,g.p+d.d);if(g.p>=100){g.l.material.emissive.setHex(0x22ff66);toast(`Generator repaired (${done()}/${gens.length})`+(done()>=gens.length?' — POWER ON. Find the key!':''));beep(440,.5,'sine')}
else if(role=='m'&&tmr-lastA>6){lastA=tmr;toast('You hear a generator running…');beep(90,.5)}break}
case'ky':if(!S.gk){S.gk=1;sc.remove(keyM);toast('The gate key was found!');beep(900,.3,'sine')}break;
case'gt':S.gate=1;sign.material.map=sG;sign.material.needsUpdate=true;toast('THE EXIT GATE IS OPEN!');gl.material.emissive.setHex(0x22ff66);beep(70,1.6);break;
case'ab':fx(d);break;case'ct':kill(d.id);break}}
function fx(d){if(d.n==3){const g=G[d.g];if(!g)return;const h=Math.abs(g.x)==10||Math.abs(g.x)==30?[.6,1.6]:[1.6,.6],b=[g.x-h[0],g.x+h[0],g.z-h[1],g.z+h[1]];W.push(b);const o=bx(g.x,g.z,h[0]*2,h[1]*2,3.4,mat(0x2a0606,0x550000));toast('A door was sealed!');setTimeout(()=>{sc.remove(o);W.splice(W.indexOf(b),1)},12000)}
if(d.n==4&&role=='s'){blk=6;toast('LIGHTS OUT');beep(60,1.5)}
if(d.n==5&&role=='s'&&Math.hypot(px-d.x,pz-d.z)<20){slow=3;toast('THE SHRIEK — you are slowed!');beep(1500,1.2,'square',.1)}}
function useAb(n){if(role!='m'||cds[n]>0)return;cds[n]=AB[n][1];
if(n==0){dash=3;beep(200,.4)}if(n==1)sense=5;
if(n==2){let b=-1,bd=14;G.forEach((g,i)=>{const d=Math.hypot(g.x-px,g.z-pz);if(d<bd){bd=d;b=i}});if(b<0){cds[n]=2;return toast('No door in reach')}send({t:'ab',n:3,g:b})}
if(n==3)send({t:'ab',n:4});if(n==4)send({t:'ab',n:5,x:px,z:pz})}
// ---- interaction ----
function near(){if(!S)return null;let b=null,bd=2.6;const c=(x,z,o)=>{const d=Math.hypot(x-px,z-pz);if(d<bd){bd=d;b=o}};
gens.forEach((g,i)=>g.p<100&&c(g.x,g.z,{k:'g',i,t:`[HOLD E] Repair generator (${g.p|0}%)`}));if(!S.gk)c(S.kx,S.kz,{k:'k',t:'[E] Take the key'});
if(!S.gate)c(GATE.x,GATE.z-1,{k:'e',t:'[E] Unlock exit gate'});return b}
function act(){if(role!='s'||st!='a'||!S)return;const n=near();if(!n)return;
if(n.k=='k')send({t:'ky'});else if(n.k=='e'){if(done()<gens.length)toast('The gate has no power — repair the generators.');else if(!S.gk)toast('The gate is locked. Find the key.');else send({t:'gt'})}}
// ---- input ----
addEventListener('keydown',e=>{if(e.target.tagName=='INPUT')return;keys[e.code]=1;if(e.code=='KeyE'&&!e.repeat)act();if(e.code.startsWith('Digit')&&mode=='play'){const n=+e.code[5]-1;if(n>=0&&n<5)useAb(n)}});
addEventListener('keyup',e=>keys[e.code]=0);
addEventListener('mousedown',e=>{md=1;if(mode=='play'&&e.target.tagName=='CANVAS'&&rd.domElement.requestPointerLock)rd.domElement.requestPointerLock()});addEventListener('mouseup',()=>md=0);
addEventListener('mousemove',e=>{if(mode!='play'||(!document.pointerLockElement&&!md))return;yaw-=e.movementX*.0024;pit=Math.max(-1.3,Math.min(1.3,pit-e.movementY*.0024))});
let pre=false,cfg={max:4,rep:60,gens:3,diff:1,pub:1},isHost=false,lobCode='',ROOM=null,R0=null,L0=[];
const ls={g:k=>{try{return localStorage.getItem(k)}catch(e){return null}},s:(k,v)=>{try{localStorage.setItem(k,v)}catch(e){}}},esc=t=>String(t).replace(/[&<>"']/g,c=>'&#'+c.charCodeAt(0)+';');
const show=id=>document.querySelectorAll('.scr').forEach(e=>e.style.display=e.id==id?'block':'none');
const ST=['Alabama','Alaska','Arizona','Arkansas','California','Colorado','Connecticut','Delaware','Florida','Georgia','Hawaii','Idaho','Illinois','Indiana','Iowa','Kansas','Kentucky','Louisiana','Maine','Maryland','Massachusetts','Michigan','Minnesota','Mississippi','Missouri','Montana','Nebraska','Nevada','New Hampshire','New Jersey','New Mexico','New York','North Carolina','North Dakota','Ohio','Oklahoma','Oregon','Pennsylvania','Rhode Island','South Carolina','South Dakota','Tennessee','Texas','Utah','Vermont','Virginia','Washington','West Virginia','Wisconsin','Wyoming'];
$('us').innerHTML=ST.map(x=>`<option>${x}</option>`).join('');$('c-max').innerHTML=[2,3,4,5,6,7,8].map(n=>`<option>${n}</option>`).join('');
let me={u:'',s:'Texas'};const frs=()=>{try{return JSON.parse(ls.g('bw_f')||'[]')}catch(e){return[]}};
function home(){$('hi').innerHTML=`Signed in as <b style="color:#ffd27a">${esc(me.u)}</b> <small>· ${esc(me.s)}</small>`;show('s-main')}
$('ub').onclick=()=>{const u=$('un').value.trim();if(!/^[A-Za-z0-9_ ]{2,14}$/.test(u)){$('ue').textContent='Use 2–14 letters, numbers, spaces or _.';return}me.u=u;me.s=$('us').value;ls.s('bw_u',u);ls.s('bw_s',me.s);home();connect()};
$('bn').onclick=()=>{$('un').value=me.u;$('us').value=me.s;show('s-user')};
document.querySelectorAll('.back').forEach(b=>b.onclick=home);
$('bf').onclick=()=>{renderFr();show('s-fr')};$('bj0').onclick=()=>{$('je').textContent=ROOM?'':'Online play isn’t available in this view. Open the shared link while signed in.';renderJoin();show('s-join')};
{const u=ls.g('bw_u');if(u){me.u=u;me.s=ls.g('bw_s')||'Texas';home();connect()}else show('s-user')}
async function connect(){try{ROOM=window.claude&&await claude.use('room');if(!ROOM)return;R0=await ROOM.join('bw-net');R0.onPeers(c=>{L0=c.peers.slice();renderJoin();renderFr()});net0()}catch(e){ROOM=null}}
function net0(){R0&&R0.presence({u:me.u,s:me.s,l:R?lobCode:'',pub:R&&isHost&&cfg.pub?1:0,n:L.length,m:cfg.max})}
function renderJoin(){$('ph').textContent='PUBLIC LOBBIES IN '+me.s.toUpperCase();const a=L0.filter(p=>!p.isMe&&p.presence&&p.presence.l&&p.presence.pub&&p.presence.s==me.s);
$('pl').innerHTML=a.map(p=>`<div class="row"><span>${esc(p.presence.u)}’s lobby <small>${+p.presence.n}/${+p.presence.m}</small></span><button class="sm" ${p.presence.n>=p.presence.m?'disabled':''} onclick="joinCode('${esc(p.presence.l)}')">JOIN</button></div>`).join('')||'<small>No public lobbies in your state right now. Create one!</small>'}
function renderFr(){const on=n=>L0.find(q=>!q.isMe&&q.presence&&String(q.presence.u).toLowerCase()==n.toLowerCase());
$('fl').innerHTML=frs().map(n=>{const p=on(n),l=p&&p.presence.l;return`<div class="row"><span>${p?'🟢':'⚪'} ${esc(n)} <small>${p?(l?'in lobby '+esc(l):'online'):'offline'}</small></span>${l?`<button class="sm" onclick="joinCode('${esc(l)}')">JOIN</button>`:''}<button class="sm" onclick="rmF('${esc(n)}')">✕</button></div>`}).join('')||'<small>No friends yet — add someone by username.</small>'}
window.rmF=n=>{ls.s('bw_f',JSON.stringify(frs().filter(x=>x!=n)));renderFr()};
$('fa').onclick=()=>{const n=$('fi').value.trim();if(/^[A-Za-z0-9_ ]{2,14}$/.test(n)&&n.toLowerCase()!=me.u.toLowerCase()&&!frs().some(x=>x.toLowerCase()==n.toLowerCase())){ls.s('bw_f',JSON.stringify(frs().concat(n)));$('fi').value='';renderFr()}};
window.joinCode=c=>enter(String(c).toUpperCase().replace(/[^A-Z0-9]/g,''),false);
$('bj').onclick=()=>{const c=$('code').value.trim();if(c.length>=3)joinCode(c);else $('je').textContent='Enter the 4-letter lobby code.'};
$('bc').onclick=()=>{if(!ROOM){alert('Online play isn’t available in this view. Open the shared link while signed in.');return}pre=true;isHost=true;R=null;L=[];$('lc').textContent='— — — —';show('s-lob');lobby()};
$('bcr').onclick=()=>{if(pre)enter(Array.from({length:4},()=>'ABCDEFGHJKLMNPQRSTUVWXYZ'[rnd()*24|0]).join(''),true)};
async function enter(code,host){pre=false;if(!ROOM){$('je').textContent='Online play isn’t available in this view.';return}try{R=await ROOM.join('bw'+code.toLowerCase());isHost=host;lobCode=code;myId='me2';
R.on('g',m=>handle(m.data,m));R.onPeers(ch=>{L=ch.peers.slice();const m=L.find(p=>p.isMe);if(m)myId=m.peer;lobby();net0();if(isHost&&ch.joined.length)R.emit('g',{t:'cfg',c:cfg})});
R.presence({u:me.u,h:host?1:0,x:0,z:0,y:0,r:'s',s:'a',v:1});L=R.peers().slice();$('lc').textContent=code;show('s-lob');lobby();net0()}catch(e){R=null;$('je').textContent='Could not join: '+(e.message||e.code||'error')}}
const hostId=()=>{const h=L.find(p=>p.presence&&p.presence.h==1);return h&&h.peer};
function lobby(){if(mode=='play')return;
const hum=pre?[{peer:'me',isMe:true,presence:{u:me.u,h:1}}]:L,hid=pre?'me':hostId();
let rows='';for(let i=0;i<cfg.max;i++){const p=hum[i];rows+=p?`<div class="row"><span>${p.peer==hid?'👑':'🧑'} <b>${esc((p.presence&&p.presence.u)||'player')}</b>${p.isMe?' <small>(you)</small>':''}${p.peer==hid?' <small>host</small>':''}</span><small style="color:#6fd49a">JOINED</small></div>`:`<div class="row"><span style="opacity:.5">🤖 BOT <small>fills this slot if nobody joins</small></span><small style="opacity:.5">waiting…</small></div>`}
$('lp').innerHTML=`<h2>PLAYERS ${Math.min(hum.length,cfg.max)}/${cfg.max} ${pre?'<small>— not created yet</small>':'<small>— updates live as people join</small>'}</h2>`+rows+(pre?'<p><small>Set up the lobby below, then press CREATE LOBBY. A code is made and friends or people in your state can join.</small></p>':'');
const c={'c-max':cfg.max,'c-rep':cfg.rep,'c-gen':cfg.gens,'c-dif':cfg.diff,'c-pub':cfg.pub};for(const k in c){$(k).value=c[k];$(k).disabled=!isHost}
$('lh').textContent=isHost?'(you are the host)':'(only the host can change these)';$('bcr').style.display=pre?'block':'none';$('bg').style.display=isHost&&!pre?'block':'none'}
['c-max','c-rep','c-gen','c-dif','c-pub'].forEach(id=>$(id).onchange=()=>{if(!isHost)return;cfg={max:+$('c-max').value,rep:+$('c-rep').value,gens:+$('c-gen').value,diff:+$('c-dif').value,pub:+$('c-pub').value};R&&R.emit('g',{t:'cfg',c:cfg});lobby();net0()});
$('bg').onclick=()=>{if(!isHost)return;const nb=Math.max(0,cfg.max-L.length),ids=L.map(p=>p.peer).concat(Array.from({length:nb},(_,i)=>'b'+(i+1)));send({t:'start',seed:(rnd()*1e9)|0,mon:ids[rnd()*ids.length|0],nb,c:cfg})};
$('bs').onclick=()=>{R=null;isHost=false;myId='me';cfg={max:4,rep:60,gens:3,diff:1,pub:0};begin((rnd()*1e9)|0,['me','b1','b2','b3'][rnd()*4|0],3)};
// ---- bots ----
const ro=(x,z)=>(x<-10?0:x<10?1:2)*3+(z<-10?0:z<10?1:2);
function wp(x,z,tx,tz){const a=ro(x,z),b=ro(tx,tz);if(a==b)return[tx,tz];const pv={};pv[a]=-1;const q=[a];while(q.length){const c=q.shift();if(c==b)break;const ci=c/3|0,cj=c%3;[[1,0],[-1,0],[0,1],[0,-1]].forEach(([di,dj])=>{const ni=ci+di,nj=cj+dj;if(ni<0||ni>2||nj<0||nj>2)return;const n=ni*3+nj;if(pv[n]===undefined){pv[n]=c;q.push(n)}})}
let c=b;while(pv[c]!==a)c=pv[c];return[(RC[a][0]+RC[c][0])/2,(RC[a][1]+RC[c][1])/2]}
function mv(b,tx,tz,sp,dt){sp*=[.9,1,1.12][cfg.diff];b.ck=(b.ck||0)+dt;if(b.ck>1.2){if(Math.hypot(b.x-(b.cx||0),b.z-(b.cz||0))<.6){b.w=2;const c=adj(ro(b.x,b.z));b.wr=c[rnd()*c.length|0]}b.ck=0;b.cx=b.x;b.cz=b.z}if(b.w>0){b.w-=dt;tx=RC[b.wr][0];tz=RC[b.wr][1]}[tx,tz]=wp(b.x,b.z,tx,tz);let a=Math.atan2(tx-b.x,tz-b.z);const stuck=b.sx!=null&&Math.hypot(b.x-b.sx,b.z-b.sz)<.004;b.sx=b.x;b.sz=b.z;if(stuck)b.t=1.1;if(b.t>0){b.t-=dt;a+=1.6}
b.x+=Math.sin(a)*sp*dt;b.z+=Math.cos(a)*sp*dt;b.yaw=a;const q={x:b.x,z:b.z};col(q,.45);b.x=q.x;b.z=q.z}
let vis=Array(9).fill(0),noise=null,pat=null;
function adj(a){const i=a/3|0,j=a%3,o=[];[[1,0],[-1,0],[0,1],[0,-1]].forEach(([di,dj])=>{const ni=i+di,nj=j+dj;if(ni>=0&&ni<3&&nj>=0&&nj<3)o.push(ni*3+nj)});return o}
function botTick(b,dt){if(b.s!='a')return;
if(b.r=='m'){const sv=[];if(role=='s'&&st=='a')sv.push({x:px,z:pz,id:'me'});bots.forEach(o=>o.r=='s'&&o.s=='a'&&sv.push({x:o.x,z:o.z,id:o.id}));
let t=null,bd=1e9;sv.forEach(o=>{const d=Math.hypot(o.x-b.x,o.z-b.z);if(d<bd){bd=d;t=o}});const sees=t&&(bd<[11,16,24][cfg.diff]||sense>0);if(sees)b.last={x:t.x,z:t.z,t:tmr};
if(cds[1]<=0&&!sees&&rnd()<.01){cds[1]=24;sense=5}
if(b.last&&tmr-b.last.t<4){if(cds[0]<=0&&bd<13){cds[0]=14;dash=3}if(cds[4]<=0&&bd<9){cds[4]=28;send({t:'ab',n:5,x:b.x,z:b.z})}
if(cds[2]<=0&&bd<14&&bd>4){let gi=-1,gd=1e9;G.forEach((g,i)=>{const d=Math.hypot(g.x-t.x,g.z-t.z);if(d<gd){gd=d;gi=i}});if(gd<8){cds[2]=18;send({t:'ab',n:3,g:gi})}}
if(cds[3]<=0&&bd>14&&rnd()<.003){cds[3]=40;send({t:'ab',n:4})}
mv(b,b.last.x,b.last.z,dash>0?5.6:3.1,dt);if(sees&&bd<1.5)send({t:'ct',id:t.id});return}
if(noise&&tmr-noise.t<14){if(Math.hypot(noise.x-b.x,noise.z-b.z)<3)noise=null;else{mv(b,noise.x,noise.z,3,dt);return}}
if(pat==null||Math.hypot(RC[pat][0]-b.x,RC[pat][1]-b.z)<3){const c=adj(ro(b.x,b.z));if(rnd()<.3)c.push(rnd()*9|0);pat=c[rnd()*c.length|0]}
mv(b,RC[pat][0],RC[pat][1],2.6,dt);return}
const w=role=='m'?{x:px,z:pz}:bots.find(o=>o.r=='m'),wd=w?Math.hypot(w.x-b.x,w.z-b.z):99,a=ro(b.x,b.z);
if(wd<12){const wr=ro(w.x,w.z);let best=a,bs=-1;adj(a).forEach(r=>{const d=Math.hypot(RC[r][0]-w.x,RC[r][1]-w.z)-(r==wr?30:0);if(d>bs){bs=d;best=r}});mv(b,RC[best][0],RC[best][1],wd<8?5.2:4.2,dt);return}
const open=gens.map((g,i)=>({g,i})).filter(o=>o.g.p<100);
if(open.length){let pk=null,ps=1e9;open.forEach(o=>{let v=Math.hypot(o.g.x-b.x,o.g.z-b.z);if(w&&Math.hypot(o.g.x-w.x,o.g.z-w.z)<14)v+=45;if(bots.some(q=>q!=b&&q.r=='s'&&q.s=='a'&&q.gi==o.i))v+=12;if(v<ps){ps=v;pk=o}});
b.gi=pk.i;if(Math.hypot(pk.g.x-b.x,pk.g.z-b.z)<1.7)send({t:'rp',i:pk.i,d:100/(cfg.rep*1.05)*dt});else mv(b,pk.g.x,pk.g.z,3.3,dt);return}
b.gi=-1;
if(!S.gk){const kr=ro(S.kx,S.kz),dc=Math.hypot(RC[a][0]-b.x,RC[a][1]-b.z);
if(kr==a&&dc<7.5){if(Math.hypot(S.kx-b.x,S.kz-b.z)<1.5)send({t:'ky'});else mv(b,S.kx,S.kz,3.3,dt);return}
if(dc<6)vis[a]=1;let tr=-1,td=1e9;RC.forEach((c,i)=>{if(!vis[i]){const d=Math.hypot(c[0]-b.x,c[1]-b.z)+(bots.some(q=>q!=b&&q.er===i)?30:0);if(d<td){td=d;tr=i}}});if(tr<0){vis.fill(0);tr=a}b.er=tr;mv(b,RC[tr][0],RC[tr][1],3.5,dt);return}
if(!S.gate){if(Math.hypot(GATE.x-b.x,GATE.z-1-b.z)<2)send({t:'gt'});else mv(b,GATE.x,GATE.z-1,3.3,dt)}
else{if(Math.hypot(GATE.x-b.x,GATE.z-b.z)<2.2)b.s='e';else mv(b,GATE.x,GATE.z-1,3.5,dt)}}
// ---- loop ----
let last=performance.now();
function frame(now){requestAnimationFrame(frame);const dt=Math.min(.05,(now-last)/1000);last=now;if(mode=='play'&&S)tick(dt);else if(mode=='menu'){cam.position.set(0,1.6,0);yaw+=dt*.1;cam.rotation.set(0,yaw,0)}rd.render(sc,cam)}
const others=()=>{if(!R)return bots.map(b=>({peer:b.id,pr:{x:b.x,z:b.z,y:b.yaw,r:b.r,s:b.s}}));
const o=L.filter(p=>!p.isMe).map(p=>({peer:p.peer,pr:p.presence||{}}));const hp=L.find(p=>p.presence&&p.presence.h==1),bl=isHost?bots.map(b=>[b.id,b.x,b.z,b.yaw,b.r,b.s]):(hp&&hp.presence.b)||[];
bl.forEach(a=>o.push({peer:a[0],pr:{x:a[1],z:a[2],y:a[3],r:a[4],s:a[5]}}));return o};
function tick(dt){tmr+=dt;if(toastT>0){toastT-=dt;if(toastT<=0)$('msg').textContent=''}
lights.forEach((l,i)=>{l.intensity=blk>0?.05:(.9+(i%4==0?Math.sin(tmr*31+i)*Math.sin(tmr*7)*.5:0))});
cds=cds.map(c=>Math.max(0,c-dt));if(role=='m')AB.forEach((a,i)=>{const e=$('ab'+i);if(e){e.classList.toggle('cd',cds[i]>0);$('cd'+i).textContent=cds[i]>0?Math.ceil(cds[i])+'s':'ready';$('cb'+i).style.width=(cds[i]>0?100*cds[i]/a[1]:0)+'%'}});
dash=Math.max(0,dash-dt);sense=Math.max(0,sense-dt);blk=Math.max(0,blk-dt);slow=Math.max(0,slow-dt);
const mon=role=='m',alive=st=='a';let moving=0;
if(alive){const f=(keys.KeyW?1:0)-(keys.KeyS?1:0),s=(keys.KeyD?1:0)-(keys.KeyA?1:0),l=Math.hypot(f,s)||1;let sp=mon?3.5:3.7;moving=f||s;
if(mon&&dash>0)sp=7;if(!mon){if(keys.ShiftLeft&&stam>0&&moving){sp=5.8;stam=Math.max(0,stam-22*dt)}else stam=Math.min(100,stam+14*dt)}if(slow>0)sp*=.5;
const q={x:px+(-Math.sin(yaw)*f+Math.cos(yaw)*s)/l*sp*dt*(moving?1:0),z:pz+(-Math.cos(yaw)*f-Math.sin(yaw)*s)/l*sp*dt*(moving?1:0)};col(q,.4);px=q.x;pz=q.z;bob+=moving?dt*8:0;
if(!mon&&keys.KeyE){const n=near();if(n&&n.k=='g'){rpT+=dt;if(rpT>.25){send({t:'rp',i:n.i,d:100/cfg.rep*rpT});rpT=0;beep(120+rnd()*60,.1,'square',.03)}}else rpT=0}else rpT=0;
if(!mon&&S.gate&&Math.hypot(px-GATE.x,pz-GATE.z)<2.2){st='e';toast('YOU ESCAPED!');beep(660,.8,'sine')}
if(mon)for(const o of others())if(o.pr.r!='m'&&o.pr.s=='a'&&Math.hypot(o.pr.x-px,o.pr.z-pz)<1.5)send({t:'ct',id:o.peer})}
$('sb').firstChild.style.width=stam+'%';
cam.position.set(px,(mon?1.9:1.6)+Math.sin(bob)*.04+(slow>0?Math.sin(tmr*40)*.04:0),pz);cam.rotation.set(pit,yaw,Math.sin(bob*.5)*.008);
const dark=blk>0&&!mon;fl.intensity=mon?0:dark?0:2.4;amb.intensity=mon?1.1:dark?.04:.55;sc.fog.density=dark?.22:mon?.05:.08;
bots.forEach(b=>botTick(b,dt));
const seen={};for(const o of others()){seen[o.peer]=1;const mn=o.pr.r=='m';let m=PM[o.peer];if(!m||m.userData.mon!=mn){if(m)sc.remove(m);m=PM[o.peer]=figure(mn,o.peer);m.position.set(o.pr.x,0,o.pr.z)}
const dx=o.pr.x-m.position.x,dz=o.pr.z-m.position.z,sp=Math.hypot(dx,dz);m.position.x+=dx*.35;m.position.z+=dz*.35;m.rotation.y=(o.pr.y||0)+Math.PI;m.visible=o.pr.s=='a';
const sw=Math.sin(tmr*10)*Math.min(1,sp*14)*.6,u=m.userData;u.ll.rotation.x=sw;u.rl.rotation.x=-sw;u.mk.visible=mon&&sense>0&&!mn}
for(const k in PM)if(!seen[k]){sc.remove(PM[k]);delete PM[k]}
if(R&&tmr-pt>.1){pt=tmr;{const pp={x:+px.toFixed(2),z:+pz.toFixed(2),y:+yaw.toFixed(2),r:role,s:st,v:1};if(isHost)pp.b=bots.map(b=>[b.id,+b.x.toFixed(1),+b.z.toFixed(1),+b.yaw.toFixed(2),b.r,b.s]);R.presence(pp)}}
const n=near();$('pr').textContent=!mon&&alive&&n?n.t:'';const h=objHTML();if($('obj').innerHTML!=h)$('obj').innerHTML=h;
gens.forEach(g=>{const w=g.p>0&&g.p<100,dn=g.p>=100,c=dn?0x44ff88:w?0xffc040:0xff3322;g.bar.scale.x=Math.max(.01,g.p/100);g.bar.material.color.setHex(c);g.beam.material.color.setHex(c);g.beam.material.opacity=dn?.1:.15+(w?Math.sin(tmr*8)*.05:0);g.pl.color.setHex(c);g.fan.rotation.z+=dt*(dn?14:w?6+g.p*.1:0);g.l.material.emissiveIntensity=.6+Math.sin(tmr*(w?10:3))*.4});
if(keyM&&!S.gk)keyM.position.y=Math.sin(tmr*2)*.08;
sign.material.opacity=1;if(S.gate){gate.position.y=Math.min(5.2,gate.position.y+dt*1.6)}
keyM&&(keyM.rotation.y+=dt*2);const dp=dust.geometry.attributes.position.array;for(let i=1;i<900;i+=3)dp[i]=((dp[i]+dt*.05+1.8)%3.6)-1.8;dust.geometry.attributes.position.needsUpdate=true;dust.position.x=px;dust.position.z=pz;
endCheck(dt)}
function endCheck(dt){endT+=dt;if(endT<1||S.end)return;endT=0;const sv=[];if(role=='s')sv.push(st);for(const o of others())if(o.pr.r!='m')sv.push(o.pr.s);
if(!sv.length||sv.includes('a'))return;S.end=1;mode='end';document.exitPointerLock&&document.exitPointerLock();const esc=sv.includes('e');
$('end').style.display='flex';$('et').textContent=esc?'SURVIVORS ESCAPED':'THE WARDEN WINS';$('et').style.color=esc?'#6fd49a':'#e23b3b';
$('es').textContent=role=='m'?(esc?'Some of them slipped through the gate.':'No one left alive.'):(st=='e'?'You made it out of Blackwood.':'You did not make it out.')}
requestAnimationFrame(frame);
</script></body></html>

