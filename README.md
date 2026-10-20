# kaamkaro--demo-


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>KaamKaro - Local Help Network</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f5f7fb;color:#182033}
header{background:#155eef;color:white;padding:24px 6%;border-radius:0 0 22px 22px}
header h1{margin:0 0 8px}
main{max-width:850px;margin:24px auto;padding:0 16px}
nav{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:18px}
button{border:0;border-radius:9px;padding:12px 16px;cursor:pointer;font-weight:bold}
nav button,.primary{background:#155eef;color:white}
.card{background:white;border:1px solid #e1e6ef;border-radius:14px;padding:18px;margin:12px 0}
input,select{width:100%;padding:12px;margin:8px 0 16px;border:1px solid #ccd3df;border-radius:8px;font-size:16px}
.price{color:#087443;font-size:20px;font-weight:bold}
small{color:#626d80}
.hidden{display:none}
</style>
</head>
<body>
<header>
<h1>KaamKaro 🤝</h1>
<p>Local skills. Real opportunities. Better communities.</p>
</header>
<main>
<nav>
<button onclick="show('explore')">Explore tasks</button>
<button onclick="show('post')">Post a task</button>
<button onclick="show('earn')">Earn with skills</button>
</nav>

<section id="explore">
<h2>Find opportunities</h2>
<input id="search" placeholder="Search design, technology..."
oninput="render()">
<div id="tasks"></div>
</section>

<section id="post" class="hidden">
<h2>Post a task</h2>
<form id="taskForm">
<label>What help do you need?</label>
<input id="title" required maxlength="100"
placeholder="e.g. Design a shop poster">
<label>Category</label>
<select id="category">
<option>Design</option>
<option>Technology</option>
<option>Marketing</option>
<option>Other</option>
</select>
<label>Payment offered (₹)</label>
<input id="pay" type="number" min="0" max="1000000"
required placeholder="300">
<button class="primary">Publish task</button>
</form>
<p id="message"></p>
</section>

<section id="earn" class="hidden">
<h2>Turn your skills into opportunities</h2>
<div class="card">
<h3>🎨 Design</h3>
<p>Posters, logos and social media creatives.</p>
</div>
<div class="card">
<h3>💻 Technology</h3>
<p>Website setup and basic computer assistance.</p>
</div>
<div class="card">
<h3>📣 Marketing</h3>
<p>Help local shops reach more customers.</p>
</div>
<p><small>Sample ideas, not verified job offers or guaranteed earnings.</small></p>
</section>
</main>
<script>
let tasks=[
{id:1,title:"Design a shop poster",category:"Design",pay:300},
{id:2,title:"Help with computer setup",category:"Technology",pay:250},
{id:3,title:"Create social media posts",category:"Marketing",pay:500}
];

function show(id){
["explore","post","earn"].forEach(s=>{
document.getElementById(s).classList.toggle("hidden",s!==id);
});
}

function render(){
let q=document.getElementById("search").value.toLowerCase();
let list=tasks.filter(t=>(t.title+" "+t.category).toLowerCase().includes(q));
document.getElementById("tasks").innerHTML=list.map(t=>`
<div class="card">
<h3>${escapeHTML(t.title)}</h3>
<p>${escapeHTML(t.category)}</p>
<p class="price">₹${t.pay}</p>
<button onclick="interest(${t.id})">I'm interested</button>
</div>`).join("")||"<p>No tasks found.</p>";
}

function escapeHTML(s){
return String(s).replace(/[&<>"']/g,c=>({
"&":"&amp;","<":"&lt;",">":"&gt;",
'"':"&quot;","'":"&#39;"
}[c]));
}

function interest(id){
let task=tasks.find(t=>t.id===id);
alert("You selected: "+task.title+
". Real applications require user accounts and a backend.");
}

document.getElementById("taskForm").addEventListener("submit",e=>{
e.preventDefault();
let title=document.getElementById("title").value.trim();
let category=document.getElementById("category").value;
let pay=Number(document.getElementById("pay").value);
if(!title||!Number.isFinite(pay)||pay<0||pay>1000000)return;
tasks.unshift({id:Date.now(),title,category,pay});
document.getElementById("message").textContent=
"Task added to this demo!";
e.target.reset();
show("explore");
render();
});

render();
</script>
</body>
</html>
