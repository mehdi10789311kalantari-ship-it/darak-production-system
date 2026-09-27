# darak-production-system
index.html
<!DOCTYPE html>
<html lang="fa">
<head>
<meta charset="UTF-8">
<title>اپ موبایلی تولید کارخانه دراک</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
    body {
        font-family: tahoma;
        background: #f0f0f0;
        padding: 10px;
        direction: rtl;
    }
    .box {
        background: white;
        padding: 18px;
        border-radius: 14px;
        margin-bottom: 18px;
        box-shadow: 0 0 12px #ccc;
    }
    h3 {
        margin-top: 0;
        font-size: 20px;
        text-align: center;
    }
    input, select {
        width: 100%;
        padding: 14px;
        margin-top: 10px;
        border-radius: 10px;
        border: 1px solid #aaa;
        font-size: 18px;
    }
    button {
        width: 100%;
        padding: 16px;
        background: #007bff;
        color: white;
        border: none;
        border-radius: 10px;
        margin-top: 18px;
        font-size: 20px;
        font-weight: bold;
        cursor: pointer;
    }
    #result {
        background: #fff;
        padding: 18px;
        border-radius: 14px;
        box-shadow: 0 0 12px #ccc;
        margin-top: 20px;
        display: none;
        font-size: 18px;
    }
</style>
</head>
<body>

<div class="box">
    <h3>ثبت تولید روزانه</h3>

    <label>دستگاه:</label>
    <select id="device">
        <option value="250">اکسترودر ۹۰</option>
        <option value="180">اکسترودر ۴۵</option>
        <option value="220">اکسترودر ۶۰</option>
        <option value="200">اکسترودر ۶۰ فوم</option>
        <option value="150">اکسترودر نسوز</option>
        <option value="300">فاین ۱</option>
        <option value="300">فاین ۲</option>
        <option value="300">فاین ۳</option>
        <option value="300">فاین ۴</option>
        <option value="200">آنیلر ۱</option>
        <option value="200">آنیلر ۲</option>
        <option value="200">آنیلر ۳</option>
        <option value="200">آنیلر ۴</option>
        <option value="100">ریواندر کابل دستی</option>
        <option value="120">ریواندر کابل اتومات</option>
        <option value="90">ریواندر سیم دستی</option>
        <option value="110">ریواندر سیم اتومات</option>
        <option value="130">بریدر ۱</option>
        <option value="130">بریدر ۲</option>
        <option value="160">کشش</option>
        <option value="140">نوارپیچ</option>
        <option value="170">بانچر</option>
        <option value="180">مدیوم</option>
        <option value="80">شیرینگ پک</option>
    </select>

    <label>تولید واقعی (کیلو):</label>
    <input type="number" id="realProd">

    <label>ضایعات (کیلو):</label>
    <input type="number" id="scrap">

    <label>توقف دستگاه (ساعت):</label>
    <input type="number" id="stop">

    <button onclick="calcOPE()">محاسبه OPE دستگاه</button>
</div>


<div class="box">
    <h3>ثبت حضور اپراتور</h3>

    <label>ساعت کار اپراتور:</label>
    <input type="number" id="opHours">

    <label>جمع ساعات کل دستگاه:</label>
    <input type="number" id="totalHours">

    <label>ضریب رفتار:</label>
    <select id="behavior">
        <option value="1">عالی (1)</option>
        <option value="0.95">خوب (0.95)</option>
        <option value="0.9">متوسط (0.9)</option>
        <option value="0.85">ضعیف (0.85)</option>
    </select>

    <button onclick="calcOperator()">محاسبه امتیاز اپراتور</button>
</div>


<div id="result"></div>


<script>
function calcOPE() {
    let std = Number(document.getElementById("device").value);
    let real = Number(document.getElementById("realProd").value);
    let scrap = Number(document.getElementById("scrap").value);
    let stop = Number(document.getElementById("stop").value);

    let shift = 8;
    let useful = shift - stop;

    let A = useful / shift;
    let P = real / (std * shift);
    let Q = (real - scrap) / real;

    let OPE = A * P * Q;

    window.OPEvalue = OPE;

    document.getElementById("result").style.display = "block";
    document.getElementById("result").innerHTML =
        "<h3>نتیجه OPE دستگاه:</h3>" +
        "<p>Availability: " + A.toFixed(3) + "</p>" +
        "<p>Performance: " + P.toFixed(3) + "</p>" +
        "<p>Quality: " + Q.toFixed(3) + "</p>" +
        "<p><b>OPE دستگاه: " + OPE.toFixed(3) + "</b></p>";
}

function calcOperator() {
    let opH = Number(document.getElementById("opHours").value);
    let totH = Number(document.getElementById("totalHours").value);
    let beh = Number(document.getElementById("behavior").value);

    let share = opH / totH;
    let score = window.OPEvalue * share * beh;

    document.getElementById("result").style.display = "block";
    document.getElementById("
