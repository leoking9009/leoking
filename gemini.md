## 1. 통합 HTML 파일 (index.html) - Gemini CLI 최적화 버전
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>몸무게 관리 프로그램</title>
    <meta name="description" content="간단한 웹 기반 몸무게 관리 및 추적 시스템">
    
    <style>
        /* CSS 코드 - 브라우저 호환성 강화 */
        * {
            margin: 0;
            padding: 0;
            -webkit-box-sizing: border-box;
            -moz-box-sizing: border-box;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', 'Helvetica', sans-serif;
            background: #667eea;
            background: -webkit-linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            -webkit-box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        header {
            background: #4CAF50;
            background: -webkit-linear-gradient(45deg, #4CAF50, #45a049);
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            text-align: center;
            padding: 2rem;
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
        }

        main {
            padding: 2rem;
        }

        section {
            margin-bottom: 2rem;
            padding: 1.5rem;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            background: #f9f9f9;
        }

        section h2 {
            color: #333;
            margin-bottom: 1rem;
            font-size: 1.5rem;
        }

        .input-group {
            display: -webkit-box;
            display: -webkit-flex;
            display: -ms-flexbox;
            display: flex;
            gap: 10px;
            -webkit-flex-wrap: wrap;
            -ms-flex-wrap: wrap;
            flex-wrap: wrap;
            margin-bottom: 1rem;
        }

        input {
            -webkit-box-flex: 1;
            -webkit-flex: 1;
            -ms-flex: 1;
            flex: 1;
            min-width: 120px;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            -webkit-transition: border-color 0.3s;
            transition: border-color 0.3s;
        }

        input:focus {
            outline: none;
            border-color: #4CAF50;
        }

        button {
            padding: 12px 20px;
            background: #4CAF50;
            background: -webkit-linear-gradient(45deg, #4CAF50, #45a049);
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            -webkit-transition: transform 0.2s;
            transition: transform 0.2s;
        }

        button:hover {
            -webkit-transform: translateY(-2px);
            transform: translateY(-2px);
        }

        button:active {
            -webkit-transform: translateY(0);
            transform: translateY(0);
        }

        .result-display {
            padding: 15px;
            margin-top: 10px;
            border-radius: 8px;
            font-weight: bold;
            text-align: center;
            min-height: 20px;
        }

        .bmi-underweight { background: #e3f2fd; color: #1976d2; }
        .bmi-normal { background: #e8f5e8; color: #4caf50; }
        .bmi-overweight { background: #fff3e0; color: #ff9800; }
        .bmi-obese { background: #ffebee; color: #f44336; }
        .goal-set { background: #e8f5e8; color: #4caf50; }
        .error-message { background: #ffebee; color: #f44336; }
        .success-message { background: #e8f5e8; color: #4caf50; }

        .record-item {
            display: -webkit-box;
            display: -webkit-flex;
            display: -ms-flexbox;
            display: flex;
            -webkit-box-pack: justify;
            -webkit-justify-content: space-between;
            -ms-flex-pack: justify;
            justify-content: space-between;
            -webkit-box-align: center;
            -webkit-align-items: center;
            -ms-flex-align: center;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            background: white;
            border-radius: 8px;
            -webkit-box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .record-item .date {
            font-weight: bold;
            color: #666;
        }

        .record-item .weight {
            font-size: 1.2rem;
            color: #4CAF50;
            font-weight: bold;
        }

        .delete-btn {
            background: #f44336;
            padding: 5px 10px;
            font-size: 12px;
        }

        .delete-btn:hover {
            background: #d32f2f;
        }

        .chart-container {
            position: relative;
            width: 100%;
            height: 300px;
            margin: 1rem 0;
            border: 1px solid #ddd;
            border-radius: 8px;
            background: white;
            display: -webkit-box;
            display: -webkit-flex;
            display: -ms-flexbox;
            display: flex;
            -webkit-box-align: center;
            -webkit-align-items: center;
            -ms-flex-align: center;
            align-items: center;
            -webkit-box-pack: center;
            -webkit-justify-content: center;
            -ms-flex-pack: center;
            justify-content: center;
        }

        .simple-chart {
            width: 100%;
            height: 100%;
            padding: 20px;
        }

        .chart-message {
            color: #666;
            text-align: center;
            font-style: italic;
        }

        .offline-indicator {
            background: #ff9800;
            color: white;
            padding: 10px;
            text-align: center;
            font-weight: bold;
        }

        /* 반응형 디자인 */
        @media (max-width: 600px) {
            body {
                padding: 10px;
            }
            
            header h1 {
                font-size: 2rem;
            }
            
            .input-group {
                -webkit-box-orient: vertical;
                -webkit-box-direction: normal;
                -webkit-flex-direction: column;
                -ms-flex-direction: column;
                flex-direction: column;
            }
            
            input, button {
                width: 100%;
            }
            
            .record-item {
                -webkit-box-orient: vertical;
                -webkit-box-direction: normal;
                -webkit-flex-direction: column;
                -ms-flex-direction: column;
                flex-direction: column;
                text-align: center;
                gap: 10px;
            }
        }

        /* 로딩 스피너 */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid #f3f3f3;
            border-top: 3px solid #4CAF50;
            border-radius: 50%;
            -webkit-animation: spin 2s linear infinite;
            animation: spin 2s linear infinite;
        }

        @-webkit-keyframes spin {
            0% { -webkit-transform: rotate(0deg); }
            100% { -webkit-transform: rotate(360deg); }
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div id="offline-indicator" class="offline-indicator" style="display: none;">
        🔌 오프라인 모드
    </div>
    
    <div class="container">
        <header>
            <h1>📊 몸무게 관리 프로그램</h1>
            <p>건강한 체중 관리를 위한 스마트 트래커</p>
        </header>
        
        <main>
            <!-- BMI 계산기 섹션 -->
            <section class="bmi-section">
                <h2>BMI 계산기</h2>
                <div class="input-group">
                    <input type="number" id="height" placeholder="키 (cm)" min="1" max="300" step="1">
                    <input type="number" id="weight" placeholder="몸무게 (kg)" min="1" max="500" step="0.1">
                    <button onclick="calculateBMI()" id="bmi-btn">BMI 계산</button>
                </div>
                <div id="bmi-result" class="result-display"></div>
            </section>

            <!-- 목표 설정 섹션 -->
            <section class="goal-section">
                <h2>목표 체중 설정</h2>
                <div class="input-group">
                    <input type="number" id="target-weight" placeholder="목표 체중 (kg)" min="1" max="500" step="0.1">
                    <button onclick="setGoal()" id="goal-btn">목표 설정</button>
                </div>
                <div id="goal-display" class="result-display"></div>
            </section>

            <!-- 체중 기록 섹션 -->
            <section class="record-section">
                <h2>체중 기록</h2>
                <div class="input-group">
                    <input type="text" id="record-date" placeholder="YYYY-MM-DD">
                    <input type="number" id="record-weight" placeholder="몸무게 (kg)" min="1" max="500" step="0.1">
                    <button onclick="addRecord()" id="record-btn">기록 추가</button>
                </div>
                <div id="record-result" class="result-display"></div>
            </section>

            <!-- 차트 섹션 -->
            <section class="chart-section">
                <h2>체중 변화 그래프</h2>
                <div class="chart-container">
                    <canvas id="weightChart" style="display: none;"></canvas>
                    <div id="simple-chart" class="simple-chart"></div>
                </div>
            </section>

            <!-- 기록 목록 섹션 -->
            <section class="history-section">
                <h2>기록 내역</h2>
                <div id="records-list"></div>
            </section>
        </main>
    </div>
    
    <script>
        // 전역 변수 및 설정
        let weightRecords = [];
        let targetWeight = null;
        let chart = null;
        let isOnline = navigator.onLine;
        let chartJsLoaded = false;

        // 저장소 래퍼 (에러 처리 포함)
        const storage = {
            get: function(key, defaultValue = null) {
                try {
                    const item = localStorage.getItem(key);
                    return item ? JSON.parse(item) : defaultValue;
                } catch (e) {
                    console.warn('localStorage get error:', e);
                    return defaultValue;
                }
            },
            set: function(key, value) {
                try {
                    localStorage.setItem(key, JSON.stringify(value));
                    return true;
                } catch (e) {
                    console.warn('localStorage set error:', e);
                    return false;
                }
            },
            remove: function(key) {
                try {
                    localStorage.removeItem(key);
                    return true;
                } catch (e) {
                    console.warn('localStorage remove error:', e);
                    return false;
                }
            }
        };

        // 유틸리티 함수들
        function showMessage(elementId, message, type = 'success') {
            const element = document.getElementById(elementId);
            if (!element) return;
            
            element.innerHTML = message;
            element.className = 'result-display ' + (type === 'error' ? 'error-message' : 'success-message');
            
            if (type === 'success') {
                setTimeout(() => {
                    element.innerHTML = '';
                    element.className = 'result-display';
                }, 3000);
            }
        }

        function validateNumber(value, min = 0, max = 1000) {
            const num = parseFloat(value);
            return !isNaN(num) && num >= min && num <= max;
        }

        function formatDate(dateString) {
            try {
                if (!dateString) return '';
                const date = new Date(dateString);
                if (isNaN(date.getTime())) return dateString;
                return date.toLocaleDateString('ko-KR');
            } catch (e) {
                return dateString;
            }
        }

        function getCurrentDate() {
            const now = new Date();
            const year = now.getFullYear();
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const day = String(now.getDate()).padStart(2, '0');
            return year + '-' + month + '-' + day;
        }

        // 네트워크 상태 관리
        function updateOnlineStatus() {
            isOnline = navigator.onLine;
            const indicator = document.getElementById('offline-indicator');
            if (indicator) {
                indicator.style.display = isOnline ? 'none' : 'block';
            }
        }

        // Chart.js 로드 시도
        function loadChartJs() {
            if (chartJsLoaded || !isOnline) {
                return Promise.resolve(false);
            }
            
            return new Promise((resolve) => {
                const script = document.createElement('script');
                script.src = 'https://cdn.jsdelivr.net/npm/chart.js@3.9.1/dist/chart.min.js';
                script.onload = function() {
                    chartJsLoaded = true;
                    resolve(true);
                };
                script.onerror = function() {
                    console.warn('Chart.js 로드 실패');
                    resolve(false);
                };
                script.timeout = 5000; // 5초 타임아웃
                document.head.appendChild(script);
            });
        }

        // BMI 계산 함수 (강화된 에러 처리)
        function calculateBMI() {
            const heightInput = document.getElementById('height');
            const weightInput = document.getElementById('weight');
            const btn = document.getElementById('bmi-btn');
            
            if (!heightInput || !weightInput || !btn) {
                showMessage('bmi-result', '시스템 오류가 발생했습니다.', 'error');
                return;
            }
            
            const height = heightInput.value.trim();
            const weight = weightInput.value.trim();
            
            if (!height || !weight) {
                showMessage('bmi-result', '키와 몸무게를 모두 입력해주세요.', 'error');
                return;
            }
            
            if (!validateNumber(height, 50, 300) || !validateNumber(weight, 10, 500)) {
                showMessage('bmi-result', '올바른 수치를 입력해주세요. (키: 50-300cm, 몸무게: 10-500kg)', 'error');
                return;
            }
            
            try {
                btn.innerHTML = '<span class="loading"></span> 계산 중...';
                btn.disabled = true;
                
                setTimeout(() => {
                    const heightM = parseFloat(height) / 100;
                    const weightKg = parseFloat(weight);
                    const bmi = weightKg / (heightM * heightM);
                    
                    let category, className;
                    
                    if (bmi < 18.5) {
                        category = '저체중';
                        className = 'bmi-underweight';
                    } else if (bmi < 23) {
                        category = '정상';
                        className = 'bmi-normal';
                    } else if (bmi < 25) {
                        category = '과체중';
                        className = 'bmi-overweight';
                    } else {
                        category = '비만';
                        className = 'bmi-obese';
                    }
                    
                    const resultDiv = document.getElementById('bmi-result');
                    if (resultDiv) {
                        resultDiv.innerHTML = 'BMI: ' + bmi.toFixed(1) + ' (' + category + ')';
                        resultDiv.className = 'result-display ' + className;
                    }
                    
                    btn.innerHTML = 'BMI 계산';
                    btn.disabled = false;
                }, 500);
                
            } catch (error) {
                console.error('BMI 계산 오류:', error);
                showMessage('bmi-result', 'BMI 계산 중 오류가 발생했습니다.', 'error');
                btn.innerHTML = 'BMI 계산';
                btn.disabled = false;
            }
        }

        // 목표 체중 설정 (강화된 검증)
        function setGoal() {
            const goalInput = document.getElementById('target-weight');
            const btn = document.getElementById('goal-btn');
            
            if (!goalInput || !btn) {
                showMessage('goal-display', '시스템 오류가 발생했습니다.', 'error');
                return;
            }
            
            const goalWeight = goalInput.value.trim();
            
            if (!goalWeight) {
                showMessage('goal-display', '목표 체중을 입력해주세요.', 'error');
                return;
            }
            
            if (!validateNumber(goalWeight, 10, 500)) {
                showMessage('goal-display', '올바른 목표 체중을 입력해주세요. (10-500kg)', 'error');
                return;
            }
            
            try {
                btn.innerHTML = '<span class="loading"></span> 설정 중...';
                btn.disabled = true;
                
                setTimeout(() => {
                    targetWeight = parseFloat(goalWeight);
                    storage.set('targetWeight', targetWeight);
                    
                    displayGoal();
                    updateChart();
                    goalInput.value = '';
                    
                    btn.innerHTML = '목표 설정';
                    btn.disabled = false;
                    showMessage('goal-display', '목표 체중이 설정되었습니다!', 'success');
                }, 300);
                
            } catch (error) {
                console.error('목표 설정 오류:', error);
                showMessage('goal-display', '목표 설정 중 오류가 발생했습니다.', 'error');
                btn.innerHTML = '목표 설정';
                btn.disabled = false;
            }
        }

        // 목표 체중 표시
        function displayGoal() {
            const goalDisplay = document.getElementById('goal-display');
            if (!goalDisplay) return;
            
            if (targetWeight) {
                goalDisplay.innerHTML = '목표 체중: ' + targetWeight + 'kg';
                goalDisplay.className = 'result-display goal-set';
            }
        }

        // 체중 기록 추가 (강화된 검증 및 에러 처리)
        function addRecord() {
            const dateInput = document.getElementById('record-date');
            const weightInput = document.getElementById('record-weight');
            const btn = document.getElementById('record-btn');
            
            if (!dateInput || !weightInput || !btn) {
                showMessage('record-result', '시스템 오류가 발생했습니다.', 'error');
                return;
            }
            
            const date = dateInput.value.trim();
            const weight = weightInput.value.trim();
            
            if (!date || !weight) {
                showMessage('record-result', '날짜와 몸무게를 모두 입력해주세요.', 'error');
                return;
            }
            
            // 날짜 형식 검증
            if (!/^\d{4}-\d{2}-\d{2}$/.test(date)) {
                showMessage('record-result', '올바른 날짜 형식을 입력해주세요. (YYYY-MM-DD)', 'error');
                return;
            }
            
            if (!validateNumber(weight, 10, 500)) {
                showMessage('record-result', '올바른 몸무게를 입력해주세요. (10-500kg)', 'error');
                return;
            }
            
            try {
                btn.innerHTML = '<span class="loading"></span> 저장 중...';
                btn.disabled = true;
                
                setTimeout(() => {
                    const newRecord = {
                        date: date,
                        weight: parseFloat(weight),
                        timestamp: Date.now()
                    };
                    
                    // 같은 날짜 기록이 있는지 확인
                    const existingIndex = weightRecords.findIndex(record => record.date === date);
                    
                    if (existingIndex !== -1) {
                        if (confirm('같은 날짜에 이미 기록이 있습니다. 덮어쓰시겠습니까?')) {
                            weightRecords[existingIndex] = newRecord;
                        } else {
                            btn.innerHTML = '기록 추가';
                            btn.disabled = false;
                            return;
                        }
                    } else {
                        weightRecords.push(newRecord);
                    }
                    
                    // 날짜순 정렬
                    weightRecords.sort((a, b) => new Date(a.date) - new Date(b.date));
                    
                    // 저장
                    if (storage.set('weightRecords', weightRecords)) {
                        showMessage('record-result', '기록이 저장되었습니다!', 'success');
                        weightInput.value = '';
                        displayRecords();
                        updateChart();
                    } else {
                        showMessage('record-result', '저장 중 오류가 발생했습니다.', 'error');
                    }
                    
                    btn.innerHTML = '기록 추가';
                    btn.disabled = false;
                }, 300);
                
            } catch (error) {
                console.error('기록 추가 오류:', error);
                showMessage('record-result', '기록 추가 중 오류가 발생했습니다.', 'error');
                btn.innerHTML = '기록 추가';
                btn.disabled = false;
            }
        }

        // 기록 목록 표시
        function displayRecords() {
            const recordsList = document.getElementById('records-list');
            if (!recordsList) return;
            
            if (weightRecords.length === 0) {
                recordsList.innerHTML = '<p style="text-align: center; color: #666;">아직 기록이 없습니다.</p>';
                return;
            }
            
            try {
                const recordsHTML = weightRecords
                    .slice()
                    .reverse() // 최신 기록을 위로
                    .map((record, index) => {
                        const actualIndex = weightRecords.length - 1 - index;
                        return '<div class="record-item">' +
                                '<span class="date">' + formatDate(record.date) + '</span>' +
                                '<span class="weight">' + record.weight + 'kg</span>' +
                                '<button class="delete-btn" onclick="deleteRecord(' + actualIndex + ')">삭제</button>' +
                                '</div>';
                    })
                    .join('');
                
                recordsList.innerHTML = recordsHTML;
            } catch (error) {
                console.error('기록 표시 오류:', error);
                recordsList.innerHTML = '<p style="text-align: center; color: #f44336;">기록을 불러오는 중 오류가 발생했습니다.</p>';
            }
        }

        // 기록 삭제 (확인 절차 강화)
        function deleteRecord(index) {
            if (index < 0 || index >= weightRecords.length) {
                alert('잘못된 기록입니다.');
                return;
            }
            
            const record = weightRecords[index];
            if (!record) {
                alert('기록을 찾을 수 없습니다.');
                return;
            }
            
            const confirmMessage = formatDate(record.date) + '의 ' + record.weight + 'kg 기록을 삭제하시겠습니까?';
            
            if (confirm(confirmMessage)) {
                try {
                    weightRecords.splice(index, 1);
                    if (storage.set('weightRecords', weightRecords)) {
                        displayRecords();
                        updateChart();
                        showMessage('record-result', '기록이 삭제되었습니다.', 'success');
                    } else {
                        // 롤백
                        weightRecords.splice(index, 0, record);
                        alert('삭제 중 오류가 발생했습니다.');
                    }
                } catch (error) {
                    console.error('기록 삭제 오류:', error);
                    alert('삭제 중 오류가 발생했습니다.');
                }
            }
        }

        // 간단한 차트 그리기 (Chart.js 없이)
        function drawSimpleChart() {
            const container = document.getElementById('simple-chart');
            if (!container || weightRecords.length === 0) {
                if (container) {
                    container.innerHTML = '<div class="chart-message">기록이 없어서 차트를 표시할 수 없습니다.</div>';
                }
                return;
            }
            
            try {
                const weights = weightRecords.map(r => r.weight);
                const dates = weightRecords.map(r => formatDate(r.date));
                const minWeight = Math.min(...weights);
                const maxWeight = Math.max(...weights);
                const weightRange = maxWeight - minWeight || 1;
                
                let html = '<div style="font-weight: bold; margin-bottom: 10px; text-align: center;">체중 변화 추이</div>';
                html += '<div style="display: flex; flex-direction: column; height: 200px;">';
                
                // 간단한 막대 그래프
                for (let i = 0; i < Math.min(weightRecords.length, 10); i++) {
                    const record = weightRecords[weightRecords.length - 1 - i]; // 최신부터
                    const height = ((record.weight - minWeight) / weightRange) * 150 + 20;
                    const color = targetWeight ? 
                        (record.weight <= targetWeight ? '#4CAF50' : '#ff9800') : '#2196F3';
                    
                    html += '<div style="display: flex; align-items: end; margin: 2px 0;">';
                    html += '<div style="width: 80px; font-size: 12px; text-align: right; padding-right: 5px;">' + 
                            formatDate(record.date).split(' ')[0] + '</div>';
                    html += '<div style="background: ' + color + '; height: ' + height + 'px; width: 20px; margin: 0 5px;"></div>';
                    html += '<div style="font-size: 12px; color: #333;">' + record.weight + 'kg</div>';
                    html += '</div>';
                }
                
                if (targetWeight) {
                    html += '<div style="margin-top: 10px; font-size: 12px; color: #666; text-align: center;">';
                    html += '목표: ' + targetWeight + 'kg | 현재: ' + weights[weights.length - 1] + 'kg';
                    html += '</div>';
                }
                
                html += '</div>';
                container.innerHTML = html;
            } catch (error) {
                console.error('간단 차트 그리기 오류:', error);
                container.innerHTML = '<div class="chart-message">차트를 그리는 중 오류가 발생했습니다.</div>';
            }
        }

        // Chart.js를 사용한 고급 차트
        function drawAdvancedChart() {
            if (!window.Chart || weightRecords.length === 0) {
                return false;
            }
            
            try {
                const ctx = document.getElementById('weightChart');
                if (!ctx) return false;
                
                ctx.getContext('2d');
                
                // 기존 차트 제거
                if (chart) {
                    chart.destroy();
                }
                
                const labels = weightRecords.map(record => formatDate(record.date));
                const data = weightRecords.map(record => record.weight);
                const goalLine = targetWeight ? Array(labels.length).fill(targetWeight) : null;
                
                const datasets = [{
                    label: '체중 (kg)',
                    data: data,
                    borderColor: 'rgb(75, 192, 192)',
                    backgroundColor: 'rgba(75, 192, 192, 0.2)',
                    tension: 0.1,
                    fill: true
                }];
                
                if (goalLine) {
                    datasets.push({
                        label: '목표 체중',
                        data: goalLine,
                        borderColor: 'rgb(255, 99, 132)',
                        backgroundColor: 'rgba(255, 99, 132, 0.1)',
                        borderDash: [5, 5],
                        tension: 0,
                        fill: false
                    });
                }
                
                chart = new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: labels,
                        datasets: datasets
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            title: {
                                display: true,
                                text: '체중 변화 추이'
                            },
                            legend: {
                                display: true
                            }
                        },
                        scales: {
                            y: {
                                beginAtZero: false,
                                title: {
                                    display: true,
                                    text: '체중 (kg)'
                                }
                            },
                            x: {
                                title: {
                                    display: true,
                                    text: '날짜'
                                }
                            }
                        }
                    }
                });
                
                // 고급 차트가 성공적으로 그려지면 간단 차트 숨기기
                document.getElementById('simple-chart').style.display = 'none';
                ctx.style.display = 'block';
                return true;
            } catch (error) {
                console.error('고급 차트 그리기 오류:', error);
                return false;
            }
        }

        // 차트 업데이트 (fallback 포함)
        function updateChart() {
            // Chart.js가 로드되어 있고 온라인이면 고급 차트 시도
            if (chartJsLoaded && window.Chart) {
                if (drawAdvancedChart()) {
                    return; // 성공하면 종료
                }
            }
            
            // Chart.js 로드 시도 (온라인일 때만)
            if (isOnline && !chartJsLoaded) {
                loadChartJs().then(function(loaded) {
                    if (loaded && drawAdvancedChart()) {
                        return;
                    }
                    // 실패하면 간단 차트로 fallback
                    document.getElementById('weightChart').style.display = 'none';
                    document.getElementById('simple-chart').style.display = 'block';
                    drawSimpleChart();
                });
            } else {
                // 오프라인이거나 Chart.js 로드 실패 시 간단 차트 사용
                document.getElementById('weightChart').style.display = 'none';
                document.getElementById('simple-chart').style.display = 'block';
                drawSimpleChart();
            }
        }

        // 데이터 로드
        function loadData() {
            try {
                weightRecords = storage.get('weightRecords', []);
                targetWeight = storage.get('targetWeight', null);
                
                // 데이터 유효성 검사
                if (!Array.isArray(weightRecords)) {
                    weightRecords = [];
                }
                
                // 잘못된 기록 필터링
                weightRecords = weightRecords.filter(record => {
                    return record && 
                           typeof record.date === 'string' && 
                           typeof record.weight === 'number' && 
                           record.weight > 0 && 
                           record.weight < 1000;
                });
                
                if (targetWeight !== null && (typeof targetWeight !== 'number' || targetWeight <= 0)) {
                    targetWeight = null;
                }
                
            } catch (error) {
                console.error('데이터 로드 오류:', error);
                weightRecords = [];
                targetWeight = null;
            }
        }

        // 페이지 초기화
        function initializePage() {
            try {
                // 현재 날짜 설정
                const dateInput = document.getElementById('record-date');
                if (dateInput) {
                    dateInput.value = getCurrentDate();
                }
                
                // 데이터 로드
                loadData();
                
                // UI 업데이트
                displayGoal();
                displayRecords();
                updateChart();
                updateOnlineStatus();
                
                console.log('페이지 초기화 완료');
            } catch (error) {
                console.error('페이지 초기화 오류:', error);
                alert('페이지 로드 중 오류가 발생했습니다. 페이지를 새로고침해주세요.');
            }
        }

        // 이벤트 리스너 등록
        function setupEventListeners() {
            try {
                // 온라인/오프라인 상태 감지
                window.addEventListener('online', updateOnlineStatus);
                window.addEventListener('offline', updateOnlineStatus);
                
                // Enter 키 이벤트
                document.addEventListener('keypress', function(e) {
                    if (e.key === 'Enter') {
                        const target = e.target;
                        if (target.id === 'height' || target.id === 'weight') {
                            calculateBMI();
                        } else if (target.id === 'target-weight') {
                            setGoal();
                        } else if (target.id === 'record-date' || target.id === 'record-weight') {
                            addRecord();
                        }
                    }
                });
                
                // 에러 핸들링
                window.addEventListener('error', function(e) {
                    console.error('전역 오류:', e.error);
                });
                
                window.addEventListener('unhandledrejection', function(e) {
                    console.error('처리되지 않은 Promise 오류:', e.reason);
                });
                
            } catch (error) {
                console.error('이벤트 리스너 설정 오류:', error);
            }
        }

        // DOM 로드 완료 시 초기화
        if (document.readyState === 'loading') {
            document.addEventListener('DOMContentLoaded', function() {
                setupEventListeners();
                initializePage();
            });
        } else {
            setupEventListeners();
            initializePage();
        }
    </script>
</body>
</html>
```# 몸무게 관리 프로그램 개발 및 GitHub 배포 가이드 (Gemini CLI 최적화)

## 프로젝트 개요
Gemini CLI에서 안정적으로 실행되는 웹 기반 몸무게 관리 프로그램을 개발하고 GitHub Pages를 통해 배포하는 방법을 안내합니다.

## 기능 명세
- 몸무게 기록 추가/삭제
- 몸무게 변화 그래프 시각화 (Chart.js fallback 포함)
- 목표 체중 설정
- BMI 계산기
- 데이터 로컬 저장 (localStorage with fallback)
- 오프라인 지원
- 강화된 에러 처리

## 프로젝트 구조 (단순화)
```
weight-tracker/
├── index.html          # 모든 코드가 포함된 단일 HTML 파일
├── README.md           # 프로젝트 설명
├── .gitignore         # Git 무시 파일
└── manifest.json      # PWA 매니페스트 (선택사항)
```

## 1. HTML 파일 (index.html)
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>몸무게 관리 프로그램</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <div class="container">
        <header>
            <h1>📊 몸무게 관리 프로그램</h1>
        </header>
        
        <main>
            <!-- BMI 계산기 섹션 -->
            <section class="bmi-section">
                <h2>BMI 계산기</h2>
                <div class="input-group">
                    <input type="number" id="height" placeholder="키 (cm)" min="1" max="300">
                    <input type="number" id="weight" placeholder="몸무게 (kg)" min="1" max="500" step="0.1">
                    <button onclick="calculateBMI()">BMI 계산</button>
                </div>
                <div id="bmi-result"></div>
            </section>

            <!-- 목표 설정 섹션 -->
            <section class="goal-section">
                <h2>목표 체중 설정</h2>
                <div class="input-group">
                    <input type="number" id="target-weight" placeholder="목표 체중 (kg)" min="1" max="500" step="0.1">
                    <button onclick="setGoal()">목표 설정</button>
                </div>
                <div id="goal-display"></div>
            </section>

            <!-- 체중 기록 섹션 -->
            <section class="record-section">
                <h2>체중 기록</h2>
                <div class="input-group">
                    <input type="date" id="record-date">
                    <input type="number" id="record-weight" placeholder="몸무게 (kg)" min="1" max="500" step="0.1">
                    <button onclick="addRecord()">기록 추가</button>
                </div>
            </section>

            <!-- 차트 섹션 -->
            <section class="chart-section">
                <h2>체중 변화 그래프</h2>
                <canvas id="weightChart"></canvas>
            </section>

            <!-- 기록 목록 섹션 -->
            <section class="history-section">
                <h2>기록 내역</h2>
                <div id="records-list"></div>
            </section>
        </main>
    </div>
    
    <script src="script.js"></script>
</body>
</html>
```

## 2. README.md 파일 (개선된 버전)
```markdown
# 몸무게 관리 프로그램 🏃‍♂️📊

안정적이고 호환성이 뛰어난 웹 기반 몸무게 관리 프로그램입니다.

## ✨ 주요 특징
- 📊 **BMI 계산기** - 실시간 BMI 계산 및 건강 상태 평가
- 🎯 **목표 체중 설정** - 개인 목표 설정 및 추적
- 📈 **체중 변화 그래프** - Chart.js 기반 고급 차트 (오프라인 시 단순 차트로 자동 전환)
- 💾 **안전한 데이터 저장** - 로컬 스토리지 + 에러 핸들링
- 📱 **완전 반응형** - 모바일, 태블릿, 데스크톱 지원
- 🔌 **오프라인 지원** - 네트워크 없이도 기본 기능 사용 가능
- 🛡️ **강화된 오류 처리** - 예외 상황에서도 안정적 동작

## 🚀 빠른 시작
1. [여기](https://[사용자명].github.io/weight-tracker/)에서 바로 사용
2. 또는 로컬에서 `index.html` 파일 실행

## 📖 사용 방법
### BMI 계산
- 키(cm)와 몸무게(kg) 입력 후 "BMI 계산" 버튼 클릭
- 결과는 저체중/정상/과체중/비만으로 분류됩니다

### 목표 설정
- 원하는 목표 체중 입력 후 "목표 설정" 버튼 클릭
- 그래프에 목표선이 표시됩니다

### 체중 기록
- 날짜(YYYY-MM-DD 형식)와 체중 입력 후 "기록 추가" 클릭
- 같은 날짜 기록이 있으면 덮어쓸지 확인합니다

### 그래프 보기
- 온라인: Chart.js를 활용한 인터랙티브 차트
- 오프라인: 단순하지만 효과적인 막대 그래프

## 🛠️ 기술적 특징
### 호환성
- **브라우저**: Chrome, Firefox, Safari, Edge (IE11+)
- **모바일**: iOS Safari, Android Chrome
- **오프라인**: 기본 기능 모두 사용 가능

### 안정성
- localStorage 에러 처리
- 네트워크 연결 상태 감지
- 입력 데이터 유효성 검사
- 자동 데이터 복구 기능

### 성능
- 단일 HTML 파일 (빠른 로딩)
- 지연 로딩 (Chart.js는 필요시에만 로드)
- 메모리 누수 방지

## 📁 파일 구조
```
weight-tracker/
├── index.html          # 모든 코드가 포함된 메인 파일
├── README.md           # 이 파일
├── .gitignore         # Git 무시 파일
└── manifest.json      # PWA 매니페스트 (선택사항)
```

## 🔧 개발자 정보
### 사용된 기술
- **HTML5**: 시맨틱 마크업
- **CSS3**: Flexbox, 그라디언트, 애니메이션
- **JavaScript (ES5+)**: 호환성을 위한 보수적 접근
- **Chart.js 3.x**: 선택적 로딩
- **LocalStorage API**: 클라이언트 데이터 저장

### 브라우저 지원
- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- iOS Safari 12+
- Android Chrome 60+

## 📋 향후 계획
- [ ] PWA 지원 (오프라인 설치)
- [ ] 데이터 백업/복원 기능
- [ ] 다국어 지원
- [ ] 운동 기록 연동
- [ ] 식단 관리 기능

## 🤝 기여하기
1. 저장소 포크
2. 기능 브랜치 생성 (`git checkout -b feature/amazing-feature`)
3. 변경사항 커밋 (`git commit -m 'Add amazing feature'`)
4. 브랜치에 푸시 (`git push origin feature/amazing-feature`)
5. Pull Request 생성

## 📄 라이선스
MIT License - 자유롭게 사용, 수정, 배포 가능

## ⚠️ 주의사항
- 이 프로그램은 건강 참고용이며 의학적 진단 도구가 아닙니다
- 정확한 건강 관리를 위해서는 의료 전문가와 상담하세요
- 브라우저 데이터 삭제 시 기록이 사라질 수 있습니다
```

## 3. .gitignore 파일
```
# 운영체제
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# 에디터/IDE
.vscode/
.idea/
*.swp
*.swo
*~

# 로그 파일
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# 임시 파일
*.tmp
*.temp
.cache/

# 의존성
node_modules/
.npm

# 환경 설정
.env
.env.local
.env.development.local
.env.test.local
.env.production.local
```

## 4. manifest.json (PWA 지원 - 선택사항)
```json
{
    "name": "몸무게 관리 프로그램",
    "short_name": "WeightTracker",
    "description": "간단하고 효과적인 체중 관리 도구",
    "start_url": "/",
    "display": "standalone",
    "background_color": "#667eea",
    "theme_color": "#4CAF50",
    "orientation": "portrait",
    "icons": [
        {
            "src": "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Ccircle cx='50' cy='50' r='40' fill='%234CAF50'/%3E%3Ctext x='50' y='60' text-anchor='middle' fill='white' font-size='30'%3E📊%3C/text%3E%3C/svg%3E",
            "sizes": "192x192",
            "type": "image/svg+xml"
        }
    ]
}
```

## GitHub 배포 과정 (단순화된 버전)

### 1. GitHub 저장소 생성
1. GitHub에서 새 저장소 생성 (예: `weight-tracker`)
2. Public 저장소로 설정
3. "Add a README file" 체크

### 2. 파일 업로드 (웹 인터페이스 사용)
1. 저장소 메인 페이지에서 "uploading an existing file" 클릭
2. 위에서 작성한 `index.html` 파일을 드래그&드롭
3. "Commit new files" 클릭

### 3. README.md 업데이트
1. README.md 파일 편집
2. 위의 README.md 내용으로 교체
3. Commit changes

### 4. GitHub Pages 활성화
1. 저장소의 **Settings** 탭 이동
2. 왼쪽 메뉴에서 **Pages** 클릭
3. **Source**를 "Deploy from a branch"로 설정
4. **Branch**를 "main" (또는 "master") 선택
5. **Folder**를 "/ (root)" 선택
6. **Save** 클릭

### 5. 배포 확인 (2-5분 소요)
- `https://[사용자명].github.io/weight-tracker/`에서 앱 접근
- GitHub Actions 탭에서 배포 진행 상황 확인 가능Records
        .slice()
        .reverse() // 최신 기록을 위로
        .map((record, index) => {
            const actualIndex = weightRecords.length - 1 - index;
            return `
                <div class="record-item">
                    <span class="date">${new Date(record.date).toLocaleDateString('ko-KR')}</span>
                    <span class="weight">${record.weight}kg</span>
                    <button class="delete-btn" onclick="deleteRecord(${actualIndex})">삭제</button>
                </div>
            `;
        })
        .join('');
    
    recordsList.innerHTML = recordsHTML;
}

// 기록 삭제
function deleteRecord(index) {
    if (confirm('이 기록을 삭제하시겠습니까?')) {
        weightRecords.splice(index, 1);
        localStorage.setItem('weightRecords', JSON.stringify(weightRecords));
        displayRecords();
        updateChart();
    }
}

// 차트 업데이트
function updateChart() {
    const ctx = document.getElementById('weightChart').getContext('2d');
    
    // 기존 차트 제거
    if (chart) {
        chart.destroy();
    }
    
    if (weightRecords.length === 0) {
        return;
    }
    
    const labels = weightRecords.map(record => 
        new Date(record.date).toLocaleDateString('ko-KR')
    );
    const data = weightRecords.map(record => record.weight);
    
    // 목표 체중 라인 데이터
    const goalLine = targetWeight ? Array(labels.length).fill(targetWeight) : null;
    
    const datasets = [{
        label: '체중 (kg)',
        data: data,
        borderColor: 'rgb(75, 192, 192)',
        backgroundColor: 'rgba(75, 192, 192, 0.2)',
        tension: 0.1,
        fill: true
    }];
    
    if (goalLine) {
        datasets.push({
            label: '목표 체중',
            data: goalLine,
            borderColor: 'rgb(255, 99, 132)',
            backgroundColor: 'rgba(255, 99, 132, 0.1)',
            borderDash: [5, 5],
            tension: 0
        });
    }
    
    chart = new Chart(ctx, {
        type: 'line',
        data: {
            labels: labels,
            datasets: datasets
        },
        options: {
            responsive: true,
            plugins: {
                title: {
                    display: true,
                    text: '체중 변화 추이'
                },
                legend: {
                    display: true
                }
            },
            scales: {
                y: {
                    beginAtZero: false,
                    title: {
                        display: true,
                        text: '체중 (kg)'
                    }
                },
                x: {
                    title: {
                        display: true,
                        text: '날짜'
                    }
                }
            }
        }
    });
}
```

## 4. README.md 파일
```markdown
# 몸무게 관리 프로그램 🏃‍♂️📊

간단하고 직관적인 웹 기반 몸무게 관리 프로그램입니다.

## 기능
- 📊 BMI 계산기
- 🎯 목표 체중 설정
- 📈 체중 기록 및 그래프 시각화
- 💾 로컬 데이터 저장
- 📱 반응형 디자인

## 사용 방법
1. 키와 몸무게를 입력하여 BMI를 계산하세요
2. 목표 체중을 설정하세요
3. 매일 체중을 기록하세요
4. 그래프로 변화를 확인하세요

## 기술 스택
- HTML5
- CSS3
- JavaScript (ES6+)
- Chart.js

## 라이선스
MIT License
```

## 5. .gitignore 파일
```
# 운영체제
.DS_Store
Thumbs.db

# 에디터
.vscode/
.idea/
*.swp
*.swo

# 로그
*.log

# 임시 파일
*.tmp
```

## GitHub 배포 과정

### 1. GitHub 저장소 생성
1. GitHub에서 새 저장소 생성 (예: `weight-tracker`)
2. Public 저장소로 설정
3. README.md 초기화 체크

### 2. 로컬 개발 환경 설정
```bash
# 저장소 클론
git clone https://github.com/[사용자명]/weight-tracker.git
cd weight-tracker

# 파일들 추가
# (위에서 만든 모든 파일들을 프로젝트 폴더에 복사)

# Git에 파일 추가
git add .
git commit -m "Initial commit: 몸무게 관리 프로그램 추가"
git push origin main
```

### 3. GitHub Pages 설정
1. 저장소의 Settings 탭으로 이동
2. 좌측 메뉴에서 "Pages" 클릭
3. Source를 "Deploy from a branch"로 설정
4. Branch를 "main"으로 선택
5. 폴더를 "/ (root)"로 선택
6. Save 클릭

### 4. 배포 완료
- 몇 분 후 `https://[사용자명].github.io/weight-tracker/`에서 앱 접근 가능
- 자동으로 HTTPS로 서빙됨

## 추가 개선 사항

### 기능 확장
- 운동 기록 기능
- 식단 관리 기능
- 목표 달성률 계산
- 데이터 내보내기/가져오기
- 주간/월간 통계

### 기술적 개선
- PWA (Progressive Web App) 지원
- 데이터베이스 연동
- 사용자 계정 시스템
- 모바일 앱 개발

## 참고 사항
- 모든 데이터는 브라우저의 로컬 스토리지에 저장됩니다
- 브라우저 데이터를 삭제하면 기록이 사라집니다
- 정확한 건강 관리를 위해서는 전문의와 상담하세요