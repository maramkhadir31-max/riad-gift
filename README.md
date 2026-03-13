<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>My Little World 💙</title>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&display=swap" rel="stylesheet">

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.spark {
    position: absolute;
    width: 5px;
    height: 5px;
    background-color: white;
    animation: sparkAnim 0.5s forwards;
}

@keyframes sparkAnim {
    0% { transform: translate(0,0) scale(1); opacity: 1; }
    50% { transform: translate(var(--x), var(--y)) scale(1.2); opacity: 0.7; }
    100% { transform: translate(var(--x), var(--y)) scale(0.5); opacity: 0; }
}

/* ===== General ===== */
body {
    font-family: 'Playfair Display', serif;
    overflow: hidden;
}

/* ===== Pages ===== */
.page {
    width: 100vw;
    height: 100vh;
    display: none;
    justify-content: center;
    align-items: center;
}

.page.active {
    display: flex;
}

/* ===== Page 1 ===== */
#page1 {
    background-color: #0a1a2f; /* navy blue */
}

.card {
    background-color: #6a4c93; /* purple */
    padding: 40px 60px;
    border-radius: 20px;
    text-align: center;
    position: relative;
    overflow: hidden;
}

/* Hearts */
.heart {
    position: absolute;
    color: rgba(255,255,255,0.4);
    font-size: 18px;
    animation: float 6s infinite ease-in-out;
}

@keyframes float {
    0% { transform: translateY(0); opacity: 0.4; }
    50% { transform: translateY(-20px); opacity: 0.8; }
    100% { transform: translateY(0); opacity: 0.4; }
}

/* Title */
.title {
    font-size: clamp(32px, 6vw, 52px);
    color: white;
    margin-bottom: 20px;
}

/* Click here */
.click {
    color: #ffffff;
    font-size: clamp(14px, 3vw, 18px);
    cursor: pointer;
    transition: 0.3s;
    animation: glow 2s infinite;
}

.click:hover {
    color: #ffd6ff;
}

@keyframes glow {
    0% { text-shadow: 0 0 5px #fff; }
    50% { text-shadow: 0 0 15px #ffd6ff; }
    100% { text-shadow: 0 0 5px #fff; }
}

/* ===== Page 2 ===== */
#page2 {
    background-color: #b9a3c8; /* soft purple */
    flex-direction: column;
    padding: 30px;
    text-align: center;
}

.text {
    max-width: 700px;
    color: #000;
    font-size: clamp(14px, 2.5vw, 18px);
    line-height: 1.8;
}

/* Pulse text */
.pulse {
    margin-top: 30px;
    font-weight: 600;
    font-size: clamp(16px, 4vw, 20px);
    animation: pulse 1.5s infinite;
}

@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.1); }
    100% { transform: scale(1); }
}

/* Back arrow */
.back {
    position: fixed;
    top: 20px;
    left: 20px;
    font-size: 35px; /* تكبير السهم */
    font-weight: bold;
    cursor: pointer;
    display: none;
    z-index: 10000; /* لضمان ظهوره فوق كل شيء */
    background: rgba(255, 255, 255, 0.2); /* خلفية خفيفة دائرية */
    width: 50px;
    height: 50px;
    display: none; /* يتم التحكم فيه بالـ JS */
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    transition: 0.3s;
}

.back:hover {
    transform: scale(1.1);
    background: rgba(255, 255, 255, 0.4);
}
/* ===== Page 3 المحدثة للهاتف ===== */
#page3 {
    background: linear-gradient(135deg, #6a11cb, #2575fc);
    flex-direction: column;
    padding: 80px 15px 40px 15px; /* زيادة Padding العلوي للسهم */
    justify-content: flex-start; /* الترتيب من الأعلى */
    overflow-y: auto; /* السماح بالتمرير */
}

.subjects-container {
    display: grid;
    /* الهاتف يعرض 2 في الصف، والحاسوب يوزعهم حسب المساحة */
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); 
    gap: 15px;
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
}

.subject {
    background-color: white;
    color: #333;
    padding: 20px 10px;
    border-radius: 15px;
    text-align: center;
    font-family: 'Playfair Display', serif;
    /* حجم خط مرن جداً */
    font-size: clamp(15px, 3.5vw, 19px); 
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 90px; /* ضمان طول موحد للمربعات */
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

/* تأثير اللمس للهاتف والحاسوب */
.subject:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(255, 255, 255, 0.4);
    background-color: #fcfcfc;
}

/* تعديلات خاصة بالشاشات الصغيرة جداً (مثل الهواتف المتوسطة) */
@media (max-width: 480px) {
    .subjects-container {
        grid-template-columns: repeat(2, 1fr); /* إجبار ظهور مربعين في الصف */
        gap: 10px;
    }
    
    .subject {
        padding: 15px 5px;
        min-height: 80px;
        border-radius: 12px;
    }

    #page3 {
        padding-top: 100px; /* مساحة إضافية للسهم في الهاتف */
    }
}

/* Hover effect مع glow أبيض */
.subject:hover {
    transform: translateY(-8px);
    box-shadow: 0 0 20px 5px rgba(255,255,255,0.8); /* توهج أبيض */
}/* خلفية خضراء فخمة للصفحات الجديدة */
#historyUnitsPage, #unitSubMenuPage, #gridPage, #lessonsListPage, #lessonDetailsPage {
    background: radial-gradient(circle, #8b5504 0%, #8b5504 100%);
    flex-direction: column;
    padding: 20px;
    overflow-y: auto; /* يسمح بالتمرير العمودي */
    justify-content: flex-start; /* يبدأ الترتيب من الأعلى لضمان ظهور أول صف */
    align-items: center;
}

/* إضافة مساحة علوية لمنع تداخل المحتوى مع السهم */
.page-title {
    color: #000000; /* ذهبي ملكي */
    margin: 60px 0 30px 0; /* مساحة علوية كبيرة للسهم */
    text-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
    text-align: center;
    width: 100%;
}

/* المربعات الكبيرة (الوحدات الأساسية فقط تبقى متوهجة إذا أردتِ، أو نحذفها كما طلبتِ) */
/* هنا حذفت التوهج الدائم عن الكل وجعلته عند اللمس فقط */
.subject, .lesson-item, .grid-box {
    background-color: white;
    color: black;
    border-radius: 12px;
    font-weight: bold;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.3s ease;
    box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    border: 1px solid rgba(212, 175, 55, 0.2);
}

/* التوهج يظهر فقط عند تمرير الفأرة أو اللمس */
.subject:hover, .lesson-item:hover, .grid-box:hover {
    transform: translateY(-5px) scale(1.02);
    box-shadow: 0 0 20px rgba(255, 255, 255, 0.8);
    background-color: #fcfcfc;
}

/* شبكة المربعات (التواريخ والمصطلحات) - تنظيم احترافي للهاتف */
.grid-container {
    display: grid;
    /* المربعات ستكون بحجم 70px وتصغر تلقائياً في الشاشات الصغيرة */
    grid-template-columns: repeat(auto-fill, minmax(70px, 1fr));
    gap: 12px;
    width: 100%;
    max-width: 900px;
    padding: 10px;
    margin-bottom: 50px; /* مساحة في الأسفل */
}

/* ضمان أن المربعات الصغيرة تكون مربعة تماماً */
.grid-box {
    aspect-ratio: 1 / 1; 
    font-size: 1rem;
}

/* تنسيق الدروس والمستطيلات */
.lessons-stack {
    display: flex;
    flex-direction: column;
    gap: 15px;
    width: 100%;
    max-width: 600px;
    margin-bottom: 50px;
}

.lesson-item {
    padding: 20px;
    text-align: center;
    min-height: 60px;
    font-size: clamp(14px, 4vw, 18px); /* خط مرن للهاتف */
}

/* تحسين للهاتف فقط */
@media (max-width: 480px) {
    .grid-container {
        grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
        gap: 8px;
    }
    .page-title {
        font-size: 1.5rem;
    }
}
@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.1); }
    100% { transform: scale(1); }
}
/* الصفحة الثالثة: فصل المستطيل الصغير */
.extra-tools-btn {
    grid-column: 1 / -1; /* يأخذ العرض كاملاً */
    background: #6a4c93; /* بنفسجي */
    color: white;
    padding: 15px;
    border-radius: 15px;
    text-align: center;
    font-weight: bold;
    cursor: pointer;
    margin-top: 25px; /* مسافة ليفصل عن المواد */
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    border: 2px solid #ffffff33;
}

/* صفحة الـ To Do List */
#todoPage {
    background-color: #5267a1; /* Navy Blue */
    flex-direction: column;
    padding: 70px 20px 30px 20px;
    align-items: center;
    overflow-y: auto;
}

.hi-baby {
    font-size: 2.5rem;
    color: #ffd6ff;
    font-weight: bold;
    margin-bottom: 10px;
    animation: glowPulse 2s infinite ease-in-out;
}

