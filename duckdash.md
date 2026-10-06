---
layout: page
title:
subtitle:
---

<style>

/* =========================
   WHOLE PAGE BACKGROUND
========================= */

html,
body,
.page-content,
.main-content,
.main,
.page,
.container,
.wrapper,
.content,
.site-content,
.page__content{
    background:#013220 !important;
}

/* =========================
   GAME WRAPPER
========================= */

.sim-wrapper{

    max-width:1200px;

    margin:20px auto;

    background:linear-gradient(
        180deg,
        #013220 0%,
        #024731 50%,
        #0b4f33 100%
    );

    padding:25px;

    border-radius:15px;

    border:4px solid #FEE123;

    box-shadow:
        0 0 25px rgba(254,225,35,.35);

}

/* =========================
   HEADER
========================= */

.sim-header{

    text-align:center;

    background:#FEE123;

    color:#024731;

    font-size:28px;

    font-weight:bold;

    padding:12px;

    border-radius:10px;

    margin-bottom:20px;

}

/* =========================
   TITLE
========================= */

.sim-title{

    text-align:center;

    color:#FEE123 !important;

    font-size:48px;

    font-weight:800;

    margin-bottom:20px;

}

/* =========================
   CARDS
========================= */

.sim-card{

    background:#0b5c39;

    color:white;

    padding:20px;

    border-radius:12px;

    margin-bottom:20px;

    border:1px solid rgba(254,225,35,.45);

}

/* Force all text white */

.sim-card,
.sim-card div,
.sim-card span,
.sim-card p,
.sim-card h2,
.sim-card h3{

    color:white !important;

}

/* =========================
   RESOURCE LABELS
========================= */

.stat-label{

    color:#FEE123 !important;

    font-weight:bold;

}

/* =========================
   RECRUIT NAME
========================= */

#recruit-name{
 
color:#FEE123 !important;
 
font-size:40px;
 
font-weight:800;
 
text-align:center;
 
line-height:1.3;
 
text-shadow:
0 0 10px rgba(254,225,35,.4);
 
}

/* =========================
   SCORE COLORS
========================= */

#oregon-score{

    color:#7CFC00 !important;

    font-weight:bold;

    font-size:1.1em;

}

#usc-score{

    color:#ff9999 !important;

    font-weight:bold;

}

#osu-score{

    color:#ffd0d0 !important;

    font-weight:bold;

}

#texas-score{

    color:#ffb07b !important;

    font-weight:bold;

}

/* =========================
   BUTTONS
========================= */

.sim-btn{

    background:#FEE123;

    color:#024731;

    border:none;

    padding:12px 16px;

    margin:5px;

    border-radius:8px;

    cursor:pointer;

    font-weight:bold;

    transition:.2s ease;

}

.sim-btn:hover{

    opacity:.9;

    transform:translateY(-1px);

}

/* =========================
   NEWS LOG
========================= */

#sim-log{

    background:#111;

    color:#ddd !important;

    padding:15px;

    border-radius:8px;

    height:250px;

    overflow-y:auto;

    border:1px solid #444;

}

/* =========================
   COMMITS
========================= */

.commit{

    color:#59ff59 !important;

    font-weight:bold;

    font-size:18px;

}

.loss{

    color:#ff7878 !important;

    font-weight:bold;

}

/* =========================
   SIGNING DAY
========================= */

#signing-day{

    background:#0b5c39;

}

</style>


<h1 class="sim-title">
🦆 FEBU Ducks Recruiting Simulator 🦆
</h1>
 
<div class="sim-wrapper">
 
<div class="sim-header">
🦆 SCO DUCKS 🦆
</div>
    
<div class="sim-card">

<span class="">💰 NIL:</span>
<span id="nil">100</span>

&nbsp;&nbsp;&nbsp;

<span class="">🏠 Coach Time:</span>
<span id="coach">20</span>

&nbsp;&nbsp;&nbsp;

<span class="">✈️ Visits:</span>
<span id="visits">6</span>

&nbsp;&nbsp;&nbsp;

<span class="stat-label">⭐ Commits:</span>
<span id="commit-count">0</span>/5
 
&nbsp;&nbsp;&nbsp;
 
<span class="stat-label">📅 Until Signing Day:</span>
<span id="recruits-left">30</span>
 
&nbsp;&nbsp;&nbsp;
 
<span class="stat-label">🎓 Scholarships:</span>
<span id="scholarships">5</span>

