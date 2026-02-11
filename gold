<!DOCTYPE html>
<html>
<head>
<title>Jewellery Gold Billing System</title>

<style>
body{
    font-family: Arial;
    margin:0;
    background:linear-gradient(135deg,#fdebd0,#f7dc6f);
}

/* HEADER */
.header{
    background:#6e2c00;
    color:white;
    padding:15px;
    text-align:center;
    font-size:28px;
    font-weight:bold;
}

/* LOGIN */
.loginBox{
    width:350px;
    margin:80px auto;
    background:white;
    padding:25px;
    border-radius:12px;
    box-shadow:0 0 10px rgba(0,0,0,0.3);
}

input,select{
    width:100%;
    padding:10px;
    margin:10px 0;
    border-radius:6px;
    border:1px solid #aaa;
}

button{
    width:100%;
    padding:12px;
    background:#b7950b;
    color:white;
    border:none;
    border-radius:8px;
    font-size:16px;
    cursor:pointer;
}

button:hover{
    background:#7d6608;
}

/* DASHBOARD */
.container{
    width:500px;
    margin:30px auto;
    background:white;
    padding:25px;
    border-radius:12px;
    box-shadow:0 0 12px rgba(0,0,0,0.3);
}

.rateDisplay{
    background:#f9e79f;
    padding:10px;
    border-radius:8px;
    text-align:center;
    margin-bottom:15px;
    font-weight:bold;
}

/* BILL */
.bill{
    background:#fdf2e9;
    padding:15px;
    margin-top:20px;
    border-radius:10px;
    line-height:28px;
}

.printBtn{
    background:green;
    margin-top:10px;
}

.adminPanel{
    background:#ebf5fb;
    padding:15px;
    border-radius:10px;
    margin-bottom:20px;
}

.logout{
    background:red;
    margin-top:10px;
}
</style>
</head>

<body>

<div class="header">💰 Jewellery Gold Billing System</div>

<!-- LOGIN PAGE -->
<div class="loginBox" id="loginPage">
<h3>Admin Login</h3>
<input type="text" id="username" placeholder="Username">
<input type="password" id="password" placeholder="Password">
<button onclick="login()">Login</button>
<p><b>Default:</b> admin / 1234</p>
</div>

<!-- MAIN APP -->
<div class="container" id="mainPage" style="display:none;">

<!-- ADMIN PANEL -->
<div class="adminPanel">
<h3>Admin Rate Update</h3>
<label>Update Today's 24K Rate (₹/gram)</label>
<input type="number" id="adminRate">
<button onclick="saveRate()">Update Rate</button>
<button class="logout" onclick="logout()">Logout</button>
</div>

<div class="rateDisplay">
Current 24K Gold Rate: ₹ <span id="currentRate">0</span> per gram
</div>

<h3>Customer Gold Calculation</h3>

<label>Customer Name</label>
<input type="text" id="custName">

<label>Gold Type</label>
<select id="goldType">
<option value="1">24K</option>
<option value="0.916">22K</option>
<option value="0.75">18K</option>
<option value="0.585">14K</option>
</select>

<label>Weight (grams)</label>
<input type="number" id="weight">

<label>Making Charges (%)</label>
<input type="number" id="making">

<button onclick="calculate()">Generate Bill</button>

<div class="bill" id="billArea"></div>
<button class="printBtn" onclick="printBill()">Print Bill</button>

</div>

<script>

/* ---------- LOGIN ---------- */
function login(){
    var u=document.getElementById("username").value;
    var p=document.getElementById("password").value;

    if(u==="admin" && p==="1234"){
        document.getElementById("loginPage").style.display="none";
        document.getElementById("mainPage").style.display="block";
        loadRate();
    }
    else{
        alert("Wrong Login!");
    }
}

function logout(){
    location.reload();
}

/* ---------- RATE STORAGE ---------- */
function saveRate(){
    var rate=document.getElementById("adminRate").value;
    localStorage.setItem("goldRate",rate);
    loadRate();
    alert("Rate Updated Successfully!");
}

function loadRate(){
    var rate=localStorage.getItem("goldRate");
    if(rate==null){
        rate=6500;
        localStorage.setItem("goldRate",rate);
    }
    document.getElementById("currentRate").innerText=rate;
}

/* ---------- CALCULATION ---------- */
function calculate(){

    var name=document.getElementById("custName").value;
    var purity=parseFloat(document.getElementById("goldType").value);
    var weight=parseFloat(document.getElementById("weight").value);
    var making=parseFloat(document.getElementById("making").value);
    var rate24=parseFloat(localStorage.getItem("goldRate"));

    if(!name || !weight || !making){
        alert("Fill all details");
        return;
    }

    var actualRate=rate24*purity;
    var goldPrice=actualRate*weight;
    var makingCharge=goldPrice*(making/100);
    var gst=(goldPrice+makingCharge)*0.03;
    var total=goldPrice+makingCharge+gst;

    var today=new Date().toLocaleDateString();

    document.getElementById("billArea").innerHTML=`
    <h2>Jewellery Shop Bill</h2>
    Date: ${today} <br>
    Customer: ${name} <br>
    ----------------------------------<br>
    Rate/gram: ₹ ${actualRate.toFixed(2)} <br>
    Gold Price: ₹ ${goldPrice.toFixed(2)} <br>
    Making Charges: ₹ ${makingCharge.toFixed(2)} <br>
    GST (3%): ₹ ${gst.toFixed(2)} <br>
    ----------------------------------<br>
    <b>Total Amount: ₹ ${total.toFixed(2)}</b>
    `;
}

/* ---------- PRINT ---------- */
function printBill(){
    window.print();
}

</script>

</body>

