<!DOCTYPE html>
<html lang="sv">
<head>
<meta charset="UTF-8">
<title>🟢 Green Guy Survivor</title>

<style>
body{
background:#111;
color:white;
text-align:center;
font-family:Arial;
}

canvas{
background:#222;
border:3px solid white;
}
</style>

</head>
<body tabindex="0">

<h1>🟢 Green Guy Survivor</h1>

<p>
Mynt:
<span id="coins">0</span>

|

Liv:
<span id="lives">5</span>
</p>

<canvas
id="game"
width="1000"
height="600">
</canvas>

<script>

const canvas =
document.getElementById("game");

const ctx =
canvas.getContext("2d");

const keys = {};

document.addEventListener(
"keydown",
e=>{
keys[e.code]=true;
}
);

document.addEventListener(
"keyup",
e=>{
keys[e.code]=false;
}
);

const player={
x:500,
y:300,
size:20,
speed:5
};

let lives=5;
let coinCount=0;

const enemies=[];
const coins=[];

function rand(min,max){

return Math.random()*
(max-min)+min;

}

function dist(
x1,
y1,
x2,
y2
){

let dx=x1-x2;
let dy=y1-y2;

return Math.sqrt(
dx*dx+
dy*dy
);

}

function spawnCoin(){

coins.push({

x:rand(20,980),

y:rand(20,580)

});

}

for(
let i=0;
i<20;
i++
){

spawnCoin();

}

function spawnEnemy(){

let side=
Math.floor(
Math.random()*4
);

let x;
let y;

if(side===0){

x=Math.random()*1000;

y=-20;

}

if(side===1){

x=1020;

y=Math.random()*600;

}

if(side===2){

x=Math.random()*1000;

y=620;

}

if(side===3){

x=-20;

y=Math.random()*600;

}

enemies.push({

x:x,

y:y,

speed:2

});

}

for(
let i=0;
i<5;
i++
){

spawnEnemy();

}

setInterval(
spawnEnemy,
2000
);

function updatePlayer(){

if(
keys["ArrowUp"]
){

player.y-=
player.speed;

}

if(
keys["ArrowDown"]
){

player.y+=
player.speed;

}

if(
keys["ArrowLeft"]
){

player.x-=
player.speed;

}

if(
keys["ArrowRight"]
){

player.x+=
player.speed;

}

if(player.x<20)
player.x=20;

if(player.y<20)
player.y=20;

if(player.x>980)
player.x=980;

if(player.y>580)
player.y=580;

}

function updateCoins(){

for(
let i=
coins.length-1;
i>=0;
i--
){

if(

dist(

player.x,
player.y,

coins[i].x,
coins[i].y

)<25

){

coins.splice(i,1);

coinCount++;

document
.getElementById(
"coins"
)
.textContent=
coinCount;

spawnCoin();

}

}

}

function updateEnemies(){

for(
let i=
enemies.length-1;
i>=0;
i--
){

const e=
enemies[i];

let dx=
player.x-e.x;

let dy=
player.y-e.y;

let len=
Math.sqrt(
dx*dx+
dy*dy
);

if(len>0){

e.x+=
(dx/len)
*e.speed;

e.y+=
(dy/len)
*e.speed;

}

if(

dist(

player.x,
player.y,

e.x,
e.y

)<25

){

enemies.splice(i,1);

lives--;

document
.getElementById(
"lives"
)
.textContent=
lives;

if(
lives<=0
){

alert(
"💀 Game Over"
);

location.reload();

}

}

}

}

function draw(){

ctx.clearRect(
0,
0,
1000,
600
);

ctx.fillStyle=
"gold";

for(
const c
of coins
){

ctx.beginPath();

ctx.arc(
c.x,
c.y,
8,
0,
Math.PI*2
);

ctx.fill();

}

ctx.fillStyle=
"red";

for(
const e
of enemies
){

ctx.beginPath();

ctx.arc(
e.x,
e.y,
15,
0,
Math.PI*2
);

ctx.fill();

}

ctx.fillStyle=
"lime";

ctx.beginPath();

ctx.arc(
player.x,
player.y,
20,
0,
Math.PI*2
);

ctx.fill();

}

function gameLoop(){

updatePlayer();

updateCoins();

updateEnemies();

draw();

requestAnimationFrame(
gameLoop
);

}

gameLoop();

</script>

