<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حاسبة السلطي</title>
    <style>
        :root {
            --bg-color: #121212;
            --card-bg: #1e1e1e;
            --input-bg: #2a2a2a;
            --border-color: #3f3f46;
            --primary-blue: #2563eb;
            --text-main: #ffffff;
            --text-muted: #a1a1aa;
            --green-accent: #22c55e;
            --red-accent: #ef4444;
            --yellow-accent: #eab308;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .calculator-card {
            background-color: var(--card-bg);
            width: 100%;
            max-width: 480px;
            border-radius: 16px;
            padding: 24px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            border: 1px solid var(--border-color);
        }

        .header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 20px;
        }

        .header h2 {
            font-size: 1.25rem;
            color: var(--text-main);
        }

        .section-box {
            border: 1px dashed var(--border-color);
            border-radius: 12px;
            padding: 16px;
            margin-bottom: 20px;
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 12px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            margin-bottom: 12px;
        }

        label {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-bottom: 6px;
        }

        input {
            background-color: var(--input-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 12px;
            color: #fff;
            font-size: 1rem;
            text-align: center;
            outline: none;
            transition: border-color 0.2s;
        }

        input:focus {
            border-color: var(--primary-blue);
        }

        .btn-submit {
            width: 100%;
            background-color: var(--primary-blue);
            color: white;
            border: none;
            padding: 14px;
            font-size: 1.05rem;
            font-weight: bold;
            border-radius: 10px;
            cursor: pointer;
            margin-top: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }

        .btn-submit:hover {
            background-color: #1d4ed8;
        }

        .results-container {
            margin-top: 24px;
            border-top: 1px solid var(--border-color);
            padding-top: 20px;
        }

        .result-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            font-size: 0.95rem;
        }

        .result-row .label {
            color: var(--text-muted);
        }

        .result-row .value {
            font-weight: bold;
            font-size: 1.1rem;
        }

        .val-red {
            color: var(--red-accent) !important;
        }

        .val-yellow {
            color: var(--yellow-accent) !important;
        }

        .val-green-highlight {
            color: var(--green-accent) !important;
            font-size: 1.4rem !important;
        }
    </style>
</head>
<body>

<div class="calculator-card">
    <div class="header">
        <h2>I'm سلطان 🌐</h2>
    </div>

    <!-- قسم الراتب الأول -->
    <div class="grid-2">
        <div class="form-group">
            <label>الراتب الأول (ريال)</label>
            <input type="number" id="salary1" value="8900" oninput="calculate()">
        </div>
        <div class="form-group">
            <label>أضعاف الراتب الأول</label>
            <input type="number" id="multiplier1" value="16" oninput="calculate()">
        </div>
    </div>

    <!-- قسم الراتب الثاني -->
    <div class="section-box">
        <div class="grid-2">
            <div class="form-group">
                <label>الراتب الثاني (ريال)</label>
                <input type="number" id="salary2" value="8900" oninput="calculate()">
            </div>
            <div class="form-group">
                <label>أضعاف الراتب الثاني</label>
                <input type="number" id="multiplier2" value="12" oninput="calculate()">
            </div>
        </div>
    </div>

    <!-- التزامات العميل وعمولة المكتب -->
    <div class="form-group">
        <label>التزامات العميل (مبلغ السداد)</label>
        <input type="number" id="commitments" value="190000" oninput="calculate()">
    </div>

    <div class="form-group">
        <label>نسبة عمولة المكتب (%)</label>
        <input type="number" step="0.1" id="commissionRate" value="8.1" oninput="calculate()">
    </div>

    <button class="btn-submit" onclick="calculate()">حساب التقرير المالي 📊</button>

    <!-- نتائج التقرير المالي -->
    <div class="results-container">
        <div class="result-row">
            <span class="label">تمويل الراتب الأول:</span>
            <span class="value" id="resLoan1">142,400 ر.س</span>
        </div>
        <div class="result-row">
            <span class="label">تمويل الراتب الثاني:</span>
            <span class="value" id="resLoan2">106,800 ر.س</span>
        </div>
        <div class="result-row">
            <span class="label">إجمالي التمويل الكامل:</span>
            <span class="value" id="resTotalLoan">249,200 ر.س</span>
        </div>
        <div class="result-row">
            <span class="label">سداد الالتزامات:</span>
            <span class="value val-red" id="resCommitments">-190,000 ر.س</span>
        </div>
        <div class="result-row">
            <span class="label">ربح المكتب:</span>
            <span class="value val-yellow" id="resCommission">-20,185.2 ر.س</span>
        </div>
        <div class="result-row" style="margin-top: 15px; border-top: 1px dashed var(--border-color); padding-top: 12px;">
            <span class="label" style="font-weight: bold; color: #fff; font-size: 1.1rem;">صافي العميل:</span>
            <span class="value val-green-highlight" id="resNetClient">39,014.8 ر.س</span>
        </div>
    </div>
</div>

<script>
function calculate() {
    const salary1 = parseFloat(document.getElementById('salary1').value) || 0;
    const mult1 = parseFloat(document.getElementById('multiplier1').value) || 0;
    const salary2 = parseFloat(document.getElementById('salary2').value) || 0;
    const mult2 = parseFloat(document.getElementById('multiplier2').value) || 0;
    const commitments = parseFloat(document.getElementById('commitments').value) || 0;
    const commRate = parseFloat(document.getElementById('commissionRate').value) || 0;

    // حساب التمويلات
    const loan1 = salary1 * mult1;
    const loan2 = salary2 * mult2;
    const totalLoan = loan1 + loan2;

    // حساب العمولة وصافي العميل
    const commission = totalLoan * (commRate / 100);
    const netClient = totalLoan - commitments - commission;

    // تحديث النتائج
    document.getElementById('resLoan1').innerText = loan1.toLocaleString('en-US') + ' ر.س';
    document.getElementById('resLoan2').innerText = loan2.toLocaleString('en-US') + ' ر.س';
    document.getElementById('resTotalLoan').innerText = totalLoan.toLocaleString('en-US') + ' ر.س';
    document.getElementById('resCommitments').innerText = '-' + commitments.toLocaleString('en-US') + ' ر.س';
    document.getElementById('resCommission').innerText = '-' + commission.toLocaleString('en-US', {maximumFractionDigits: 2}) + ' ر.س';
    document.getElementById('resNetClient').innerText = netClient.toLocaleString('en-US', {maximumFractionDigits: 2}) + ' ر.س';
}

// التشغيل الأولي عند التحميل
calculate();
</script>

</body>
</html>