</div>

<div class="sim-card">

<div id="recruit-name">
Loading...
</div>

<br>

🦆 Oregon:
<span id="oregon-score"></span>

<br><br>

✌ USC:
<span id="usc-score"></span>

<br><br>

🌰 Ohio State:
<span id="osu-score"></span>

<br><br>

🤘 Texas:
<span id="texas-score"></span>

<br><br>

Actions Remaining:
<span id="actions"></span>

</div>

<div class="sim-card">

<button class="sim-btn" onclick="useAction('nike')">
👟 Nike Pitch
</button>

<button class="sim-btn" onclick="useAction('nil')">
💰 NIL Package
</button>

<button class="sim-btn" onclick="useAction('coach')">
🏠 Home Visit
</button>

<button class="sim-btn" onclick="useAction('visit')">
✈️ Official Visit
</button>

<button class="sim-btn" onclick="skipRecruit()">
⏭ Skip Recruit
</button>

</div>

<div class="sim-card">

<h3>Recruiting News</h3>

<div id="sim-log"></div>

</div>

<div id="signing-day" class="sim-card" style="display:none;"></div>

</div> <!-- closes sim-wrapper -->

<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>

<script>

const FIRST_NAMES = [
"Jayden","Bryce","Wyatt","Jordan","Cole","Caleb","Jackson","Ryan","Sir Gregory",
"Aiden","Dante","Cam","Micah","Kellz","J.J.","Doug","Jalen","Noah","Evan","Trey",
"Tyler","Connor","Mason","Jev","Granby","Dre","Niraj","Bo","Justin","Marcus","Sir Gregory",
"Derrick","Tanner","Dillon","Troy","Joey","Zayden","Malachi","Caden","Kaden","Deacon",
"Braylon","Xavier","Kingston","Jaxon","Ashton","Ryder","Nico","Isaiah","Landon","Kobe","Kellz","J.J.","Doug",
"Jace","Tatum","Cash","Maddox","Colton","Jev","Zeke","Braxton","Sawyer","Hudson","Roman","Granby","Dre","Niraj",
"Kamari","Trevon","Keon","Jabari","Desmond"
];

const LAST_NAMES = [
"Johnson","Brown","Smith","Rourke","Vaughn","Taylor","Wilson","Miller","Jackson","Harris",
"Williams","Carter","Morgan","Walker","Davis","Thomas","Moore","Anderson","White","Martin",
"Thompson","Clark","Lewis","Young","Allen","King","Scott","Green","Baker","Hall","Turner","Hayes",
"Robinson","Mitchell","Parker","Simmons","Evans","Ford","Reed","Bell","Murphy","Cooper",
"Powell","Perry","Bennett","Cook","Coleman","Henderson","Richardson","Jenkins","Brooks","Ward",
"Stewart","Sanders","Price","Woodson","Graham","Foster","Owens","Daniels","Fields","Manning",
"Prescott","Hunter","McCoy","Bishop","Hawkins","Pearson","Burton","Webb","Morris","Griffin",
"Black","Stokes","Banks","Sullivan","Maddox","West","Irving","Fleming","Holloway","Cross"
];

const LEGENDARY_NAMES = [
    "Mariota","Barner","Herbert","Ngata","Harrington","Howry","Ducksworth",
    "Belotti","Chung","Nix","Sewell","Wilcox","Mallard","Swoosh","Quackston","Autzenson"
];
   
const POSITIONS = [
"QB","RB","WR","TE","OT",
"EDGE","DL","LB","CB","S","ATH"
];

const INTERESTS = [
"nike",
"nil",
"coach",
"visit"
];

 const COMMIT_MESSAGES = [
"shut down recruitment and committed to Oregon!",
"cancelled all remaining visits!",
"picked the Ducks over the field!",
"is officially all in for Oregon!",
"called Dan Lanning with the good news!",
"ended the recruiting battle early!",
"committed on the spot!"
];  

let scholarships = 5;
let nilBudget = 100;
let coachTime = 20;
let visits = 6;

let recruits = [];
let currentRecruit = null;
let recruitIndex = 0;

let classScore = 0;
let signedPlayers = [];
let totalCommits = 0;

function log(text)
{
    let box=document.getElementById("sim-log");

    box.innerHTML += text+"<br>";

    box.scrollTop=box.scrollHeight;
}

function getStars()
{
    let roll=Math.random();

    if(roll<0.1) return 5;
    if(roll<0.4) return 4;

    return 3;
}

