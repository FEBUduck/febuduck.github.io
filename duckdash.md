---
layout: page
title: 🦆 Duck Dash 🦆
subtitle: Fans first. Ducks always.
---

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Oregon Recruiting Simulator</title>

<style>
body{
    background:#024731;
    color:white;
    font-family:Arial,sans-serif;
    margin:0;
    padding:20px;
}

.container{
    max-width:900px;
    margin:auto;
}

.card{
    background:#0b5e3c;
    padding:20px;
    border-radius:10px;
    margin-bottom:20px;
}

button{
    padding:12px;
    margin:5px;
    border:none;
    border-radius:5px;
    cursor:pointer;
    font-weight:bold;
    background:#f5c842;
}

button:hover{
    opacity:.9;
}

#log{
    height:250px;
    overflow-y:auto;
    background:#111;
    padding:10px;
    border-radius:10px;
}

h1{
    color:#f5c842;
}

.stat{
    display:inline-block;
    margin-right:20px;
    font-weight:bold;
}

.recruit-name{
    font-size:28px;
    color:#f5c842;
}

.commit{
    color:lime;
}

.loss{
    color:red;
}
</style>
</head>

<body>

<div class="container">

<h1>🦆 Oregon Recruiting Simulator</h1>

<div class="card">

<div class="stat">💰 NIL Budget: <span id="nil">100</span></div>
<div class="stat">🏠 Coach Visits: <span id="coach">20</span></div>
<div class="stat">✈️ Official Visits: <span id="visit">5</span></div>

</div>

<div class="card">

<div class="recruit-name" id="name"></div>

<p id="details"></p>

<p>
Interest Level:
<b><span id="interest"></span>%</b>
</p>

<div id="buttons">
<button onclick="pitchNike()">Nike Pitch</button>
<button onclick="pitchNIL()">NIL Package</button>
<button onclick="coachVisit()">Home Visit</button>
<button onclick="officialVisit()">Official Visit</button>
<button onclick="advanceRecruit()">Move To Next Recruit</button>
</div>

</div>

<div class="card">
<h2>Recruiting News</h2>
<div id="log"></div>
</div>

</div>

<script>

let recruits = [
{
name:"⭐⭐⭐⭐⭐ QB Throwin Mahomes",
likes:"NIL",
interest:50
},
{
name:"⭐⭐⭐⭐⭐ DL Sack Barmstrong",
likes:"Coach",
interest:45
},
{
name:"⭐⭐⭐⭐⭐ WR Fast McSpeed",
likes:"Visit",
interest:55
},
{
name:"⭐⭐⭐⭐ OT Pancake Johnson",
likes:"Coach",
interest:50
},
{
name:"⭐⭐⭐⭐⭐ CB Lockdown Lewis",
likes:"Visit",
interest:48
},
{
name:"⭐⭐⭐⭐ RB Truck Stick",
likes:"NIL",
interest:52
},
{
name:"⭐⭐⭐⭐⭐ LB Boom Tagovailoa",
likes:"Coach",
interest:47
},
{
name:"⭐⭐⭐⭐ WR Touchdown Tommy",
likes:"Visit",
interest:54
},
{
name:"⭐⭐⭐⭐ Edge Bryce Smash",
likes:"Coach",
interest:50
},
{
name:"⭐⭐⭐⭐⭐ ATH Autzen Legend",
likes:"NIL",
interest:40
}
];

let current = 0;

let signed = [];
let classPoints = 0;

let nilBudget = 100;
let coachTime = 20;
let visits = 5;

function updateResources()
{
document.getElementById("nil").innerText=nilBudget;
document.getElementById("coach").innerText=coachTime;
document.getElementById("visit").innerText=visits;
}

function random(min,max)
{
return Math.floor(Math.random()*(max-min+1))+min;
}

function log(text)
{
const div=document.getElementById("log");
div.innerHTML += text+"<br>";
div.scrollTop=div.scrollHeight;
}

function loadRecruit()
{
if(current>=recruits.length)
{
finishClass();
return;
}

let r=recruits[current];

document.getElementById("name").innerText=r.name;

document.getElementById("details").innerHTML=
"Competition: USC, Ohio State, Texas";

document.getElementById("interest").innerText=r.interest;
}

function addInterest(amount)
{
recruits[current].interest += amount;

if(recruits[current].interest>100)
recruits[current].interest=100;

document.getElementById("interest").innerText=
recruits[current].interest;
}

function pitchNike()
{
let gain=random(4,10);

if(recruits[current].likes==="Visit")
gain-=2;

addInterest(gain);

log("👟 Nike pitch worked. Interest +" + gain);
}

function pitchNIL()
{
if(nilBudget<20)
{
log("💰 Not enough NIL money.");
return;
}

nilBudget-=20;

let gain=random(15,30);

if(recruits[current].likes==="NIL")
gain+=10;

addInterest(gain);

updateResources();

log("💰 NIL package offered. Interest +" + gain);
}

function coachVisit()
{
if(coachTime<2)
{
log("🏠 No coach visits remaining.");
return;
}

coachTime-=2;

let gain=random(10,20);

if(recruits[current].likes==="Coach")
gain+=10;

addInterest(gain);

updateResources();

log("🏠 Dan Lanning home visit. Interest +" + gain);
}

function officialVisit()
{
if(visits<1)
{
log("✈️ No visits remaining.");
return;
}

visits--;

let gain=random(12,25);

if(recruits[current].likes==="Visit")
gain+=10;

addInterest(gain);

updateResources();

log("✈️ Recruit visits Autzen Stadium. Interest +" + gain);
}

function advanceRecruit()
{
let r=recruits[current];

let roll=random(1,100);

if(r.interest>=roll)
{
signed.push(r.name);

let stars=(r.name.match(/⭐/g)||[]).length;

classPoints+=stars;

log(
"<span class='commit'>✅ BOOM! "
+ r.name +
" committed to Oregon.</span>"
);
}
else
{
let rivals=[
"USC",
"Ohio State",
"Texas",
"Washington"
];

let rival=
rivals[random(0,rivals.length-1)];

log(
"<span class='loss'>❌ "
+ r.name +
" committed to "
+ rival +
"</span>"
);
}

current++;

setTimeout(loadRecruit,400);
}

function finishClass()
{
document.getElementById("buttons").style.display="none";

let ranking;

if(classPoints>=40)
ranking="#1 Class - Dynasty Mode";
else if(classPoints>=35)
ranking="Top 3 Class";
else if(classPoints>=30)
ranking="Top 10 Class";
else if(classPoints>=20)
ranking="Solid Class";
else
ranking="Time to Fire Up the Transfer Portal";

document.querySelector(".card").innerHTML=
`
<h2>National Signing Day</h2>

<p><b>Signed:</b> ${signed.length} recruits</p>

<p><b>Class Score:</b> ${classPoints}</p>

<p><b>Result:</b> ${ranking}</p>

<button onclick="location.reload()">
Start New Class
</button>
`;

log("📣 Recruiting cycle complete.");
}

updateResources();
loadRecruit();

</script>

</body>
</html>
