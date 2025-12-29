<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Life in The Go</title>

<style>
*{box-sizing:border-box;}
body{
  margin:0;
  font-family: 'Segoe UI',sans-serif;
  color:white;
  background:
    linear-gradient(rgba(0,0,0,.55),rgba(0,0,0,.55)),
    url("https://images.unsplash.com/photo-1500530855697-b586d89ba3ee");
  background-size:cover;
  background-position:center;
  min-height:100vh;
  transition:.4s;
}

.light{
  background:
    linear-gradient(rgba(255,255,255,.7),rgba(255,255,255,.7)),
    url("https://images.unsplash.com/photo-1500530855697-b586d89ba3ee");
  color:#000;
}

.screen{
  display:none;
  padding:30px 20px;
  animation:fade .6s ease;
}
.show{display:block;}

@keyframes fade{
  from{opacity:0;transform:translateY(20px);}
  to{opacity:1;transform:translateY(0);}
}

.logo{
  width:90px;height:90px;
  border-radius:50%;
  background:rgba(30,136,229,.9);
  margin:20px auto;
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:36px;
  font-weight:bold;
  box-shadow:0 0 20px rgba(30,136,229,.6);
}

h1,h2{margin:10px 0;}

.card{
  background:rgba(0,0,0,.45);
  padding:25px;
  border-radius:18px;
  backdrop-filter:blur(6px);
  max-width:420px;
  margin:0 auto;
}

input,textarea{
  width:100%;
  padding:14px;
  margin:10px 0;
  border:none;
  border-radius:12px;
  font-size:15px;
}

textarea{resize:none;height:80px;}

.btn{
  width:100%;
  padding:14px;
  margin:10px 0;
  border:none;
  border-radius:30px;
  font-size:16px;
  color:white;
  cursor:pointer;
  transition:.3s;
}
.btn:hover{transform:scale(1.03);}

.blue{background:linear-gradient(45deg,#1e88e5,#42a5f5);}
.red{background:linear-gradient(45deg,#e53935,#ef5350);}
.green{background:linear-gradient(45deg,#43a047,#66bb6a);}
.gray{background:linear-gradient(45deg,#546e7a,#78909c);}

img,video{
  max-width:100%;
  border-radius:14px;
  margin-top:10px;
}

.saveBox{
  margin-top:15px;
  padding:15px;
  background:rgba(255,255,255,.15);
  border-radius:14px;
}

.footer{
  position:fixed;
  bottom:12px;
  left:50%;
  transform:translateX(-50%);
  width:92%;
}

.small{opacity:.8;font-size:14px;}
</style>
</head>

<body id="body">

<!-- HOME -->
<div class="screen show" id="home">
  <div class="logo">LG</div>
  <h1>Life in The Go</h1>
  <p class="small">Welcome Durjoy</p>

  <div class="card">
    <button class="btn blue" onclick="openUser()">User Login</button>
    <button class="btn red" onclick="openMaster()">Master Login</button>
  </div>
</div>

<!-- USER LOGIN -->
<div class="screen" id="userLogin">
  <div class="card">
    <h2>User Login</h2>
    <input placeholder="Phone or Gmail">
    <input type="password" placeholder="Password">
    <button class="btn blue" onclick="openUserPanel()">Login</button>
  </div>
</div>

<!-- MASTER LOGIN -->
<div class="screen" id="masterLogin">
  <div class="card">
    <h2>Master Login</h2>
    <input type="password" id="mpass" placeholder="Master Password">
    <button class="btn red" onclick="openMasterPanel()">Enter</button>
  </div>
</div>

<!-- USER PANEL -->
<div class="screen" id="userPanel">
  <div class="card">
    <h2>User Space</h2>

    <input type="file" id="file" accept="image/*,video/*">
    <textarea id="note" placeholder="Write something to save..."></textarea>

    <button class="btn green" onclick="savePost()">Save</button>

    <div id="output"></div>
  </div>
</div>

<!-- MASTER PANEL -->
<div class="screen" id="masterPanel">
  <div class="card">
    <h2>👑 Master Panel</h2>
    <p>Owner: Durjoy</p>
    <p>Users: Demo</p>
  </div>
</div>

<!-- FOOTER -->
<div class="footer">
  <button class="btn gray" onclick="toggle()">Dark / Light</button>
</div>

<script>
function hideAll(){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('show'));
}

function openUser(){hideAll();userLogin.classList.add('show');}
function openMaster(){hideAll();masterLogin.classList.add('show');}
function openUserPanel(){hideAll();userPanel.classList.add('show');}

function openMasterPanel(){
  if(mpass.value==="durjoy123"){
    hideAll();masterPanel.classList.add('show');
  }else alert("Wrong password");
}

function savePost(){
  let f=file.files[0];
  let text=note.value;
  if(!f && !text){alert("Add something to save");return;}

  let box=document.createElement("div");
  box.className="saveBox";

  if(text) box.innerHTML+=`<p>${text}</p>`;

  if(f){
    let url=URL.createObjectURL(f);
    if(f.type.startsWith("image"))
      box.innerHTML+=`<img src="${url}">`;
    else
      box.innerHTML+=`<video src="${url}" controls></video>`;
  }
  output.prepend(box);
  file.value=""; note.value="";
}

function toggle(){
  body.classList.toggle("light");
}
</script>

</body>
</html>
