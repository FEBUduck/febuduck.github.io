---
layout: page
title: 🦆 Duck Dash 🦆
subtitle: Fans first. Ducks always.
---

Recruiting Simulator
<html>
<head>
<meta charset="UTF-8">
<title>FEBU Ducks Recruiting Simulator</title>

<style>

body{
    background:#024731;
    color:white;
    font-family:Arial, sans-serif;
    max-width:900px;
    margin:auto;
    padding:20px;
}

h1{
    color:#FEE123;
}

.card{
    background:#0d5d3f;
    padding:20px;
    margin-top:15px;
    border-radius:10px;
}

button{
    background:#FEE123;
    color:black;
    border:none;
    margin:5px;
    padding:10px 15px;
    font-weight:bold;
    cursor:pointer;
    border-radius:5px;
}

button:disabled{
    opacity:.4;
    cursor:not-allowed;
}

#log{
    background:#111;
    padding:10px;
    height:250px;
    overflow-y:auto;
    border-radius:10px;
}

.commit{
    color:#66ff66;
}

.loss{
    color:#ff6666;
}

.stat{
    margin-right:20px;
    display:inline-block;
    font-weight:bold;
}

</style>
</head>

<body>

<h1>🦆 FEBU Ducks Recruiting Simulator</h1>

<div class="card">

<span class="stat">💰 NIL: <span id="nil">100</span></span>
<span class="stat">🏠 Coach Time: <span id="coach">20</span></span>
<span class="stat">✈️ Visits: <span id="visit">6</span></span>

</div>

<div class="card">

<h2 id="name"></h2>

<div>
<strong>Oregon:</strong>
<span id="oregonScore"></span>
</div>

<div>
<strong>USC:</strong>
<span id="uscScore"></span>
</div>

<div>
<strong>Ohio State:</strong>
<span id="osuScore"></span>
</div>

<br>

<div>
<strong>Actions Remaining:</strong>
<span id="actions"></span>
</div>

<br>

<button id="nikeBtn" onclick="useAction('nike')">
👟 Nike Pitch
</button>

<button id="nilBtn" onclick="useAction('nil')">
💰 NIL Package
</button>

<button id="coachBtn" onclick="useAction('coach')">
🏠 Home Visit
</button>

<button id="visitBtn" onclick="useAction('visit')">
✈️ Official Visit
</button>

</div>

<div class="card">
<h3>Recruiting News</h3>
<div id="log"></div>
</div>

<script>

const recruits = [

{
name:"⭐⭐⭐⭐⭐ QB Throwin Mahomes",
likes:"nil"
},

{
name:"⭐⭐⭐⭐⭐ EDGE Sack Barmstrong",
likes:"coach"
},

{
name:"⭐⭐⭐⭐⭐ WR Fast McSpeed",
likes:"visit"
},

{
name:"⭐⭐⭐⭐ OT Pancake Johnson",
likes:"coach"
},

{
name:"⭐⭐⭐⭐⭐ CB Lockdown Lewis",
likes:"nike"
},

{
name:"⭐⭐⭐⭐ RB Truck Stick",
likes:"nil"
},

{
name:"⭐⭐⭐⭐⭐ LB Boom Johnson",
likes:"coach"
},

{
name:"⭐⭐⭐⭐ WR Route Runner Rick",
likes:"visit"
},

{
name:"⭐⭐⭐⭐⭐ ATH Autzen Legend",
likes:"nil"
},

{
name:"⭐⭐⭐⭐ DT Big Chungus Jr",
likes:"coach"
}

];

let index = 0;

let nilBudget = 100;
let coachTime = 20;
let visits = 6;

let commits = [];
let classScore = 0;

let recruit;

function random(min,max){
return Math.floor(Math.random()*(max-min+1))+min;
}

function log(text){

const div = document.getElementById("log");

div.innerHTML += text + "<br>";

div.scrollTop = div.scrollHeight;

}

function updateResources(){

document.getElementById("nil").textContent=nilBudget;
document.getElementById("coach").textContent=coachTime;
document.getElementById("visit").textContent=visits;

}

function loadRecruit(){

if(index >= recruits.length){

finishClass();
return;

}

recruit = {

...recruits[index],

oregon:random(35,55),
usc:random(35,55),
osu:random(35,55),

actions:3,

usedNike:false,
usedNIL:false,
usedCoach:false,
usedVisit:false

};

updateRecruitDisplay();

}

