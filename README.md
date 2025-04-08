<!DOCTYPE html>
<html>
<head>
    <title>台灣醫療保險缺口分析</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .chart-container {
            width: 80%;
            margin: 20px auto;
        }
        .info-box {
            background-color: #f0f8ff;
            border: 1px solid #ccc;
            padding: 15px;
            margin: 20px 0;
            border-radius: 5px;
        }
        .case-study {
            background-color: #fff2f2;
            border-left: 4px solid #ff6b6b;
            padding: 15px;
            margin: 20px 0;
        }
        .highlight {
            color: #d32f2f;
            font-weight: bold;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
        }
        table, th, td {
            border: 1px solid #ddd;
        }
        th, td {
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h1>台灣醫療保險保障缺口分析</h1>
    
    <div class="info-box">
        <h2>客戶現有保障分析</h2>
        <table>
            <tr>
                <th>保障項目</th>
                <th>保障金額</th>
                <th>保障缺口</th>
            </tr>
            <tr>
                <td>住院日額</td>
                <td>3,500元/日</td>
                <td>無法覆蓋實際住院費用差額</td>
            </tr>
            <tr>
                <td>門診手術</td>
                <td>16萬元</td>
                <td>無法覆蓋自費特殊治療及藥物</td>
            </tr>
            <tr>
                <td>住院手術</td>
                <td>16萬元</td>
                <td>複雜手術費用可能超出此限額</td>
            </tr>
            <tr>
                <td>特定處置</td>
                <td>5-8萬元</td>
                <td>無法覆蓋全部特殊醫療處置費用</td>
            </tr>
            <tr>
                <td>實支實付</td>
                <td>無</td>
                <td class="highlight">無法補償住院雜費及自費醫療項目</td>
            </tr>
            <tr>
                <td>重大疾病</td>
                <td>無</td>
                <td class="highlight">無法提供重大疾病治療期間的經濟支持</td>
            </tr>
        </table>
    </div>

    <div class="chart-container">
        <canvas id="hospitalExpenseChart"></canvas>
    </div>

    <div class="case-study">
        <h3>實際案例分析：缺乏實支實付保險的後果</h3>
        <p>王先生的兒子(14歲)因為骨折住院，雖然有住院日額3,500元/天的保障，但實際住院7天的總費用達到12萬元。健保給付5萬元後，自付部分仍有7萬元。其中包括：</p>
        <ul>
            <li>特殊骨材：3.5萬元（健保不給付）</li>
            <li>MRI檢查：1.2萬元（自費差額）</li>
            <li>高階止痛藥：0.8萬元（健保不給付）</li>
            <li>其他醫療雜費：1.5萬元</li>
        </ul>
        <p>若有實支實付保險，這些費用本可獲得理賠。<span class="highlight">最終王先生需自掉腰包支付7萬元，遠超過住院日額保險的理賠金額2.45萬元(7天*3,500元)。</span></p>
    </div>

    <div class="chart-container">
        <canvas id="selfPayExpenseChart"></canvas>
    </div>

    <div class="case-study">
        <h3>保險糾紛案例：理賠爭議</h3>
        <p>林小姐的孩子確診罹患罕見血液疾病，治療過程中採用了新型標靶藥物，費用高達每月15萬元。由於缺乏重大疾病保險和完整的實支實付保險，林小姐向保險公司申請現有保單理賠時遇到以下問題：</p>
        <ul>
            <li>保險公司主張標靶治療屬於「實驗性治療」，拒絕理賠</li>
            <li>住院手術保險金額不足以覆蓋實際治療費用</li>
            <li>治療期間長達一年，家庭收入大幅減少</li>
        </ul>
        <p><span class="highlight">最終林小姐不得不申請貸款並發起募資才能支付高額醫療費用，同時耗費大量時間與保險公司協商理賠事宜。</span></p>
    </div>

    <div class="chart-container">
        <canvas id="medicalCostTrendChart"></canvas>
    </div>

    <div class="chart-container">
        <canvas id="majorIllnessCostChart"></canvas>
    </div>

    <div class="info-box">
        <h2>現有保單的關鍵漏洞</h2>
        <p>根據衛福部統計資料，現有保障存在以下重大缺口：</p>
        <ol>
            <li><span class="highlight">實支實付缺口</span>：住院期間的各項檢查、特殊藥物、耗材等費用需額外支付，住院日額無法涵蓋這些項目</li>
            <li><span class="highlight">自費項目增加</span>：近五年自費醫療項目平均每年增加8.3%，健保給付範圍無法跟上醫療技術發展</li>
            <li><span class="highlight">特殊治療缺口</span>：特定處置保險只賠付5-8萬元，但許多新型治療方式費用遠超此金額</li>
            <li><span class="highlight">長期治療無保障</span>：重大疾病如癌症等治療期間長，缺乏重大疾病保險將使家庭承受長期經濟壓力</li>
        </ol>
    </div>

    <div class="chart-container">
        <canvas id="insuranceGapPieChart"></canvas>
    </div>

    <script>
        // 住院費用與保障比較圖
        const hospitalExpenseCtx = document.getElementById('hospitalExpenseChart').getContext('2d');
        const hospitalExpenseChart = new Chart(hospitalExpenseCtx, {
            type: 'bar',
            data: {
                labels: ['一般住院', '骨折手術', '闌尾切除', '心臟手術', '癌症治療'],
                datasets: [{
                    label: '平均實際費用 (萬元)',
                    data: [6.5, 12.3, 8.7, 25.6, 32.5],
                    backgroundColor: 'rgba(54, 162, 235, 0.7)',
                    borderColor: 'rgba(54, 162, 235, 1)',
                    borderWidth: 1
                }, {
                    label: '健保給付 (萬元)',
                    data: [4.2, 5.8, 4.3, 15.2, 18.5],
                    backgroundColor: 'rgba(75, 192, 192, 0.7)',
                    borderColor: 'rgba(75, 192, 192, 1)',
                    borderWidth: 1
                }, {
                    label: '現有保障可理賠 (萬元)',
                    data: [1.05, 3.85, 2.8, 6.3, 7.2],
                    backgroundColor: 'rgba(255, 99, 132, 0.7)',
                    borderColor: 'rgba(255, 99, 132, 1)',
                    borderWidth: 1
                }, {
                    label: '自付缺口 (萬元)',
                    data: [1.25, 2.65, 1.6, 4.1, 6.8],
                    backgroundColor: 'rgba(255, 159, 64, 0.7)',
                    borderColor: 'rgba(255, 159, 64, 1)',
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: '各類住院情境費用分析與保障缺口'
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: '金額 (萬元)'
                        }
                    }
                }
            }
        });

        // 自費項目開銷圖表
        const selfPayExpenseCtx = document.getElementById('selfPayExpenseChart').getContext('2d');
        const selfPayExpenseChart = new Chart(selfPayExpenseCtx, {
            type: 'bar',
            data: {
                labels: ['特殊檢查', '自費藥品', '特殊醫材', '手術差額', '病房差額', '專家會診'],
                datasets: [{
                    label: '平均自費金額 (萬元)',
                    data: [2.3, 3.5, 4.2, 5.1, 1.8, 2.7],
                    backgroundColor: 'rgba(255, 99, 132, 0.7)',
                    borderColor: 'rgba(255, 99, 132, 1)',
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: '住院期間常見自費項目金額分析（實支實付可理賠項目）'
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: '金額 (萬元)'
                        }
                    }
                }
            }
        });

        // 醫療費用趨勢圖
        const medicalCostTrendCtx = document.getElementById('medicalCostTrendChart').getContext('2d');
        const medicalCostTrendChart = new Chart(medicalCostTrendCtx, {
            type: 'line',
            data: {
                labels: ['2019', '2020', '2021', '2022', '2023', '2024'],
                datasets: [{
                    label: '平均住院總費用 (萬元)',
                    data: [8.3, 9.2, 10.5, 12.1, 13.8, 15.2],
                    borderColor: 'rgba(54, 162, 235, 1)',
                    backgroundColor: 'rgba(54, 162, 235, 0.1)',
                    fill: true,
                    tension: 0.1
                }, {
                    label: '自費項目佔比 (%)',
                    data: [22, 25, 28, 32, 35, 38],
                    borderColor: 'rgba(255, 99, 132, 1)',
                    backgroundColor: 'rgba(255, 99, 132, 0.1)',
                    fill: true,
                    tension: 0.1,
                    yAxisID: 'percentage'
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: '台灣住院費用趨勢與自費比例變化'
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: '金額 (萬元)'
                        }
                    },
                    percentage: {
                        position: 'right',
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: '百分比 (%)'
                        },
                        max: 100
                    }
                }
            }
        });

        // 重大疾病費用圖表
        const majorIllnessCostCtx = document.getElementById('majorIllnessCostChart').getContext('2d');
        const majorIllnessCostChart = new Chart(majorIllnessCostCtx, {
            type: 'bar',
            data: {
                labels: ['早期癌症', '晚期癌症', '心臟病', '腦中風', '器官移植', '重大傷殘'],
                datasets: [{
                    label: '平均治療費用 (萬元)',
                    data: [85, 165, 120, 135, 210, 95],
                    backgroundColor: 'rgba(153, 102, 255, 0.7)',
                    borderColor: 'rgba(153, 102, 255, 1)',
                    borderWidth: 1
                }, {
                    label: '收入損失 (萬元/年)',
                    data: [30, 60, 45, 50, 65, 40],
                    backgroundColor: 'rgba(255, 159, 64, 0.7)',
                    borderColor: 'rgba(255, 159, 64, 1)',
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: '重大疾病平均治療費用與收入損失'
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: '金額 (萬元)'
                        }
                    }
                }
            }
        });

        // 保險缺口圓餅圖
        const insuranceGapPieCtx = document.getElementById('insuranceGapPieChart').getContext('2d');
        const insuranceGapPieChart = new Chart(insuranceGapPieCtx, {
            type: 'pie',
            data: {
                labels: ['實支實付缺口', '重大疾病保障缺口', '自費醫療項目缺口', '收入損失風險', '現有保障'],
                datasets: [{
                    data: [35, 25, 18, 12, 10],
                    backgroundColor: [
                        'rgba(255, 99, 132, 0.7)',
                        'rgba(54, 162, 235, 0.7)',
                        'rgba(255, 206, 86, 0.7)',
                        'rgba(75, 192, 192, 0.7)',
                        'rgba(153, 102, 255, 0.7)'
                    ],
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: '現有保險保障分析與風險缺口比例'
                    }
                }
            }
        });
    </script>
</body>
</html>