</body>
</html>const enemies=[];
const coins=[];const swords=[];function addSword(){

swords.push({

angle:
Math.random()
*
Math.PI
*
2,

distance:
60+
(
swords.length
*
20
),

speed:
0.05

});

}function showUpgrade(){

let choice=

prompt(

`UPPGRADERING

1 = Svärd

2 = +1 Liv

3 = Snabbare Gubbe`

);

if(
choice==="1"
){

addSword();

}

if(
choice==="2"
){

lives++;

document
.getElementById(
"lives"
)
.textContent=
lives;

}

if(
choice==="3"
){

player.speed++;

}

}spawnCoin();if(
coinCount
%
5
===
0
){

showUpgrade();

}function updateSwords(){

for(
let sword
of swords
){

sword.angle +=
sword.speed;

sword.x =

player.x +

Math.cos(
sword.angle
)

*

sword.distance;

sword.y =

player.y +

Math.sin(
sword.angle
)

*

sword.distance;

for(

let i=
enemies.length-1;

i>=0;

i--

){

if(

dist(

sword.x,
sword.y,

enemies[i].x,
enemies[i].y

)

<25

){

enemies.splice(
i,
1
);

}

}

}

}ctx.fillStyle=
"cyan";

for(
const sword
of swords
){

ctx.beginPath();

ctx.arc(

sword.x,

sword.y,

10,

0,

Math.PI*2

);

ctx.fill();

}updateEnemies();

draw();updateEnemies();

updateSwords();

draw();setInterval(
spawnEnemy,
2000
);let enemyRate=
2000;

setInterval(()=>{

spawnEnemy();

},enemyRate);

setInterval(()=>{

spawnEnemy();

spawnEnemy();

},10000);const upgrades = [

"Svärd",
"Eldboll",
"Blixt",
"Boomerang",
"Laser",
"Isring",
"Yxa",
"Hammare",
"Bomb",
"Meteor",

"Gift",
"Stjärna",
"Kristall",
"Drake",
"Spöke",
"Bin",
"Taggar",
"Magnet",
"Pilregn",
"Solstråle",

"Månblad",
"Lava",
"Vattenvåg",
"Kugghjul",
"Virvel",
"Raketer",
"Plasma",
"Orb",
"MiniBoss",
"Tur"

];

const ownedWeapons = {};function showUpgrade(){

let a =
upgrades[
Math.floor(
Math.random()
*
upgrades.length
)
];

let b =
upgrades[
Math.floor(
Math.random()
*
upgrades.length
)
];

let c =
upgrades[
Math.floor(
Math.random()
*
upgrades.length
)
];

let choice = prompt(

`UPPGRADERING

1 = ${a}

2 = ${b}

3 = ${c}

4 = Uppgradera befintligt vapen`

);

if(choice==="1"){

giveUpgrade(a);

}

if(choice==="2"){

giveUpgrade(b);

}

if(choice==="3"){

giveUpgrade(c);

}

if(choice==="4"){

upgradeExisting();

}

}function giveUpgrade(name){

if(
ownedWeapons[name]
==
undefined
){

ownedWeapons[name]=1;

}
else{

ownedWeapons[name]++;

}

if(
name==="Svärd"
){

addSword();

}

if(
name==="Tur"
){

coinCount+=5;

}

}function upgradeExisting(){

let text =
"Välj vapen:\n\n";

let list =
Object.keys(
ownedWeapons
);

for(
let i=0;
i<list.length;
i++
){

text +=

(i+1)

+

" = "

+

list[i]

+

" nivå "

+

ownedWeapons[
list[i]
]

+

"\n";

}

let choice =
prompt(text);

let index =
parseInt(choice)-1;

if(
list[index]
){

ownedWeapons[
list[index]
]++;

alert(

list[index]

+

" är nu nivå "

+

ownedWeapons[
list[index]
]

);

}

}if(

dist(

sword.x,
sword.y,

enemies[i].x,
enemies[i].y

)

<

25 +

(
ownedWeapons[
"Svärd"
]||0
)

*2

){

enemies.splice(
i,
1
);

}const fireballs = [];
const boomerangs = [];
const lightning = [];function shootFireball(){

if(
!ownedWeapons["Eldboll"]
)
return;

let nearest = null;
let nearestDist = 999999;

for(
let enemy
of enemies
){

let d = dist(
player.x,
player.y,
enemy.x,
enemy.y
);

if(
d < nearestDist
){

nearestDist = d;
nearest = enemy;

}

}

if(!nearest)
return;

let dx =
nearest.x-player.x;

let dy =
nearest.y-player.y;

let len =
Math.sqrt(
dx*dx+
dy*dy
);

fireballs.push({

x:player.x,
y:player.y,

vx:
(dx/len)*6,

vy:
(dy/len)*6

});

}setInterval(()=>{

shootFireball();

},1000);function updateFireballs(){

for(
let i=
fireballs.length-1;
i>=0;
i--
){

let f =
fireballs[i];

f.x += f.vx;
f.y += f.vy;

for(
let j=
enemies.length-1;
j>=0;
j--
){

if(

dist(

f.x,
f.y,

enemies[j].x,
enemies[j].y

)

<20

){

enemies.splice(
j,
1
);

fireballs.splice(
i,
1
);

break;

}

}

}

}function spawnBoomerang(){

if(
!ownedWeapons[
"Boomerang"
]
)
return;

boomerangs.push({

angle:0,
distance:0

});

}function updateBoomerangs(){

for(
let b
of boomerangs
){

b.angle += 0.1;

b.distance += 2;

b.x =

player.x +

Math.cos(
b.angle
)

*

b.distance;

b.y =

player.y +

Math.sin(
b.angle
)

*

b.distance;

for(
let i=
enemies.length-1;
i>=0;
i--
){

if(

dist(

b.x,
b.y,

enemies[i].x,
enemies[i].y

)

<25

){

enemies.splice(
i,
1
);

}

}

}

}function lightningStrike(){

if(
!ownedWeapons[
"Blixt"
]
)
return;

if(
enemies.length===0
)
return;

let enemy =

enemies[
Math.floor(
Math.random()
*
enemies.length
)
];

lightning.push({

x:enemy.x,
y:enemy.y,

timer:20

});

}setInterval(()=>{

lightningStrike();

},2000);function updateLightning(){

for(
let i=
lightning.length-1;
i>=0;
i--
){

lightning[i].timer--;

for(
let j=
enemies.length-1;
j>=0;
j--
){

if(

dist(

lightning[i].x,
lightning[i].y,

enemies[j].x,
enemies[j].y

)

<50

){

enemies.splice(
j,
1
);

}

}

if(
lightning[i].timer
<=0
){

lightning.splice(
i,
1
);

}

}

}ctx.fillStyle=
"orange";