function generateRecruit()
{
    // 3% chance of a legendary Ducks recruit

    if(Math.random() < 0.03)
    {
        return {

    name:
        "⭐⭐⭐⭐⭐ " +
        POSITIONS[Math.floor(Math.random()*POSITIONS.length)] +
        " " +
        FIRST_NAMES[Math.floor(Math.random()*FIRST_NAMES.length)] +
        " " +
        LEGENDARY_NAMES[Math.floor(Math.random()*LEGENDARY_NAMES.length)],

    stars:5,

    legendary:true,

    likes:
        INTERESTS[
            Math.floor(Math.random()*INTERESTS.length)
        ],

    potential:"elite",

            oregon:55,
            usc:40,
            osu:40,
            texas:40,

            actions:3,

            usedNike:false,
            usedNIL:false,
            usedCoach:false,
            usedVisit:false

        };
    }

    let stars=getStars();

    let potentialPool=[
        "elite",
        "good",
        "average",
        "bust"
    ];

    return{

        name:
            "⭐".repeat(stars)+
            " "+
            POSITIONS[Math.floor(Math.random()*POSITIONS.length)]
            +" "+
            FIRST_NAMES[Math.floor(Math.random()*FIRST_NAMES.length)]
            +" "+
            LAST_NAMES[Math.floor(Math.random()*LAST_NAMES.length)],

        stars:stars,

        likes:
            INTERESTS[
                Math.floor(Math.random()*INTERESTS.length)
            ],

        potential:
            potentialPool[
                Math.floor(Math.random()*potentialPool.length)
            ],

        oregon:40+Math.floor(Math.random()*15),

        usc:40+Math.floor(Math.random()*15),

        osu:40+Math.floor(Math.random()*15),

        texas:40+Math.floor(Math.random()*15),

        actions:3,

        usedNike:false,
        usedNIL:false,
        usedCoach:false,
        usedVisit:false

    };
}

function updateResources()
{
    document.getElementById("nil").innerText =
        nilBudget;

    document.getElementById("coach").innerText =
        coachTime;

    document.getElementById("visits").innerText =
        visits;

    document.getElementById("scholarships").innerText =
        scholarships;

    document.getElementById("commit-count").innerText =
        totalCommits;

    document.getElementById("recruits-left").innerText =
        recruits.length - recruitIndex;
}

function updateRecruitDisplay()
{
    if(currentRecruit.legendary)
    {
        document.getElementById("recruit-name").innerHTML =
            "🔥 GENERATIONAL PROSPECT 🔥<br>" +
            currentRecruit.name;
    }
    else
    {
        document.getElementById("recruit-name").innerText =
            currentRecruit.name;
    }

    document.getElementById("oregon-score").innerText=
        currentRecruit.oregon;

    document.getElementById("usc-score").innerText=
        currentRecruit.usc;

    document.getElementById("osu-score").innerText=
        currentRecruit.osu;

    document.getElementById("texas-score").innerText=
        currentRecruit.texas;

    document.getElementById("actions").innerText=
        currentRecruit.actions;
}

function rivalRecruiting()
{
    currentRecruit.usc += random(8,18);
    currentRecruit.osu += random(8,18);
    currentRecruit.texas += random(8,18);
}

function random(min,max)
{
    return Math.floor(Math.random()*(max-min+1))+min;
}

function triggerEvent()
{
    if(Math.random()>.3)
        return;

    const events=[

    function(){
        currentRecruit.oregon+=10;
        log("🦆 Dan Lanning visited. +10 Oregon");
    },

    function(){
        currentRecruit.oregon+=25;
        log("💰 Phil Knight made a call. +25 Oregon");
    },

    function(){
        currentRecruit.usc+=15;
        log("✌ USC increased NIL. +15 USC");
    },

    function(){
        currentRecruit.osu+=15;
        log("🌰 Ohio State pushed hard. +15 Ohio State");
    },

    function(){
        currentRecruit.oregon+=15;
        log("🏟 Recruit loved Autzen at night. +15 Oregon");
    },

       function(){
currentRecruit.oregon -= 25;
log("🚨 JHop caught in Recruits sisters' DM's. -25 Oregon");
},
  
       function(){
currentRecruit.oregon -= 15;
log("🚨 Recruits Family took the bus with DuckZone503. -15 Oregon");
},
       
function(){
currentRecruit.oregon -= 15;
log("🌯 A mysterious burrito incident damaged relations. -15 Oregon");
},

    function(){
        currentRecruit.oregon-=10;
        log("😬 Recruit watched Oklahoma State tape. -10 Oregon");
    }

    ];

    events[Math.floor(Math.random()*events.length)]();
}