function updateRecruitDisplay(){

document.getElementById("name").innerText=recruit.name;

document.getElementById("oregonScore").innerText=recruit.oregon;
document.getElementById("uscScore").innerText=recruit.usc;
document.getElementById("osuScore").innerText=recruit.osu;

document.getElementById("actions").innerText=recruit.actions;

}

function runRivals(){

recruit.usc += random(2,8);
recruit.osu += random(2,8);

}

function randomEvent(){

if(Math.random() > .25)
return;

const event = random(1,5);

switch(event){

case 1:
recruit.oregon += 10;
log("🦆 Recruit watched Oregon beat USC. +10 Oregon");
break;

case 2:
recruit.osu += 12;
log("🌰 Ohio State sweetened its NIL offer. +12 Ohio State");
break;

case 3:
recruit.oregon += 8;
log("🏟️ Recruit loved Autzen Stadium clips. +8 Oregon");
break;

case 4:
recruit.usc += 10;
log("✌️ USC hosted recruit on campus. +10 USC");
break;

case 5:
recruit.oregon -= 6;
log("😬 Recruit rewatched Oklahoma State highlights. -6 Oregon");
break;

}

}

function useAction(type){

if(recruit.actions <= 0)
return;

let gain = 0;

switch(type){

case "nike":

if(recruit.usedNike){
log("You've already used the Nike pitch.");
return;
}

recruit.usedNike=true;

gain=random(5,10);

if(recruit.likes==="nike")
gain+=15;

log("👟 Nike pitch. +" + gain);
break;

case "nil":

if(recruit.usedNIL){
log("You've already used NIL.");
return;
}

if(nilBudget < 20){

log("Not enough NIL funds.");
return;

}

nilBudget -= 20;

recruit.usedNIL=true;

gain=random(10,20);

if(recruit.likes==="nil")
gain+=20;

log("💰 NIL package. +" + gain);
break;

case "coach":

if(recruit.usedCoach){
log("You've already used a home visit.");
return;
}

if(coachTime < 2){

log("No coach time remaining.");
return;

}

coachTime -= 2;

recruit.usedCoach=true;

gain=random(10,20);

if(recruit.likes==="coach")
gain+=20;

log("🏠 Dan Lanning visit. +" + gain);
break;

case "visit":

if(recruit.usedVisit){
log("Official visit already used.");
return;
}

if(visits < 1){

log("No visits remaining.");
return;

}

visits--;

recruit.usedVisit=true;

gain=random(10,20);

if(recruit.likes==="visit")
gain+=20;

log("✈️ Official visit. +" + gain);
break;

}

recruit.oregon += gain;

runRivals();

randomEvent();

recruit.actions--;

updateResources();
updateRecruitDisplay();

if(recruit.actions === 0){

setTimeout(commitDecision,800);

}

}

function commitDecision(){

let winner="Oregon";
let score=recruit.oregon;

if(recruit.usc > score){

winner="USC";
score=recruit.usc;

}

if(recruit.osu > score){

winner="Ohio State";
score=recruit.osu;

}

if(winner==="Oregon"){

commits.push(recruit.name);

let stars = (recruit.name.match(/⭐/g)||[]).length;

classScore += stars * 10;

log(
"<span class='commit'>✅ BOOM! "
+
recruit.name +
" committed to Oregon!</span>"
);

}else{

log(
"<span class='loss'>❌ "
+
recruit.name +
" committed to "
+
winner +
"</span>"
);

}

index++;

setTimeout(loadRecruit,1500);

}

function finishClass(){

document.body.innerHTML +=
`
<div class="card">

<h2>National Signing Day</h2>

<p><strong>Commits:</strong> ${commits.length}</p>

<p><strong>Class Score:</strong> ${classScore}</p>

<p><strong>National Ranking:</strong> ${rankClass()}</p>

<button onclick="location.reload()">
Start New Class
</button>

</div>
`;

}

function rankClass(){

if(classScore >= 350)
return "#1 Class - Dynasty Mode";

if(classScore >= 250)
return "Top 5 Class";

if(classScore >= 180)
return "Top 10 Class";

if(classScore >= 120)
return "Top 25 Class";

return "Transfer Portal Time";

}

updateResources();
loadRecruit();

</script>

</body>
</html>
