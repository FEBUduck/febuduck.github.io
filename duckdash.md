---
layout: page
title: 🦆 Duck Dash 🦆
subtitle: Fans first. Ducks always.
---

Recruiting Simulator
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>FEBU Ducks Recruiting Simulator</title>

<style>

/* ==========================
   PAGE
========================== */

body{
    background:#024731;
    color:white;
    font-family:Arial,sans-serif;
    max-width:1000px;
    margin:auto;
    padding:20px;
}

h1{
    color:#FEE123;
    text-align:center;
}

/* ==========================
   CARDS
========================== */

.card{
    background:#0d5d3f;
    padding:20px;
    border-radius:10px;
    margin-bottom:20px;
}

/* ==========================
   RESOURCES
========================== */

.resource{
    display:inline-block;
    margin-right:20px;
    font-weight:bold;
}

/* ==========================
   BUTTONS
========================== */

button{
    background:#FEE123;
    color:black;
    border:none;
    padding:10px 15px;
    margin:5px;
    border-radius:5px;
    cursor:pointer;
    font-weight:bold;
}

button:hover{
    opacity:.9;
}

/* ==========================
   RECRUIT CARD
========================== */

#recruit-name{
    color:#FEE123;
    font-size:28px;
    margin-bottom:10px;
}

.school-score{
    margin:5px 0;
}

/* ==========================
   LOG
========================== */

#log{
    background:#111;
    height:250px;
    overflow-y:auto;
    padding:10px;
    border-radius:5px;
}

/* ==========================
   SIGNING DAY
========================== */

#signing-day{
    display:none;
}

</style>
</head>
<body>

<h1>🦆 FEBU Ducks Recruiting Simulator</h1>

<!-- ==========================
     RESOURCES
========================== -->

<div class="card">

<div class="resource">
💰 NIL:
<span id="nil-budget">100</span>
</div>

<div class="resource">
🏠 Coach Time:
<span id="coach-time">20</span>
</div>

<div class="resource">
✈️ Visits:
<span id="visits">6</span>
</div>

<div class="resource">
🎓 Scholarships:
<span id="scholarships">5</span>
</div>

</div>

<!-- ==========================
     RECRUIT CARD
========================== -->

<div id="recruit-card" class="card">

<div id="recruit-name">
⭐⭐⭐⭐⭐ QB Example Recruit
</div>

<p>
Hidden Preference:
???
</p>

<div class="school-score">
🦆 Oregon:
<span id="oregon-score">50</span>
</div>

<div class="school-score">
✌ USC:
<span id="usc-score">45</span>
</div>

<div class="school-score">
🌰 Ohio State:
<span id="osu-score">42</span>
</div>

<br>

<div>
Actions Remaining:
<span id="actions">3</span>
</div>

</div>

<!-- ==========================
     ACTIONS
========================== -->

<div class="card">

<button id="nike-btn" onclick="nikePitch()">
👟 Nike Pitch
</button>

<button id="nil-btn">
💰 NIL Package
</button>

<button id="coach-btn">
🏠 Home Visit
</button>

<button id="visit-btn">
✈️ Official Visit
</button>

<button id="skip-btn" onclick="skipRecruit()">
⏭ Skip Recruit
</button>

</div>

<!-- ==========================
     LOG
========================== -->

<div class="card">

<h2>Recruiting News</h2>

<div id="log"></div>

</div>

<!-- ==========================
     SIGNING DAY
========================== -->

<div id="signing-day" class="card">

<h2>National Signing Day</h2>

<div id="signing-results"></div>

</div>

<script>

/* ==================================
   CONFIG
================================== */

const CONFIG = {

    SCHOLARSHIPS:5,

    NIL_BUDGET:100,

    COACH_TIME:20,

    VISITS:6,

    RECRUIT_POOL_SIZE:30

};

/* ==================================
   ARRAYS
================================== */

/* ==================================
   ARRAYS
================================== */

const FIRST_NAMES = [
    "Jayden","Bryce","Malik","Jordan",
    "Ty","Cooper","Jackson","Ryan",
    "Aiden","Dante","Cam","Micah"
];

c*nst LAST_NAMES = [
    "Johnson","Brown","Smith","Walker",
    "Davis","Taylor","Wilson","Miller",
    "Jackson","Harris"
];

const POSITIO*S = [
    "QB","RB","WR","TE","OT",
    "IOL","EDGE","DL","LB","CB","S"
];

const INTERESTS = [
    "nike",
    "nil",
    "coach",
    "visit"
];

/* ==================================
   GAME STATE
================================== */

let scholarships = CONFIG.SCHOLARSHIPS;