function useAction(type)
{
    if(currentRecruit.actions<=0)
        return;

    let gain=0;

    switch(type)
    {
        case "nike":

            if(currentRecruit.usedNike)
            {
                log("👟 Already used Nike pitch.");
                return;
            }

            currentRecruit.usedNike=true;

            gain=random(5,10);

            if(currentRecruit.likes==="nike")
                gain+=10;

        break;

        case "nil":

            if(currentRecruit.usedNIL)
            {
                log("💰 NIL already offered.");
                return;
            }

            if(nilBudget<20)
            {
                log("Out of NIL funds.");
                return;
            }

            nilBudget-=20;

            currentRecruit.usedNIL=true;

            gain=random(10,20);

            if(currentRecruit.likes==="nil")
                gain+=10;

        break;

        case "coach":

            if(currentRecruit.usedCoach)
            {
                log("🏠 Already visited.");
                return;
            }

            if(coachTime<2)
            {
                log("Out of coach time.");
                return;
            }

            coachTime-=2;

            currentRecruit.usedCoach=true;

            gain=random(10,20);

            if(currentRecruit.likes==="coach")
                gain+=10;

        break;

        case "visit":

            if(currentRecruit.usedVisit)
            {
                log("✈ Visit already used.");
                return;
            }

            if(visits<1)
            {
                log("Out of visits.");
                return;
            }

            visits--;

            currentRecruit.usedVisit=true;

            gain=random(10,20);

            if(currentRecruit.likes==="visit")
                gain+=12;

        break;
    }

currentRecruit.oregon += gain;

currentRecruit.actions--;

rivalRecruiting();

triggerEvent();

let rivalLeader = Math.max(
    currentRecruit.usc,
    currentRecruit.osu,
    currentRecruit.texas
);

if(currentRecruit.stars === 5)
{
    if(
        currentRecruit.oregon >= 155 &&
        currentRecruit.oregon >= rivalLeader + 10
    )
    {
        earlyCommit();
        return;
    }
}
else if(currentRecruit.stars === 4)
{
    if(
        currentRecruit.oregon >= 115 &&
        currentRecruit.oregon >= rivalLeader + 10
    )
    {
        earlyCommit();
        return;
    }
}
else
{
    if(
        currentRecruit.oregon >= 95 &&
        currentRecruit.oregon >= rivalLeader + 10
    )
    {
        earlyCommit();
        return;
    }
}

updateResources();
updateRecruitDisplay();

log("✅ Oregon gained +" + gain);

    if(currentRecruit.actions===0)
    {
        setTimeout(commitDecision,500);
    }
}
function earlyCommit()
{
    signedPlayers.push(currentRecruit);

    totalCommits++;

    scholarships--;

    if(currentRecruit.stars === 5)
        classScore += 100;
    else if(currentRecruit.stars === 4)
        classScore += 50;
    else
        classScore += 25;

 updateResources();

log(
    "📰 RECRUITING ALERT: " +
    currentRecruit.name +
    " has made a decision."
);

const message =
    COMMIT_MESSAGES[
        Math.floor(Math.random()*COMMIT_MESSAGES.length)
    ];

log(
    "<span class='commit'>🚨 EARLY COMMIT! " +
    currentRecruit.name +
    " " +
    message +
    "</span>"
);
   
    recruitIndex++;

    if(scholarships <= 0)
    {
        finishClass();
        return;
    }

    loadRecruit();
}
   
function commitDecision()
{
    let winner="Oregon";
    let score=currentRecruit.oregon;

    if(currentRecruit.usc>score)
    {
        winner="USC";
        score=currentRecruit.usc;
    }

    if(currentRecruit.osu>score)
    {
        winner="Ohio State";
        score=currentRecruit.osu;
    }

if(currentRecruit.texas > score)
{
    winner = "Texas";
    score = currentRecruit.texas;
}

    if(winner==="Oregon")
    {
        signedPlayers.push(currentRecruit);

totalCommits++;

scholarships--;

updateResources();

        if(currentRecruit.stars===5)
            classScore+=100;
        else if(currentRecruit.stars===4)
            classScore+=50;
        else
            classScore+=25;

        log(
            "<span class='commit'>✅ BOOM! "+
            currentRecruit.name+
            " committed to Oregon!</span>"
        );

        if(scholarships<=0)
        {
            finishClass();
            return;
        }
    }
   else
{
   if(currentRecruit.usedNIL)
{
let refund = random(10,20);
 
nilBudget += refund;
 
log(
"💰 NIL collective recovered $" +
refund +
"M from unused commitments."
);
}

    log(
        "<span class='loss'>❌ " +
        currentRecruit.name +
        " committed to " +
        winner +
        "</span>"
    );
}

    recruitIndex++;
   updateResources();
    loadRecruit();
}

