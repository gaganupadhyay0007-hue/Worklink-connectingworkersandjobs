# Worklink-connectingworkersandjobs
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WorkLinks Platform</title>

<style>
:root{--p:#6366f1;--d:#0f172a;--l:#f8fafc}
*{margin:0;padding:0;box-sizing:border-box;font-family:Segoe UI}
body{background:linear-gradient(120deg,#e0e7ff,#f8fafc);min-height:100vh}
nav{background:var(--d);color:white;padding:14px 28px;display:flex;justify-content:space-between;align-items:center}
nav button{background:none;border:none;color:white;margin-left:16px;font-weight:600;cursor:pointer}
nav button:hover{color:#60a5fa}

.container{max-width:1250px;margin:auto;padding:25px}
.hidden{display:none}

.card{background:white;padding:25px;border-radius:14px;box-shadow:0 10px 25px rgba(0,0,0,.1);margin-bottom:25px;animation:fade .5s}
@keyframes fade{from{opacity:0;transform:translateY(15px)}to{opacity:1}}

.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:20px}

input,textarea,select{width:100%;padding:12px;margin-top:10px;border-radius:8px;border:1px solid #d1d5db}

button.primary{background:var(--p);color:white;border:none;padding:12px;border-radius:8px;cursor:pointer;width:100%;margin-top:15px}
button.primary:hover{background:#4f46e5}

.job{background:#f9fafb;padding:16px;border-radius:10px;border-left:5px solid var(--p)}

.statgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:20px;margin-bottom:25px}

.stat{background:white;padding:20px;border-radius:12px;text-align:center;box-shadow:0 8px 18px rgba(0,0,0,.08)}
.stat h3{font-size:30px;color:var(--p)}

.panelgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:20px}

.panel{background:white;padding:20px;border-radius:12px;box-shadow:0 8px 18px rgba(0,0,0,.08);cursor:pointer;transition:.3s}
.panel:hover{transform:translateY(-4px);box-shadow:0 14px 25px rgba(0,0,0,.15)}

.panel h4{margin-bottom:6px;color:#111827}
.panel p{font-size:14px;color:#475569}

.sectiontitle{font-size:20px;margin-bottom:15px;color:#111827}

.hero{background:white;padding:40px;border-radius:16px;box-shadow:0 12px 28px rgba(0,0,0,.12);margin-bottom:30px;text-align:center}
.hero h1{font-size:38px;color:#111827;margin-bottom:10px}
.hero p{color:#475569;font-size:16px}

.featuregrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:20px}

.feature{background:white;padding:22px;border-radius:12px;box-shadow:0 8px 18px rgba(0,0,0,.08);text-align:center;transition:.3s}
.feature:hover{transform:translateY(-4px)}
.feature h4{margin-bottom:6px}

</style>
</head>

<body>

<nav>
<b>WorkLinks</b>
<div>
<button onclick="page('home')">Home</button>
<button onclick="page('jobs')">Jobs</button>
<button onclick="page('post')">Post</button>
<button onclick="page('dash')">Dashboard</button>
<button onclick="logout()">Logout</button>
</div>
</nav>

<div class="container">

<div id="login">
<div class="card">
<h2>Login</h2>
<input id="lu" placeholder="Username">
<input id="lp" type="password" placeholder="Password">
<button class="primary" onclick="login()">Login</button>
<p onclick="swap()" style="cursor:pointer;color:var(--p);margin-top:10px">Create account</p>
</div>
</div>

<div id="signup" class="hidden">
<div class="card">
<h2>Signup</h2>
<input id="su" placeholder="Username">
<input id="sp" type="password" placeholder="Password">
<select id="sr">
<option value="worker">Worker</option>
<option value="recruiter">Recruiter</option>
<option value="admin">Admin</option>
</select>
<button class="primary" onclick="signup()">Register</button>
<p onclick="swap()" style="cursor:pointer;color:var(--p);margin-top:10px">Back</p>
</div>
</div>

<div id="home" class="hidden">

<div class="hero">
<h1>Smart Hiring Platform</h1>
<p>Connecting workers with opportunities and recruiters with talent.</p>
</div>

<div class="sectiontitle">Platform Features</div>

<div class="featuregrid">

<div class="feature">
<h4>Job Discovery</h4>
<p>Search thousands of jobs across industries.</p>
</div>

<div class="feature">
<h4>Easy Hiring</h4>
<p>Recruiters can post and manage jobs instantly.</p>
</div>

<div class="feature">
<h4>Application Tracking</h4>
<p>Track job applications and progress in one place.</p>
</div>

<div class="feature">
<h4>Professional Dashboard</h4>
<p>View analytics, activity and platform insights.</p>
</div>

</div>

</div>

<div id="jobs" class="hidden">
<div class="card">
<input id="search" placeholder="Search jobs..." onkeyup="jobsView()">
<div id="joblist" class="grid" style="margin-top:20px"></div>
</div>
</div>

<div id="post" class="hidden">
<div class="card">
<h2>Post Job</h2>
<input id="jt" placeholder="Job Title">
<input id="jc" placeholder="Company">
<textarea id="jd" placeholder="Description"></textarea>
<button class="primary" onclick="post()">Publish</button>
</div>
</div>

<div id="dash" class="hidden">

<div class="statgrid">
<div class="stat"><h3 id="u"></h3><p>Total Users</p></div>
<div class="stat"><h3 id="j"></h3><p>Total Jobs</p></div>
<div class="stat"><h3 id="a"></h3><p>Applications</p></div>
</div>

<div class="sectiontitle">Dashboard Tools</div>

<div class="panelgrid">
<div class="panel" onclick="page('jobs')">
<h4>Browse Jobs</h4>
<p>Explore opportunities posted by recruiters.</p>
</div>

<div class="panel" onclick="page('post')">
<h4>Post Job</h4>
<p>Create job openings for candidates.</p>
</div>

<div class="panel">
<h4>Profile Center</h4>
<p>Manage your profile and account details.</p>
</div>

<div class="panel">
<h4>Application History</h4>
<p>Track submitted applications.</p>
</div>

<div class="panel">
<h4>Notifications</h4>
<p>Updates and alerts about jobs.</p>
</div>

<div class="panel">
<h4>Analytics</h4>
<p>Platform statistics and activity insights.</p>
</div>
</div>

<div class="card" style="margin-top:25px">
<h2>My Applications</h2>
<div id="apps"></div>
</div>

</div>

</div>

<script>

let users=JSON.parse(localStorage.getItem("users"))||[]
let jobs=JSON.parse(localStorage.getItem("jobs"))||[]
let appsData=JSON.parse(localStorage.getItem("apps"))||[]
let current=null

function page(id){
document.querySelectorAll(".container>div").forEach(d=>d.classList.add("hidden"))
document.getElementById(id).classList.remove("hidden")
}

function swap(){
login.classList.toggle("hidden")
signup.classList.toggle("hidden")
}

function signup(){
let u=su.value.trim()
let p=sp.value.trim()
let r=sr.value
if(!u||!p)return
if(users.find(x=>x.u==u))return
users.push({u,p,r})
localStorage.setItem("users",JSON.stringify(users))
swap()
}

function login(){
let u=lu.value.trim()
let p=lp.value.trim()
let f=users.find(x=>x.u==u&&x.p==p)
if(!f)return
current=f
page("home")
stats()
jobsView()
}

function logout(){location.reload()}

function post(){
if(!current||current.r!="admin"&&current.r!="recruiter")return
let t=jt.value.trim()
let c=jc.value.trim()
let d=jd.value.trim()
if(!t||!c||!d)return
let id=Date.now()
jobs.push({id,t,c,d})
localStorage.setItem("jobs",JSON.stringify(jobs))
jobsView()
stats()
}

function apply(id){
if(!current||current.r!="worker")return
appsData.push({id:Date.now(),job:id,user:current.u})
localStorage.setItem("apps",JSON.stringify(appsData))
stats()
}

function jobsView(){
let s=search?.value.toLowerCase()||""
joblist.innerHTML=""
jobs.filter(j=>j.t.toLowerCase().includes(s)||j.c.toLowerCase().includes(s)).forEach(j=>{
joblist.innerHTML+=`
<div class="job">
<h3>${j.t}</h3>
<p><b>${j.c}</b></p>
<p>${j.d}</p>
<button onclick="apply(${j.id})">Apply</button>
</div>`
})
}

function stats(){
u.innerText=users.length
j.innerText=jobs.length
a.innerText=appsData.length
apps.innerHTML=""
if(!current)return
appsData.filter(x=>x.user==current.u).forEach(a=>{
let jx=jobs.find(j=>j.id==a.job)
if(jx)apps.innerHTML+=`<div style="margin-top:8px">${jx.t}</div>`
})
}

</script>

</body>
</html>
