# -<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ابزارهای ریاضی پیشرفته</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            overflow: hidden;
        }
        
        header {
            background: #2c3e50;
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        
        .tabs {
            display: flex;
            flex-wrap: wrap;
            background: #34495e;
            padding: 0;
            gap: 1px;
        }
        
        .tab {
            padding: 15px 20px;
            cursor: pointer;
            color: white;
            border: none;
            background: #4a6fa5;
            font-size: 14px;
            transition: all 0.3s ease;
            flex: 1;
            min-width: 120px;
        }
        
        .tab:hover {
            background: #5a7fb5;
        }
        
        .tab.active {
            background: #e74c3c;
        }
        
        .tab-content {
            display: none;
            padding: 30px;
            min-height: 500px;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .calculator {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            align-items: start;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        input, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #bdc3c7;
            border-radius: 8px;
            font-size: 16px;
        }
        
        button {
            background: #e74c3c;
            color: white;
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s ease;
            margin: 5px;
        }
        
        button:hover {
            background: #c0392b;
        }
        
        .result {
            background: #ecf0f1;
            padding: 20px;
            border-radius: 8px;
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
            white-space: pre-wrap;
        }
        
        .multi-input {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        
        .multi-input input {
            flex: 1;
        }
        
        @media (max-width: 768px) {
            .calculator {
                grid-template-columns: 1fr;
            }
            
            .tabs {
                flex-direction: column;
            }
            
            .tab {
                min-width: auto;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🧮 ابزارهای ریاضی پیشرفته</h1>
            <p>محاسبات ریاضی را ساده و سریع انجام دهید</p>
        </header>
        
        <div class="tabs" id="tabsContainer">
            <!-- تب‌ها با JavaScript ساخته خواهند شد -->
        </div>
        
        <div id="tabContents">
            <!-- محتوای تب‌ها با JavaScript ساخته خواهد شد -->
        </div>
    </div>

    <script>
        const mathTools = [
            'تشخیص اول',
            'تجزیه عوامل',
            'شمارش مقسوم‌علیه',
            'ب م م / ک م م',
            'توان',
            'فاکتوریل',
            'رادیکال',
            'دایره',
            'فیثاغورث',
            'ضلع مجهول',
            'زوایای چندضلعی',
            'ماشین حساب',
            'کسر مصری',
            'ترکیب',
            'مثلث خیام',
            'میانگین'
        ];

        const tabsContainer = document.getElementById('tabsContainer');
        const tabContents = document.getElementById('tabContents');

        mathTools.forEach((tool, index) => {
            const tab = document.createElement('button');
            tab.className = 'tab' + (index === 0 ? ' active' : '');
            tab.textContent = tool;
            tab.onclick = () => switchTab(index);
            tabsContainer.appendChild(tab);

            const content = document.createElement('div');
            content.className = 'tab-content' + (index === 0 ? ' active' : '');
            content.id = 'tab' + index;
            content.innerHTML = createToolContent(tool);
            tabContents.appendChild(content);
        });

        function switchTab(index) {
            document.querySelectorAll('.tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            document.querySelectorAll('.tab')[index].classList.add('active');
            document.getElementById('tab' + index).classList.add('active');
        }

        function createToolContent(toolName) {
            const contents = {
                'تشخیص اول': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عدد را وارد کنید:</label>
                                <input type="number" id="primeInput" min="2" placeholder="مثلا: 17">
                            </div>
                            <button onclick="checkPrime()">بررسی اول بودن</button>
                        </div>
                        <div class="result" id="primeResult"></div>
                    </div>
                `,
                
                'تجزیه عوامل': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عدد را وارد کنید:</label>
                                <input type="number" id="factorInput" min="2" placeholder="مثلا: 36">
                            </div>
                            <button onclick="factorize()">تجزیه عوامل اول</button>
                        </div>
                        <div class="result" id="factorResult"></div>
                    </div>
                `,
                
                'شمارش مقسوم‌علیه': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عدد را وارد کنید:</label>
                                <input type="number" id="divisorInput" min="1" placeholder="مثلا: 12">
                            </div>
                            <button onclick="countDivisors()">شمارش مقسوم‌علیه‌ها</button>
                        </div>
                        <div class="result" id="divisorResult"></div>
                    </div>
                `,
                
                'ب م م / ک م م': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عدد اول:</label>
                                <input type="number" id="num1" placeholder="مثلا: 12">
                            </div>
                            <div class="input-group">
                                <label>عدد دوم:</label>
                                <input type="number" id="num2" placeholder="مثلا: 18">
                            </div>
                            <button onclick="calculateGCDLCM()">محاسبه ب م م و ک م م</button>
                        </div>
                        <div class="result" id="gcdlcmResult"></div>
                    </div>
                `,
                
                'توان': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>پایه:</label>
                                <input type="number" id="baseInput" placeholder="مثلا: 2">
                            </div>
                            <div class="input-group">
                                <label>توان:</label>
                                <input type="number" id="exponentInput" placeholder="مثلا: 3">
                            </div>
                            <button onclick="calculatePower()">محاسبه توان</button>
                        </div>
                        <div class="result" id="powerResult"></div>
                    </div>
                `,
                
                'فاکتوریل': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عدد را وارد کنید:</label>
                                <input type="number" id="factorialInput" min="0" max="100" placeholder="مثلا: 5">
                            </div>
                            <button onclick="calculateFactorial()">محاسبه فاکتوریل</button>
                        </div>
                        <div class="result" id="factorialResult"></div>
                    </div>
                `,
                
                'رادیکال': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عدد زیر رادیکال:</label>
                                <input type="number" id="radicandInput" min="0" placeholder="مثلا: 16">
                            </div>
                            <div class="input-group">
                                <label>درجه رادیکال:</label>
                                <input type="number" id="degreeInput" min="2" value="2" placeholder="مثلا: 2">
                            </div>
                            <button onclick="calculateRoot()">محاسبه رادیکال</button>
                        </div>
                        <div class="result" id="rootResult"></div>
                    </div>
                `,
                
                'دایره': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>شعاع دایره:</label>
                                <input type="number" id="radiusInput" min="0" placeholder="مثلا: 5">
                            </div>
                            <button onclick="calculateCircle(1)">محیط</button>
                            <button onclick="calculateCircle(2)">مساحت</button>
                            <button onclick="calculateCircle(3)">هر دو</button>
                        </div>
                        <div class="result" id="circleResult"></div>
                    </div>
                `,
                
                'فیثاغورث': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>ضلع اول (a):</label>
                                <input type="number" id="sideA" min="0" placeholder="مثلا: 3">
                            </div>
                            <div class="input-group">
                                <label>ضلع دوم (b):</label>
                                <input type="number" id="sideB" min="0" placeholder="مثلا: 4">
                            </div>
                            <button onclick="calculatePythagoras()">محاسبه وتر</button>
                        </div>
                        <div class="result" id="pythagorasResult"></div>
                    </div>
                `,
                
                'ضلع مجهول': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>وتر (c):</label>
                                <input type="number" id="hypotenuse" min="0" placeholder="مثلا: 5">
                            </div>
                            <div class="input-group">
                                <label>ضلع معلوم (a یا b):</label>
                                <input type="number" id="knownSide" min="0" placeholder="مثلا: 3">
                            </div>
                            <button onclick="findMissingSide()">پیدا کردن ضلع مجهول</button>
                        </div>
                        <div class="result" id="missingSideResult"></div>
                    </div>
                `,
                
                'زوایای چندضلعی': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>تعداد اضلاع (n):</label>
                                <input type="number" id="sidesCount" min="3" placeholder="مثلا: 5">
                            </div>
                            <button onclick="calculatePolygonAngles()">محاسبه زوایا</button>
                        </div>
                        <div class="result" id="polygonResult"></div>
                    </div>
                `,
                
                'ماشین حساب': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>عبارت ریاضی:</label>
                                <input type="text" id="calcInput" placeholder="مثلا: 2+3*4 یا sin(30)">
                            </div>
                            <button onclick="calculateExpression()">محاسبه</button>
                        </div>
                        <div class="result" id="calcResult"></div>
                    </div>
                `,
                
                'کسر مصری': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>صورت کسر:</label>
                                <input type="number" id="numerator" min="1" placeholder="مثلا: 4">
                            </div>
                            <div class="input-group">
                                <label>مخرج کسر:</label>
                                <input type="number" id="denominator" min="2" placeholder="مثلا: 5">
                            </div>
                            <button onclick="egyptianFraction()">تبدیل به کسر مصری</button>
                        </div>
                        <div class="result" id="egyptianResult"></div>
                    </div>
                `,
                
                'ترکیب': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>تعداد کل (n):</label>
                                <input type="number" id="nComb" min="1" placeholder="مثلا: 5">
                            </div>
                            <div class="input-group">
                                <label>تعداد انتخاب (r):</label>
                                <input type="number" id="rComb" min="0" placeholder="مثلا: 2">
                            </div>
                            <button onclick="calculateCombination()">محاسبه ترکیب</button>
                        </div>
                        <div class="result" id="combinationResult"></div>
                    </div>
                `,
                
                'مثلث خیام': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>سطر مورد نظر (0 تا 15):</label>
                                <input type="number" id="pascalRow" min="0" max="15" placeholder="مثلا: 5">
                            </div>
                            <button onclick="generatePascal()">نمایش سطر</button>
                            <button onclick="generatePascalTriangle()">نمایش مثلث</button>
                        </div>
                        <div class="result" id="pascalResult"></div>
                    </div>
                `,
                
                'میانگین': `
                    <div class="calculator">
                        <div>
                            <div class="input-group">
                                <label>اعداد (با کاما جدا کنید):</label>
                                <input type="text" id="numbersInput" placeholder="مثلا: 10,20,30,40">
                            </div>
                            <button onclick="calculateMean()">میانگین حسابی</button>
                            <button onclick="calculateMedian()">میانگین میانه</button>
                            <button onclick="calculateAllAverages()">همه میانگین‌ها</button>
                        </div>
                        <div class="result" id="averageResult"></div>
                    </div>
                `
            };

            return contents[toolName];
        }

        // توابع محاسباتی
        function checkPrime() {
            const num = parseInt(document.getElementById('primeInput').value);
            if (isNaN(num) || num < 2) {
                document.getElementById('primeResult').textContent = 'لطفا عددی بزرگتر از 1 وارد کنید';
                return;
            }

            let isPrime = true;
            for (let i = 2; i <= Math.sqrt(num); i++) {
                if (num % i === 0) {
                    isPrime = false;
                    break;
                }
            }

            document.getElementById('primeResult').textContent = 
                `${num} ${isPrime ? 'عدد اول است' : 'عدد اول نیست'}`;
        }

        function factorize() {
            const num = parseInt(document.getElementById('factorInput').value);
            if (isNaN(num) || num < 2) {
                document.getElementById('factorResult').textContent = 'لطفا عددی بزرگتر از 1 وارد کنید';
                return;
            }

            let factors = [];
            let temp = num;
            let divisor = 2;

            while (temp > 1) {
                if (temp % divisor === 0) {
                    factors.push(divisor);
                    temp /= divisor;
                } else {
                    divisor++;
                }
            }

            document.getElementById('factorResult').textContent = 
                `${num} = ${factors.join(' × ')}`;
        }

        function countDivisors() {
            const num = parseInt(document.getElementById('divisorInput').value);
            if (isNaN(num) || num < 1) {
                document.getElementById('divisorResult').textContent = 'لطفا عدد صحیح مثبت وارد کنید';
                return;
            }

            let count = 0;
            let divisors = [];
            for (let i = 1; i <= num; i++) {
                if (num % i === 0) {
                    count++;
                    divisors.push(i);
                }
            }

            document.getElementById('divisorResult').textContent = 
                `تعداد مقسوم‌علیه‌ها: ${count}\nمقسوم‌علیه‌ها: ${divisors.join(', ')}`;
        }

        function calculateGCDLCM() {
            const a = parseInt(document.getElementById('num1').value);
            const b = parseInt(document.getElementById('num2').value);
            
            if (isNaN(a) || isNaN(b)) {
                document.getElementById('gcdlcmResult').textContent = 'لطفا دو عدد وارد کنید';
                return;
            }

            function gcd(x, y) {
                return y === 0 ? x : gcd(y, x % y);
            }

            const gcdValue = gcd(Math.abs(a), Math.abs(b));
            const lcmValue = Math.abs(a * b) / gcdValue;

            document.getElementById('gcdlcmResult').textContent = 
                `ب م م (${a}, ${b}) = ${gcdValue}\nک م م (${a}, ${b}) = ${lcmValue}`;
        }

        function calculatePower() {
            const base = parseFloat(document.getElementById('baseInput').value);
            const exponent = parseFloat(document.getElementById('exponentInput').value);
            
            if (isNaN(base) || isNaN(exponent)) {
                document.getElementById('powerResult').textContent = 'لطفا مقادیر معتبر وارد کنید';
                return;
            }

            const result = Math.pow(base, exponent);
            document.getElementById('powerResult').textContent = 
                `${base}^${exponent} = ${result}`;
        }

        function calculateFactorial() {
            const num = parseInt(document.getElementById('factorialInput').value);
            if (isNaN(num) || num < 0) {
                document.getElementById('factorialResult').textContent = 'لطفا عدد صحیح غیرمنفی وارد کنید';
                return;
            }

            let result = 1n;
            for (let i = 2; i <= num; i++) {
                result *= BigInt(i);
            }

            document.getElementById('factorialResult').textContent = 
                `${num}! = ${result}`;
        }

        function calculateRoot() {
            const radicand = parseFloat(document.getElementById('radicandInput').value);
            const degree = parseFloat(document.getElementById('degreeInput').value);
            
            if (isNaN(radicand) || isNaN(degree) || radicand < 0) {
                document.getElementById('rootResult').textContent = 'لطفا مقادیر معتبر وارد کنید';
                return;
            }

            const result = Math.pow(radicand, 1/degree);
            document.getElementById('rootResult').textContent = 
                `⁰√${radicand} = ${result.toFixed(6)}`;
        }

        function calculateCircle(type) {
            const radius = parseFloat(document.getElementById('radiusInput').value);
            
            if (isNaN(radius) || radius < 0) {
                document.getElementById('circleResult').textContent = 'لطفا شعاع معتبر وارد کنید';
                return;
            }

            const circumference = (2 * Math.PI * radius).toFixed(4);
            const area = (Math.PI * radius * radius).toFixed(4);

            let result = '';
            if (type === 1) result = `محیط دایره: ${circumference}`;
            else if (type === 2) result = `مساحت دایره: ${area}`;
            else result = `محیط: ${circumference}\nمساحت: ${area}`;

            document.getElementById('circleResult').textContent = result;
        }

        function calculatePythagoras() {
            const a = parseFloat(document.getElementById('sideA').value);
            const b = parseFloat(document.getElementById('sideB').value);
            
            if (isNaN(a) || isNaN(b) || a < 0 || b < 0) {
                document.getElementById('pythagorasResult').textContent = 'لطفا اعداد معتبر وارد کنید';
                return;
            }

            const c = Math.sqrt(a*a + b*b).toFixed(4);
            document.getElementById('pythagorasResult').textContent = 
                `c = √(${a}² + ${b}²) = ${c}`;
        }

        function findMissingSide() {
            const hypotenuse = parseFloat(document.getElementById('hypotenuse').value);
            const knownSide = parseFloat(document.getElementById('knownSide').value);
            
            if (isNaN(hypotenuse) || isNaN(knownSide) || hypotenuse <= knownSide) {
                document.getElementById('missingSideResult').textContent = 'لطفا مقادیر معتبر وارد کنید (وتر باید بزرگتر از ضلع معلوم باشد)';
                return;
            }

            const missingSide = Math.sqrt(hypotenuse*hypotenuse - knownSide*knownSide).toFixed(4);
            document.getElementById('missingSideResult').textContent = 
                `ضلع مجهول = √(${hypotenuse}² - ${knownSide}²) = ${missingSide}`;
        }

        function calculatePolygonAngles() {
            const n = parseInt(document.getElementById('sidesCount').value);
            
            if (isNaN(n) || n < 3) {
                document.getElementById('polygonResult').textContent = 'لطفا عددی بزرگتر یا مساوی 3 وارد کنید';
                return;
            }

            const interiorAngle = ((n - 2) * 180 / n).toFixed(2);
            const exteriorAngle = (360 / n).toFixed(2);

            document.getElementById('polygonResult').textContent = 
                `چندضلعی ${n} ضلعی:\nزاویه داخلی: ${interiorAngle}°\nزاویه خارجی: ${exteriorAngle}°`;
        }

        function calculateExpression() {
            const expression = document.getElementById('calcInput').value;
            try {
                // تبدیل توابع مثلثاتی به رادیان
                let processedExpr = expression
                    .replace(/sin\(/g, 'Math.sin(Math.PI/180*')
                    .replace(/cos\(/g, 'Math.cos(Math.PI/180*')
                    .replace(/tan\(/g, 'Math.tan(Math.PI/180*')
                    .replace(/log\(/g, 'Math.log10(')
                    .replace(/ln\(/g, 'Math.log(');

                const result = eval(processedExpr);
                document.getElementById('calcResult').textContent = 
                    `${expression} = ${result}`;
            } catch (e) {
                document.getElementById('calcResult').textContent = 
                    'عبارت نامعتبر است';
            }
        }

        function egyptianFraction() {
            let numerator = parseInt(document.getElementById('numerator').value);
            let denominator = parseInt(document.getElementById('denominator').value);
            
            if (isNaN(numerator) || isNaN(denominator) || numerator >= denominator) {
                document.getElementById('egyptianResult').textContent = 'صورت باید کوچکتر از مخرج باشد';
                return;
            }

            let result = [];
            while (numerator > 0) {
                let x = Math.ceil(denominator / numerator);
                result.push(`1/${x}`);
                numerator = numerator * x - denominator;
                denominator = denominator * x;
            }

            document.getElementById('egyptianResult').textContent = 
                `کسر مصری: ${result.join(' + ')}`;
        }

        function calculateCombination() {
            const n = parseInt(document.getElementById('nComb').value);
            const r = parseInt(document.getElementById('rComb').value);
            
            if (isNaN(n) || isNaN(r) || r > n || n < 0 || r < 0) {
                document.getElementById('combinationResult').textContent = 'لطفا مقادیر معتبر وارد کنید';
                return;
            }

            function factorial(x) {
                let result = 1n;
                for (let i = 2; i <= x; i++) result *= BigInt(i);
                return result;
            }

            const comb = factorial(n) / (factorial(r) * factorial(n - r));
            document.getElementById('combinationResult').textContent = 
                `C(${n}, ${r}) = ${comb}`;
        }

        function generatePascal() {
            const row = parseInt(document.getElementById('pascalRow').value);
            
            if (isNaN(row) || row < 0 || row > 15) {
                document.getElementById('pascalResult').textContent = 'لطفا عددی بین 0 تا 15 وارد کنید';
                return;
            }

            function pascalRow(n) {
                let row = [1];
                for (let i = 1; i <= n; i++) {
                    row.push(row[i-1] * (n - i + 1) / i);
                }
                return row;
            }

            const resultRow = pascalRow(row);
            document.getElementById('pascalResult').textContent = 
                `سطر ${row}: ${resultRow.join(' ')}`;
        }

        function generatePascalTriangle() {
            const rows = parseInt(document.getElementById('pascalRow').value);
            
            if (isNaN(rows) || rows < 0 || rows > 10) {
                document.getElementById('pascalResult').textContent = 'لطفا عددی بین 0 تا 10 وارد کنید';
                return;
            }

            let triangle = [];
            for (let i = 0; i <= rows; i++) {
                let row = [1];
                for (let j = 1; j <= i; j++) {
                    row.push(row[j-1] * (i - j + 1) / j);
                }
                triangle.push(row.join(' '));
            }

            document.getElementById('pascalResult').textContent = 
                `مثلث خیام-پاسکال:\n${triangle.join('\n')}`;
        }

        function calculateMean() {
            const numbers = document.getElementById('numbersInput').value
                .split(',')
                .map(num => parseFloat(num.trim()))
                .filter(num => !isNaN(num));

            if (numbers.length === 0) {
                document.getElementById('averageResult').textContent = 'لطفا اعداد معتبر وارد کنید';
                return;
            }

            const mean = numbers.reduce((a, b) => a + b) / numbers.length;
            document.getElementById('averageResult').textContent = 
                `میانگین حسابی: ${mean.toFixed(4)}`;
        }

        function calculateMedian() {
            const numbers = document.getElementById('numbersInput').value
                .split(',')
                .map(num => parseFloat(num.trim()))
                .filter(num => !isNaN(num))
                .sort((a, b) => a - b);

            if (numbers.length === 0) {
                document.getElementById('averageResult').textContent = 'لطفا اعداد معتبر وارد کنید';
                return;
            }

            let median;
            const mid = Math.floor(numbers.length / 2);
            
            if (numbers.length % 2 === 0) {
                median = (numbers[mid-1] + numbers[mid]) / 2;
            } else {
                median = numbers[mid];
            }

            document.getElementById('averageResult').textContent = 
                `میانه: ${median.toFixed(4)}`;
        }

        function calculateAllAverages() {
            const numbers = document.getElementById('numbersInput').value
                .split(',')
                .map(num => parseFloat(num.trim()))
                .filter(num => !isNaN(num))
                .sort((a, b) => a - b);

            if (numbers.length === 0) {
                document.getElementById('averageResult').textContent = 'لطفا اعداد معتبر وارد کنید';
                return;
            }

            const mean = numbers.reduce((a, b) => a + b) / numbers.length;
            
            let median;
            const mid = Math.floor(numbers.length / 2);
            if (numbers.length % 2 === 0) {
                median = (numbers[mid-1] + numbers[mid]) / 2;
            } else {
                median = numbers[mid];
            }

            // مد
            let frequency = {};
            let maxFreq = 0;
            let modes = [];
            
            numbers.forEach(num => {
                frequency[num] = (frequency[num] || 0) + 1;
                if (frequency[num] > maxFreq) {
                    maxFreq = frequency[num];
                    modes = [num];
                } else if (frequency[num] === maxFreq) {
                    modes.push(num);
                }
            });

            const modeText = maxFreq > 1 ? modes.join(', ') : 'بدون مد';

            document.getElementById('averageResult').textContent = 
                `میانگین حسابی: ${mean.toFixed(4)}\nمیانه: ${median.toFixed(4)}\nمد: ${modeText}`;
        }
    </script>
</body>
</html>