function skipRecruit()
{
    log("⏭ Passed on " + currentRecruit.name);

    recruitIndex++;

    updateResources();

    loadRecruit();
}

function evaluateRecruit(r)
{
    if(r.legendary)
    {
        const legendaryOutcomes = [
            "🐐 Ducks Mount Rushmore",
            "🏆 National Champion",
            "🏆 Heisman Winner",
            "🏆 Program Legend",
            "🏆 Statue Outside Autzen",
            "🏆 Number Retired",
            "🏆 First Ballot Hall of Fame",
            "🏆 Greatest Duck Of His Era"
        ];

        return legendaryOutcomes[
            Math.floor(Math.random()*legendaryOutcomes.length)
        ];
    }

    if(r.potential === "elite")
    {
        const eliteOutcomes = [
            "🏆 All-American",
            "🏆 First Round Draft Pick",
            "🏆 Ducks Legend",
            "🏆 Heisman Finalist",
            "🏆 Ring of Honor",
            "🏆 NFL Pro Bowler",
            "🏆 School Record Holder",
            "🏆 Hall of Fame Candidate"
        ];

        return eliteOutcomes[
            Math.floor(Math.random()*eliteOutcomes.length)
        ];
    }

    if(r.potential === "good")
    {
        const goodOutcomes = [
            "✅ Team Captain",
            "✅ Multi-Year Starter",
            "✅ Fan Favorite",
            "✅ All-Conference Selection",
            "✅ Reliable Starter",
            "✅ Defensive Leader",
            "✅ Offensive Playmaker",
            "✅ Beloved by Duck Fans"
        ];

        return goodOutcomes[
            Math.floor(Math.random()*goodOutcomes.length)
        ];
    }

    if(r.potential === "average")
    {
        const averageOutcomes = [
            "👍 Valuable Depth Piece",
            "👍 Spot Starter",
            "👍 Quality Contributor",
            "👍 Special Teams Ace",
            "👍 Rotation Player",
            "👍 Reliable Backup",
            "👍 Practice Legend",
            "👍 Occasional Starter"
        ];

        return averageOutcomes[
            Math.floor(Math.random()*averageOutcomes.length)
        ];
    }

   if(
r.potential === "bust" &&
r.name.includes("J.J.")
)
{
return "🚪 Cut from the team due to uncontrollable weight gain";
}

if(
    r.potential === "bust" &&
    r.name.includes("Doug")
)
{
    return "🚪 Accidentally became a full-time golf influencer";
}
   
   if(
r.potential === "bust" &&
r.name.includes("Kellz")
)
{
return "🚪 Ran away with a Big Booty Latina and never reported to fall camp";
}
   
    const bustOutcomes = [
        "🚪 Entered Transfer Portal",
        "🚪 Left After Spring Game",
        "🚪 Buried On Depth Chart",
        "🚪 Justin Flowe's plus 1",
        "🚪 Dissappeared with Niraj's GF",
        "🚪 Injury Problems",
        "🚪 Transferred To A Rival",
        "🚪 Waiting on a Spanish Test",
        "🚪 Fell off a Scooter and missed Freshman year and transferred"
    ];

   return bustOutcomes[
Math.floor(Math.random()*bustOutcomes.length)
];

}

   function getNationalRanking()
{
    if(classScore >= 500) return "#1";
    if(classScore >= 450) return "#2";
    if(classScore >= 400) return "#3";
    if(classScore >= 350) return "#5";
    if(classScore >= 300) return "#8";
    if(classScore >= 250) return "#12";
    if(classScore >= 200) return "#18";
    if(classScore >= 150) return "#25";

    return "Unranked";
}


