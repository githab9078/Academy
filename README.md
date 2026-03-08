দারুন! 😎 তাহলে আমরা পুরো Interactive Academy Frontend বানাবো যা সম্পূর্ণ ব্রাউজারে রান করবে। এতে থাকবে:

ফিচারসমূহ:
User Login/Register – প্রতিটি ব্যবহারকারীর আলাদা লগইন
Admin Panel – অ্যাডমিন সব ব্যবহারকারীর তালিকা দেখতে, এডিট/ডিলিট করতে পারবে
Course Dashboard – প্রতিটি কোর্সে ঢুকে Payment Simulation ও স্ট্যাটাস দেখতে পারবে
QR Payment Simulation – প্রতিটি কোর্সের জন্য QR কোড জেনারেশন
Interactive Frontend – হোম, কোর্স, আমাদের সম্পর্কে, যোগাযোগ সব থাকবে

আমি এখানে একটি এক ফাইলের সম্পূর্ণ উদাহরণ দিচ্ছি যা HTML + CSS + JS একসাথে।
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>সাইবার সিকিউরিটি একাডেমি</title>
<style>
/* Basic Reset */
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif;}
body{background:#0a0a23;color:#fff;line-height:1.6;}
a{text-decoration:none;color:inherit;}
header{background:#111144;padding:15px 0;position:sticky;top:0;z-index:100;}
nav{width:90%;margin:auto;display:flex;justify-content:space-between;align-items:center;}
nav .logo{font-size:1.8em;font-weight:bold;color:#00ffcc;}
nav ul{list-style:none;display:flex;}
nav ul li{margin-left:20px;}
nav ul li a{padding:6px 12px;transition:0.3s;}
nav ul li a:hover{background:#00ffcc;color:#111144;border-radius:5px;}

/* Hero */
.hero{background:url('https://images.unsplash.com/photo-1605902711622-cfb43c4439c0?auto=format&fit=crop&w=1950&q=80') no-repeat center center/cover;height:70vh;display:flex;justify-content:center;align-items:center;text-align:center;}
.hero h1{font-size:3em;background:rgba(0,0,0,0.6);padding:20px;border-radius:10px;color:#00ffcc;}

/* Sections */
section{width:90%;margin:50px auto;}
.courses{display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;}
.course-card{background:#111144;padding:20px;border-radius:10px;transition:0.3s;}
.course-card:hover{background:#222266;transform:translateY(-5px);}
.course-card h3{margin-bottom:10px;color:#00ffcc;}
.about,.contact{background:#111144;padding:30px;border-radius:10px;}

/* Footer */
footer{background:#000011;text-align:center;padding:20px 0;margin-top:50px;font-size:0.9em;color:#8888ff;}

/* Buttons */
.btn{display:inline-block;padding:10px 20px;background:#00ffcc;color:#111144;border-radius:5px;margin-top:10px;transition:0.3s;}
.btn:hover{background:#00cc99;cursor:pointer;}

/* Modals */
.modal{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.8);justify-content:center;align-items:center;z-index:200;}
.modal-content{background:#111144;padding:30px;border-radius:10px;width:90%;max-width:400px;}
.modal-content h2{text-align:center;margin-bottom:20px;color:#00ffcc;}
.modal-content input{width:100%;padding:10px;margin:10px 0;border-radius:5px;border:none;}
.modal-content .close{float:right;cursor:pointer;font-size:1.2em;color:#00ffcc;}

/* Admin Panel */
#adminPanel{display:none;background:#111144;padding:20px;border-radius:10px;margin-top:20px;}
#adminPanel h3{color:#00ffcc;margin-bottom:10px;}
#userTable{width:100%;border-collapse:collapse;margin-top:10px;}
#userTable th,#userTable td{border:1px solid #00ffcc;padding:8px;text-align:center;}
#userTable th{background:#222266;}

/* Course Dashboard */
#dashboard{display:none;background:#111144;padding:20px;border-radius:10px;margin-top:20px;}
#dashboard h3{color:#00ffcc;margin-bottom:10px;}
#paymentStatus{margin-top:10px;color:#00ffcc;}

/* QR Payment */
.qr-box{background:#222266;padding:15px;margin-top:10px;text-align:center;border-radius:10px;}
.qr-box img{width:150px;height:150px;}
</style>
</head>
<body>

<!-- Header -->
<header>
<nav>
    <div class="logo">সাইবার সিকিউরিটি একাডেমি</div>
    <ul>
        <li><a href="#hero">হোম</a></li>
        <li><a href="#courses">কোর্স</a></li>
        <li><a href="#about">আমাদের সম্পর্কে</a></li>
        <li><a href="#contact">যোগাযোগ</a></li>
        <li><a class="btn" onclick="openModal('loginModal')">Login</a></li>
        <li><a class="btn" onclick="openModal('registerModal')">Register</a></li>
        <li><a class="btn" onclick="openModal('adminLoginModal')">Admin</a></li>
    </ul>
</nav>
</header>

<!-- Hero -->
<section class="hero" id="hero"><h1>আপনার সাইবার সিকিউরিটি যাত্রা শুরু করুন</h1></section>

<!-- Courses -->
<section id="courses">
<h2 style="text-align:center;margin-bottom:30px;">আমাদের কোর্সসমূহ</h2>
<div class="courses">
<div class="course-card">
<h3>ইথিক্যাল হ্যাকিং</h3>
<p>শিখুন প্রফেশনাল হ্যাকারদের মতো সিকিউরিটি টেস্টিং।</p>
<a class="btn" onclick="openCourse('Ethical Hacking')">ড্যাশবোর্ড</a>
</div>
<div class="course-card">
<h3>নেটওয়ার্ক সিকিউরিটি</h3>
<p>নেটওয়ার্ক সিস্টেম সুরক্ষা ও ঝুঁকি কমানোর কৌশল।</p>
<a class="btn" onclick="openCourse('Network Security')">ড্যাশবোর্ড</a>
</div>
<div class="course-card">
<h3>ডিজিটাল ফরেনসিক্স</h3>
<p>ডিজিটাল অপরাধ তদন্তের জন্য প্র্যাক্টিক্যাল স্কিল।</p>
<a class="btn" onclick="openCourse('Digital Forensics')">ড্যাশবোর্ড</a>
</div>
</div>
</section>

<!-- About -->
<section id="about" class="about">
<h2 style="text-align:center;margin-bottom:20px;">আমাদের সম্পর্কে</h2>
<p>সাইবার সিকিউরিটি একাডেমি আপনাকে প্রফেশনাল হ্যাকিং, নেটওয়ার্ক সিকিউরিটি এবং ডিজিটাল ফরেনসিক্সে দক্ষ করে গড়ে তুলবে। আমরা বাস্তবভিত্তিক ট্রেনিং এবং প্রজেক্ট বেসড লার্নিং দিয়ে শিক্ষার্থীদের প্রস্তুত করি।</p>
</section>

<!-- Contact -->
<section id="contact" class="contact">
<h2 style="text-align:center;margin-bottom:20px;">যোগাযোগ</h2>
<p style="text-align:center;">ইমেইল: info@cyberacademy.com | ফোন: ০১৮৮৮৬১০৭৯৬</p>
</section>

<!-- Welcome -->
<div id="welcome" style="text-align:center;margin:20px;font-size:1.5em;color:#00ffcc;"></div>

<!-- Admin Panel -->
<section id="adminPanel">
<h3>অ্যাডমিন প্যানেল - ব্যবহারকারীর তালিকা</h3>
<table id="userTable">
<thead><tr><th>নাম</th><th>ইমেইল</th><th>Action</th></tr></thead>
<tbody></tbody>
</table>
</section>

<!-- Course Dashboard -->
<section id="dashboard">
<h3 id="dashCourse"></h3>
<div class="qr-box" id="courseQR"></div>
<div id="paymentStatus"></div>
<a class="btn" onclick="payCourse()">পেমেন্ট করুন</a>
</section>

<!-- Modals -->
<div id="registerModal" class="modal">
<div class="modal-content">
<span class="close" onclick="closeModal('registerModal')">&times;</span>
<h2>রেজিস্টার</h2>
<input type="text" id="regName" placeholder="নাম">
<input type="email" id="regEmail" placeholder="ইমেইল">
<input type="password" id="regPass" placeholder="পাসওয়ার্ড">
<a class="btn" onclick="registerUser()">Register</a>
</div>
</div>

<div id="loginModal" class="modal">
<div class="modal-content">
<span class="close" onclick="closeModal('loginModal')">&times;</span>
<h2>লগইন</h2>
<input type="email" id="loginEmail" placeholder="ইমেইল">
<input type="password" id="loginPass" placeholder="পাসওয়ার্ড">
<a class="btn" onclick="loginUser()">Login</a>
</div>
</div>

<div id="adminLoginModal" class="modal">
<div class="modal-content">
<span class="close" onclick="closeModal('adminLoginModal')">&times;</span>
<h2>অ্যাডমিন লগইন</h2>
<input type="text" id="adminUser" placeholder="Username">
<input type="password" id="adminPass" placeholder="Password">
<a class="btn" onclick="adminLogin()">Login</a>
</div>
</div>

<script>
// Modal functions
function openModal(id){document.getElementById(id).style.display='flex';}
function closeModal(id){document.getElementById(id).style.display='none';}

// Users
let users=[]; 
let loggedUser=null;
function registerUser(){
    const name=document.getElementById('regName').value;
    const email=document.getElementById('regEmail').value;
    const pass=document.getElementById('regPass').value;
    if(!name||!email||!pass){alert('সব তথ্য পূরণ করুন');return;}
    if(users.some(u=>u.email===email)){alert('এই ইমেইল ইতিমধ্যেই ব্যবহৃত হয়েছে');return;}
    users.push({name,email,pass,payments:[]});
    alert('রেজিস্ট্রেশন সফল!');
    closeModal('registerModal');
}

function loginUser(){
    const email=document.getElementById('loginEmail').value;
    const pass=document.getElementById('loginPass').value;
    const user=users.find(u=>u.email===email&&u.pass===pass);
    if(user){loggedUser=user;document.getElementById('welcome').innerText=`স্বাগতম ${user.name}!`;closeModal('loginModal');}else{alert('ইমেইল বা পাসওয়ার্ড ভুল');}
}

// Admin
function adminLogin(){
    const user=document.getElementById('adminUser').value;
    const pass=document.getElementById('adminPass').value;
    if(user==='admin'&&pass==='1234'){alert('অ্যাডমিন লগইন সফল!');document.getElementById('adminPanel').style.display='block';updateUserTable();closeModal('adminLoginModal');}else{alert('ইউজারনেম বা পাসওয়ার্ড ভুল');}
}
function updateUserTable(){
    const tbody=document.querySelector('#userTable tbody');tbody.innerHTML='';
    users.forEach((u,i)=>{const tr=document.createElement('tr');tr.innerHTML=`<td>${u.name}</td><td>${u.email}</td><td><button onclick="deleteUser(${i})" class="btn">Delete</button></td>`;tbody.appendChild(tr);});
}
function deleteUser(i){if(confirm('আপনি কি ব্যবহারকারী ডিলিট করতে চান?')){users.splice(i,1);updateUserTable();}}

// Course Dashboard
let currentCourse='';
function openCourse(course){
    if(!loggedUser){alert('প্রথমে লগইন করুন');return;}
    currentCourse=course;
    document.getElementById('dashboard').style.display='block';
    document.getElementById('dashCourse').innerText=course;
    showQRCourse();
}
function showQRCourse(){
    const qrBox=document.getElementById('courseQR');
    qrBox.innerHTML=`<img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=Pay%20for%20${encodeURIComponent(currentCourse)}" alt="QR Code"><p>Scan করে পেমেন্ট করুন</p>`;
    const paid=loggedUser.payments.includes(currentCourse);
    document.getElementById('paymentStatus').innerText=paid?'পেমেন্ট সম্পন্ন':'পেমেন্ট বাকি';
}
function payCourse(){if(!loggedUser.payments.includes(currentCourse)){loggedUser.payments.push(currentCourse);alert('পেমেন্ট সফল!');showQRCourse();}}
</script>

</body>
</html>


✅ ফিচারস এই ভার্সনে:
User Login/Register – JS array তে সব তথ্য সংরক্ষণ
Admin Panel – অ্যাডমিন admin/1234 দিয়ে লগইন করে সব ব্যবহারকারী দেখতে ও ডিলিট করতে পারবে
Course Dashboard per user – লগইন ব্যবহারকারী প্রতিটি কোর্সে ঢুকতে পারবে
QR Payment Simulation – প্রতিটি কোর্সের জন্য QR কোড জেনারেশন
Payment Status – প্রতিটি ব্যবহারকারীর পেমেন্ট স্ট্যাটাস দেখানো

যদি চান, আমি পরবর্তী ধাপে এটিতে Admin থেকে User Payment Edit/Reset + Full Dashboard Analytics যোগ করে প্রকৃত প্রফেশনাল Academy Simulator বানিয়ে দিতে পারি।
আপনি কি সেটা চাইবেন?







পদ্ধতি ৩: Termux বা মোবাইল টার্মিনালে (Android)
Termux ইনস্টল করুন
ফাইল তৈরি করুন

nano index.html


 কোড পেস্ট করুন, সেভ করুন।
Python সার্ভার ইনস্টল করুন (যদি না থাকে)


pkg install python

সার্ভার চালান

python3 -m http.server 8000


মোবাইল ব্রাউজারে ওপেন করুন

http://127.0.0.1:8000
