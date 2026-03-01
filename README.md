<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hope Foundation NGO</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family: Arial, Helvetica, sans-serif;
}

body{
    line-height:1.6;
    background:#f4f7f9;
    color:#333;
}

/* NAVBAR */
nav{
    background:#0a3d62;
    padding:15px 8%;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

nav h2{
    color:white;
}

nav ul{
    list-style:none;
    display:flex;
    gap:25px;
    align-items:center;
}

nav ul li{
    color:white;
    cursor:pointer;
}

.admin-btn{
    background:#1abc9c;
    padding:6px 12px;
    border-radius:5px;
}

/* HERO */
.hero{
    background:url('https://images.unsplash.com/photo-1509099836639-18ba1795216d') no-repeat center/cover;
    height:80vh;
    display:flex;
    justify-content:center;
    align-items:center;
    color:white;
    text-align:center;
}

.hero h1{
    font-size:50px;
    background:rgba(0,0,0,0.5);
    padding:20px;
    border-radius:10px;
}

/* SECTION */
section{
    padding:60px 8%;
}

.section-title{
    text-align:center;
    margin-bottom:30px;
    font-size:28px;
    color:#0a3d62;
}

/* CARDS */
.cards{
    display:flex;
    gap:20px;
    justify-content:center;
    flex-wrap:wrap;
}

.card{
    background:white;
    width:300px;
    padding:20px;
    border-radius:10px;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
    transition:0.3s;
}

.card img{
    width:100%;
    height:200px;
    object-fit:cover;
    border-radius:10px;
    margin-bottom:15px;
}

/* ADMIN PANEL */
.admin-panel{
    display:none;
    background:white;
    padding:20px;
    max-width:600px;
    margin:30px auto;
    border-radius:10px;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
}

.admin-panel input{
    width:100%;
    padding:8px;
    margin:8px 0;
}

.admin-panel button{
    padding:8px 15px;
    background:#0a3d62;
    color:white;
    border:none;
    cursor:pointer;
}

/* FOOTER */
footer{
    background:#0a3d62;
    color:white;
    text-align:center;
    padding:20px;
}
</style>
</head>

<body>

<nav>
    <h2>Hope Foundation</h2>
    <ul>
        <li>Home</li>
        <li>About</li>
        <li>Programs</li>
        <li>Contact</li>
        <li class="admin-btn" onclick="adminLogin()">Admin</li>
    </ul>
</nav>

<div class="hero">
    <h1>Helping People. Changing Lives.</h1>
</div>

<!-- ADMIN PANEL -->
<div class="admin-panel" id="adminPanel">
    <h3>Add New Program</h3>
    <input type="text" id="programTitle" placeholder="Program Title">
    <input type="text" id="programImage" placeholder="Image URL">
    <input type="text" id="programDesc" placeholder="Program Description">
    <button onclick="addProgram()">Add Program</button>
</div>

<section>
    <h2 class="section-title">Our Programs</h2>
    <div class="cards" id="programContainer"></div>
</section>

<footer>
    © 2026 Hope Foundation NGO | All Rights Reserved
</footer>

<script>
// Default programs
let defaultPrograms = [
    {
        title: "Education Support",
        image: "https://images.unsplash.com/photo-1509062522246-3755977927d7",
        desc: "Scholarships and mentorship for underprivileged children."
    }
];

// Load Programs
function loadPrograms(){
    let programs = JSON.parse(localStorage.getItem("programs")) || defaultPrograms;
    let container = document.getElementById("programContainer");
    container.innerHTML = "";

    programs.forEach((program, index) => {
        container.innerHTML += `
            <div class="card">
                <img src="${program.image}">
                <h3>${program.title}</h3>
                <p>${program.desc}</p>
                <button onclick="deleteProgram(${index})">Delete</button>
            </div>
        `;
    });
}

loadPrograms();

// Admin Login
function adminLogin(){
    let password = prompt("Enter Admin Password:");
    if(password === "admin123"){
        document.getElementById("adminPanel").style.display = "block";
        alert("Admin Access Granted");
    }else{
        alert("Wrong Password");
    }
}

// Add Program
function addProgram(){
    let title = document.getElementById("programTitle").value;
    let image = document.getElementById("programImage").value;
    let desc = document.getElementById("programDesc").value;

    let programs = JSON.parse(localStorage.getItem("programs")) || defaultPrograms;

    programs.push({title, image, desc});
    localStorage.setItem("programs", JSON.stringify(programs));

    loadPrograms();
}

// Delete Program
function deleteProgram(index){
    let programs = JSON.parse(localStorage.getItem("programs")) || defaultPrograms;
    programs.splice(index,1);
    localStorage.setItem("programs", JSON.stringify(programs));
    loadPrograms();
}
</script>

</body>
</html>