for(
let f
of fireballs
){

ctx.beginPath();

ctx.arc(
f.x,
f.y,
6,
0,
Math.PI*2
);

ctx.fill();

}
ctx.fillStyle=
"yellow";

for(
let b
of boomerangs
){

ctx.beginPath();

ctx.arc(
b.x,
b.y,
8,
0,
Math.PI*2
);

ctx.fill();

}ctx.strokeStyle=
"cyan";

for(
let l
of lightning
){

ctx.beginPath();

ctx.moveTo(
l.x,
0
);

ctx.lineTo(
l.x,
l.y
);

ctx.stroke();

}updateFireballs();

updateBoomerangs();

updateLightning();const bosses = [];if(
coinCount % 50 === 0
){

spawnBoss();

}function spawnBoss(){

bosses.push({

x:500,

y:-100,

hp:100,

speed:1,

size:50

});

}function updateBosses(){

for(
let i=
bosses.length-1;
i>=0;
i--
){

let b=
bosses[i];

let dx=
player.x-b.x;

let dy=
player.y-b.y;

let len=
Math.sqrt(
dx*dx+
dy*dy
);

if(len>0){

b.x +=
(dx/len)
*
b.speed;

b.y +=
(dy/len)
*
b.speed;

}

if(

dist(

player.x,
player.y,

b.x,
b.y

)

<50

){

lives--;

document
.getElementById(
"lives"
)
.textContent=
lives;

}

}

}const dragons = [];function summonDragon(){

dragons.push({

angle:0,

distance:150

});

}if(
name==="Drake"
){

summonDragon();

}function updateDragons(){

for(
let d
of dragons
){

d.angle +=
0.02;

d.x =

player.x +

Math.cos(
d.angle
)

*
d.distance;

d.y =

player.y +

Math.sin(
d.angle
)

*
d.distance;

for(
let i=
enemies.length-1;
i>=0;
i--
){

if(

dist(

d.x,
d.y,

enemies[i].x,
enemies[i].y

)

<40

){

enemies.splice(
i,
1
);

}

}

}

}function meteorStorm(){

for(
let i=0;
i<10;
i++
){

setTimeout(()=>{

let x=
Math.random()
*
1000;

let y=
Math.random()
*
600;

for(
let j=
enemies.length-1;
j>=0;
j--
){

if(

dist(

x,
y,

enemies[j].x,
enemies[j].y

)

<100

){

enemies.splice(
j,
1
);

}

}

},i*300);

}

}if(
name==="Meteor"
){

meteorStorm();

}let highscore =

localStorage.getItem(
"ggs_highscore"
);

if(
!highscore
){

highscore=0;

}if(
coinCount >
highscore
){

localStorage.setItem(
"ggs_highscore",
coinCount
);

}<p>
Highscore:
<span id="highscore"></span>
</p>document
.getElementById(
"highscore"
)
.textContent=
highscore;"Legend"if(
name==="Legend"
){

player.speed += 3;

lives += 10;

for(
let i=0;
i<5;
i++
){

addSword();

}

}updateBosses();

updateDragons();