@keyframes glowPulse {
    0% { text-shadow: 0 0 5px #414042; transform: scale(1); }
    50% { text-shadow: 0 0 25px #160f7c, 0 0 40px #160f7c; transform: scale(1.05); }
    100% { text-shadow: 0 0 5px #414042; transform: scale(1); }
}

.mood-section {
    color: #ccc;
    font-size: 1.1rem;
    margin-bottom: 30px;
}

.mood-input {
    background: transparent;
    border: none;
    border-bottom: 2px dotted #ffffff;
    color: white;
    width: 150px;
    outline: none;
    text-align: center;
}

/* مستطيل القائمة الكبير (ورقة الكراس) */
.notebook-container {
    width: 100%;
    max-width: 450px;
    margin-bottom: 30px;
}

.todo-label {
    background: #160f7c; /* أسود */
    color: white;
    padding: 10px;
    border-radius: 12px 12px 0 0;
    font-weight: bold;
    text-align: center;
    border: 1px solid #444;
}

.paper {
    background: white;
    background-image: linear-gradient(#91defd 1px, transparent 1px), linear-gradient(90deg, #f19999 1px, transparent 1px);
    background-size: 100% 30px, 30px 100%;
    background-position: 0 0, 40px 0;
    border-radius: 0 0 12px 12px;
    padding: 10px 10px 10px 50px;
    min-height: 250px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.5);
}

.paper textarea {
    width: 100%;
    height: 230px;
    border: none;
    background: transparent;
    line-height: 30px;
    font-family: 'Arial', sans-serif;
    font-size: 18px;
    color: #333;
    resize: none;
    outline: none;
    overflow-y: scroll; /* سهم الـ Scroll */
}


.btn-choice {
    padding: 10px 25px;
    margin: 10px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
    font-weight: bold;
    transition: 0.3s;
}

.btn-yes { background: #160f7c; color: white; }
.btn-no { background: #160f7c; color: white; }

.response-text {
    margin-top: 15px;
    min-height: 25px;
    font-weight: 600;
    color: #ffd6ff;
}

/* تنسيق ورقة الكراس المخططة */
.paper {
    background: white;
    /* رسم الخطوط السوداء الأفقية */
    background-image: linear-gradient(#e0e0e0 1px, transparent 1px);
    background-size: 100% 30px; /* المسافة بين كل سطر وسطر 30px */
    border-radius: 0 0 12px 12px;
    padding: 0 10px 10px 50px; /* مساحة 50px من اليسار للهامش */
    min-height: 300px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.5);
    position: relative;
    border-left: 1px solid #ddd;
}
.paper textarea {
    width: 100%;
    height: 280px;
    border: none;
    background: transparent;
    /* أهم جزء: جعل طول السطر متناسق مع طول سطر الخلفية */
    line-height: 30px; 
    font-family: 'Courier New', Courier, monospace; /* خط يشبه الكتابة اليدوية */
    font-size: 18px;
    color: #222; /* لون الكتابة أسود داكن */
    resize: none;
    outline: none;
    padding-top: 0;
    overflow-y: scroll;
}
/* صفحة البومودورو الجديدة */
#pomodoroPage {
    background-color: #0a1a2f; /* Navy Blue */
    flex-direction: column;
    padding: 80px 20px;
    align-items: center;
    color: white;
}

.pomo-title {
    font-size: 3rem;
    font-weight: bold;
    color: #ffd6ff;
    text-shadow: 0 0 20px #6a4c93;
    margin-bottom: 30px;
    animation: glowPulse 2s infinite;
}

/* عداد الوقت الكلي (اليوم) */
.total-study-time {
    position: absolute;
    top: 80px;
    right: 20px;
    background: white;
    color: #0a1a2f;
    padding: 10px;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    box-shadow: 0 0 15px rgba(255,255,255,0.3);
}

.total-study-time span { font-weight: bold; font-size: 1.1rem; }
.reset-total { cursor: pointer; font-size: 1.2rem; margin-top: 5px; transition: 0.3s; }
.reset-total:hover { transform: rotate(-180deg); color: #6a4c93; }

/* مربعات الوقت */
.pomo-container {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
    max-width: 800px;
}

.pomo-card {
    background: #1e2a3a;
    border: 2px solid #6a4c93;
    border-radius: 20px;
    padding: 25px;
    width: 320px;
    text-align: center;
    transition: 0.3s;
}

.pomo-card:hover { border-color: #ffd6ff; transform: translateY(-5px); }

.pomo-card h3 { margin-bottom: 15px; font-size: 1.3rem; color: #ffd6ff; }

.timer-display {
    font-size: 3rem;
    font-family: monospace;
    margin: 15px 0;
    color: white;
}

.pomo-divider {
    height: 2px;
    background: linear-gradient(90deg, transparent, #6a4c93, transparent);
    margin: 15px 0;
}

.time-input {
    background: transparent;
    border: none;
    border-bottom: 2px solid #6a4c93;
    color: white;
    font-size: 2rem;
    width: 100px;
    text-align: center;
    outline: none;
}

.pomo-btn {
    background: #6a4c93;
    color: white;
    border: none;
    padding: 10px 30px;
    border-radius: 50px;
    font-weight: bold;
    cursor: pointer;
    margin-top: 15px;
}

.pomo-btn:hover { background: #ffd6ff; color: #0a1a2f; 
}
.page {
    width: 100vw;
    height: 100vh;
    display: none; /* مخفية افتراضياً */
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
}

.page.active {
    display: flex !important; /* تظهر فقط عندما تأخذ الكلاس active */
}
/* تعديلات خاصة بالهواتف (الشاشات الأصغر من 600px) */
@media (max-width: 600px) {
    /* 1. جعل المربعات تظهر تحت بعضها بدلاً من بجانب بعض */
    .pomo-container {
        flex-direction: column;
        gap: 20px;
        padding: 10px;
        width: 95%;
    }

    /* 2. تصغير حجم المربعات لتناسب عرض شاشة الهاتف */
    .pomo-card {
        width: 100% !important;
        min-width: unset !important;
        padding: 15px;
    }

    /* 3. تصغير الخطوط لكي لا تخرج عن الإطار */
    .timer-display {
        font-size: 3rem !important; /* تصغير وقت العداد */
    }

    .pomo-title {
        font-size: 2.5rem !important;
        margin-bottom: 15px;
    }

    /* 4. جعل الأزرار أسهل للمس بالأصبع */
    .pomo-btn {
        width: 100%;
        padding: 12px;
        font-size: 1rem;
    }

    /* 5. تعديل مكان المربع الأبيض (الوقت الكلي) */
    .total-study-time {
        top: 10px;
        right: 10px;
        padding: 8px 12px;
        font-size: 0.9rem;
    }
}
@keyframes pulse-geo {
    0% { transform: scale(1); opacity: 1; }
    50% { transform: scale(1.1); opacity: 0.8; }
    100% { transform: scale(1); opacity: 1; }
}

.pulsing-text-geo {
    animation: pulse-geo 1.5s infinite;
    display: inline-block; /* ضروري لكي يعمل التكبير بشكل صحيح */
}
/* ستايل المربعات البيضاء الفخمة */
.history-lesson-card {
    background: #ffffff;
    color: #3e2723;
    padding: 25px;
    border-radius: 15px;
    font-weight: bold;
    font-size: 1.2rem;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    width: 100%;
    border: 2px solid transparent;
}

/* تأثير عند تقريب الفأرة أو اللمس */
.history-lesson-card:hover {
    transform: scale(1.05); /* تكبير الحجم قليلاً */
    box-shadow: 0 0 20px rgba(255, 255, 255, 0.6); /* توهج أبيض */
    background: #fdfdfd;
    border-color: #d7ccc8;
}

/* لضمان التجاوب مع الهواتف */
@media (max-width: 600px) {
    .history-lesson-card {
        font-size: 1rem;
        padding: 20px;
    }
}
/* نظام الشبكة للمربعات */
.lesson-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* 3 أعمدة في الحاسوب */
    gap: 20px;
    width: 100%;
    max-width: 500px;
    margin: 0 auto;
}

/* ستايل المربع البني الفاتح */
.part-box {
    background: #8d6e63; /* بني فاتح */
    color: white;
    aspect-ratio: 1 / 1; /* يجعله مربعاً تماماً */
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    font-weight: bold;
    border-radius: 15px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 10px rgba(0,0,0,0.3);
}

/* تأثير التوهج والتكبير */
.part-box:hover {
    transform: scale(1.1);
    background: #a1887f; /* تفتيح اللون قليلاً عند الحوم */
    box-shadow: 0 0 20px rgba(255, 255, 255, 0.5); /* توهج أبيض */
}

/* تعديل للهواتف: نخليهم مربعات في صفين أو 3 حسب الشاشة */
@media (max-width: 480px) {
    .lesson-grid {
        grid-template-columns: repeat(2, 1fr); /* مربعين في الصف في الهواتف الصغيرة */
        gap: 15px;
    }
    .part-box {
        font-size: 1.5rem;
    }
}
.solution-card {
    background: #ffffff;
    color: #3e2723;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    text-align: right;
    direction: rtl;
}
.solution-card h3 {
    border-bottom: 2px solid #8d6e63;
    padding-bottom: 10px;
    margin-bottom: 10px;
    color: #1b0000;
}
.solution-card ul {
    list-style-type: square;
    padding-right: 20px;
}
.solution-card li {
    margin-bottom: 8px;
    line-height: 1.4;
}
/* لضمان التجاوب */
@media (max-width: 600px) {
    .solution-card { font-size: 0.9rem; padding: 15px; }
}
/* تأكد أن الصفحة تقبل التمرير ولا تخفي المحتوى */
.page {
    -webkit-overflow-scrolling: touch; /* تمرير ناعم في الآيفون */
}

/* تنسيق منطقة التحدي لتبدو أفضل في الهاتف */
.challenge-section {
    padding: 20px;
    margin-bottom: 50px; /* مساحة في الأسفل لكي لا يختفي الزر تحت الشاشة */
}

.solution-card h3 {
    font-size: 1.1rem;
    line-height: 1.6;
}
</style>
</style>
</head>

<meta name="viewport" content="width=device-width, initial-scale=1.0">
<body>

<!-- ===== Back Arrow ===== -->
<div class="back" id="backBtn">←</div>

<!-- ===== Page 1 ===== -->
<div class="page active" id="page1">
    <div class="card">
        <!-- hearts -->
        <div class="heart" style="top:10%; left:15%;">🤍</div>
        <div class="heart" style="top:30%; right:20%;">🤍</div>
        <div class="heart" style="bottom:20%; left:25%;">🤍</div>
        <div class="heart" style="bottom:10%; right:15%;">🤍</div>
        <div class="heart" style="top:5%; left:10%;">🤍</div>
        <div class="heart" style="top:15%; right:25%;">🤍</div>
        <div class="heart" style="top:40%; left:50%;">🤍</div>
        <div class="heart" style="top:60%; right:10%;">🤍</div>
        <div class="heart" style="bottom:5%; left:40%;">🤍</div>
        <div class="heart" style="bottom:20%; right:30%;">🤍</div>
        <div class="heart" style="top:25%; left:70%;">🤍</div>
        <div class="title">💙 Welcome my baby 💙</div>
        <div class="click" id="goPage2">click here</div>
    </div>
</div>

<!-- ===== Page 2 ===== -->
<div class="page" id="page2">
    <div class="text">
        Welcome, my love, to your own special world, created with all my love just for you.<br><br>
        My idea was to support you in every possible way and to show you that you will never walk your path alone.
        I hope this site will be useful to you and help you along the way.<br><br>
        This is my way of saying: I am here, I support you, and I love you — always. 💙
        <div class="pulse" id="goPage3">Come here my heart</div>
    </div>
</div>
<!-- ===== Page 3 ===== -->
<div class="page" id="page3">
    <div class="subject" style="width: 100%; max-width: 600px; margin-top: 20px; background: white; color: black;" onclick="showPage('todoPage')">
    To-Do List / Pomodoro 📝
</div>
    <div class="subjects-container">
        <div class="subject">رياضيات</div>
        <div class="subject">فيزياء</div>
        <div class="subject">هندسة ميكانيكية</div>
        <div class="subject">لغة عربية</div>
        <div class="subject">لغة فرنسية</div>
        <div class="subject">لغة انجليزية</div>
        <div class="subject">علوم اسلامية</div>
        <div class="subject">التاريخ</div>
        <div class="subject">الجغرافيا</div>
        <div class="subject">الفلسفة</div>
    </div>
</div>
<div class="page" id="pageHistory">
    <h1 class="history-title">التاريخ</h1>
    <div class="subjects-container">
        <div class="subject" onclick="showUnit('coldWar')">حركات التحرر</div>
        <div class="subject" onclick="showUnit('revolution')">الثورة التحريرية</div>
        <div class="subject" onclick="showUnit('liberation')">الحرب الباردة</div>
    </div>
</div>

<div class="page" id="pageUnitContent">
    <h1 id="unitTitle" class="history-title" style="color: white;"></h1>
    <div class="subjects-container">
        <div class="subject" onclick="showDetail('characters')">الشخصيات</div>
        <div class="subject" onclick="showDetail('dates')">التواريخ</div>
        <div class="subject" onclick="showDetail('terms')">المصطلحات</div>
        <div class="subject" onclick="showDetail('lessons')">الدروس</div>
    </div>
</div>
<div class="page" id="historyUnitsPage">
    <h1 class="page-title">مادة التاريخ</h1>
    <div class="subjects-container">
        <div class="subject" onclick="showSubMenu('حركات التحرر')">حركات التحرر</div>
        <div class="subject" onclick="showSubMenu('الثورة التحريرية')">الثورة التحريرية</div>
        <div class="subject" onclick="showSubMenu('الحرب الباردة')">الحرب الباردة</div>
    </div>
</div>

<div class="page" id="unitSubMenuPage">
    <h1 id="unitMenuTitle" class="page-title"></h1>
    <div class="subjects-container">
        <div class="subject" onclick="showDetailsGrid('شخصيات', 40)">الشخصيات</div>
        <div class="subject" onclick="showDetailsGrid('تواريخ', 60)">التواريخ</div>
        <div class="subject" onclick="showDetailsGrid('مصطلحات', 80)">المصطلحات</div>
        <div class="subject" id="lessonsBtn">الدروس</div>
    </div>
</div>

<div class="page" id="gridPage">
    <h1 id="gridTitle" class="page-title"></h1>
    <div class="grid-container" id="gridItems"></div>
</div>

<div class="page" id="lessonsListPage">
    <h1 class="page-title">دروس الحرب الباردة</h1>
    <div class="lessons-stack">
        <div class="lesson-item" onclick="showLessonParts('الدرس 1', 7)">الدرس الأول: بروز الصراع و تشكل العالم</div>
        <div class="lesson-item" onclick="showLessonParts('الدرس 2', 9)">الدرس الثاني: مساعي الإنفراج الدولي</div>
        <div class="lesson-item" onclick="showLessonParts('الدرس 3', 4)">الدرس الثالث: من الثنائية إلى الأحادية القطبية</div>
    </div>
</div>
<div class="page" id="yaltaPage" style="background: radial-gradient(circle, #4f9e05 0%, #4f9e05 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title">تحدي التواريخ</h1>
    
    <div style="display: flex; flex-direction: column; align-items: center; width: 100%; gap: 20px; margin-top: 40px;">
        <div id="yaltaQuestion" class="lesson-detail-item" style="max-width: 500px; cursor: default; border-right: none; border-bottom: 5px solid #4f9e05;">
            اذكر تاريخ انعقاد مؤتمر يالطا
        </div>

        <div style="display: flex; gap: 15px; width: 100%; max-width: 500px;">
            <div class="subject" onclick="showYaltaAnswer()" style="flex: 1; min-height: 60px; background-color: #ffffff; color: rgb(0, 0, 0);">Show</div>
            <div class="subject" onclick="goToLovePage()" style="flex: 1; min-height: 60px; background-color: #ffffff; color: rgb(0, 0, 0);">Done</div>
        </div>

        <div id="yaltaAnswerArea" style="display: none; text-align: center;">
            <div id="yaltaAnswer" class="lesson-detail-item" style="background-color: #f0f0f0; color: #000000;">
             04-11 /02  /1945
            </div>
            <p style="color: white; font-style: italic; margin-top: 10px; font-size: 1.2rem;">Try again my honey 💕</p>
        </div>
    </div>
</div>

<div class="page" id="lovePage" style="background-color: #e492a0; flex-direction: column; text-align: center;">
    <h1 style="color: red; font-size: clamp(30px, 8vw, 60px); font-family: 'Playfair Display', serif; animation: pulse 1s infinite;">
        Mwah my baby ❤️
    </h1>
</div>
<div class="page" id="hiroshimaPage" style="background: radial-gradient(circle, #046638 0%, #95cfb0 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title">تحدي التواريخ</h1>
    
    <div style="display: flex; flex-direction: column; align-items: center; width: 100%; gap: 20px; margin-top: 40px;">
        <div class="lesson-detail-item" style="max-width: 500px; cursor: default; border-right: none; border-bottom: 5px solid #062c1a;">
            متى تم تفجير القنبلة الذرية على هيروشيما؟
        </div>

        <div style="display: flex; gap: 15px; width: 100%; max-width: 500px;">
            <div class="subject" onclick="showHiroshimaAnswer()" style="flex: 1; min-height: 60px; background-color: #d4af37; color: white;">Show</div>
            <div class="subject" onclick="goToLovePage()" style="flex: 1; min-height: 60px; background-color: #062c1a; color: white;">Done</div>
        </div>

        <div id="hiroshimaAnswerArea" style="display: none; text-align: center; width: 100%;">
            <div class="lesson-detail-item" style="background-color: #f0f0f0; color: #062c1a; margin: 0 auto; max-width: 500px;">
                06 /08 /1945 
            </div>
            <p style="color: white; font-style: italic; margin-top: 15px; font-size: 1.2rem;">Try again my honey 💕</p>
        </div>
    </div>
</div>
<div class="page" id="hitlerPage" style="background: radial-gradient(circle, #2c0466 0%, #a3b9c8 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #ffd6ff;">تعريف الشخصيات</h1>
    
    <div style="display: flex; flex-direction: column; align-items: center; width: 100%; gap: 20px; margin-top: 40px;">
        <div class="lesson-detail-item" style="max-width: 500px; cursor: default; border-right: none; border-bottom: 5px solid ;">
            أدولف هتلر
        </div>

        <div style="display: flex; gap: 15px; width: 100%; max-width: 500px;">
            <div class="subject" onclick="showHitlerAnswer()" style="flex: 1; min-height: 60px; background-color: #6a4c93; color: white;">Show</div>
            <div class="subject" onclick="showIlysmPage()" style="flex: 1; min-height: 60px; background-color: #2c0466; color: white;">Done</div>
        </div>

        <div id="hitlerAnswerArea" style="display: none; text-align: center; width: 100%;">
            <div class="lesson-detail-item" style="background-color: #f0f0f0; color: #2c0466; margin: 0 auto; max-width: 500px; font-size: 0.95rem; line-height: 1.6;">
                حاكم ألمانيا النازية، زعيم و مؤسس حزب العمال الألماني الإشتراكي، شهدت فترته توسعات ألمانيا ما تسبب في الحرب العالمية الثانية
            </div>
            <p style="color: white; font-style: italic; margin-top: 15px; font-size: 1.2rem;">keep going sweetie 💌</p>
        </div>
    </div>
</div>

<div class="page" id="ilysmPage" style="background-color: #ffc0cb; flex-direction: column; justify-content: center; align-items: center;">
    <h1 style="color: #ff4d6d; font-size: clamp(30px, 10vw, 70px); text-align: center; animation: pulse 1s infinite;">
        ilysm ❤️
    </h1>
</div>
<div class="page" id="termPage" style="background: radial-gradient(circle, #1a2a6c 0%, #1a2a6c 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #ffd6ff;">قاموس المصطلحات</h1>
    
    <div style="display: flex; flex-direction: column; align-items: center; width: 100%; gap: 20px; margin-top: 40px;">
        <div id="termNameDisplay" class="lesson-detail-item" style="max-width: 500px; cursor: default; border-right: none; border-bottom: 5px solid #1a2a6c; color: #000; font-weight: bold;">
            </div>

        <div style="display: flex; gap: 15px; width: 100%; max-width: 500px;">
            <div class="subject" onclick="showTermAnswer()" style="flex: 1; min-height: 60px; background-color: #ffffff; color: #1a2a6c; border-radius: 15px;">Show</div>
            <div class="subject" onclick="showIlysmPage()" style="flex: 1; min-height: 60px; background-color: #ffffff; color: #1a2a6c; border-radius: 15px;">Done</div>
        </div>

        <div id="termAnswerArea" style="display: none; text-align: center; width: 100%;">
            <div id="termDescDisplay" class="lesson-detail-item" style="background-color: #f0f0f0; color: #000000; margin: 0 auto; max-width: 500px; font-size: 0.95rem; line-height: 1.6; border-right: none; border-left: 5px solid;">
                </div>
            <p style="color: white; font-style: italic; margin-top: 15px; font-size: 1.1rem; text-shadow: 1px 1px 2px rgba(0,0,0,0.5);">
                you're doing great my heart 😔💙
            </p>
        </div>
    </div>
</div>
<div class="page" id="dzDatesPage" style="background-color: #f0f2f5; flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #000; ">تواريخ الثورة الجزائرية 🇩🇿</h1>
    
    <div style="display: flex; flex-direction: column; align-items: center; width: 100%; gap: 20px; margin-top: 40px;">
        <div id="dzQuestion" class="lesson-detail-item" style="max-width: 500px; background: #f0f2f5; color: #000;  cursor: default;">
            </div>

        <div style="display: flex; gap: 15px; width: 100%; max-width: 500px;">
            <div class="subject" onclick="showDzAnswer()" style="flex: 1; background-color: #000; color: #f0f2f5; border-radius: 10px;">Show</div>
            <div class="subject" onclick="showInLovePage()" style="flex: 1; background-color: #333; color: #f0f2f5; border-radius: 10px;">Done</div>
        </div>

        <div id="dzAnswerArea" style="display: none; text-align: center; width: 100%;">
            <div id="dzAnswerDisplay" class="lesson-detail-item" style="background-color: #f0f2f5; color: #000;  margin: 0 auto; max-width: 500px; font-weight: bold; font-size: 1.4rem;">
                </div>
            <p style="color: #302f2f; font-style: italic; margin-top: 15px;">keep going my baby 😙❤️</p>
        </div>
    </div>
</div>

<div class="page" id="inLovePage" style="background-color: #6faac2; flex-direction: column; justify-content: center; align-items: center;">
    <h1 style="color: #e21668; font-size: clamp(30px, 8vw, 60px); text-align: center; animation: pulse 1.2s infinite; font-family: 'Arial', sans-serif; text-shadow: 2px 2px 10px rgba(255,255,255,0.5);">
        I'm in love with you 💙
    </h1>
</div>
<div class="page" id="dzCharactersPage" style="background: radial-gradient(circle, #063a1e 0%, #0c5c31 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #ffffff;">تعريف شخصيات الثورة</h1>
    
    <div style="display: flex; flex-direction: column; align-items: center; width: 100%; gap: 20px; margin-top: 40px;">
        <div id="dzCharName" class="lesson-detail-item" style="max-width: 500px; cursor: default;  color: black;">
            </div>

        <div style="display: flex; gap: 15px; width: 100%; max-width: 500px;">
            <div class="subject" onclick="showDzCharAnswer()" style="flex: 1; min-height: 60px; background-color: #d4af37; color: rgb(0, 0, 0);">Show</div>
            <div class="subject" onclick="showAmwahPage()" style="flex: 1; min-height: 60px; background-color: #d4af37; color: #000000;">Done</div>
        </div>

        <div id="dzCharAnswerArea" style="display: none; text-align: center; width: 100%;">
            <div id="dzCharDesc" class="lesson-detail-item" style="background-color: #000000; color: #063a1e; margin: 0 auto; max-width: 500px; font-size: 0.95rem; line-height: 1.6;">
                </div>
            <p style="color: white; font-style: italic; margin-top: 15px; font-size: 1.2rem;">You're doing great, my hero!❤️</p>
        </div>
    </div>
</div>
<div class="page" id="amwahPage" style="background-color: #6d6b6b; flex-direction: column; justify-content: center; align-items: center;">
    <h1 style="color: #e21668; font-size: clamp(30px, 8vw, 60px); text-align: center; animation: pulse 1.2s infinite; font-family: 'Arial', sans-serif; text-shadow: 2px 2px 10px rgba(255,255,255,0.5);">
       اااااااااامممممممموووووووووواااااااااااححححححححح❤️
</div>
</div>
<div class="page" id="geoUnitsPage" style="background: radial-gradient(circle, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8;">مادة الجغرافيا</h1>
    <div class="subjects-container">
        <div class="subject" style="background: #5d4037; color: #fff;" onclick="showGeoSubMenu('واقع الاقتصاد العالمي')">واقع الاقتصاد العالمي</div>
        <div class="subject" style="background: #5d4037; color: #fff;" onclick="showGeoSubMenu('القوى الاقتصادية الكبرى في العالم')">القوى الاقتصادية الكبرى في العالم</div>
        <div class="subject" style="background: #5d4037; color: #fff;" onclick="showGeoSubMenu('الوحدة الثالثة')">الوحدة الثالثة</div>
    </div>
</div>

<div class="page" id="geoSubMenuPage" style="background: radial-gradient(circle, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 id="geoUnitMenuTitle" class="page-title" style="color: #d7ccc8;"></h1>
    <div class="subjects-container">
        <div class="subject" style="background: #8d6e63; color: #fff;" id="geoTermsBtn">المصطلحات</div>
        <div class="subject" style="background: #8d6e63; color: #fff;" id="geoLessonsBtn">الدروس</div>
    </div>
</div>

<div class="page" id="geoLessonsListPage" style="background: radial-gradient(circle, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 id="geoLessonsTitle" class="page-title" style="color: #d7ccc8;">الدروس</h1>
    <div class="lessons-stack" id="geoLessonsStack">
        </div>
</div>
<div class="page" id="iLoveYouGeoPage" style="background-color: #5d4037; flex-direction: column; justify-content: center; align-items: center;">
    <h1 style="color: #d7ccc8; font-size: clamp(30px, 10vw, 70px); text-align: center; animation: pulse 1s infinite; font-family: 'Cairo', sans-serif;">
        أحبك ❤️
    </h1>
</div>
<div class="page" id="todoPage">
    <div class="hi-baby">Hi my baby</div>
    <div class="mood-section">
        how are you today? <input type="text" class="mood-input" placeholder="..........">
    </div>
    <div class="notebook-container">
        <div class="todo-label">To Do List</div>
        <div class="paper">
            <textarea placeholder="Write your tasks here..."></textarea>
        </div>
    </div>
    <div class="ask-section">
        <p style="color: white; margin-bottom: 10px;">درت ڨع واش كتبت قلبي؟</p>
        <button class="btn-choice btn-yes" onclick="answerTodo('yes')">Yes</button>
        <button class="btn-choice btn-no" onclick="answerTodo('no')">No</button>
        <div id="todoResponse" class="response-text"></div>
    </div>
    <div class="pomo-box" onclick="showPage('pomodoroPage')" style="cursor: pointer; border: 2px solid #ffd6ff; background: rgba(106, 76, 147, 0.2); padding: 15px; border-radius: 15px; margin-top: 20px; width: 100%; max-width: 450px; text-align: center;">
        <h3 style="color: #ffd6ff; margin: 0;">⏳ Pomodoro Timer</h3>
    </div>
</div>

<div class="page" id="pomodoroPage">
    <div class="total-study-time">
        <span id="totalDisplay">00:00:00</span>
        <div class="reset-total" onclick="resetTotalStudyTime()">🔃</div>
    </div>

    <h1 class="pomo-title">Pomodoro</h1>

    <div class="pomo-container">
        <div class="pomo-card" id="studyCard">
            <h3>بدا تقرا حبيبي</h3>
            <div class="pomo-divider"></div>
            <div id="studyDisplay" class="timer-display">25:00</div>
            
            <div id="studyControls">
                <button class="pomo-btn" id="studyStartBtn" onclick="startTimer('study')">Start</button>
                <div id="studyPauseOptions" style="display:none; gap:10px; justify-content:center; margin-top:15px;">
                    <button class="pomo-btn" style="background:#4caf50" onclick="continueTimer('study')">Continue</button>
                    <button class="pomo-btn" style="background:#f44336" onclick="resetTimer('study')">Done</button>
                </div>
            </div>
            <input type="number" id="studyInput" class="time-input" placeholder="25" style="margin-top:10px; font-size:1rem; width:60px;">
        </div>

        <div class="pomo-card" id="breakCard">
            <h3>ريح شوية يا البطل الخارق😔</h3>
            <div class="pomo-divider"></div>
            <div id="breakDisplay" class="timer-display">05:00</div>
            
            <div id="breakControls">
                <button class="pomo-btn" id="breakStartBtn" onclick="startTimer('break')">Start</button>
                <div id="breakPauseOptions" style="display:none; justify-content:center; margin-top:15px;">
                    <button class="pomo-btn" style="background:#f44336" onclick="resetTimer('break')">Done</button>
                </div>
            </div>
            <input type="number" id="breakInput" class="time-input" placeholder="5" style="margin-top:10px; font-size:1rem; width:60px;">
        </div>
    </div>
</div>
<div class="page" id="geoSuccessPage" style="background-color: #8d6e63; display: none; flex-direction: column; justify-content: center; align-items: center; text-align: center; width: 100%; height: 100vh; position: fixed; top: 0; left: 0; z-index: 1000;">
    <h1 class="pulsing-text-geo" style="color: #fff; font-size: clamp(25px, 7vw, 50px); font-family: 'Cairo', sans-serif; line-height: 1.6; padding: 20px;">
        ساجي ولدي هاك بوسة 😗❤️
    </h1>
</div>
</div>
<div class="page" id="geoUnit2Page" style="background-color: #5d4037; display: none; flex-direction: column; justify-content: center; align-items: center; text-align: center; width: 100%; height: 100vh; position: fixed; top: 0; left: 0; z-index: 1000;">
    <h1 class="pulsing-text-geo" style="color: #fff; font-size: clamp(30px, 8vw, 60px); font-family: 'Cairo', sans-serif;">
        أحبك ❤️
    </h1>
</div>
<div class="page" id="geoUnit3Page" style="background-color: #3e2723; display: none; flex-direction: column; justify-content: center; align-items: center; text-align: center; width: 100%; height: 100vh; position: fixed; top: 0; left: 0; z-index: 1000;">
    <h1 class="pulsing-text-geo" style="color: #fff; font-size: clamp(30px, 8vw, 60px); font-family: 'Cairo', sans-serif;">
        i love you ❤️
    </h1>
</div>
<div class="page" id="historyLessonsPage" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8; font-family: 'Cairo', sans-serif; margin-bottom: 30px;">دروس الحرب الباردة</h1>
    
    <div class="subjects-container" style="gap: 20px; width: 100%; max-width: 600px;">
        <div class="history-lesson-card" onclick="showLessonParts('بروز الصراع وتشكّل العالم')">بروز الصراع و تشكل العالم</div>
        <div class="history-lesson-card" onclick="showLessonParts('مساعي الإنفراج الدولي')">مساعي الإنفراج الدولي</div>
        <div class="history-lesson-card" onclick="showLessonParts('من الثنائية إلى الأحادية القطبية')">من الثنائية إلى الأحادية القطبية</div>
    </div>
</div>
<div class="page" id="lesson1Page" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    
    <h1 class="page-title" style="color: #d7ccc8; font-family: 'Cairo', sans-serif; text-align: center; margin-bottom: 40px; font-size: clamp(1.5rem, 5vw, 2.5rem);">
        بروز الصراع وتشكل العالم
    </h1>

    <div class="lesson-grid">
        <div class="part-box" onclick="showPartDetail(1)">1</div>
        <div class="part-box" onclick="showPartDetail(2)">2</div>
        <div class="part-box" onclick="showPartDetail(3)">3</div>
        <div class="part-box" onclick="showPartDetail(4)">4</div>
        <div class="part-box" onclick="showPartDetail(5)">5</div>
        <div class="part-box" onclick="showPartDetail(6)">6</div>
        <div class="part-box" onclick="showPartDetail(7)">7</div>
    </div>
</div>
<div class="page" id="questionPage1" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8;">معايير تشكل العالم</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال: اذكر معايير تشكل العالم بعد الحرب العالمية الثانية؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem;" onclick="showPage('answerPage1')">الحل</div>
</div>

<div class="page" id="answerPage1" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
            <h3>المعايير التاريخية و السياسية:</h3>
            <ul>
                <li>القضاء على الأنظمة الديكتاتورية (الفاشية - النازية).</li>
                <li>تراجع القوى التقليدية الاستعمارية (فرنسا - بريطانيا) وبروز قوى جديدة (الـ و.م.أ - السوفيات).</li>
                <li>انقسام العالم إيديولوجيا وتجدد صراع الحرب الباردة.</li>
                <li>تغير الخريطة السياسية لأوروبا والعالم بعد ح ع 2.</li>
                <li>ظهور حركات التحرر في المستعمرات والاستقلال المبكر لبعض الدول.</li>
                <li>ظهور هيئة الأمم المتحدة 24 أكتوبر 1945 للحفاظ على السلم والأمن.</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>المعايير الإجتماعية و الإقتصادية:</h3>
            <ul>
                <li>انقسام العالم إلى شمال متقدم يعيش الرفاه وجنوب متخلف يعيش المشاكل الاجتماعية.</li>
                <li>خروج أوروبا مفلسة ومدمرة (الديون - دمار المصانع - توقف الإنتاج).</li>
                <li>الاستفادة المادية للو م أ من الحرب ع 2.</li>
                <li>بروز النظام المالي الجديد (بروتن وودز 1944/07/22) وصندوق النقد الدولي.</li>
                <li>تبني دول أوروبا الشرقية للنظام الاشتراكي.</li>
                <li>الخسائر البشرية الفادحة وانتشار الآفات الاجتماعية والفقر.</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>المعايير العلمية والتكنولوجية:</h3>
            <ul>
                <li>تطور الأسلحة واكتشاف السلاح النووي.</li>
                <li>تطور البحث العلمي ووسائل الإعلام والاتصال السلكية واللاسلكية.</li>
                <li>تطور البحوث العلمية في المجال الصحي وغزو الفضاء.</li>
            </ul>
        </div>

        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah()">واه</button>
                <button id="noBtn" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>
<div class="page" id="questionPage2" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto;">
    <h1 class="page-title" style="color: #d7ccc8; text-align: center;">طبيعة العلاقة بين الكتلتين</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال: حدد مظاهر صراع الحرب الباردة؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem; margin: 0 auto;" onclick="showPage('answerPage2')">الحل</div>
</div>

<div class="page" id="answerPage2" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">
    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
            <h3>علاقة صراع و توتر و تأزم ميزها:</h3>
            <ul>
                <li>السباق نحو التسلح بين القوتين.</li>
                <li>اعتماد الو م أ لسياسة ملء الفراغ الاستعمارية.</li>
                <li>انتهاج سياسة الاحتواء والتطويق ضد السوفيات لمنع انتشار الشيوعية.</li>
                <li>تبني سياسة المشاريع الاقتصادية والتكتلات الاقتصادية (مارشال - الكوميكون).</li>
                <li>انتشار الأزمات الدولية مثل أزمة (برلين - كوريا - كوبا - السويس).</li>
            </ul>
        </div>

        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah2()">واه</button>
                <button id="noBtn2" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse2" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>

<div class="page" id="questionPage3" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto;">
    <h1 class="page-title" style="color: #d7ccc8; text-align: center;"> أسباب صراع الحرب الباردة</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال: ماهي أسباب صراع الحرب الباردة ؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem; margin: 0 auto;" onclick="showPage('answerPage3')">الحل</div>
</div>

<div class="page" id="answerPage3" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">
    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
            <h3>أسباب صراع الحرب الباردة:</h3>
            <ul>
                <li>زوال مبررات التحالف بين النظامين الرأسمالي والاشتراكي بنهاية الحرب ع 2.</li>
                <li>السباق نحو التسلح واكتشاف الأسلحة النووية.</li>
                <li>الاختلاف الإيديولوجي بين المذهبين الرأسمالي والاشتراكي.</li>
                <li>القيادة المتشددة للقوتين الو.م.أ والسوفيات (هاري ترومان - جوزيف ستالين).</li>
                <li>اشتداد الصراع حول مناطق النفوذ واختلاف وتصادم المصالح بين القوتين.</li>
                <li>دعم السوفيات للأنظمة الشيوعية وأطماعه التوسعية في أوروبا والعالم.</li>
            </ul>
        </div>

        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah3()">واه</button>
                <button id="noBtn3" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse3" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>

<div class="page" id="questionPage4" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8;">استراتيجيات الكتلة الغربية</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال: اذكر استراتيجيات الكتلة الغربية؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem;" onclick="showPage('answerPage4')">الحل</div>
</div>
<div class="page" id="answerPage4" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
            <h3>الاستراتيجيات الاقتصادية:</h3>
            <ul>
                <li>التكتلات الاقتصادية بين دول المعسكر الغربي (تكثيف التعاون والتبادل التجاري).</li>
                <li>مقاطعة المعسكر الشرقي اقتصادياً وفرض الحصار الاقتصادي على بعض دوله (كوبا).</li>
                <li>المشاريع الاقتصادية: بتقديم قروض ومساعدات مالية لبعض الدول بهدف استقطابها إلى جانبها في صراعها ضد السوفيات مثل: (مشروع مارشال - مشروع ترومان - مشروع أيزنهاور).</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>الاستراتيجيات العسكرية:</h3>
            <ul>
                <li>السباق نحو التسلح (القنبلة النووية 1945 - الصواريخ الباليستية 1951) ودعم الانقلابات العسكرية.</li>
                <li>إقامة القواعد العسكرية في العالم لحماية مصالحها.</li>
                <li>إنشاء وكالة المخابرات الأمريكية CIA.</li>
                <li>سياسة إنشاء الأحلاف العسكرية: (حلف الشمال الأطلسي 04-04-1949، حلف الأنزوس 01-09-1951، حلف جنوب شرق آسيا 08-09-1954 وحلف بغداد 24-02-1955).</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>الاستراتيجيات السياسية:</h3>
            <ul>
                <li>اتباع سياسة الاستقطاب الدولي لكسب حلفاء جدد إلى جانبها.</li>
                <li>الإعلان عن مبدأ ترومان 12 مارس 1947 (التصريح بالتدخل العسكري الأمريكي في أي منطقة لحماية مصالحها).</li>
                <li>اتباع سياسة الاحتواء والتطويق ضد السوفيات للحد من انتشار المد الشيوعي.</li>
                <li>إثارة المعارضة ضد الأنظمة الشيوعية.</li>
                <li>إتباع سياسة ملء الفراغ (الاستعمارية) في بلدان العالم الثالث (الهند الصينية، فلسطين).</li>
            </ul>
        </div>

        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah4()">واه</button>
                <button id="noBtn" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse4" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>

<div class="page" id="questionPage5" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8;">استراتيجيات الكتلة الشرقية</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال: اذكر استراتيجيات الكتلة الشرقية؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem;" onclick="showPage('answerPage5')">الحل</div>
</div>
<div class="page" id="answerPage5" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
            <h3>الاستراتيجيات الاقتصادية:</h3>
            <ul>
                <li>مقاطعة منتجات المعسكر الغربي الرأسمالي تجارياً.</li>
                <li>إنشاء منظمة الكوميكون: (مجلس التعاون والتبادل التجاري الحر) 25 جانفي 1949 تضم: (السوفيات - منغوليا - بولونيا - رومانيا - المجر - بلغاريا - كوبا - تشيكوسلوفاكيا - ألمانيا الشرقية) جاءت رداً على مشروع مارشال ومن أهدافها: تكثيف التعاون التجاري الحر بين الدول الأعضاء، مواجهة المشاريع الغربية الرأسمالية، نشر الاشتراكية في العالم.</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>الاستراتيجيات العسكرية:</h3>
            <ul>
                <li>اتكثيف جهود المخابرات السوفياتية (KGB) وإنشاء فروع لها في الكثير من مناطق العالم.</li>
                <li>إقامة القواعد العسكرية .</li>
                <li>العمل على تطوير وتعزيز قدراته العسكرية (القنبلة النووية 1949 - الصواريخ الباليستية 1953).</li>
                <li>التدخل السوفياتي في أفغانستان 1979 بهدف دعم الحكومة الأفغانية الحليفة للسوفيات.</li>
                <li>تأسيس حلف وارسو: (معاهدة الصداقة والتعاون والمساعدة المشتركين) 14 ماي 1955 مقره بولونيا ويضم (السوفيات - بولونيا - بلغاريا - ألمانيا الشرقية - تشيكوسلوفاكيا - رومانيا - المجر) يهدف للسيطرة على أوروبا الشرقية ومواجهة تهديدات المعسكر الغربي خاصة بعد تأسيس الحلف الأطلسي.</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>الاستراتيجيات السياسية:</h3>
            <ul>
                <li>الإعلان عن مبدأ جدانوف: 22 سبتمبر 1947، أطلقه أندري جدانوف، قسّم من خلاله العالم إلى معسكر غربي رأسمالي استعماري ومعسكر شرقي شيوعي ديمقراطي يدعم حركات التحرر.</li>
                <li>تأسيس مكتب الكومنفورم: 06 أكتوبر 1947، هو مكتب استخبارات شيوعي، يضم 9 أحزاب شيوعية في أوروبا، يهدف لنشر الشيوعية، ودعم الأحزاب الشيوعية في العالم.</li>
                <li>دعم الحركات التحررية في العالم الثالث بهدف استقطابها.</li>
            </ul>
        </div>

        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah5()">واه</button>
                <button id="noBtn" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse5" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>

<div class="page" id="questionPage6" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8;">نتائج الصراع بين المعسكرين</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال: اذكر نتائج الصراع بين المعسكرين؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem;" onclick="showPage('answerPage6')">الحل</div>
</div>
<div class="page" id="answerPage6" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
            <h3>نتائجها على العالم الثالث</h3>
            <ul>
                <li>تحول دوله لمسرح صراع الحرب الباردة (السويس، كوريا، كوبا).</li>
                <li>الخسائر المادية والبشرية (حوالي 3 مليون قتيل في أزمة كوريا).</li>
                <li>تجزئة الوحدات السياسية لبعض دوله (تقسيم كوريا وفيتنام..).</li>
                <li>الهيمنة العسكرية والاقتصادية على دوله (الأحلاف، القواعد، المشاريع).</li>
                <li>تحول الصراع من (شرق - غرب) إلى (شمال - جنوب) بعد الحرب الباردة.</li>
                <li>استنزاف ثرواته الطبيعية وطاقاته البشرية.</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>نتائجها على قارة أوروبا</h3>
            <ul>
                <li>انقسام أوروبا إلى شرقية شيوعية وغربية رأسمالية.</li>
                <li>انقسام ألمانيا إلى ألمانيا شرقية شيوعية وألمانيا غربية رأسمالية.</li>
                <li>إقامة الأحلاف والقواعد العسكرية على أراضيها (حلف وارسو - الأطلسي).</li>
                <li>ربط اقتصادها بالاقتصاد الأمريكي (مشروع مارشال) والسوفياتي (الكوميكون).</li>
                <li>الهيمنة الأمريكية على أوروبا (الحلف الأطلسي) والسوفياتية (حلف وارسو).</li>
            </ul>
        </div>
        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah6()">واه</button>
                <button id="noBtn" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse6" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>

<div class="page" id="questionPage7" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; padding: 20px;">
    <h1 class="page-title" style="color: #d7ccc8;">أهداف الولايات المتحدة الأمريكية من إنشاء الأحلاف العسكرية</h1>
    <div class="history-lesson-card" style="cursor: default; background: #8d6e63; color: white; margin-bottom: 20px;">
        السؤال:بيّن أهداف الولايات المتحدة الأمريكية من إنشاء الأحلاف العسكرية؟
    </div>
    <div class="part-box" style="width: 150px; height: 60px; font-size: 1.2rem;" onclick="showPage('answerPage6')">الحل</div>
</div>
<div class="page" id="answerPage7" style="background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%); flex-direction: column; justify-content: flex-start; padding: 60px 20px 20px 20px; overflow-y: auto; height: 100vh;">    <div class="solution-container" style="width: 100%; max-width: 800px; display: flex; flex-direction: column; gap: 15px;">
        
        <div class="solution-card">
        <h3>الأهداف المعلنة</h3>
            <ul>
                <li>إرساء التعاون بين الدول الأعضاء.</li>
                <li>الخسائر المادية والبشرية (حوالي 3 مليون قتيل في أزمة كوريا).</li>
                <li>الدفاع المشترك بين الدول الأعضاء.</li>
                <li>الاستفادة من الخبرات العسكرية.</li>
            </ul>
        </div>

        <div class="solution-card">
            <h3>الأهداف الخفية</h3>
            <ul>
                <li>احتواء السوفيات ومنعه من نشر أيديولوجيته (الشيوعية).</li>
                <li>فرض الهيمنة الأمريكية على الدول الأعضاء في الأحلاف.</li>
                <li>حماية المصالح الأمريكية في مناطق إنشاء الأحلاف العسكرية.</li>
                <li>ربط اقتصادها بالاقتصاد الأمريكي (مشروع مارشال) والسوفياتي (الكوميكون).</li>
                <li>نشر الأيديولوجية الأمريكية (النظام الرأسمالي).</li>
            </ul>
        </div>
        <div class="challenge-section" style="text-align: center; margin-top: 30px; position: relative; min-height: 150px;">
            <p style="color: white; font-size: 1.3rem; font-weight: bold;">تحفظهم ڨع ياك 🙂</p>
            <div style="display: flex; justify-content: center; gap: 20px; margin-top: 15px;">
                <button class="btn-choice" style="background: #4caf50; padding: 10px 30px; border-radius: 10px; color: white; border: none; cursor: pointer;" onclick="answerWah7()">واه</button>
                <button id="noBtn" class="btn-choice" style="background: #f44336; padding: 10px 30px; border-radius: 10px; color: white; border: none; position: relative;">لاء</button>
            </div>
            <p id="wahResponse7" style="color: #ffd6ff; margin-top: 20px; font-weight: bold; display: none;">علابالي ولدي يساعفني ❤️</p>
        </div>
    </div>
</div>
<script>
    const appData = {
    "الحرب الباردة": {
        "شخصيات": {
    1: { name: "أدولف هتلر", desc: "حاكم ألمانيا النازية، زعيم ومؤسس حزب العمال الألماني الاشتراكي، حكم ألمانيا 1933-1945 شهدت فترته توسعات ألمانيا في شرق أوروبا ما تسبب في اندلاع الحرب ع 2." },
    2: { name: "بنيتو موسوليني", desc: "حاكم إيطاليا 1922-1944 شغل منصب رئيس الدولة ورئيس وزرائها، من مؤسسي الحركة الفاشية الإيطالية وزعمائها، من الشخصيات البارزة في الحرب ع 2." },
    3: { name: "جورج مارشال", desc: "جنرال ثم وزير خارجية الو.م. أ اقترن اسمه بمشروع اقتصادي لإعادة إعمار أوروبا بعد ح ع 2 'مشروع مارشال' جوان 1947 ويعتبر من رموز الحرب الباردة." },
    4: { name: "فرانكلين روزفلت", desc: "رئيس الو.م. أ (1933-1945)، شهدت فترته الحرب ع 2، ديمقراطي، الرئيس الوحيد الذي تولى الرئاسة لثلاث عهدات، كان له الفضل في حل أزمة 1929." },
    5: { name: "هاري ترومان", desc: "رئيس الو.م. أ بين 1945-1953 ديمقراطي، صاحب قرار تفجير القنبلة الذرية ضد اليابان، صاحب مبدأ ترومان 1947 تميز بتعصبه للرأسمالية وعدائه للشيوعية." },
    6: { name: "أيزنهاور", desc: "رئيس الو.م. أ 1953-1961 جمهوري، قائد الحلف الأطلسي سنة 1949، أنهى الحرب الكورية 1953، شهدت فترته أزمة السويس 1956، صاحب المشروع الذي يحمل اسمه." },
    7: { name: "جون كينيدي", desc: "رئيس الو.م. أ بين 1961-1963 ديمقراطي، صاحب مشروع أبولو الفضائي، شهدت فترته أزمة الصواريخ 1962، اغتيل 1963." },
    8: { name: "ريتشارد نيكسون", desc: "رئيس الو.م. أ بين 1969-1974 جمهوري، شهدت فترته انتهاء حرب الفيتنام وتوقيف تصدير النفط العربي 1973، وقع معاهدة سالت 1" },
    9: { name: "جيمي كارتر", desc: "رئيس الو.م. أ بين 1977-1981 ديمقراطي، وقع اتفاقية سالت الثانية مع السوفيات، شهدت فترته أزمة أفغانستان 1979." },
    10: { name: "رونالد ريغن", desc: "رئيس الو.م. أ بين 1981-1989 جمهوري، تميز بالتشدد تجاه الاتحاد السوفياتي وتعصبه للرأسمالية صاحب مشروع حرب النجوم." },
    11: { name: "جورج بوش الأب", desc: "رئيس الو.م. أ بين 1989-1993، وقع مع غورباتشوف اتفاقيات التعاون والإعلان عن نهاية الحرب الباردة، أعلن عن النظام العالمي الجديد، شهدت فترته حرب الخليج 1991." },
    12: { name: "ونستن تشرشل", desc: "رئيس وزراء بريطانيا لفترتين 1940-1945 ثم 1951-1955، ساهم في صمود بلاده أمام ألمانيا النازية خلال الحرب ع 2، وهو صاحب مصطلح الستار الحديدي للدلالة على انقسام أوروبا." },
    13: { name: "جوزيف ستالين", desc: "زعيم سوفياتي 1924-1953، من رموز الحرب الباردة تميزت فترة حكمه بالفردية والتشدد وعدائه للغرب، شهدت فترته أزمة برلين، وتأسيس مكتب الكومنفورم والكوميكون." },
    14: { name: "أندري جدانوف", desc: "سياسي سوفياتي صاحب أطروحة الكتلتين (الكتلة الشرقية- الكتلة الغربية) من رموز الحرب الباردة، صاحب مشروع جدانوف، من مؤسسي مكتب الكومنفورم 1947." },
    15: { name: "نيكيتا خروتشوف", desc: "سياسي سوفياتي، أحد قيادة الترويكا، صاحب مبادرة التعايش السلمي، أول زعيم سوفياتي يزور الو.م. أ، حدثت في عهده عدة أزمات أخطرها أزمة الصواريخ بكوبا 1962." },
    16: { name: "مالينكوف", desc: "رئيس وزراء السوفيات عقب وفاة ستالين، أجبره المكتب السياسي على التخلي عن منصب رئاسة الحزب الشيوعي لصالح خروتشوف." },
    17: { name: "بولغانين", desc: "سياسي سوفياتي، رئيس مجلس وزراء السوفيات، شغل منصب وزير الدفاع بعد وفاة ستالين 1953، كان حليفا لخروتشوف، ويعتبر من مؤيدي إصلاحات خروتشوف." },
    18: { name: "بريجنيف", desc: "زعيم السوفيات 1964-1982، خلف خروتشوف سنة 1964 عرفت فترته الكثير من الأزمات مثل أزمة براغ 1968 وأفغانستان 1979، وقع معاهدة سالت 1 و 2." },
    19: { name: "ميخائيل غورباتشوف", desc: "آخر زعيم للسوفيات 1985-1991 يعرف بمهندس الإصلاحات (البروسترويكا والغلاسنوست) كان وراء إنهاء صراع الحرب الباردة سنة 1989، حضر مؤتمري باريس ومالطا مع بوش." },
    20: { name: "صدام حسين", desc: "رئيس العراق 1979-2003، الأمين العام لحزب البعث العربي الاشتراكي، شهدت فترته حرب الخليج 1991، والغزو الأمريكي للعراق 2003." },
    21: { name: "جمال عبد الناصر", desc: "من الضباط الأحرار، رئيس الجمهورية المصرية 1954-1970 مؤمم قناة السويس 1956، من مؤسسي حركة عدم الانحياز 1961 والشخصيات البارزة في العالم الثالث ومدعمي حركات التحرر." },
    22: { name: "غاندي", desc: "سياسي هندي، ساهم في استقلال الهند 1947، مهندس فلسفة اللاعنف (العصيان المدني)، اغتيل عام 1948، يعتبر من زعماء وقادة العالم الثالث." },
    23: { name: "جوزيف بروز تيتو", desc: "سياسي يوغسلافي ورئيسها 1945-1980، قائد الحزب الشيوعي والمقاومة ضد النازية خلال الحرب ع 2، من مؤسسي حركة عدم الانحياز سنة 1961 ببلغراد." },
    24: { name: "جواهر لال نهرو", desc: "سياسي هندي، أحد زعماء حركة الاستقلال في الهند، رئيس وزراء الهند 1947-1964 من مؤسسي حركة عدم الانحياز 1961 ومدعمي حركات التحرر في العالم." },
    25: { name: "شي غيفارا", desc: "أرجنتيني الأصل من مناضلي الحركات الثورية في أمريكا اللاتينية، قاد الثورة الكوبية إلى جانب كاسترو شارك في ثورات عدة بأمريكا الجنوبية وافريقيا، حارب الرأسمالية الاحتكارية." },
    26: { name: "هوشي منه", desc: "سياسي فيتنامي، قائد الحركة التحررية في الهند الصينية ضد الاستعمار الفرنسي والأمريكي، مؤسس الحزب الشيوعي الفيتنامي 1931، أسس جمهورية فيتنام الشمالية بعد الاستقلال." },
    27: { name: "أحمد سوكارنو", desc: "سياسي أندونيسي، أحد زعماء حركة الاستقلال في بلاده، أول رئيس لأندونيسيا المستقلة، ترأس مؤتمر باندونغ 1955، من أبرز مؤسسي حركة عدم الانحياز 1961 وشخصيات العالم الثالث." },
    28: { name: "فيدال كاسترو", desc: "زعيم ثوري كوبي أطاح بنظام باتيستا العميل، أصبح رئيسا لكوبا سنة 1959 واجه الهيمنة الأمريكية بكوبا وشهدت فترته أزمة الصواريخ 1962 تخلى عن السلطة لأسباب صحية." },
    29: { name: "محمد علي جناح", desc: "رئيس باكستان بعد الاستقلال، ناضل لتحرير شبه القارة الهندية من الوجود البريطاني إلى جانب غاندي ونهرو، من مؤسسي حركة عدم الانحياز." }
        },
        "تواريخ": {
     1: { name: "11-4 فيفري 1945", date: "مؤتمر يالطا بين الو.م. أ - الإتحاد السوفياتي - بريطانيا." },
     2: { name: "17 جويلية - 02 أوت 1945", date: "مؤتمر بوتسدام (بريطانيا - السوفيات - الو.م. أ) أقر تقسيم ألمانيا." },
     3: { name: "9-6 أوت 1945", date: "تفجير قنبلتي هيروشيما وناكازاكي باليابان." },
     4: { name: "24 أكتوبر 1945", date: "تأسيس هيئة الأمم المتحدة." },
     5: { name: "12 مارس 1947", date: "الإعلان عن مبدأ هاري ترومان." },
     6: { name: "05 جوان 1947", date: "الإعلان عن مشروع جورج مارشال." },
     7: { name: "22 سبتمبر 1947", date: "الإعلان عن مبدأ جدانوف." },
     8: { name: "06 أكتوبر 1947", date: "إنشاء مكتب الكومنفورم." },
     9: { name: "03 جوان 1948", date: "اجتماع لندن وتأسيس حكومة رأسمالية في بون الألمانية." },
    10: { name: "23 جوان 1948", date: "حصار السوفيات لبرلين." },
    11: { name: "25 جوان 1948", date: "إنشاء جسر جوي إلى برلين وفك الحصار عنها." },
    12: { name: "25 جانفي 1949", date: "تأسيس منظمة الكوميكون." },
    13: { name: "08 ماي 1949", date: "تأسيس ألمانيا الغربية الرأسمالية الاتحادية عاصمتها بون." },
    14: { name: "12 ماي 1949", date: "رفع الحصار عن برلين." },
    15: { name: "07 أكتوبر 1949", date: "تأسيس ألمانيا الديمقراطية الشرقية الشيوعية عاصمتها برلين الشرقية." },
    16: { name: "04 أفريل 1949", date: "تأسيس حلف الشمال الأطلسي (الناتو)." },
    17: { name: "01 أكتوبر 1949", date: "نجاح الثورة الشيوعية الصينية." },
    18: { name: "25 جوان 1950", date: "اندلاع الحرب الكورية بغزو القسم الشمالي للجنوب." },
    19: { name: "01 سبتمبر 1951", date: "تأسيس حلف الأنزيوس." },
    20: { name: "05 مارس 1953", date: "وفاة الزعيم السوفياتي ستالين." },
    21: { name: "27 جويلية 1953", date: "نهاية الحرب الأهلية الكورية." },
    22: { name: "08 سبتمبر 1954", date: "تأسيس حلف جنوب شرق آسيا (السياتو)." },
    23: { name: "24 فيفري 1955", date: "تأسيس حلف بغداد." },
    24: { name: "24-18 أفريل 1955", date: "مؤتمر باندونغ." },
    25: { name: "05 ماي 1955", date: "اعتراف السوفيات بألمانيا الغربية الإتحادية." },      
    26: { name: "14 ماي 1955", date: "تأسيس حلف وارسو." },
    27: { name: "14 فيفري 1956", date: "تبني خروتشوف سياسة التعايش السلمي." },
    28: { name: "17 أفريل 1956", date: "حل مكتب الكومنفورم." },
    29: { name: "29 أكتوبر 1956", date: "العدوان الثلاثي على مصر." },
    30: { name: "05 نوفمبر 1956", date: "تهديد السوفيات باستعمال السلاح النووي ضد دول العدوان الثلاثي." },
    31: { name: "05 جانفي 1957", date: "الإعلان عن مشروع أيزنهاور." },
    32: { name: "13 أوت 1961", date: "بناء جدار برلين." },
    33: { name: "15-18 سبتمبر 1959", date: "زيارة خروتشوف إلى واشنطن." },
    34: { name: "1-6 سبتمبر 1961", date: "تأسيس حركة عدم الانحياز ببلغراد بيوغسلافيا." },
    35: { name: "07 فيفري 1962", date: "فرض الحصار الاقتصادي الأمريكي على كوبا." },
    36: { name: "22 أكتوبر 1962", date: "فرض الحصار العسكري الأمريكي على كوبا." },
    37: { name: "28 أكتوبر 1962", date: "قرار سحب السوفيات للصواريخ من كوبا ونهاية الأزمة الكوبية." },
    38: { name: "20 جوان 1963", date: "إنشاء الخط الهاتفي الأحمر." },
    39: { name: "26 ماي 1972", date: "توقيع اتفاقية سالت الأولى للحد من الأسلحة الاستراتيجية." },
    40: { name: "5-9 سبتمبر 1973", date: "المؤتمر الرابع لحركة عدم الانحياز بالجزائر." },
    41: { name: "18 جوان 1979", date: "توقيع اتفاقية سالت الثانية بفيينا." },
    42: { name: "27 ديسمبر 1979", date: "تدخل السوفيات عسكريا في أفغانستان." },
    43: { name: "3-4 ديسمبر 1989", date: "مؤتمر مالطا بين غورباتشوف وجورج بوش والإعلان عن زوال القطبية الثنائية." },
    44: { name: "09 نوفمبر 1989", date: "تحطيم جدار برلين." },
    45: { name: "03 أكتوبر 1990", date: "توحيد الألمانيتين." },
    46: { name: "19-21 نوفمبر 1990", date: "مؤتمر باريس وإعلان نهاية الحرب الباردة رسميا." },
    47: { name: "28 جوان 1991", date: "حل منظمة الكوميكون." },
    48: { name: "01 جويلية 1991", date: "حل حلف وارسو." },
    49: { name: "05 سبتمبر 1991", date: "حل الحزب الشيوعي السوفياتي." },
    50: { name: "21 ديسمبر 1991", date: "مؤتمر 'ألما آتا' وزوال الاتحاد السوفياتي وظهور الجمهوريات المستقلة." },
    51: { name: "25 ديسمبر 1991", date: "استقالة غورباتشوف من رئاسة الاتحاد السوفياتي." }
},
        "مصطلحات": {
    1: { name: "الحرب العالمية الثانية", desc: "نزاع عالمي (1939-1945) وقع بين دول الحلفاء (فرنسا-بريطانيا- الو.م. أ- السوفيات) ودول المحور (ألمانيا - إيطاليا- اليابان) بسبب فشل تسويات السلام بعد ح ع 1." },
    2: { name: "دول المحور", desc: "حلف عسكري خلال ح ع 2، تتألف دول المحور من ألمانيا وإيطاليا واليابان، انهزمت أمام قوات الحلفاء." },
    3: { name: "دول الحلفاء", desc: "حلف عسكري خلال ح ع 2، تتألف دول الحلفاء من فرنسا وبريطانيا والو.م. أ والسوفيات، انتصرت على دول المحور." },
    4: { name: "الفاشية", desc: "النظام الذي أسسه موسوليني بإيطاليا 1922، تقوم على تشجيع وتعزيز العسكرية والقومية المتطرفة، وتعتبر من الأنظمة الديكتاتورية التي ظهرت بأوروبا بعد ح ع 1." },
    5: { name: "النازية", desc: "ايديولوجية سياسية متطرفة مشابهة للفاشية تبناها حزب العمال الألماني الاشتراكي الذي كان هتلر من أعضائه المؤسسين، ظهرت بأوروبا بعد ح ع 1." },
    6: { name: "عالم الشمال", desc: "مجموعة الدول التي تمثل العالم المتقدم الصناعي والغني، ويضم الدول الرأسمالية والاشتراكية وتقع في النصف الشمالي للعالم إضافة لأستراليا ونيوزيلندا." },
    7: { name: "عالم الجنوب", desc: "مجموعة الدول التي تمثل العالم المتخلف الواقعة في الجزء الجنوبي للعالم ويضم دول إفريقيا وآسيا ودول أمريكا اللاتينية." },
    8: { name: "العالم الثالث", desc: "مصطلح أطلقه الفرنسي ألفريد صوفي على الدول حديثة العهد بالاستقلال والتي كانت تعاني من العجز الاقتصادي والتخلف في شتى الميادين بعد استقلالها." },
    9: { name: "العالم المتقدم", desc: "الدول الواقعة شمال العالم إضافة إلى أستراليا ونيوزيلندا، والتي تعيش تطور الاقتصادي والاجتماعي والحضاري وتتحكم في التكنولوجيا." },
    10: { name: "الليبرالية", desc: "مذهب يرتكز على مبدأ الحرية الفردية، من أهم مبادئه عدم تدخل الدولة في الشؤون الاقتصادية وترك المجال للأفراد وفق مبدأ دعه يعمل اتركه يمر." },
    11: { name: "الرأسمالية", desc: "نظام اقتصادي مبني على الملكية الخاصة لوسائل الانتاج والتوزيع والتبادل، يقوم فيه أصحاب المال بإدارة ملكياتهم بغية جني الأرباح." },
    12: { name: "الشيوعية", desc: "مذهب سياسي يقصد به سياسة الحزب الواحد ظهر بعد نجاح الثورة البلشفية 1917، تبناها السوفيات ودول شرق أوروبا بعد ح ع 2." },
    13: { name: "الاشتراكية", desc: "نظام اقتصادي سياسي ظهر بعد 1917 يعتمد على الملكية الجماعية لوسائل الانتاج والثروات الطبيعية، تبناها السوفيات ودول أوروبا الشرقية." },
    14: { name: "الاتحاد السوفياتي", desc: "جمهورية فيدرالية شيوعية في شرق أوروبا وشمال آسيا دامت من 1922 إلى 1991، كان مؤلفا من 15 جمهورية." },
    15: { name: "الاستعمار التقليدي", desc: "الاستعمار الذي ظهر بعد الثورة الصناعية تزعمته بريطانيا وفرنسا، استعملت فيه أساليب قمعية، تراجعت قوته بعد ح ع 2." },
    16: { name: "الامبرالية", desc: "هيمنة الو.م. أ وحلفائها على العالم وتوجيه العلاقات الدولية وفقا لمصالحها وهي أعلى مستويات الرأسمالية." },
    17: { name: "الشرق", desc: "يقصد به دول شرق أوروبا والصين والسوفيات وهي الدول التي تبنت النظام الاشتراكي بعد الحرب ع 2." },
    18: { name: "الغرب", desc: "الدول الرأسمالية التي تقع غرب أوروبا إضافة للو.م. أ وكندا والتي تبنت النظام الرأسمالي وتحالفت ضد المعسكر الشرقي." },
    19: { name: "سياسة الأحلاف", desc: "سياسة عسكرية لمواجهة الطرف الآخر عبر تحالف دولتين أو أكثر لمواجهة أي عدوان أو القيام بمناورات مشتركة مثل الناتو ووارسو." },
    20: { name: "مؤتمر بوتسدام", desc: "اجتماع زعماء الحلفاء (ستالين، ترومان، تشيرشل) بعد هزيمة ألمانيا لتقرير مصيرها وتنفيذ قرارات مؤتمر يالطا." },
    21: { name: "مؤتمر يالطا", desc: "مؤتمر بين رؤساء دول الحلفاء (تشيرشل، روزفلت، ستالين) ناقش كيفية تقسيم ألمانيا ومحاكمة النازيين." },
    22: { name: "الحلف الأطلسي", desc: "تكتل عسكري غربي تأسس 04 أفريل 1949 يهدف للدفاع المشترك والحد من انتشار الشيوعية، مقره بروكسل." },
    23: { name: "المجال الحيوي", desc: "سياسة تهدف لاستعمار مناطق خارج المجال الجغرافي لتأمين الطاقة والثروات، كانت سببا في اندلاع ح ع 2." },
    24: { name: "حلف وارسو", desc: "تكتل عسكري شرقي تأسس 14 ماي 1955، جاء رداً على سياسة الو.م. أ، مقره وارسو ببولونيا." },
    25: { name: "حلف جنوب شرق آسيا", desc: "تكتل عسكري غربي تأسس 1954 للوقوف في وجه المد الشيوعي، مقره الفلبيين." },
    26: { name: "حلف بغداد", desc: "تكتل عسكري غربي تأسس 1955 ضم بعض دول الشرق الأوسط للوقوف في وجه المد الشيوعي، مقره العراق." },
    27: { name: "الصراع الايديولوجي", desc: "صراع عقائدي فكري بين النظامين الشيوعي والرأسمالي، يقوم على استحالة تعايشهما في عالم واحد." },
    28: { name: "الإيديولوجية", desc: "يقصد بها الأفكار والمذاهب والعقائد والتوجهات الفكرية والسياسية." },
    29: { name: "سياسة ملء الفراغ", desc: "سياسة اتبعتها الو.م. أ لتحل محل القوى التقليدية (فرنسا وبريطانيا) في مستعمراتها بعد تراجع قوتهما." },
    30: { name: "صراع النفوذ", desc: "التنافس بين القوى العالمية على المجالات الجغرافية خارج أراضيها في افريقيا وآسيا وأمريكا اللاتينية." },
    31: { name: "سياسة التكتل", desc: "تحالف الدول في مجال أو أكثر (عسكري أو اقتصادي) لتعزيز التعاون بين الأعضاء مثل حلف وارسو والاتحاد الاوروبي." },
    32: { name: "سياسة المشاريع", desc: "سياسة أمريكية لاستقطاب الدول عبر مشاريع اقتصادية لمحاربة الشيوعية مثل مشروع مارشال وترومان." },
    33: { name: "الأزمات الدولية", desc: "فترات التوتر السياسي الحاد بين القوتين التي كادت تنذر بحرب عالمية نووية مثل أزمة كوبا والكوريتين." },
    34: { name: "العدوان الثلاثي", desc: "هجومات عسكرية مباغتة قامت بها بريطانيا، فرنسا، والاحتلال الإسرائيلي ضد مصر." },
    35: { name: "حرب نووية", desc: "الحرب التي تستخدم فيها الأسلحة الذرية النووية التي تمتلكها القوى العالمية الكبرى." },
    36: { name: "أزمة كوبا (الصواريخ) 1962", desc: "مواجهة بين الو.م. أ والسوفيات بعد اكتشاف الطائرات الأمريكية لصواريخ نووية سوفياتية موجهة نحو الو.م. أ، وتعتبر أخطر أزمات الحرب الباردة." },
    37: { name: "الحرب الباردة", desc: "صراع إيديولوجي بين المعسكرين الشرقي الشيوعي والغربي الرأسمالي (1945 - 1989)، استعملت فيها كل وسائل الصراع باستثناء المواجهة العسكرية المباشرة." },
    38: { name: "الخطر (الزحف أو المد) الشيوعي", desc: "امتداد وانتشار الإيديولوجية الشيوعية إلى مناطق النفوذ الرأسمالي." },
    39: { name: "الانفراج الدولي", desc: "مصطلح سياسي يطلق على التحسن وتخفيف حدة التوتر وتطور العلاقات بين المعسكرين، وهي سياسة جديدة ظهرت بعد أزمة الصواريخ بكوبا 1962." },
    40: { name: "التعايش السلمي", desc: "مفهوم جديد في العلاقات الدولية دعا إليه الزعيم السوفياتي خروتشوف عقب وفاة ستالين، يهدف إلى ضرورة تقبل فكرة التعايش بين المذهبين وتعددهما." },
    41: { name: "الشرعية الدولية", desc: "يقصد بها الالتزام بتنفيذ القرارات الدولية الصادرة عن الهيئات والمنظمات الدولية مثل هيئة الأمم المتحدة وأجهزتها التي تستعملها الو.م. أ وفقا لمصالحها." },
    42: { name: "المنظمات غير الحكومية", desc: "هي منظمات أو جمعيات عالمية خيرية غير تجارية تعرف بالمجتمع المدني تنشط في كافة الميادين كالبيئة والصحة والإغاثة لكن لديها أعمال خفية لصالح القوى العظمى." },
    43: { name: "منظمة التجارة العالمية", desc: "منظمة تأسست في 1995 خلفا للغات، تعمل على وضع القواعد والقوانين التي تنظم التجارة العالمية، من أهدافها فض النزاعات التجارية وإلغاء الحواجز الجمركية." },
    44: { name: "الثنائية القطبية", desc: "يقصد به توجيه العلاقات الدولية وفقا لتصور المعسكرين الشرقي بزعامة الإتحاد السوفياتي والغربي بزعامة الو.م. أ في إطار صراع الحرب الباردة." },
    45: { name: "الستار الحديدي", desc: "مصطلح استعمله الوزير الأول البريطاني ونستن تشرشل وهو عبارة عن ستار يمتد من بحر البلطيق إلى البحر الأدرياتيكي يفصل بين الديمقراطيات الشعبية وأوروبا الغربية." },
    46: { name: "النظام الدولي الجديد", desc: "النظام الذي أعلن عنه بوش الأب بمؤتمر مالطا بعد نهاية الحرب الباردة، وهو مجموعة القواعد والأسس التي تعمل على تسيير العلاقات الدولية وفق المنظور الأمريكي." },
    47: { name: "سياسة الاحتواء", desc: "سياسة أمريكية تقوم على إنشاء سلسلة من الأحلاف والقواعد العسكرية والمشاريع الاقتصادية بهدف تطويق السوفيات ومنع انتشار الشيوعية." },
    48: { name: "الاستقطاب", desc: "سعي كل كتلة لجذب دول من العالم لصفها من خلال عضوية الأحلاف والمشاريع الاقتصادية." },
    49: { name: "حركة عدم الانحياز", desc: "تكتل سياسي دولي تأسس بمؤتمر بلغراد 1961 تضم دول العالم الثالث المستقلة، يهدف إلى عدم الميل إلى أي معسكر من المعسكرين." },
    50: { name: "الحياد الإيجابي", desc: "سياسة تبنتها حركة عدم الانحياز تقوم على عدم الميل لأي كتلة من الكتلتين والعمل على دعوة القوى للتعايش سلميا وإنهاء الخلافات بالطرق الدبلوماسية." },
    51: { name: "مؤتمر باندونغ", desc: "مؤتمر أفرو-آسيوي انعقد بأندونيسيا 18-24 أفريل 1955 لدعم حركات التحرر ووضع مبادئ حركة عدم الانحياز من أهمها الدعوة للتعايش السلمي." },
    52: { name: "تقرير المصير", desc: "أحد مبادئ هيئة الأمم المتحدة يدعو إلى حرية الشعوب في اختيار مصيرها بنفسها." },
    53: { name: "العلاقات الدولية", desc: "مجموعة القواعد والأسس والاتفاقيات والمعاهدات التي تنظم العلاقات بين الدول والتي تميزت بالتوتر بين المعسكرين 1945-1989." },
    54: { name: "البروسترويكا", desc: "(بالروسية إعادة البناء) إعادة هيكلة الاقتصاد بالانفتاح على العالم وتشير إلى السياسة الداخلية المنتهجة في عهد الرئيس غورباتشوف 1985." },
    55: { name: "الغلاسنوست", desc: "تعني الشفافية وتشير إلى السياسة الداخلية المنتهجة في عهد غورباتشوف لمحاربة البيروقراطية والفساد الاداري للنهوض بالاتحاد السوفياتي." },
    56: { name: "هيئة الأمم المتحدة", desc: "هيئة أممية تأسست 24 أكتوبر 1945 بسان فرانسيسكو الو.م. أ خلفا لعصبة الأمم، تضم الدول المستقلة مقرها نيويورك تهدف لتحقيق السلم وتنظيم العلاقات الدولية." },
    57: { name: "مجلس الأمن", desc: "الجهاز التنفيذي في هيئة الأمم المتحدة يتكون من 15 عضوا، 5 دائمون و 10 ينتخبون لمدة سنتين، ويعتبر أحد الهياكل الرئيسية لهيئة الأمم المتحدة." },
    58: { name: "حق الفيتو", desc: "امتياز تتمتع به الدول دائمة العضوية في مجلس الأمن بالامتناع أو الاعتراض على قرار صادر منه، توظفه القوى الكبرى لخدمة مصالحها." },
    59: { name: "سباق التسلح", desc: "سياسة عسكرية منتهجة من طرف المعسكرين بهدف التفوق في المجال العسكري لمختلف أنواع الأسلحة الاستراتيجية مثل الهيدروجينية والنووية وامتلاك أكبر الجيوش." },
    60: { name: "التوازن الدولي", desc: "توازن عسكري نووي منبثق عن امتلاك كل من الو.م. أ والسوفيات للسلاح النووي واستحالة تدمير طرف للآخر." },
    61: { name: "الديكتاتورية", desc: "مصطلح يطلق على الأنظمة الفردية أي استيلاء فرد أو الجماعة على زمام السلطة وتهميش دور مؤسسات الدولة مثل: (النازية - الفاشية)." },
    62: { name: "الجيش الأحمر", desc: "مصطلح أطلق على الجيش السوفياتي خلال الحرب ع 2 والحرب الباردة." },
    63: { name: "الأحادية القطبية", desc: "نظام دولي بعد انهيار الكتلة الشرقية وانفراد الكتلة الغربية بزعامة الو.م. أ بالزعامة الدولية والهيمنة على العالم في مختلف المجالات." },
    64: { name: "جدار برلين", desc: "شيده السوفيات 13 أوت 1961 يقسم مدينة برلين إلى شرقية شيوعية وغربية رأسمالية، هدم في 9 نوفمبر 1989 إيذانا بتوحيد الألمانيتين 1990." },
    65: { name: "المعسكرين (الكتلتين-القطبين)", desc: "دول المعسكر الشيوعي بزعامة السوفيات، ودول المعسكر الرأسمالي بزعامة الولايات المتحدة الأمريكية." },
    66: { name: "القوتين (العملاقين - البلدين)", desc: "يقصد بها القوى التي برزت بعد ح ع 2 كقوى عالمية تمثلت في السوفيات والولايات المتحدة الامريكية." },
    67: { name: "مشروع ترومان", desc: "مشروع جاء به الرئيس الأمريكي ترومان 1947 تضمن مجموعة من القروض والمساعدات الاقتصادية لتركيا واليونان بهدف محاربة المد الشيوعي وفرض الهيمنة الأمريكية." },
    68: { name: "مشروع أيزنهاور", desc: "مشروع سياسي اقتصادي أطلقه الرئيس الأمريكي أيزنهاور 1957 يتمثل في تقديم مساعدات اقتصادية لمنطقة الشرق الأوسط، بهدف محاربة المد الشيوعي وفرض الهيمنة الأمريكية." },
    69: { name: "مشروع مارشال", desc: "مشروع مساعدات اقتصادية منحتها الو.م. أ عن طريق وزير خارجيتها جورج مارشال لدول أوروبا لتجاوز مخلفات ح ع 2، بهدف محاربة المد الشيوعي وفرض الهيمنة الأمريكية." },
    70: { name: "مبدأ جدانوف", desc: "نسبة لصاحبه أندري جدانوف قيادي في الحزب السوفياتي الشيوعي، قسم العالم إلى شرقي شيوعي مسالم يدعم حركات التحرر وغربي رأسمالي استعماري." },
    71: { name: "الكومنفورم", desc: "مكتب الأخبار الشيوعي، أسسه الإتحاد السوفياتي 1947 يضم معظم الأحزاب الشيوعية في العالم، مهمته تنسيق مواقف الأحزاب الشيوعية في العالم." },
    72: { name: "منظمة الكوميكون", desc: "تكتل اقتصادي 1949، ضم السوفيات وبعض حلفائه تهدف للتعاون بين الدول الأعضاء وإلغاء الحواجز الجمركية، تأسست كرد على مشروع مارشال." }
}
    },
    "الثورة التحريرية": {
        "شخصيات": {
    1: { name: "محمد البشير الإبراهيمي", desc: "من أعلام الفكر والإصلاح في الجزائر، عضو جمعية العلماء، ترأس الجمعية بعد وفاة ابن باديس، توفي سنة 1965، حارب الطرقية والبدع والخرافات وساهم في إصلاح المجتمع الجزائري." },
    2: { name: "أحمد زبانة", desc: "مناضل حزب الشعب، كلفه العربي بن مهيدي بوهران بتدريب المناضلين، وشارك في العمليات الأولى للثورة بالغرب الجزائري، ويعتبر أول شهيد في صفوف الثورة بعد إعدامه." },
    3: { name: "محمد بلوزداد", desc: "مناضل حزب الشعب، أحد قادة حركة الانتصار، أول رئيس للمنظمة الخاصة 1947، توفي جانفي 1952." },
    4: { name: "مصالي الحاج", desc: "مناضل سياسي، تزعم التيار الاستقلالي، أمين عام حزب نجم شمال افريقيا ثم حزب الشعب الجزائري 1937، فحركة الانتصار للحريات الديمقراطية، هناك تضارب حول موقفه من الثورة، أسس الحركة الوطنية الجزائرية." },
    5: { name: "فرحات عباس", desc: "أول رئيس للحكومة الجزائرية المؤقتة اشتهر ببيان فيفري 1943، تزعم التيار الإدماجي بعد الحرب ع 1 انضم للثورة سنة 1956، ترأس اللجنة التأسيسية للجمهورية الجزائرية سبتمبر 1962." },
    6: { name: "بن يوسف بن خدة", desc: "عضو بحزب الشعب، ثم حركة انتصار الحريات الديمقراطية، ثاني رئيس للحكومة الجزائرية المؤقتة 1960-1962، أعلن عن وقف إطلاق النار، أحد الشخصيات البارزة في مؤتمر طرابلس 1962." },
    7: { name: "حسين آيت أحمد", desc: "مناضل بحزب الشعب ثم عضو حركة الانتصار للحريات الديمقراطية، وعضوا بارزا في المنظمة الخاصة، يعتبر من أعضاء الوفد الخارجي بالقاهرة، وأحد المختطفين في المغرب (القرصنة الجوية)." },
    8: { name: "محمد بوضياف", desc: "مناضل حزب الشعب، وحركة الانتصار للحريات الديمقراطية عضو المنظمة الخاصة ومجموعة 22، عضو بارز في قيادة الثورة، كان ضمن المختطفين بالطائرة 1956، رئيس الدولة الجزائرية 1992، اغتيل في نفس السنة." },
    9: { name: "محمد خيضر", desc: "مناضل حزب الشعب الجزائري ثم حركة الانتصار للحريات الديمقراطية والمنظمة الخاصة، وأحد أعضاء الوفد الخارجي، كان من بين المختطفين في حادثة الطائرة 1956." },
    10: { name: "أحمد بن بلة", desc: "مناضل بحزب الشعب الجزائري، قيادي في المنظمة الخاصة، عضو اللجنة الثورية للوحدة والعمل وأحد مفجري الثورة التحريرية، من أعضاء الوفد الخارجي، تم اعتقاله في عملية القرصنة الجوية، أول رئيس للجزائر 1962-1965." },
    11: { name: "مصطفى بن بولعيد", desc: "1917-1956 ثوري جزائري، مناضل في حزب الشعب وحركة الانتصار للحريات الديمقراطية، عضو المنظمة الخاصة ومجموعة 22، عضو لجنة 6 ومن أبرز مفجري الثورة، قائد المنطقة الأولى (الأوراس)، استشهد سنة 1956." },
    12: { name: "رابح بيطاط", desc: "مناضل بحزب الشعب وحركة الانتصار والمنظمة الخاصة، عضو اللجنة الثورية للوحدة والعمل ومجموعة 22، عضو لجنة 6، أحد مفجري الثورة، قائد المنطقة الرابعة (الجزائر)." },
    13: { name: "ديدوش مراد", desc: "أحد مفجري الثورة، عضو مجموعة 22، عضو لجنة 6 من مؤسسي اللجنة الثورية للوحدة والعمل، تولى قيادة المنطقة الثانية (الشمال القسنطيني)، استشهد سنة 1955." },
    14: { name: "كريم بلقاسم", desc: "مناضل جزائري، عضو لجنة 6 أحد مفجري الثورة، تولى قيادة المنطقة الثالثة (القبائل)، شارك في مؤتمر الصومام 1956 ورئيس الوفد الجزائري في اتفاقيات إيفيان." },
    15: { name: "العربي بن مهيدي", desc: "1923-1957 مناضل حزب الشعب، ثم حركة الانتصار، عضو المنظمة الخاصة، عضو مجموعة 22 قائد المنطقة الخامسة (وهران)، عضو لجنة 6." },
    16: { name: "زيغود يوسف", desc: "1921-1956 مناضل حزب الشعب ثم المنظمة الخاصة، عضو مجموعة 22، قاد الهجوم القسنطيني 20 أوت 1955، استشهد في 23/09/1956." },
    17: { name: "عبان رمضان", desc: "1920-1957 سياسي وثوري جزائري، عضو حزب الشعب ثم حركة الانتصار، مساعد قائد الولاية 3 ومهندس مؤتمر الصومام استشهد بالمغرب 1958." },
    18: { name: "عيسات إيدير", desc: "مناضل جزائري، من مؤسسي الاتحاد العام للعمال الجزائريين، أفنى حياته في الدفاع عن العمال الجزائريين، عذبته السلطات الاستعمارية وتوفي 1959." },
    19: { name: "حسيبة بن بوعلي", desc: "مناضلة جزائرية خلال الثورة، شاركت في صنع ونقل المتفجرات، من أبرز المناضلات في معركة الجزائر، استشهدت 08/10/1957." },
    20: { name: "هواري بومدين", desc: "مناضل وسياسي جزائري، شارك في الثورة، تولى قيادة أركان الجيش، عُين وزيرا للدفاع بعد الاستقلال ثم رئيسا لمجلس الوزراء 1965، ثم رئيسا لمجلس الثورة والدولة 1965-1978." },
    21: { name: "الشاذلي بن جديد", desc: "سياسي وعسكري جزائري، شارك في الثورة، عضو مجلس الثورة سنة 1965 ورئيسا للجزائر ما بين 1979-1992 عرفت فترته الكثير من الاضطرابات وفي عهده أقرت التعددية السياسية." },
    22: { name: "عبد الرحمان فارس", desc: "محامي جزائري، من النخبة المتشبعة بالثقافة الفرنسية، عُين رئيسا للجنة التنفيذية المؤقتة التي تم تشكيلها بعد وقف القتال 19 مارس 1962 بهدف تسيير المرحلة الانتقالية." },
    23: { name: "مليكة قايد", desc: "مناضلة جزائرية، كان لها دور كبير في تنظيم المظاهرات، عملت طبيبة أثناء الثورة، وكلفت بصناعة القنابل والمتفجرات، استشهدت عام 1958 وهي تعالج بعض المرضى." },
    24: { name: "جميلة بوحيرد", desc: "مناضلة جزائرية، انضمت لصفوف جبهة التحرير الوطني عند اندلاع الثورة، نسقت بين قادة الجيش وقادة الجبال، صدر قرار استعماري ضدها بالإعدام." },
    25: { name: "جاك سوستال", desc: "عُين واليا عاما على الجزائر سنة 1955 وهو صاحب مشروع سوستال، نصب نفسه مدافعا عن 'الجزائر الفرنسية' وسياسة الإدماج." },
    26: { name: "غي موليه", desc: "رئيس حكومة فرنسا 1956-1957، وكانت حكومته من الحكومات المتعاقبة التي فشلت في القضاء على الثورة، شهدت فترته معركة الجزائر." },
    27: { name: "شارل ديغول", desc: "سياسي وعسكري فرنسي، قاد المقاومة ضد النازية، عاد إلى الحكم 1958، أرغمته الثورة على التفاوض والاعتراف بالاستقلال بعد فشل مشاريعه الإغرائية والعسكرية." },
    28: { name: "مانديس فرانس", desc: "محامي فرنسي ورئيس وزراء فرنسا بين 1954-1955 لكن لم تدم حكومته لفترة طويلة بسبب قوة الثورة الجزائرية." },
    29: { name: "الجنرال ماسو", desc: "عسكري فرنسي، شارك في العدوان الثلاثي على مصر، وكلف بالحفاظ على الأمن بالجزائر بعد انطلاق معركة الجزائر، كان من المعارضين لوقف القتال وأحد أعضاء المنظمة الإرهابية الفرنسية." },  
    30: { name: "الجنرال موريس", desc: "وزير الدفاع الفرنسي، صاحب فكرة عزل الجزائر عن تونس والمغرب بخط من الأسلاك الملغمة والمكهربة على طول الحدود والذي أصبح يحمل اسمه (خط موريس)." },
    31: { name: "الجنرال شال", desc: "القائد العام للقوات الفرنسية في الجزائر 1958-1960، صاحب المخطط الكهربائي (شال) الموازي لخط موريس، منفذ السياسة العسكرية لديغول في الجزائر." },
    32: { name: "لويس جوكس", desc: "سياسي فرنسي، عينه الجنرال ديغول وزيرا للشؤون الجزائرية، رئيس الوفد الفرنسي الموقع لاتفاقيات إيفيان 1962 والتي أفضت باستقلال الجزائر." },
    33: { name: "فرانسوا ميتيران", desc: "رئيس فرنسا، ينتمي للحزب الاشتراكي الفرنسي، يعتبر من الرافضين لسياسة ديغول بخصوص الثورة الجزائرية (وقف إطلاق النار)، عُرف بسياسته التعسفية ضد الجزائريين." }
},
        "تواريخ": {
     1: { name: "07 جوان 1936", date: "المؤتمر الإسلامي." },
     2: { name: "03 فيفري 1943", date: "بيان الشعب الجزائري." },
     3: { name: "08 ماي 1945", date: "مظاهرات ومجازر 08 ماي." },
     4: { name: "16 مارس 1946", date: "إعادة بناء الحركة الوطنية." },
     5: { name: "15-16 فيفري 1947", date: "إنشاء المنظمة الخاصة." },
     6: { name: "20 سبتمبر 1947", date: "القانون الخاص (دستور الجزائر)." },
     7: { name: "23 مارس 1954", date: "إنشاء اللجنة الثورية للوحدة والعمل." },
     8: { name: "23 جوان 1954", date: "اجتماع مجموعة 22 التاريخية." },
     9: { name: "10 أكتوبر 1954", date: "اجتماع لجنة الستة الأول." },
    10: { name: "23 أكتوبر 1954", date: "اجتماع لجنة الستة الثاني (اجتماع الحسم)." },
    11: { name: "05 فيفري 1955", date: "سقوط حكومة مانديس فرانس." },
    12: { name: "15 فيفري 1955", date: "تعيين جاك سوستال حاكما عاما للجزائر (مشروع سوستال)." },
    13: { name: "03 أفريل 1955", date: "إعلان حالة الطوارئ." },
    14: { name: "20 أوت 1955", date: "هجومات الشمال القسنطيني." },
    15: { name: "24 فيفري 1956", date: "تأسيس الاتحاد العام للعمال الجزائريين." },
    16: { name: "22 أفريل 1956", date: "حل الاتحاد الديمقراطي للبيان الجزائري والتحاق فرحات عباس بالثورة." },
    17: { name: "19 ماي 1956", date: "إضراب الطلبة الجزائريين والتحاقهم بالثورة." },
    18: { name: "20 أوت 1956", date: "انعقاد مؤتمر الصومام." },
    19: { name: "22 أكتوبر 1956", date: "اختطاف طائرة قادة الوفد الخارجي للثورة بالمغرب (القرصنة الجوية)." },
    20: { name: "28 جانفي - 04 فيفري 1957", date: "إضراب الثمانية أيام." },
    21: { name: "08 فيفري 1958", date: "قصف ساقية سيدي يوسف (تونس)." },
    22: { name: "13 ماي 1958", date: "تمرد جنرالات فرنسا في الجزائر." },
    23: { name: "01 جوان 1958", date: "انتخاب ديغول رئيسا لفرنسا (تأسيس الجمهورية الخامسة)." },
    24: { name: "19 سبتمبر 1958", date: "تأسيس الحكومة الجزائرية المؤقتة." },
    25: { name: "03 أكتوبر 1958", date: "الإعلان عن مشروع قسنطينة." },
    26: { name: "23 أكتوبر 1958", date: "الإعلان عن مشروع سلم الشجعان (الأبطال)." },
    27: { name: "11 ديسمبر 1960", date: "مظاهرات الشعب الجزائري بالمدن الكبرى." },
    28: { name: "20 ماي 1961", date: "محاكمات إيفيان الأولى." },
    29: { name: "17 أكتوبر 1961", date: "مظاهرات الجزائريين في المهجر (فرنسا)." },
    30: { name: "18 مارس 1962", date: "توقيع اتفاقيات إيفيان الثانية." },
    31: { name: "25 سبتمبر 1962", date: "الإعلان عن قيام الدولة الجزائرية." }, 
    32: { name: "19 مارس 1962", date: "وقف إطلاق النار." },
    33: { name: "27 ماي - 04 جوان 1962", date: "انعقاد مؤتمر طرابلس." },
    34: { name: "01 جويلية 1962", date: "استفتاء تقرير المصير." },
    35: { name: "05 جويلية 1962", date: "الاستقلال الرسمي للجزائر." },
    36: { name: "16 أوت 1962", date: "انضمام الجزائر لجامعة الدول العربية." },
    37: { name: "08 أكتوبر 1962", date: "انضمام الجزائر إلى هيئة الأمم المتحدة." },
    38: { name: "19 جوان 1965", date: "التصحيح الثوري وعزل بن بلّة." },
    39: { name: "24 فيفري 1971", date: "تأميم المحروقات." },
    40: { name: "27 ديسمبر 1978", date: "وفاة الرئيس هواري بومدين." },
    41: { name: "05 أكتوبر 1988", date: "مظاهرات الشعب الجزائري (مظاهرات أكتوبر)." },
    42: { name: "23 فيفري 1989", date: "دستور الجزائر الجديد وإقرار التعددية الحزبية." },
    43: { name: "11 جانفي 1992", date: "استقالة الرئيس الشاذلي بن جديد." }  
     },
       "مصطلحات": {
    1: { name: "حزب التحرير الجزائرية", desc: "مجموعة الجهود العسكرية والسياسية التي شهدتها الجزائر في الفترة الممتدة 1954-1962 بهدف تحقيق الاستقلال واسترجاع السيادة." },
    2: { name: "الثورة التحريرية", desc: "رد فعل الشعب الجزائري على الوجود الاستعماري 1954-1962 باستعمال مختلف وسائل الكفاح بقيادة جبهة وجيش التحرير الوطني، بهدف تحقيق الاستقلال واسترجاع السيادة الوطنية." },
    3: { name: "تعبئة الجماهير (التعبئة الشعبية)", desc: "تجنيد الشعب بمختلف شرائحه، وإعداده للالتفاف حول الثورة الجزائرية بهدف ضمان نجاحها." },
    4: { name: "سياسة الإغراء", desc: "تتمثل في الإصلاحات والمشاريع السياسية والاقتصادية مثل مشروع سوستال ومشروع قسنطينة 1958 والتي أقرتها فرنسا، لإغراء الجزائريين بهدف ضرب الثورة." },
    5: { name: "سياسة القمع", desc: "جملة القوانين والإجراءات التعسفية الإجرامية التي أقدمت عليها فرنسا في حق الجزائريين باستعمال وسائل التنكيل والتعذيب من أجل إخضاعه وقتل روح المقاومة مثل مجازر 8 ماي." },
    6: { name: "مجازر 8 ماي", desc: "الأعمال الوحشية والقمعية الاستعمارية الفرنسية ضد المتظاهرين الجزائريين في الشرق الجزائري الذين خرجوا للاحتفال بنهاية الحرب ع 2، ومن أهم مخلفات المجازر 45 ألف شهيد." },
    7: { name: "التيار الثوري", desc: "مجموعة الشباب المتحمس للعمل المسلح الثوري، وهم أفراد المنظمة الخاصة، قاموا بتشكيل اللجنة الثورية للوحدة والعمل ثم جبهة وجيش التحرير الوطني وتفجير الثورة التحريرية." },
    8: { name: "حركة الانتصار للحريات الديمقراطية", desc: "تنظيم سياسي تأسس 1946 وهو امتداد لحزب الشعب، بقيادة مصالي الحاج، يمثل الاتجاه الاستقلالي، عرف أزمة سياسية حادة 1953 عرفت بأزمة الحركة." },
    9: { name: "المنظمة الخاصة", desc: "الجناح العسكري لحركة الانتصار للحريات الديمقراطية تأسست 1947 ترأسها محمد بلوزداد، هدفها التحضير للثورة الجزائرية، تم اكتشافها عام 1950." },
    10: { name: "اللجنة الثورية للوحدة والعمل", desc: "تأسست 23 مارس 1954 ضمت أعضاء المنظمة الخاصة وبعض المركزيين، هدفها توحيد الصفوف بعد أزمة الحركة والتحضير لتفجير الثورة." },
    11: { name: "المقاومة", desc: "شكل من أشكال نضال الشعوب المستعمرة (سياسيا-اقتصاديا-عسكريا) ضد الاحتلال وهو وسيلة حركات التحرر من أجل الاستقلال واستعادة سيادتها." },
    12: { name: "جبهة التحرير الوطني", desc: "تنظيم سياسي ثوري (الجناح السياسي للثورة) تأسس 23 أكتوبر 1954، وتعتبر الممثل الشرعي والوحيد للشعب الجزائري، تهدف إلى تحرير الجزائر من الاستعمار." },
    13: { name: "جيش التحرير الوطني", desc: "تنظيم عسكري (الجناح العسكري للثورة) تأسس 23 أكتوبر 1954، مهمته القيام بالعمليات العسكرية والفدائية ضد الاستعمار بهدف تحرير الجزائر." },
    14: { name: "تصفية الاستعمار", desc: "الجهود والتضحيات التي قدمتها الشعوب في قارتي افريقيا وآسيا وأمريكا اللاتينية لمحاربة الاستعمار واسترجاع سيادتها وتحقيق الاستقلال." },
    15: { name: "المد التحرري", desc: "النضال الوطني للشعوب ضد قوى الاستعمار التقليدية (فرنسا-بريطانيا) في أفريقيا وآسيا وأمريكا اللاتينية، وقد أخذ شكل النضال السياسي بعد ح ع 1 والعسكري بعد ح ع 2." },
    16: { name: "المواثيق", desc: "مجموعة القرارات المتفق عليها والتي تأخذ صفة المبادئ والأسس مثل (ميثاق الصومام - وميثاق طرابلس)." },
    17: { name: "البرنامج", desc: "مجموعة الأطروحات والقرارات المتفق عليها وهو عبارة عن خطة عمل بأهداف وإجراءات وآجال محددة ودقيقة." },
    18: { name: "البيان", desc: "تصريح كتابي يتعلق بقضية معينة مثل بيان 01 نوفمبر 1954." },
    19: { name: "بيان 1 نوفمبر", desc: "أول وثيقة سياسية رسمية لجبهة التحرير حددت مبادئ الثورة وأهدافها ووسائلها." },
    20: { name: "المجلس الوطني للثورة الجزائرية", desc: "المؤسسة التشريعية للثورة الجزائرية، تشكل بمقتضى قرارات مؤتمر الصومام 1956، يتكون من 34 عضو يجتمع مرة في السنة من صلاحياته وقف القتال." },
    21: { name: "لجنة التنسيق والتنفيذ", desc: "المؤسسة التنفيذية للثورة تسهر على تنفيذ قرارات المجلس الوطني للثورة ومراقبة أجهزة الثورة، تشكلت بمقتضى قرارات مؤتمر الصومام 1956." },
    22: { name: "الدبلوماسية الجزائرية", desc: "الجهود التي بذلتها الثورة بإنشاء جهاز دبلوماسي في مختلف العواصم والمحافل الدولية لكسب الدعم السياسي والتعاطف العالمي مع الثورة الجزائرية." },
    23: { name: "الدبلوماسية الفرنسية", desc: "الجهود التي بذلها الساسة الفرنسيون في المحافل الدولية بهدف تشويه صورة الثورة الجزائرية والقضاء عليها." },
    24: { name: "السند الدبلوماسي", desc: "الدعم السياسي الذي تلقته الثورة الجزائرية من الدول في المحافل الدولية." },
    25: { name: "تدويل القضية الجزائرية", desc: "عرضها والتعريف بها في الهيئات والمنظمات الدولية لكسب التعاطف الدولي." },
    26: { name: "المحافل الدولية", desc: "المنابر التي تعرض فيها الشعوب قضاياها للرأي العام العالمي مثل هيئة الأمم المتحدة." },
    27: { name: "مشروع سوستال", desc: "مشروع إغرائي لصاحبه جاك سوستال الوالي العام على الجزائر عام 1955 تناول عدة جوانب إصلاحية الهدف منه خلق طبقة ثالثة لضرب الثورة الجزائرية." },
    28: { name: "المكاتب العربية", desc: "جهاز إداري خاص أقامته الإدارة الفرنسية منذ احتلالها للجزائر بهدف الجوسسة من خلال جمع المعلومات والاحصاءات عن الجزائريين." },
    29: { name: "القوة الثالثة (العملاء)", desc: "طبقة برجوازية عميلة في المجتمع الجزائري دعمتها فرنسا كبديل عن الثورة وقد استفادت هذه الطبقة من السكنات ومناصب العمل لذلك أصبحت من الحركات المناوئة للثورة." },
    30: { name: "تطويق الثورة", desc: "محاصرة الثورة ومنعها من التوسع والانتشار وعزلها عن الدعم الشعبي والخارجي." },
    31: { name: "المحتشدات", desc: "معتقلات جماعية لسكان الأرياف، في مناطق مفتوحة محاطة بالأسلاك الشائكة المكهربة والمراقبة عسكريا بهدف عزل الثورة عن الشعب." },
    32: { name: "معركة الجزائر", desc: "العمليات الفدائية التي قام بها عناصر من الثورة الجزائرية بالعاصمة 1957." },
    33: { name: "مشروع قسنطينة", desc: "مشروع فرنسي إغرائي أعلنه ديغول 03 أكتوبر 1958 بقسنطينة يتضمن مساعدات ومشاريع اقتصادية الهدف منه إبعاد الشعب عن الثورة وخلق طبقة موالية لفرنسـا." },
    34: { name: "خط شال وموريس", desc: "عبارة عن إجراءات عسكرية شاملة تهدف للقضاء على الثورة من خلال تكثيف العمليات العسكرية، وعزل الثورة بغلق الحدود التونسية والمغربية بإنشاء خطوط مكهربة وملغمة." },
    35: { name: "مخطط شال", desc: "مجموعة من الخطط العسكرية نسبة للجنرال موريس شال تتمثل في عمليات تمشيطية برية وبحرية وجوية بحثا عن المجاهدين، مثل عملية الشرارة والأحجار الكريمة." },
    36: { name: "القرصنة الجوية", desc: "اختطاف فرنسا لطائرة الوفد الجزائري الخارجي المتجهة من المغرب إلى تونس." },
    37: { name: "المناطق المحرمة", desc: "مناطق اعتبرتها فرنسا استراتيجية فحرمتها على الجزائريين أي يمنع السكن فيها وحتى عبورها خاصة في الحدود والجبال." },
    38: { name: "حرب العصابات", desc: "أسلوب حربي يعتمد على مباغتة العدو وإحداث الذعر في صفوفه، يتميز بسرعة الحركة وتفادي المواجهة المباشرة مع العدو." },
    39: { name: "سلم الشجعان", desc: "مناورة سياسية أطلقها الجنرال ديغول 23 أكتوبر 1958 تقضي بتسليم الثوار أسلحتهم مقابل ضمان حريتهم يهدف إلى ضرب الثورة، رُفض من طرف الثوار." },
    40: { name: "الاستراتيجية الديجولية", desc: "المخططات العسكرية والسياسية والاقتصادية الاستعمارية الفرنسية في فترة شارل ديغول بهدف ضرب الثورة والقضاء عليها مثل إنشاء خطي شال وموريس وبناء المحتشدات." },
    41: { name: "الثورة الزراعية", desc: "تنظيم زراعي صدر سنة 1972 تحت شعار الأرض لمن يخدمها يهدف إلى تحديث القطاع الزراعي وتطوير الريف عبر سياسة التوازن الجهوي." },
    42: { name: "النشاط المسلح", desc: "مجموع العمليات العسكرية والفدائية التي قام بها الثوار الجزائريون داخل وخارج الوطن في الفترة 1954-1962 والتي توجت بالاستقلال." },
    43: { name: "هجومات الشمال القسنطيني", desc: "هجومات قادها الشهيد زيغود يوسف 20 أوت 1955 بالمنطقة الثانية، وتعتبر من المحطات الهامة في الثورة الجزائرية بنقلها من الأرياف للمدن وفك الحصار على الأوراس." },
    44: { name: "الحكومة الجزائرية المؤقتة", desc: "تأسست بالقاهرة 19 سبتمبر 1958 برئاسة فرحات عباس كممثل للشعب الجزائري وثورته بالمشاركة في المؤتمرات وتمثيل الثورة والتفاوض مع الاستعمار." },
    45: { name: "مؤتمر الصومام", desc: "أول مؤتمر تقييمي للثورة انعقد 20 أوت 1956 بالمنطقة الثالثة (القبائل) ويعتبر من الانتصارات الكبرى للثورة الجزائرية." },
    46: { name: "مؤتمر طرابلس", desc: "ثاني مؤتمر للثورة بعد مؤتمر الصومام، انعقد بطرابلس 27 ماي-04 جوان 1962 حضره معظم قادة الثورة، وحدد معالم الدولة الجزائرية المستقلة." },
    47: { name: "السيادة الوطنية", desc: "هي السلطة الفعلية للدولة على إقليمها وما فيه من سكان وموارد، والحرية في المواقف والاختيارات الكبرى لبناء الدولة." },
    48: { name: "اتفاقية إيفيان", desc: "وقعت في 18 مارس 1962 بمدينة إيفيان بين الطرفين الجزائري والفرنسي، احتوت على العديد من القرارات أهمها وقف إطلاق النار." },
    49: { name: "الهدنة", desc: "توقيف العمليات العسكرية لفترة زمنية محددة." },
    50: { name: "المفاوضات", desc: "صيغة دبلوماسية لحل أزمة ما في شكل لقاءات سرية أو علنية مثل مفاوضات إيفيان." },
    51: { name: "الهيئة التنفيذية المؤقتة", desc: "هيئة منبثقة عن مفاوضات إيفيان برئاسة عبد الرحمان فارس هدفها التحضير لإجراء استفتاء تقرير مصير الجزائريين وتسيير المرحلة الانتقالية." },
    52: { name: "وقف إطلاق النار", desc: "وقف كل العمليات العسكرية ونهاية المواجهة العسكرية بموجب اتفاقيات إيفيان بين الحكومة الجزائرية المؤقتة والحكومة الفرنسية طبقت في 19 مارس 1962." },
    53: { name: "منظمة الجيش الفرنسي (OAS)", desc: "تنظيم إرهابي أسسه قادة الجيش الفرنسي والمستوطنون بهدف افشال وقف إطلاق النار بين الجزائريين وفرنسا." },
    54: { name: "الأحزاب (الحركة) الوطنية", desc: "مجموع التنظيمات السياسية التي ظهرت في الجزائر بعد ح ع 1 إلى 1954 والمتشكلة من تيارات حزبية (دعاة الاستقلال - الاصلاح - المساواة - الادماج)." },
    55: { name: "المخططات الإنمائية", desc: "يقصد بها المخططات المتبعة من طرف الدولة الجزائرية المستقلة للنهوض بالاقتصاد الوطني والقطاعات الثلاث من الفترة الممتدة 1967-1990." },
    56: { name: "التأميمات", desc: "سياسة اتبعتها الجزائر المستقلة قصد استرجاع السيادة الوطنية على الثروات الطبيعية والمؤسسات المالية من الاستعمار الفرنسي مثل تأميم (الأراضي - البنوك...)." },
    57: { name: "مكاتب لاصاص (LA SAS)", desc: "أنشئت سنة 1955 خلال فترة سوستال تمثلت مهمتها في تكثيف العمل الاجتماعي والسيكولوجي للجيش الفرنسي في الأوساط الجماهيرية بهدف عزل الثورة عن الجماهير." },
    58: { name: "الثورة الثقافية", desc: "يقصد بها الجهود المبذولة من طرف الدولة للنهوض بالقطاع الثقافي من خلال إنشاء المدارس والجامعات والمعاهد ومراكز التكوين المهني لرفع نسبة التعليم والتقليل من نسبة الأمية." },
    59: { name: "الثورة الصناعية", desc: "ويقصد بها القفزة التي حققتها الجزائر المستقلة في المجال الصناعي بعد أن أولت الدولة اهتمامها بهذا القطاع بعد الاستقلال ببناء مؤسسات ومصانع وتكوين الاطارات." },
    60: { name: "الاستفتاء", desc: "إدلاء الشعب برأيه في قضية ما، عن طريق التصويت، مثل استفتاء تقرير مصير الجزائريين." }

        }
    },
    // === الجغرافيا ===
    "واقع الاقتصاد العالمي": {
        "مصطلحات": {
    1: { name : "تبييض الأموال (غسيل الأموال)", desc: "إخفاء المصدر الحقيقي للأموال المحصلة بطرق غير مشروعة وتحويلها إلى أموال شرعية عبر استثمارات قانونية." },
    2: { name: "التنمية", desc: "مجموع القرارات والإجراءات والمشاريع التي تهدف إلى الاستغلال الأمثل للإمكانات الطبيعية والبشرية لتحقيق التطور الاقتصادي والرفاهية الاجتماعية." },
    3: { name: "مؤشر التنمية البشرية", desc: "مقياس إحصائي يتراوح بين (0-1) لقياس درجة تقدم الدول بناءً على ثلاثة معايير: أمد الحياة، مستوى التعليم، والدخل الفردي." },
    4: { name: "الناتج المحلي (الداخلي) الخام", desc: "قيمة الثروة المنتجة داخل البلاد فقط من طرف مختلف الفئات الشغالة خلال سنة واحدة." },
    5: { name: "الناتج الوطني (القومي) الخام", desc: "قيمة الثروة المنتجة داخل وخارج البلاد خلال سنة واحدة." },
    6: { name: "الدخل الفردي", desc: "هو حاصل قسمة الدخل المحلي الخام على عدد السكان في سنة معينة." },
    7: { name: "العملة الصعبة", desc: "هي العملات القابلة للتحويل والمعتمدة في التعاملات التجارية الدولية مثل الدولار الأمريكي والأورو الأوروبي." },
    8: { name: "رؤوس الأموال", desc: "مجموع الأموال والمواد والأدوات اللازمة لإنشاء نشاط اقتصادي، وتعتبر المحرك الأساسي لأي مشروع." },
    9: { name: "الاستثمار", desc: "توظيف أو تشغيل رؤوس الأموال في مشاريع تنموية اقتصادية أو اجتماعية لتحقيق أرباح أو فوائد عامة." },
    10: { name: "المديونية (الديون)", desc: "مبالغ مالية تم اقتراضها من البنوك والمؤسسات المالية بفوائد معينة مع الالتزام بدفعها في آجال محددة." },
    11: { name: "القروض", desc: "مبالغ مالية يتم الحصول عليها من البنوك والمؤسسات المالية مقابل الالتزام بردها مع دفع فوائدها." },
    12: { name: "المحاصيل النقدية", desc: "هي الزراعات التجارية التي تهدف من خلالها الدول لتحقيق الربح المالي مثل تجارة قصب السكر، الكاكاو، والبن." },
    13: { name: "المواد الأولية الطاقوية", desc: "هي المواد الحيوية للصناعات مثل البترول والغاز الطبيعي والتي تساهم في الإنتاج الصناعي وتطور البلاد." },
    14: { name: "مجموعة الثمانية", desc: "منظمة اقتصادية عالمية تضم القوى الاقتصادية الكبرى في العالم (الو.م.أ، كندا، فرنسا، بريطانيا، ألمانيا، إيطاليا، روسيا، اليابان)." },
    15: { name: "التضخم", desc: "هو الارتفاع المتزايد في أسعار السلع والخدمات بسبب فقدان العملة لقيمتها النقدية." },
    16: { name: "البنوك", desc: "هي مؤسسات مصرفية تقوم بالعمليات المالية وتعمل تحت إشراف ومراقبة البنك المركزي." },
    17: { name: "البورصة (الأسواق المالية)", desc: "سوق مالية يتم فيها تبادل الأسهم والسندات وشراء العملات وتحديد قيمتها." },
    18: { name: "المضاربة", desc: "هي المخاطرة بالبيع والشراء بناءً على توقع تقلبات أسعار السوق لتحقيق ربح سريع." },
    19: { name: "السندات", desc: "أوراق مالية تصدرها الشركات أو الدول لاقتراض الأموال، حيث يحصل حامل السند على فائدة ثابتة." },
    20: { name: "المعيار", desc: "جملة من الأسس والمؤشرات التي يستند إليها لتحديد ضعف أو قوة اقتصاد دولة ما." },        
    21: { name: "المؤشر", desc: "وهو الدليل الرقمي أو الإحصائيات والنسب التي تثبت وتوضح واقع ظاهرة معينة كنسبة النمو الديمغرافي أو كمية الإنتاج أو متوسط العمر ونسبة المساهمة في التجارة الدولية (بأرقام)." },
    22: { name: "الأسهم", desc: "هي قيم مالية خاصة بالشركات يتم تداولها في البورصة، يقوم الأفراد بشرائها، فتمنح لهم صكوك تثبت ملكيتهم لحصص في الشركة صاحبة الأسهم، وتكون خاضعة للربح والخسارة." },
    23: { name: "العملة", desc: "هي النقود المتداولة في بلد ما، وهي عملة ضرورية للتعامل في المبادلات التجارية، وهي تختلف من دولة إلى أخرى وتمثل العملة وسيلة لتسهيل التبادل التجاري." },
    24: { name: "الصناعة التحويلية", desc: "صناعة أساسية تعتمد على تحويل المواد الخام لمنتجات مصنعة أو نصف مصنعة." },
    25: { name: "الميزان التجاري", desc: "هو الفرق بين قيمة الواردات وصادرات بلد ما خلال سنة ما." },
    26: { name: "ميزان المدفوعات", desc: "سجل تسجل فيه القيم النقدية لمختلف المعاملات التجارية والمالية التي تتم بين الأشخاص والمؤسسات خلال سنة ما." },
    27: { name: "التكنولوجيا", desc: "هي أعلى درجات التطور العلمي والمقصود بها علم التقنيات المطبقة في مختلف المجالات." },
    28: { name: "الأسواق العالمية", desc: "الفضاءات المسخرة لتداول جميع السلع (بيع - شراء - مقايضة) وعقد الصفقات التجارية." },
    29: { name: "الشركات", desc: "مؤسسات مالية اقتصادية متخصصة متعددة المجالات، في أنشطة مختلفة، تساهم في اقتصاد دولها من خلال إنتاجيتها ونشاطها التجاري." },
    30: { name: "الفوائد", desc: "القيم المالية الناتجة عن بيع منتج معين أو استثمار في مجال ما أو مقابل تقديم قروض بنكية." },
    31: { name: "الإعلام", desc: "كافة الوسائل التي وصل إليها الإنسان (مكتوبة، مرئية، مسموعة) ويتمثل اليوم في (القنوات الإعلامية، مواقع التواصل الاجتماعي، الصحف والمجلات)." },
    32: { name: "الإشهار والدعاية", desc: "عملية ترويجية لسلعة أو خدمة عن طريق وسائل الإعلام كالقنوات والصحف." },
    33: { name: "العولمة", desc: "معناها الشمولية، أو انتشار نفس النمط الاقتصادي والسياسي والثقافي في العالم، بإزالة الحواجز الجمركية أمام الانتقال الحر للسلع والخدمات والأموال والمعلومات بين دول العالم." },
    34: { name: "منظمة الأوبيك", desc: "منظمة الدول المصدرة للبترول تأسست 1960 من طرف: إيران، السعودية، العراق، الكويت، فنزويلا، بهدف حماية مصالح الأعضاء ومحاربة سياسات الشركات الاحتكارية، مقرها فيينا." },
    35: { name: "البرميل", desc: "وحدة قياس تستعمل في التجارة البترولية وتقدر سعة البرميل بحوالي 158.97 لتر." },
    36: { name: "الشركات متعددة الجنسيات", desc: "شركات عملاقة تقع مقراتها بالدول المتقدمة خاصة الو.م.أ، لها فروع في أنحاء العالم تهيمن على مختلف الأنشطة الاقتصادية والخدماتية." },
    37: { name: "الشركات الاحتكارية", desc: "الشركات التابعة للقوى الاقتصادية الكبرى التي تحتكر تجارة المواد الاستراتيجية سواء الطاقوية مثل شركة بتروليوم (تجارة البترول) أو الغذائية مثل شركة بونج (تجارة القمح)." },
    38: { name: "التكتلات الاقتصادية", desc: "معاهدات تهدف إلى توحيد السياسات الاقتصادية وتنقسم لتكتلات أفقية تتم بين الدول كالاتحاد الأوروبي وتكتلات رأسية تتم بين الشركات، هدفها تحقيق مصالح مشتركة." },
    39: { name: "المؤسسات المالية الاقتصادية", desc: "يقصد بها البنوك والمنظمات المالية الاقتصادية العالمية مثل صندوق النقد والبنك العالمي التي انبثقت عن اتفاقية بروتن وودز 1944 وظفها الو.م.أ وحلفائها للهيمنة على العالم." },
    40: { name: "صندوق النقد الدولي", desc: "مؤسسة مالية عالمية أنشئت سنة 1945 لمراقبة النظام النقدي العالمي وإعطاء القروض للبلدان التي تعاني عجزاً في الميزان التجاري." },
    41: { name: "البنك الدولي للإنشاء والتعمير", desc: "مؤسسة مالية عالمية تم إنشاؤها 1946 بهدف تعمير الدول المتضررة من الحرب ع 2، وتمويل المشاريع التنموية الاقتصادية للدول الأعضاء." },
    42: { name: "التقدم", desc: "مصطلح يدل على حالة اقتصادية واجتماعية مزدهرة نتيجة التطور العلمي والتكنولوجي، من مظاهره قوة الإنتاج وتحقيق الاكتفاء الذاتي." },
    43: { name: "التخلف", desc: "مصطلح يدل على حالة اقتصادية يميزها الركود الاقتصادي والثقافي والتدهور الاجتماعي، ويعني عدم القدرة على استغلال الإمكانيات المتاحة لإنتاج الثروة." },
    44: { name: "الدول النامية", desc: "الدول التي استقلت حديثاً (دول العالم الثالث) وتعرف نمواً اقتصادياً بطيئاً، وتعاني من مشاكل عديدة، تتواجد معظمها في افريقيا، آسيا، أمريكا اللاتينية." },
    45: { name: "البلدان الصاعدة", desc: "دول تنتمي للعالم الثالث نجحت في تحقيق تطوراً في نموها الاقتصادي بسبب التطور الصناعي الذي حققته مثل الصين، الهند، البرازيل.. إلخ." },
    46: { name: "اقتصاد السوق (الاقتصاد الحر)", desc: "أحد مبادئ النظام الرأسمالي قائم على عدم تدخل الدولة في تحديد الأسعار وتنظيم الأسواق وتقليص دورها، إذ تضبط الأسعار وفق قانون العرض والطلب." },
    47: { name: "الاقتصاد الموجه (الاقتصاد المخطط)", desc: "أحد مبادئ النظام الاشتراكي قائم على تحديد الدولة للسلع التي يجب انتاجها وضبط أسعارها." },
    48: { name: "الخوصصة", desc: "تحويل مؤسسات القطاع العام إلى الخواص عن طريق البيع أو التنازل لتنمية القطاع الخاص." },
    49: { name: "القطاع الخاص", desc: "امتلاك الأشخاص والمؤسسات غير التابعة للدولة لوسائل الانتاج والخدمات." },
    50: { name: "القطاع العام", desc: "امتلاك الدولة لوسائل الانتاج والخدمات بهدف تحقيق التنمية بالشكل الصحيح." },
    51: { name: "الاكتفاء الذاتي", desc: "قدرة الدولة على توفير حاجيات سكانها اعتماداً على الإمكانيات المحلية وانتاجها ودون اللجوء للاستيراد من الخارج." },
    52: { name: "الأمن الغذائي", desc: "قدرة الدولة على توفير حاجيات سكانها سواء عن طريق انتاجها المحلي أو الاستيراد." },
    53: { name: "السلاح الأخضر", desc: "توظيف الغذاء كوسيلة للضغط على الدول الضعيفة مقابل تحقيق مصالحها." },
    54: { name: "الثالوث الاقتصادي", desc: "الأقطاب الاقتصادية المتحكمة في الاقتصاد العالمي وتتمثل في الو.م.أ - الاتحاد الأوروبي - القطب الآسيوي." },
    55: { name: "النمو الاقتصادي", desc: "هو التطور الذي تشهده مختلف القطاعات الاقتصادية لدولة ما، يزداد مع زيادة الإنتاج وتوسع الاستثمارات، وتنعكس نتائجه بارتفاع الدخل القومي وتحسن مستوى المعيشة." },
    56: { name: "التوازن الاقتصادي", desc: "مصطلح اقتصادي يقصد به تحقيق التكامل بين القطاعات الاقتصادية الثلاث." },
    57: { name: "المناطق الحرة", desc: "هي المناطق المعفاة من الرسوم الجمركية وتخضع لتسهيل حركة الأشخاص والسلع والأموال." },
    58: { name: "الحواجز الجمركية", desc: "الرسوم التي تفرضها الدول على تنقل السلع والبضائع والأشخاص والخدمات من دولة لأخرى." },
    59: { name: "التقسيم الدولي للعمل", desc: "توزيع للأدوار بين العالمين المتقدم والمتخلف (تصدير العالم المتخلف للخامات وتحويلها لمنتجات من طرف العالم المتقدم)." },
    60: { name: "الخدمات", desc: "هي الأنشطة المكملة للنشاط الاقتصادي مثل النقل، التجارة.. إلخ." },
    61: { name: "المبادلات التجارية (التجارة الدولية)", desc: "عملية التبادل التجاري للسلع والخدمات في الأسواق العالمية (الصادرات والواردات) بين دولتين أو أكثر بهدف تحقيق منافع متبادلة." },
    62: { name: "البريكس", desc: "تكتل اقتصادي عالمي بدأت فكرة تأسيسه عام 2006 والبريكس اختصار للحروف الأولى للدول العضوة البرازيل-الهند-روسيا-الصين-جنوب أفريقيا، تم توسيع عضويتها في 24 أوت 2023 لتضم 6 دول أخرى." }
}
    },
    "القوى الاقتصادية الكبرى في العالم": {
        "مصطلحات": {
    1: { name: "تنظيم الإقليم", desc: "عبارة عن هيكلة للمظاهر الجغرافية والبشرية والاقتصادية على مستوى الإقليم بوضع مخططات لتوفير جميع الحاجيات تأخذ بعين الاعتبار الإمكانيات المتاحة للإقليم." },
    2: { name: "الهيمنة والنفوذ", desc: "سيطرة واستغلال تمارسها الدول القوية ذات الإمكانيات الضخمة على الدول الضعيفة." },
    3: { name: "الدورة الزراعية", desc: "هي زراعة محاصيل (حبوب وخضروات) بتعاقب منظم لعدد من السنين طبقاً لنظام معين بهدف الحفاظ على خصوبة التربة." },
    4: { name: "الواجهة الأطلسية", desc: "هي المنطقة الشمالية الشرقية للو.م.أ المطلة على المحيط الأطلسي والتي تتميز بحركية اقتصادية وتجارية وتركيز سكاني." },
    5: { name: "الاتحاد", desc: "يقصد به التعاون والتنسيق لتقليص الفوارق بين مجموعة دول في مختلف الميادين مثل الاتحاد الأوروبي." },
    6: { name: "الإتحاد الأوروبي", desc: "تكتل اقتصادي سياسي ثقافي اجتماعي، ظهر بموجب معاهدة روما 1957 ويبلغ تعداد دوله حالياً 27 دولة بعد انسحاب بريطانيا، يهدف لتحقيق التعاون والتكامل بين دوله." },
    7: { name: "الاندماج (التكامل) الاقتصادي", desc: "يقصد به توحيد السياسات الاقتصادية بين عدة دول من خلال الاستغلال الموحد للإمكانيات الطبيعية والبشرية مما يؤدي لزيادة الإنتاجية المشتركة للدول." },
    8: { name: "التكتل", desc: "توحيد كل الإمكانيات المتاحة في دولتين أو أكثر واستغلالها بطريقة مشتركة لرفع القدرة الإنتاجية وقد يكون تكتل سياسي أو اقتصادي أو عسكري." },
    9: { name: "معاهدة روما", desc: "25 مارس 1957 بإيطاليا ضمت كل من (فرنسا - إيطاليا - ألمانيا غ - بلجيكا - لكسمبورغ - هولندا) تنص على إنشاء سوق أوروبية مشتركة مقرها بروكسل تعتبر نواة الاتحاد الأوروبي." },
    10: { name: "البينيلوكس", desc: "اتحاد اقتصادي تأسس 1944 ضم كل من (هولندا - بلجيكا - لكسمبورغ) ومنه جاءت فكرة إنشاء السوق الأوروبية المشتركة." },
    11: { name: "الاستقطاب", desc: "جذب للأموال، الأفراد والشركات والمشاريع نحو (دولة، منطقة، إقليم) لتحقيق الربح المالي." },
    12: { name: "الأراضي المنخفضة", desc: "مملكة هولندا أطلقت عليها هذه التسمية لأن أراضيها تحت مستوى سطح البحر." },
    13: { name: "معاهدة ماستريخت", desc: "تأسس من خلالها الاتحاد الأوروبي وُقعت في مدينة ماستريخت الهولندية 1992 ودخلت حيز التنفيذ 1993 حددت كل شروط الانضمام للاتحاد وقوانين." },
    14: { name: "السوق المشتركة", desc: "منظمة إقليمية تهدف لتحقيق التكامل الاقتصادي بين الدول الأعضاء أنشأتها معاهدة روما 1957 بإنشاء سوق موحدة وإلغاء الرسوم الجمركية بين الدول الأعضاء." },
    15: { name: "منطقة اليورو", desc: "مجموعة دول داخل الاتحاد الأوروبي اعتمدت عملة موحدة \"الأورو\" أنشئت في 1999 تضم 19 دولة بدأ العمل بها في 01 جانفي 2002." },
    16: { name: "التنينات الأربعة", desc: "مصطلح جغرافي اقتصادي، يطلق على أربع دول آسيوية حققت نمواً اقتصادياً سريعاً وهي: (كوريا الجنوبية، هونغ كونغ، سنغافورة، تايوان)." },
    17: { name: "النمور الأربعة", desc: "جمعية جنوب شرق آسيا تأسست بتايلندا 1967 تضم عشر دول مقرها أندونيسيا وتضم (أندونيسيا - تايلندا - سنغافورة - الفلبين - ماليزيا - بروناي - فيتنام - لاوس - ميانمار - كمبوديا)." },
    18: { name: "الآسيان", desc: "جمعية جنوب شرق آسيا تأسست بتايلندا 1967 تضم عشر دول مقرها أندونيسيا وتضم (أندونيسيا - تايلندا - سنغافورة - الفلبين - ماليزيا - بروناي - فيتنام - لاوس - ميانمار - كمبوديا)." },
    19: { name: "اتفاقية لومي", desc: "اتفاقية وقعت 1975 بين الاتحاد الأوروبي ودول أفريقيا وتمنح الاتفاقية للصادرات الإفريقية إلى الاتحاد الأوروبي مزايا منها إعفاء من الرسوم الجمركية." },
    20: { name: "القطب الاقتصادي", desc: "مركز يمثل نقطة قوة ونشاط اقتصادي تتوفر على جميع الشروط من أموال وبنية تحتية وتكنولوجيا ويتنافس مع أقطاب أخرى." },
    21: { name: "الوزن الديمغرافي", desc: "القوة البشرية الفتية التي تمثل عامل قوة عند استثمارها عقلانياً في العملية الإنتاجية لتحقيق التنمية." },
    22: { name: "مجمع المدن (ميغالوبوليس)", desc: "تجمع حضري لمجموعة من المدن الكبرى ذات كثافة سكانية كبيرة وذات نشاط اقتصادي كثيف." }       
        }
    }
};

let currentUnit = ""; 
let navigationStack = ['page1'];
const backBtn = document.getElementById("backBtn");

// 1. تعريف الصوت في البداية (تأكدي أن الرابط يعمل)
let alarm = new Audio('https://actions.google.com/sounds/v1/alarms/digital_watch_alarm_long.ogg');
alarm.loop = true; 

// 2. دالة التنقل الموحدة
function showPage(pageId) {
    const allPages = document.querySelectorAll('.page');
    allPages.forEach(p => {
        p.classList.remove('active');
        p.style.display = 'none';
    });

    const target = document.getElementById(pageId);
    if (target) {
        target.classList.add('active');
        target.style.display = 'flex';
        if (navigationStack[navigationStack.length - 1] !== pageId) {
            navigationStack.push(pageId);
        }
    }

    backBtn.style.display = (pageId === "page1") ? "none" : "flex";
}

// 3. زر الرجوع
backBtn.onclick = () => {
    if (navigationStack.length > 1) {
        navigationStack.pop(); 
        const previousPage = navigationStack[navigationStack.length - 1];
        
        document.querySelectorAll('.page').forEach(p => {
            p.classList.remove('active');
            p.style.display = 'none';
        });
        
        const target = document.getElementById(previousPage);
        if (target) {
            target.classList.add('active');
            target.style.display = 'flex';
        }
        backBtn.style.display = (previousPage === "page1") ? "none" : "flex";
    }
};

// 4. ربط الأزرار والوحدات
document.getElementById("goPage2").onclick = () => showPage('page2');
document.getElementById("goPage3").onclick = () => showPage('page3');

document.querySelectorAll('.subject').forEach(sub => {
    let text = sub.innerText.trim();
    if(text === "التاريخ") sub.onclick = () => showPage('historyUnitsPage');
    if(text === "الجغرافيا") sub.onclick = () => showPage('geoUnitsPage');
});

function showSubMenu(unitName) {
    currentUnit = unitName;
    document.getElementById('unitMenuTitle').innerText = unitName;
    showPage('unitSubMenuPage');
}
// تعديل زر الدروس في قائمة التاريخ
document.getElementById('lessonsBtn').onclick = function() {
    if (currentUnit === "الحرب الباردة") {
        showPage('historyLessonsPage');
    } else {
        // هنا يمكنك إضافة دروس الوحدات الأخرى لاحقاً
        alert("دروس " + currentUnit + " ستتوفر قريباً");
    }
};

// دالة مؤقتة لما يحدث عند الضغط على الدرس (يمكننا تطويرها لاحقاً)
function showLessonParts(lessonName) {
    console.log("تم اختيار درس: " + lessonName);
    // يمكنك هنا توجيه المستخدم لصفحة تفاصيل الدرس
}
// 6. الجغرافيا
let currentGeoUnit = "";
function showGeoSubMenu(unitName) {
    currentGeoUnit = unitName;
    document.getElementById('geoUnitMenuTitle').innerText = unitName;
    document.getElementById('geoTermsBtn').onclick = () => {
        let count = (unitName === 'واقع الاقتصاد العالمي') ? 65 : (unitName === 'القوى الاقتصادية الكبرى في العالم' ? 25 : 22);
        showDetailsGrid('مصطلحات', count);
    };
    document.getElementById('geoLessonsBtn').onclick = () => setupGeoLessons(unitName);
    showPage('geoSubMenuPage');
}

function setupGeoLessons(unitName) {
    const stack = document.getElementById('geoLessonsStack');
    document.getElementById('geoLessonsTitle').innerText = "دروس " + unitName;
    stack.innerHTML = ""; 
    let lessons = (unitName === 'واقع الاقتصاد العالمي') ? ["الدرس الأول", "الدرس الثاني"] : 
                  (unitName === 'القوى الاقتصادية الكبرى في العالم' ? ["الدرس الأول", "الدرس الثاني", "الدرس الثالث"] : ["الدرس الأول", "الدرس الثاني"]);
    lessons.forEach(lesson => {
        const div = document.createElement('div');
        div.classList.add('lesson-item');
        div.innerText = lesson;
        stack.appendChild(div);
    });
    showPage('geoLessonsListPage');
}

// 7. دوال العرض
function startChallenge(q, a) {
    document.getElementById('yaltaQuestion').innerText = q;
    document.getElementById('yaltaAnswer').innerText = a;
    document.getElementById('yaltaAnswerArea').style.display = "none";
    showPage('yaltaPage');
}
function showYaltaAnswer() { document.getElementById('yaltaAnswerArea').style.display = "block"; }
function goToLovePage() { showPage('lovePage'); }
function showHitlerAnswer() { document.getElementById('hitlerAnswerArea').style.display = "block"; }
function showIlysmPage() { showPage('ilysmPage'); }
function showInLovePage() { showPage('inLovePage'); }
function showAmwahPage() { showPage('amwahPage'); }

function startTermChallenge(name, desc) {
    document.getElementById('termNameDisplay').innerText = name;
    document.getElementById('termDescDisplay').innerText = desc;
    document.getElementById('termAnswerArea').style.display = "none";
    showPage('termPage');
}
function showTermAnswer() { document.getElementById('termAnswerArea').style.display = "block"; }

function startDzChallenge(q, a) {
    document.getElementById('dzQuestion').innerText = q;
    document.getElementById('dzAnswerDisplay').innerText = a;
    document.getElementById('dzAnswerArea').style.display = "none";
    showPage('dzDatesPage');
}
function showDzAnswer() { document.getElementById('dzAnswerArea').style.display = "block"; }

function startDzCharChallenge(name, desc) {
    document.getElementById('dzCharName').innerText = name;
    document.getElementById('dzCharDesc').innerText = desc;
    document.getElementById('dzCharAnswerArea').style.display = "none"; 
    showPage('dzCharactersPage');
}
function showDzCharAnswer() { document.getElementById('dzCharAnswerArea').style.display = "block"; }

// 8. الشرر
document.addEventListener("click", (e) => {
    for(let i=0; i<8; i++){
        const spark = document.createElement("div");
        spark.classList.add("spark");
        spark.style.left = e.pageX + "px";
        spark.style.top = e.pageY + "px";
        spark.style.setProperty('--x', (Math.random()*60 - 30) + 'px');
        spark.style.setProperty('--y', (Math.random()*60 - 30) + 'px');
        document.body.appendChild(spark);
        setTimeout(() => spark.remove(), 500);
    }
});

function answerTodo(choice) {
    const res = document.getElementById('todoResponse');
    res.innerText = (choice === 'yes') ? "come to mommy so I give you a kiss 🫦" : "انا نسلم في كل الأحوال زعما 😉";
}

// 9. بومودورو المطور (النسخة النهائية مع تفعيل زر 🔃)
let timers = {
    study: { seconds: 1500, initial: 1500, interval: null, running: false },
    break: { seconds: 300, initial: 300, interval: null, running: false }
};
let totalStudySeconds = 0;

function startTimer(type) {
    if (timers[type].running) return;

    // الحصول على الوقت المكتوب في الخانة
    let valInput = parseInt(document.getElementById(type + 'Input').value);
    let userSetSeconds = valInput ? valInput * 60 : (type === 'study' ? 1500 : 300);

    // إذا كان العداد في البداية أو منتهياً، نعتمد الوقت الجديد
    if (timers[type].seconds === timers[type].initial || timers[type].seconds <= 0) {
        timers[type].initial = userSetSeconds;
        timers[type].seconds = userSetSeconds;
    }

    timers[type].running = true;
    const btn = document.getElementById(type + 'StartBtn');
    btn.innerText = "Pause";
    btn.onclick = () => pauseTimer(type);

    timers[type].interval = setInterval(() => {
        if (timers[type].seconds > 0) {
            timers[type].seconds--;
            updateTimerDisplay(type);
        } else {
            finishSession(type);
        }
    }, 1000);
}

function pauseTimer(type) {
    clearInterval(timers[type].interval);
    timers[type].running = false;
    
    const btn = document.getElementById(type + 'StartBtn');
    btn.innerText = "Start";
    btn.onclick = () => startTimer(type);

    document.getElementById(type + 'PauseOptions').style.display = 'flex';
}

function continueTimer(type) {
    alarm.pause();
    alarm.currentTime = 0;
    document.getElementById(type + 'PauseOptions').style.display = 'none';
    startTimer(type); 
}

function resetTimer(type) {
    alarm.pause();
    alarm.currentTime = 0;

    // الزيادة في المربع الأبيض تحدث فقط هنا عند ضغط Done للدراسة
    if (type === 'study') {
        let timeSpent = timers.study.initial - timers.study.seconds;
        if (timeSpent > 0) {
            totalStudySeconds += timeSpent;
            updateTotalDisplay();
        }
    }

    clearInterval(timers[type].interval);
    timers[type].running = false;
    
    let valInput = parseInt(document.getElementById(type + 'Input').value);
    let resetVal = valInput ? valInput * 60 : (type === 'study' ? 1500 : 300);
    timers[type].seconds = resetVal;
    timers[type].initial = resetVal;
    
    updateTimerDisplay(type);
    document.getElementById(type + 'PauseOptions').style.display = 'none';
    
    const btn = document.getElementById(type + 'StartBtn');
    btn.style.display = 'inline-block';
    btn.innerText = "Start";
    btn.onclick = () => startTimer(type);
}

function finishSession(type) {
    clearInterval(timers[type].interval);
    timers[type].running = false;

    alarm.play(); // رنين المنبه

    // المربع الأبيض لا يزيد تلقائياً هنا (ينتظر ضغط Done)
    const btn = document.getElementById(type + 'StartBtn');
    btn.innerText = "Start";
    btn.onclick = () => startTimer(type);
    document.getElementById(type + 'PauseOptions').style.display = 'flex';
}

function updateTimerDisplay(type) {
    let m = Math.floor(timers[type].seconds / 60), s = timers[type].seconds % 60;
    document.getElementById(type + 'Display').innerText = `${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
}

// --- الدوال الخاصة بالمربع الأبيض وإعادة التعيين الكلي ---

function updateTotalDisplay() {
    let h = Math.floor(totalStudySeconds / 3600), m = Math.floor((totalStudySeconds % 3600) / 60), s = totalStudySeconds % 60;
    document.getElementById('totalDisplay').innerText = 
        `${h.toString().padStart(2, '0')}:${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
}

// هذه الدالة مرتبطة برمز 🔃 لصفر المربع الأبيض
function resetTotalStudyTime() {  
        totalStudySeconds = 0;
        updateTotalDisplay();
    }


function startGeoTermChallenge(name, desc, targetPage, encouragementMsg) {
    document.getElementById('termNameDisplay').innerText = "عرف: " + name;
    document.getElementById('termDescDisplay').innerText = desc;
    
    // تغيير رسالة التشجيع بناءً على ما أرسلناه في الدالة
    const encouragement = document.querySelector('#termAnswerArea p');
    if (encouragement) {
        encouragement.innerText = encouragementMsg;
        // تغيير اللون قليلاً للوحدة الثالثة ليتماشى مع القلب البنفسجي
        encouragement.style.color = (encouragementMsg.includes('تعنيقة')) ? "#d1c4e9" : "#ffd6ff"; 
    }

    const termPage = document.getElementById('termPage');
    const doneBtn = termPage.querySelector('.subject:last-child');
    if (doneBtn) {
        doneBtn.setAttribute("onclick", `showPage('${targetPage}')`);
    }

    document.getElementById('termAnswerArea').style.display = "none";
    showPage('termPage');
}
function showDetailsGrid(title, count) {
    const unitName = currentUnit || currentGeoUnit;
    document.getElementById('gridTitle').innerText = title + " - " + unitName;
    const container = document.getElementById('gridItems');
    container.innerHTML = ""; 

    for(let i=1; i<=count; i++) {
        const box = document.createElement('div');
        box.classList.add('grid-box');
        box.innerText = i;
        
        box.onclick = () => {
            // البحث عن البيانات في الـ Object
            const unitItems = appData[unitName];
            const itemType = title; // "شخصيات" أو "تواريخ" أو "مصطلحات"
            
            if (unitItems && unitItems[itemType] && unitItems[itemType][i]) {
                const data = unitItems[itemType][i];
                
                // تحديد أي تحدي سنعرض بناءً على النوع
                if (itemType === "تواريخ") {
                    if (unitName === "الثورة التحريرية") startDzChallenge(data.name, data.date);
                    else startChallenge(data.name, data.date);
                } 
                else if (itemType === "شخصيات") {
                    if (data.name === "أدولف هتلر") showPage('hitlerPage');
                    else if (unitName === "الثورة التحريرية") startDzCharChallenge(data.name, data.desc);
                    else startChallenge(data.name, data.desc);
                }
                else if (itemType === "مصطلحات") {
                    if (currentGeoUnit) {
                        // تخصيص صفحة النجاح حسب الوحدة في الجغرافيا
                        let target = currentGeoUnit === 'واقع الاقتصاد العالمي' ? 'geoSuccessPage' : 'geoUnit2Page';
                        startGeoTermChallenge(data.name, data.desc, target, "باينة ولدي عرفها و راه يتأكد ياك؟😔");
                    } else {
                        startTermChallenge(data.name, data.desc);
                    }
                }
            } else {
                alert("هذا المربع فارغ حالياً، أضيفي بياناته في appData!");
            }
        };
        container.appendChild(box);
    }
    showPage('gridPage');
}
// تعديل الدالة لفتح صفحة الدرس الأول
function showLessonParts(lessonName) {
    if (lessonName === 'بروز الصراع وتشكّل العالم') {
        showPage('lesson1Page');
    }
}

// دالة مؤقتة عند الضغط على الأرقام 1-6
function showPartDetail(partNumber) {
    console.log("تم فتح الجزء رقم: " + partNumber);
    // هنا سنضع لاحقاً محتوى كل عنصر (مثلاً: معايير تشكل العالم، طبيعة الصراع، إلخ)
}
// تعديل دالة الضغط على المربع رقم 1
function showPartDetail(partNumber) {
    if (partNumber === 1) {
        showPage('questionPage1');
    }
    else if (partNumber === 2) {
        showPage('questionPage2');
    }
    else if (partNumber === 3) {
        showPage('questionPage3');
    }
    else if (partNumber === 4) {
        showPage('questionPage4');
    }
    else if (partNumber === 5) {
        showPage('questionPage5');
    }
    else if (partNumber === 6) {
        showPage('questionPage6');
    }
    else if (partNumber === 7) {
        showPage('questionPage7');
    }
}
// دالة الرد بـ "واه"
function answerWah() {
    document.getElementById('wahResponse').style.display = 'block';
}

// منطق هروب زر "لاء"
const noBtn = document.getElementById('noBtn');
function answerWah2() {
    document.getElementById('wahResponse2').style.display = 'block';
}
const noBtn2 = document.getElementById('noBtn2');

if(noBtn2) {
    noBtn2.addEventListener('mouseover', () => moveButton(noBtn2));
    noBtn2.addEventListener('touchstart', (e) => {
        e.preventDefault();
        moveButton(noBtn2);
    });
}
function answerWah3() {
    document.getElementById('wahResponse3').style.display = 'block';
}
const noBtn3 = document.getElementById('noBtn3');

if(noBtn3) {
    noBtn3.addEventListener('mouseover', () => moveButton(noBtn3));
    noBtn3.addEventListener('touchstart', (e) => {
        e.preventDefault();
        moveButton(noBtn3);
    });
}
// دالة التحريك الذكية
function moveButton(btn) {
    // تحديد منطقة التحرك (داخل حدود الشاشة مع ترك مسافة أمان)
    const padding = 50;
    const maxX = window.innerWidth - btn.clientWidth - padding;
    const maxY = window.innerHeight - btn.clientHeight - padding;

    const randomX = Math.floor(Math.random() * maxX);
    const randomY = Math.floor(Math.random() * maxY);

    btn.style.position = 'fixed';
    btn.style.transition = 'all 0.2s ease'; // حركة سريعة وسلسة
    btn.style.left = randomX + 'px';
    btn.style.top = randomY + 'px';
    btn.style.zIndex = '9999';
}

// الهروب عند مرور الفأرة (للحاسوب)
noBtn.addEventListener('mouseover', () => moveButton(noBtn));

// الهروب عند اللمس (للهاتف)
noBtn.addEventListener('touchstart', (e) => {
    e.preventDefault(); // يمنع النقر الفعلي
    moveButton(noBtn);
});
</script>

</body>
</html>
