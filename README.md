<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Minecraft PVP排行榜</title>
<link rel="stylesheet" href="https://fontsapi.zeoseven.com/570/main/result.css">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:"Fusion Pixel 12px M latin",sans-serif}
body{background:#111;color:#eee;padding:30px 15px;max-width:1100px;margin:0 auto}
h1{text-align:center;font-size:32px;margin-bottom:30px;color:#fff}
.ripple{position:fixed;width:20px;height:20px;border:2px solid #fff;border-radius:50%;pointer-events:none;animation:rippleAnim 0.5s ease-out forwards;z-index:9999}
@keyframes rippleAnim{0%{transform:scale(1);opacity:1}100%{transform:scale(8);opacity:0}}
.top-left-area{position:relative}
.open-upload-btn{padding:10px 18px}
.upload-box{background:#222;border:1px solid #444;padding:20px;border-radius:8px;max-width:360px;margin-top:12px;display:none}
.upload-box.show{display:block}
.login-box{background:#222;border:1px solid #444;padding:18px;border-radius:8px;max-width:360px;margin-bottom:16px}
label{display:block;margin-bottom:8px;font-size:15px;color:#ddd}
select,input[type="text"],input[type="password"],input[type="file"]{width:100%;padding:10px;border-radius:4px;border:1px solid #444;font-size:15px;margin-bottom:14px;background:#181818;color:#eee}
button{border:none;border-radius:4px;background:#3366dd;color:#fff;font-size:15px;cursor:pointer;padding:10px}
button:hover{background:#4477ee}
button:disabled{background:#333;color:#777;cursor:not-allowed}
.upload-submit{width:100%}
.center-select-wrap{text-align:center;margin:40px 0}
.center-select{padding:14px 20px;font-size:16px}
.region-title{font-size:20px;margin:20px 0 12px;color:#fff}
.video-card{background:#1b1b1b;padding:16px;border-radius:6px;margin:10px 0;border:1px solid #333}
.player-name{cursor:pointer;font-size:17px;display:flex;align-items:center;gap:6px}
.player-videos{margin-top:10px;padding-left:20px;display:none}
.player-videos.open{display:block}
video{max-width:100%;border-radius:4px;margin:8px 0}
.rank-tag{display:inline-block;background:#ffc107;color:#000;padding:3px 8px;border-radius:3px;font-weight:bold;margin-left:10px}
.no-perm-tip{color:#f55}
.admin-panel{display:none;margin-top:20px}
.admin-panel.show{display:block}
.admin-input{display:flex;gap:10px;margin:10px 0}
.admin-input input{flex:1;margin-bottom:0}
.admin-btn{padding:10px 16px}
.password-line{text-align:center;margin-top:50px;color:#888;font-size:13px;cursor:pointer}
.password-input-wrap{display:none;margin-top:10px;max-width:320px;margin:0 auto}
.password-input-wrap.show{display:block}
.user-info{color:#8cf;margin-bottom:10px}
.theme-footer-wrap{margin-top:60px;text-align:center}
#toggleOldThemeBtn{padding:12px 24px}

body.old-theme{background:#fff;color:#222}
body.old-theme h1{color:#ff3366}
body.old-theme .upload-box{background:#f3f3f3;border:1px solid #ddd}
body.old-theme .login-box{background:#f3f3f3;border:1px solid #ddd}
body.old-theme select,
body.old-theme input[type="text"],
body.old-theme input[type="password"],
body.old-theme input[type="file"]{background:#fff;color:#222;border:1px solid #ccc}
body.old-theme .video-card{background:#f8f8f8;border:1px solid #eee}
body.old-theme .region-title{color:#222}
body.old-theme .no-perm-tip{color:#f33}
body.old-theme .user-info{color:#27b}
</style>
</head>
<body>
<h1>Minecraft PVP排行榜</h1>

<div class="login-box" id="authBox">
<div class="user-info" id="userInfo"></div>
<label>用户名</label>
<input type="text" id="usernameInput" placeholder="账号">
<label>密码</label>
<input type="password" id="pwdInput" placeholder="密码">
<div style="display:flex;gap:8px">
<button id="regBtn">注册</button>
<button id="loginBtn">登录</button>
<button id="logoutBtn" style="display:none">退出</button>
</div>
</div>

<div class="top-left-area">
<button class="open-upload-btn" id="openUploadBtn">打开上传界面</button>
<div class="upload-box" id="uploadBox">
<label>选择你的省/自治区/直辖市</label>
<select id="regionSelectUpload">
<option value="">请选择地区</option>
<option value="北京市">北京市</option>
<option value="天津市">天津市</option>
<option value="上海市">上海市</option>
<option value="重庆市">重庆市</option>
<option value="河北省">河北省</option>
<option value="山西省">山西省</option>
<option value="辽宁省">辽宁省</option>
<option value="吉林省">吉林省</option>
<option value="黑龙江省">黑龙江省</option>
<option value="江苏省">江苏省</option>
<option value="浙江省">浙江省</option>
<option value="安徽省">安徽省</option>
<option value="福建省">福建省</option>
<option value="江西省">江西省</option>
<option value="山东省">山东省</option>
<option value="河南省">河南省</option>
<option value="湖北省">湖北省</option>
<option value="湖南省">湖南省</option>
<option value="广东省">广东省</option>
<option value="海南省">海南省</option>
<option value="四川省">四川省</option>
<option value="贵州省">贵州省</option>
<option value="云南省">云南省</option>
<option value="甘肃省">甘肃省</option>
</select>
<label>玩家名称（必须和榜单里名字一致）</label>
<input type="text" id="playerName" placeholder="填写选手名字，例如 CHan390">
<label>上传PVP视频</label>
<input type="file" id="videoFile" accept="video/*">
<button class="upload-submit" id="uploadBtn" disabled>上传视频到当前地区榜单</button>
</div>
</div>

<div class="center-select-wrap">
<select id="mainRegionSelect" class="center-select">
<option value="">请选择省/直辖市/自治区</option>
<option value="北京市">北京市</option>
<option value="天津市">天津市</option>
<option value="上海市">上海市</option>
<option value="重庆市">重庆市</option>
<option value="河北省">河北省</option>
<option value="山西省">山西省</option>
<option value="辽宁省">辽宁省</option>
<option value="吉林省">吉林省</option>
<option value="黑龙江省">黑龙江省</option>
<option value="江苏省">江苏省</option>
<option value="浙江省">浙江省</option>
<option value="安徽省">安徽省</option>
<option value="福建省">福建省</option>
<option value="江西省">江西省</option>
<option value="山东省">山东省</option>
<option value="河南省">河南省</option>
<option value="湖北省">湖北省</option>
<option value="湖南省">湖南省</option>
<option value="广东省">广东省</option>
<option value="海南省">海南省</option>
<option value="四川省">四川省</option>
<option value="贵州省">贵州省</option>
<option value="云南省">云南省</option>
<option value="甘肃省">甘肃省</option>
</select>
</div>

<div id="regionVideoList"></div>

<div class="video-card admin-panel" id="adminPanel">
<h2 style="color:#fff;margin-bottom:15px">🔐 开发者管理面板 - 全部视频</h2>
<div id="allVideoList"></div>
</div>

<div class="password-line" id="openPassword">管理员开发入口</div>
<div class="password-input-wrap" id="passwordWrap">
<input type="text" id="adminPwd" placeholder="输入管理员密码">
<button id="loginAdminBtn">进入开发者模式</button>
</div>

<div class="theme-footer-wrap">
<button id="toggleOldThemeBtn">开启原版主题</button>
</div>

<script>
let lastRipple = 0;
document.addEventListener("mousedown",e=>{
    const now = Date.now();
    if(now - lastRipple < 500){
        alert("不要点太快！");
        return;
    }
    lastRipple = now;
    const div = document.createElement("div");
    div.className = "ripple";
    div.style.left = e.clientX + "px";
    div.style.top = e.clientY + "px";
    document.body.appendChild(div);
    setTimeout(()=>div.remove(),500);
})

const toggleThemeBtn = document.getElementById("toggleOldThemeBtn");
let isOldTheme = localStorage.getItem("useOldTheme") === "1";
function applyTheme(){
    if(isOldTheme){
        document.body.classList.add("old-theme");
        toggleThemeBtn.innerText = "关闭原版主题";
    }else{
        document.body.classList.remove("old-theme");
        toggleThemeBtn.innerText = "开启原版主题";
    }
}
toggleThemeBtn.onclick = ()=>{
    isOldTheme = !isOldTheme;
    localStorage.setItem("useOldTheme", isOldTheme ? "1":"0");
    applyTheme();
}
applyTheme();

let db;
const DB_NAME = "McPvpVideoDB";
const STORE_NAME = "videos";
function openDB(){
    return new Promise((resolve,reject)=>{
        const req = indexedDB.open(DB_NAME,1);
        req.onupgradeneeded = e=>{
            db = e.target.result;
            db.createObjectStore(STORE_NAME,{keyPath:"id"});
        }
        req.onsuccess = e=>{db = e.target.result;resolve(db)}
        req.onerror = e=>reject(e.target.error)
    })
}
function saveVideoBlob(item){
    return new Promise(resolve=>{
        const tx = db.transaction(STORE_NAME,"readwrite");
        const st = tx.objectStore(STORE_NAME);
        st.put(item);
        tx.oncomplete = ()=>resolve();
    })
}
function getVideoBlob(id){
    return new Promise(resolve=>{
        const tx = db.transaction(STORE_NAME,"readonly");
        const st = tx.objectStore(STORE_NAME);
        const r = st.get(id);
        r.onsuccess = ()=>resolve(r.result);
    })
}

let userList = JSON.parse(localStorage.getItem("userList")) || {};
let loginUser = localStorage.getItem("loginUser") || "";
const usernameInput = document.getElementById("usernameInput");
const pwdInput = document.getElementById("pwdInput");
const regBtn = document.getElementById("regBtn");
const loginBtn = document.getElementById("loginBtn");
const logoutBtn = document.getElementById("logoutBtn");
const userInfoDom = document.getElementById("userInfo");
const uploadBtn = document.getElementById("uploadBtn");

function refreshAuthUI(){
    if(loginUser){
        userInfoDom.innerText = "✅ 当前登录："+loginUser;
        logoutBtn.style.display = "block";
        uploadBtn.disabled = false;
    }else{
        userInfoDom.innerText = "❌ 未登录，请注册并登录才能上传";
        logoutBtn.style.display = "none";
        uploadBtn.disabled = true;
    }
}
regBtn.onclick = ()=>{
    const u = usernameInput.value.trim();
    const p = pwdInput.value.trim();
    if(!u||!p) return alert("用户名密码不能为空");
    if(userList[u]) return alert("账号已存在！");
    userList[u] = p;
    localStorage.setItem("userList",JSON.stringify(userList));
    alert("注册成功，可以登录！");
}
loginBtn.onclick = ()=>{
    const u = usernameInput.value.trim();
    const p = pwdInput.value.trim();
    if(!userList[u]) return alert("账号不存在");
    if(userList[u]!==p) return alert("密码错误");
    loginUser = u;
    localStorage.setItem("loginUser",u);
    refreshAuthUI();
    alert("登录成功");
}
logoutBtn.onclick = ()=>{
    loginUser = "";
    localStorage.removeItem("loginUser");
    refreshAuthUI();
}
refreshAuthUI();

// --------------------------
// 24地区 × 10人 = 240唯一名字，甘肃第一名固定 CHan390
// --------------------------
const regionList = [
    "北京市","天津市","上海市","重庆市","河北省","山西省","辽宁省","吉林省","黑龙江省",
    "江苏省","浙江省","安徽省","福建省","江西省","山东省","河南省","湖北省","湖南省",
    "广东省","海南省","四川省","贵州省","云南省","甘肃省"
];
const namePoolAll = [
    "SnowWolf01","RedAxer02","EndFighter03","SkyBlade04","NetherKnight05","StoneSmasher06","EchoRush07","VoidRunner08","FlameDash09","IronPunch10",
    "BreezeHit11","CaveJumper12","GoldSlash13","ShadowStrike14","WaveClash15","LeafSword16","RapidShot17","DarkLeap18","BrickBash19","CloudDart20",
    "LavaFury21","FrostClaw22","OakGuard23","SandSting24","MoonThrust25","RustBlade26","GlowStab27","TideCharge28","BoulderRam29","TwistJab30",
    "SwiftVein31","AshSwipe32","MistPierce33","SpireBump34","CoralStab35","HazeCut36","PeakSlam37","RidgeThorn38","DriftLunge39","Bramble40",
    "PebbleHit41","GustSlash42","EmberThrust43","BogLeap44","CragSwipe45","FernStrike46","FjordDash47","GaleJab48","HollowCut49","IvySlam50",
    "JadeThorn51","KelpLunge52","LichenHit53","MossStab54","NebulaSlash55","OnyxDash56","PaleJab57","QuartzSlam58","ReefThrust59","SageCut60",
    "TumbleStrike61","UmberLeap62","VeinSlash63","WispJab64","XenonHit65","YewThrust66","ZirconSlam67","AuroraDash68","BerylStab69","CrimsonCut70",
    "DuskLunge71","EclipseHit72","FjellSlash73","GarnetJab74","HaloThrust75","IrisSlam76","JetStrike77","KyanDash78","LunarCut79","MyrrhStab80",
    "NimbusLunge81","OliveHit82","PyroSlash83","QuillJab84","RavenThrust85","SableSlam86","TalonStrike87","UmberDash88","ValeCut89","WrenStab90",
    "XylemLunge91","YewHit92","ZestSlash93","AmethJab94","BreezeThrust95","CinderSlam96","DewStrike97","EmberDash98","FrostCut99","GaleStab100",
    "HazeLunge101","IvyHit102","JadeSlash103","KelpJab104","LichenThrust105","MossSlam106","NebulaStrike107","OnyxDash108","PaleCut109","QuartzStab110",
    "ReefLunge111","SageHit112","TumbleSlash113","UmberJab114","VeinThrust115","WispSlam116","XenonStrike117","YewDash118","ZirconCut119","AuroraStab120",
    "BerylLunge121","CrimsonHit122","DuskSlash123","EclipseJab124","FjellThrust125","GarnetSlam126","HaloStrike127","IrisDash128","JetCut129","KyanStab130",
    "LunarLunge131","MyrrhHit132","NimbusSlash133","OliveJab134","PyroThrust135","QuillSlam136","RavenStrike137","SableDash138","TalonCut139","ValeStab140",
    "WrenLunge141","XylemHit142","ZestSlash143","AmethJab144","BreezeThrust145","CinderSlam146","DewStrike147","EmberDash148","FrostCut149","GaleStab150",
    "HazeLunge151","IvyHit152","JadeSlash153","KelpJab154","LichenThrust155","MossSlam156","NebulaStrike157","OnyxDash158","PaleCut159","QuartzStab160",
    "ReefLunge161","SageHit162","TumbleSlash163","UmberJab164","VeinThrust165","WispSlam166","XenonStrike167","YewDash168","ZirconCut169","AuroraStab170",
    "BerylLunge171","CrimsonHit172","DuskSlash173","EclipseJab174","FjellThrust175","GarnetSlam176","HaloStrike177","IrisDash178","JetCut179","KyanStab180",
    "LunarLunge181","MyrrhHit182","NimbusSlash183","OliveJab184","PyroThrust185","QuillSlam186","RavenStrike187","SableDash188","TalonCut189","ValeStab190",
    "WrenLunge191","XylemHit192","ZestSlash193","AmethJab194","BreezeThrust195","CinderSlam196","DewStrike197","EmberDash198","FrostCut199","GaleStab200",
    "HazeLunge201","IvyHit202","JadeSlash203","KelpJab204","LichenThrust205","MossSlam206","NebulaStrike207","OnyxDash208","PaleCut209","QuartzStab210",
    "ReefLunge211","SageHit212","TumbleSlash213","UmberJab214","VeinThrust215","WispSlam216","XenonStrike217","YewDash218","ZirconCut219","AuroraStab220",
    "BerylLunge221","CrimsonHit222","DuskSlash223","EclipseJab224","FjellThrust225","GarnetSlam226","HaloStrike227","IrisDash228","JetCut229","KyanStab230",
    "LunarLunge231","MyrrhHit232","NimbusSlash233","OliveJab234","PyroThrust235","QuillSlam236","RavenStrike237","SableDash238","TalonCut239"
];

function buildDefaultData(){
    const arr = [];
    let nameIdx = 0;
    for(let r=0;r<regionList.length;r++){
        const reg = regionList[r];
        for(let i=0;i<10;i++){
            let playerName;
            if(reg === "甘肃省" && i === 0){
                playerName = "CHan390";
            }else{
                playerName = namePoolAll[nameIdx++];
            }
            arr.push({
                id:`${reg}-${i}`,
                region:reg,
                name:playerName,
                blobId:"",
                rank:`第${i+1}名`
            })
        }
    }
    return arr;
}

let videoData = JSON.parse(localStorage.getItem("mcPvpVideoMeta"));
if(!videoData || !Array.isArray(videoData) || videoData.length!==240){
    videoData = buildDefaultData();
    saveMeta();
}

const openUploadBtn = document.getElementById("openUploadBtn");
const uploadBox = document.getElementById("uploadBox");
const regionSelectUpload = document.getElementById("regionSelectUpload");
const playerNameInput = document.getElementById("playerName");
const videoFileInput = document.getElementById("videoFile");
const mainRegionSelect = document.getElementById("mainRegionSelect");
const regionVideoList = document.getElementById("regionVideoList");
const adminPanel = document.getElementById("adminPanel");
const allVideoList = document.getElementById("allVideoList");
const openPassword = document.getElementById("openPassword");
const passwordWrap = document.getElementById("passwordWrap");
const adminPwd = document.getElementById("adminPwd");
const loginAdminBtn = document.getElementById("loginAdminBtn");

openUploadBtn.onclick = function(){
    uploadBox.classList.toggle("show");
    openUploadBtn.innerText = uploadBox.classList.contains("show") ? "关闭上传界面" : "打开上传界面";
}

async function renderRegionVideo(){
    const selRegion = mainRegionSelect.value;
    regionVideoList.innerHTML = "";
    if(!selRegion) return;
    const regionVideos = videoData.filter(item=>item.region === selRegion);
    let html = `<div class="region-title">📍 ${selRegion} PVP视频榜单</div>`;
    const group = {};
    regionVideos.forEach(v=>{if(!group[v.name]) group[v.name]=[];group[v.name].push(v)});
    for(const player of Object.keys(group)){
        const arr = group[player];
        html += `<div class="video-card"><div class="player-name" onclick="togglePlayer(this)">▶ ${player}</div><div class="player-videos">`;
        for(const v of arr){
            if(v.blobId){
                const blobItem = await getVideoBlob(v.blobId);
                if(blobItem?.blob){
                    const url = URL.createObjectURL(blobItem.blob);
                    html += `<div style="margin:8px 0"><video controls src="${url}"></video><div>排名：${v.rank||"未排名"}</div></div>`;
                }else{
                    html += `<div style="margin:8px 0"><video controls><source src="" type="video/mp4"></video><div class="no-perm-tip">视频丢失<br>排名：${v.rank||"未排名"}</div></div>`;
                }
            }else{
                html += `<div style="margin:8px 0"><video controls><source src="" type="video/mp4"></video><div class="no-perm-tip">暂无视频<br>排名：${v.rank||"未排名"}</div></div>`;
            }
        }
        html += `</div></div>`;
    }
    regionVideoList.innerHTML = html;
}

window.togglePlayer = function(el){
    const box = el.nextElementSibling;
    box.classList.toggle("open");
    el.innerHTML = box.classList.contains("open") ? `▼ ${el.innerText.slice(2)}` : `▶ ${el.innerText.slice(2)}`;
}

async function renderAdminAll(){
    allVideoList.innerHTML = "";
    if(videoData.length === 0){
        allVideoList.innerHTML = "<p>暂无上传视频</p>";
        return;
    }
    let html = "";
    for(let idx=0;idx<videoData.length;idx++){
        const item = videoData[idx];
        let vhtml = "";
        if(item.blobId){
            const blobItem = await getVideoBlob(item.blobId);
            if(blobItem?.blob){
                const url = URL.createObjectURL(blobItem.blob);
                vhtml = `<video controls src="${url}"></video>`;
            }else{
                vhtml = `<video controls><source src="" type="video/mp4"></video><p class="no-perm-tip">视频丢失</p>`;
            }
        }else{
            vhtml = `<video controls><source src="" type="video/mp4"></video><p class="no-perm-tip">无视频</p>`;
        }
        html += `<div class="video-card"><p>地区：${item.region}</p><p>玩家ID：${item.name}</p>${vhtml}<div class="admin-input"><input type="text" placeholder="设置排名，例如：第3名" value="${item.rank||''}" id="rank-${idx}"><button class="admin-btn" onclick="setRank(${idx})">保存排名</button></div><div class="rank-tag">当前：${item.rank||"未排名"}</div></div>`;
    }
    allVideoList.innerHTML = html;
}

window.setRank = function(idx){
    const val = document.getElementById(`rank-${idx}`).value.trim();
    videoData[idx].rank = val;
    saveMeta();
    renderAdminAll();
    renderRegionVideo();
}
function saveMeta(){
    localStorage.setItem("mcPvpVideoMeta", JSON.stringify(videoData));
}

uploadBtn.onclick = async function(){
    const region = regionSelectUpload.value;
    const name = playerNameInput.value.trim();
    const file = videoFileInput.files[0];
    if(!region) return alert("请先选择省/自治区/直辖市！");
    if(!name) return alert("请输入选手名字！");
    if(!file) return alert("请选择视频文件！");
    await openDB();
    // 找到这个选手条目，直接覆盖它的视频
    const targetItem = videoData.find(x=>x.region===region && x.name===name);
    if(!targetItem){
        return alert("该地区没有这个选手名字！核对名字");
    }
    const blobId = "vid_"+Date.now();
    await saveVideoBlob({id:blobId, blob:file});
    targetItem.blobId = blobId;
    saveMeta();
    alert("上传成功！榜单已更新");
    renderRegionVideo();
    renderAdminAll();
}

openPassword.onclick = function(){passwordWrap.classList.toggle("show")}
loginAdminBtn.onclick = function(){
    if(adminPwd.value === "123312"){
        adminPanel.classList.add("show");
        renderAdminAll();
        alert("✅ 进入开发者模式，可以给视频排名！");
    }else{
        alert("❌ 密码错误");
    }
}

mainRegionSelect.onchange = renderRegionVideo;
openDB();
</script>
</body>
</html>