function getEnding()
{
    if(classScore>=500)
    {
        return `
        <h3>★★★★★ DYNASTY MODE ★★★★★</h3>
        Nick Saban called.<br>
        He wants recruiting advice.<br>
        Sco Ducks.
        `;
    }

    if(classScore>=400)
    {
        return `
        <h3>Grade: A+</h3>
        Phil Knight approved this class.<br>
        Washington fans are upset.
        `;
    }

    if(classScore>=250)
    {
        return `
        <h3>Grade: A</h3>
        Solid class.<br>
        Message boards remain calm.
        `;
    }

    if(classScore>=150)
    {
        return `
        <h3>Grade: C</h3>
        Transfer Portal Emergency.<br>
        Fans are evaluating JUCO tape.
        `;
    }

    return `
    <h3>Grade: F</h3>
    Congratulations.<br>
    You accidentally became Florida State.
    `;
}

function finishClass()
{
    document.getElementById("signing-day").style.display="block";

    let html="<h2>National Signing Day</h2>";

let finalCommits = totalCommits;

    html+="<ul>";

   // 5% chance Oregon lands a surprise Signing Day flip
   
if(Math.random() < 0.05)
{
    const isLegendary = Math.random() < 0.25;

    const flipRecruit = {
        name:
            "⭐⭐⭐⭐⭐ " +
            POSITIONS[Math.floor(Math.random()*POSITIONS.length)] +
            " " +
            FIRST_NAMES[Math.floor(Math.random()*FIRST_NAMES.length)] +
            " " +
            LAST_NAMES[Math.floor(Math.random()*LAST_NAMES.length)],

        stars: 5,
        potential: "elite",
        legendary: isLegendary,
        signingDayFlip: true
    };

    signedPlayers.push(flipRecruit);

    totalCommits++;

    if(isLegendary)
    {
        classScore += 150;
    }
    else
    {
        classScore += 100;
    }

    html +=
        "<li>🦆💣 SIGNING DAY SHOCKER! " +
        flipRecruit.name +
        " flipped to Oregon on Signing Day! " +
        "FEBU Discord called this and a burrito has mysteriously disappeared. 🌯</li>";
}
   
  signedPlayers.forEach(p =>
{
    let flipChance = 0.10;

    if(p.legendary)
    {
        flipChance = 0.03;
    }

   if(!p.signingDayFlip && Math.random() < flipChance)
    {
        const school =
            ["Texas","USC","Ohio State"][
                Math.floor(Math.random()*3)
            ];

        if(p.legendary)
        {
            classScore -= 150;
        }
        else if(p.stars === 5)
        {
            classScore -= 100;
        }
        else if(p.stars === 4)
        {
            classScore -= 50;
        }
        else
        {
            classScore -= 25;
        }

        finalCommits--;

        if(p.legendary)
        {
            html +=
                "<li>🚨💔 " +
                p.name +
                " SHOCKINGLY flipped to " +
                school +
                " on Signing Day!</li>";
        }
        else
        {
            html +=
                "<li>💔 " +
                p.name +
                " flipped to " +
                school +
                " on Signing Day!</li>";
        }
    }
    else
    {
        html +=
            "<li>" +
            p.name +
            " - " +
            evaluateRecruit(p) +
            "</li>";
    }
});

    html+="</ul>";

    html+="<h3>🏆 National Ranking: "+getNationalRanking()+"</h3>";

html+="<h3>⭐ Commits: "+finalCommits+"/5</h3>";

html+="<h3>Class Score: "+classScore+"</h3>";

    html+=getEnding();

   html+=`
<br><br>

<button class="sim-btn"
        onclick="saveClassImage()">
📸 Save Recruiting Class
</button>

<button class="sim-btn"
        onclick="location.reload()">
🔄 Start New Recruiting Class
</button>
`;

    document.getElementById("signing-day").innerHTML=
        html;
}

function loadRecruit()
{
    if(recruitIndex>=recruits.length)
    {
        finishClass();
        return;
    }

    currentRecruit=recruits[recruitIndex];

    updateRecruitDisplay();
}

   function saveClassImage()
{
    const card =
        document.getElementById("signing-day");

    html2canvas(card).then(canvas =>
    {
        const link =
            document.createElement("a");

        link.download =
            "febu-recruiting-class.png";

        link.href =
            canvas.toDataURL("image/png");

        link.click();
    });
}

for(let i=0;i<30;i++)
{
    recruits.push(generateRecruit());
}

updateResources();

loadRecruit();

log("🦆 Recruiting season has begun.");

</script>
