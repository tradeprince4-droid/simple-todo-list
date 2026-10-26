# simple-todo-list
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>To-Do List</title>
<style>
body{margin:0;background:#f1f5f9;color:#172033;font-family:Arial;padding:25px}
main{max-width:600px;margin:auto}
input{padding:13px;width:70%;box-sizing:border-box;border:1px solid #cbd5e1;border-radius:8px}
button{padding:12px;border:0;border-radius:8px;background:#4f46e5;color:white;cursor:pointer}
li{list-style:none;display:flex;gap:10px;align-items:center;justify-content:space-between;padding:13px;margin:10px 0;background:white;border-radius:9px;box-shadow:0 2px 7px #0000000a}
li span{overflow-wrap:anywhere}
.done{text-decoration:line-through;color:#94a3b8}
.delete{background:#dc3545}
</style>
</head>
<body>
<main>
<h1>✅ My Tasks</h1>
<p>Plan your day and finish what matters.</p>
<form id="form">
<input id="task" placeholder="Enter a task..." required>
<button>Add</button>
</form>
<p id="count">0 tasks remaining</p>
<ul id="list"></ul>
</main>
<script>
const $=id=>document.getElementById(id);
let tasks=JSON.parse(localStorage.todoTasks||"[]");
function render(){
$("list").innerHTML="";
tasks.forEach((t,i)=>{
const li=document.createElement("li");
const check=document.createElement("input");
check.type="checkbox";check.checked=t.done;
check.onchange=()=>{t.done=check.checked;render()};
const span=document.createElement("span");
span.textContent=t.text;
if(t.done)span.className="done";
const del=document.createElement("button");
del.textContent="Delete";del.className="delete";
del.onclick=()=>{tasks.splice(i,1);render()};
li.append(check,span,del);$("list").appendChild(li);
});
$("count").textContent=tasks.filter(t=>!t.done).length+" tasks remaining";
localStorage.todoTasks=JSON.stringify(tasks);
}
$("form").onsubmit=e=>{
e.preventDefault();
tasks.push({text:$("task").value,done:false});
$("task").value="";render();
};
render();
</script>
</body>
</html>