let nilBudget = CONFIG.NIL_BUDGET;

let coachTime = CONFIG.COACH_TIME;

let visits = CONFIG.VISITS;

let signedPlayers = [];

let currentRecruit = null;

let classScore = 0;

/* ================*=================
   RECRUIT GENER*TION
=============================*==== */

function getStars()
{
   *let roll = Math.random();

    if(*oll < 0.05) return 5;
    if*roll < 0.30)*return 4;

    return 3;
}

*unction generateRecruit()
{
    le* stars = get*tars();

    const potentials = [
*       "elite",
        "good",
  *     "average",
       *"bust"
    ];

    return {

     *  name:
            "⭐".repeat(sta*s) +
            "*" +
            POS*TIONS[Math.floor(Math.random() * P*SITIONS.length)] +
            " "*+
            FIRST_NAMES[Math.flo*r(Math.random() * FIRST_NAMES.leng*h)] +
            " " +
          * LAST_NAMES[Math.floor(Math.random*) * LAST_NAMES.length)],

        *tars: stars,

        likes:
     *      INTERESTS[Math.floor(Math.ra*dom() * INTERESTS.length)],

     *  potential:
            potential*[Math.floor(Math.random() * potent*als.length)],

        oregon: Mat*.floor(Math.random() * 20) + 40,

*       usc: Math*floor(Math.random() * *0) + 40,

        osu: Math.floor(*ath.random() * 20) + 40,

        *ctions: 3,

        usedNike: fals*,
        used*IL: false*
        usedCoach: false,
       *usedVisit: false

    };
}
/* ==================================
   UI FUNCTIONS
================================== */

function updateResources()
{
    document.getElementById("nil-budget").innerText =
        nilBudget;

    document.getElementById("coach-time").innerText =
        coachTime;

    document.getElementById("visits").innerText =
        visits;

    document.getElementById("scholarships").innerText =
        scholarships;
}

function updateRecruitDisplay()
{
    document.getElementById("recruit-name").innerText =
        currentRecruit.name;

    document.getElementById("oregon-score").innerText =
        currentRecruit.oregon;

    document.getElementById("usc-score").innerText =
        currentRecruit.usc;

    document.getElementById("osu-score").innerText =
        currentRecruit.osu;

    document.getElementById("actions").innerText =
        currentRecruit.actions;
}

function logMessage(message){

    const log =
        document.getElementById("log");

    log.innerHTML += message + "<br>";

    log.scrollTop =
        log.scrollHeight;
}

/* ==================================
   ACTIONS
================================== */

function nikePitch()
{
    if(currentRecruit.usedNike)
    {
        logMessage(
            "👟 You've already used the Nike pitch."
        );

        return;
    }

    currentRecruit.usedNike = true;

    let gain =
        Math.floor(Math.random() * 6) + 5;

    if(currentRecruit.likes === "nike")
    {
        gain += 15;

        logMessage(
            "🔥 Recruit loved the Nike pitch!"
        );
    }

    currentRecruit.oregon += gain;

    currentRecruit.actions--;

    updateRecruitDisplay();

    logMessage(
        "👟 Nike Pitch: +" +
        gain +
        " Oregon interest"
    );
}

function nilPitch(){

}

function homeVisit(){

}

function officialVisit(){

}

function skipRecruit()
{
    logMessage(
        "⏭ Passed on " +
        currentRecruit.name
    );

    recruitIndex++;

    loadRecruit();
}

/* ==================================
   RIVALS
================================== */

function rivalRecruiting(){

}

/* ==================================
   RANDOM EVENTS
================================== */

function randomEvent(){

}

/* ==================================
   COMMITMENT
================================== */

function finalizeRecruit(){

}

/* ==================================
   GEMS/BUSTS
================================== */

function evaluatePlayer(){

}

/* ==================================
   SIGNING DAY
================================== */

function finishClass(){

}

/* ==================================
   ENDINGS
================================== */

function getFunnyEnding(){

}

/* ==================================
   GAME FLOW
================================== */

function loadRecruit()
{
    if(recruitIndex >= recruits.length)
    {
        logMessage("No more recruits available.");
        return;
    }

    currentRecruit = recruits[recruitIndex];

    updateRecruitDisplay();
}

function startGame(){

    logMessage(
        "🦆 Welcome to FEBU Ducks Recruiting Simulator."
    );

    for(let i = 0; i < 30; i++)
    {
        recruits.push(generateRecruit());
    }

    updateResources();

    loadRecruit();

}

/* ==================================
   START GAME
================================== */

startGame();

</script>

</body>
</html>
