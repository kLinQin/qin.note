---
{"dg-publish":true,"permalink":"/qinnn/notes/wawa/resonator/build/havoc/chisa/chisa-chart/","created":"2025-12-07T14:37:48.113+07:00","updated":"2025-12-10T22:58:11.411+07:00"}
---

<style>
    .chart-container {
        height: 500px;
        width: 100%;
    }
</style>

<center><h3>SEQUENCE PRIORITY </h3></center>

<div class="chart-container">
    <canvas id="sequenceChart"></canvas> <!-- ID diubah -->
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
    document.addEventListener('DOMContentLoaded', function() {
        const canvas = document.getElementById('sequenceChart'); // ID sesuai
        if (!canvas) {
            console.error('Canvas element not found!');
            return;
        }
        
        const barCtx = canvas.getContext('2d');
        
        const dataValues = [290430264, 356426433, 442993930, 574833520];
        const baseline = dataValues[0];
        const percentages = dataValues.map(value => 
            ((value / baseline * 100).toFixed(1) + '%')
        );

        const myBarChart = new Chart(barCtx, {
            type: 'bar',
            data: {
                labels: ["S0", "S1", "S2", "S3"],
                datasets: [{
                    label: 'Chisa Damage Data',
                    data: dataValues,
                    backgroundColor: [
                        'rgba(255, 99, 132, 0.7)',
                        'rgba(54, 162, 235, 0.7)',
                        'rgba(255, 206, 86, 0.7)',
                        'rgba(75, 192, 192, 0.7)'
                    ],
                    borderColor: [
                        'rgba(255, 99, 132, 1)',
                        'rgba(54, 162, 235, 1)',
                        'rgba(255, 206, 86, 1)',
                        'rgba(75, 192, 192, 1)'
                    ],
                    borderWidth: 2
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'top',
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                label += context.parsed.y.toLocaleString();
                                label += ' (' + percentages[context.dataIndex] + ' relatif ke S0)';
                                return label;
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: false,
                        title: {
                            display: false,
                            text: 'Damage Value'
                        },
                        ticks: {
                            callback: function(value) {
                                return value.toLocaleString();
                            }
                        }
                    },
                    x: {
                        title: {
                            display: true,
                            text: 'Sequence (Sequence 0 = 100% baseline)'
                        }
                    }
                }
            },
            plugins: [{
                id: 'percentOnTop',
                afterDatasetsDraw(chart) {
                    const { ctx, data } = chart;
                    ctx.save();
                    
                    const meta = chart.getDatasetMeta(0);
                    
                    data.datasets[0].data.forEach((datapoint, index) => {
                        const element = meta.data[index];
                        
                        const x = element.x;
                        const y = element.y;
                        
                        ctx.font = 'bold 12px Arial';
                        ctx.fillStyle = '#939393';
                        ctx.textAlign = 'center';
                        ctx.textBaseline = 'bottom';
                        
                        ctx.fillText(percentages[index], x, y - 4);
                    });
                    
                    ctx.restore();
                }
            }]
        });
    });
</script>

<div style="margin-top: 8px; padding: 15px; background-color: #2a2a2a; border-radius: 8px; border-left: 4px solid #194c3b;">
  <p style="margin: 0 0 1px 0; font-size: 0.9em;">
    <strong>Note Sequence </strong> </p>
    <p style="margin: 0 0 10px 0; font-size: 0.9em;"><font color="#00b050">S2</font>: Mengabaikan 10% Havoc Res saat memberikan damage; Resonator dengan [Thread of Bane] mendapatkan 50% All-Attribute DMG Bonus. </p>
     <p style="margin: 0 0 10px 0; font-size: 0.9em;"><font color="#00b050">S3</font>: Pengkali atau multiplier DMG untuk [Chainsaw Mode] ditingkatkan sebesar 120%. Penting untuk <font color="#00b050">personal damage</font>.</p>
     <p style="margin: 0 0 1px 0; font-size: 0.9em;"><font color="#00b050">S2</font>: Mengabaikan 10% Havoc Res saat memberikan damage; Resonator dengan [Thread of Bane] mendapatkan 50% All-Attribute DMG Bonus. </p>
</div>

<br>
<center><h3>DAMAGE DISTRIBUTION </h3></center>

<div class="chart-container">
    <canvas id="distributionChart"></canvas> <!-- ID diubah -->
</div>

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const canvas = document.getElementById('distributionChart'); // ID sesuai
        if (!canvas) {
            console.error('Canvas element not found!');
            return;
        }
        
        const barCtx = canvas.getContext('2d');
        
        const dataValues = [3.2, 3.8, 83.4, 7.8];
        const percentages = dataValues.map(value => 
            value + '%'
        );

        const myRadarChart = new Chart(barCtx, {
            type: 'radar',
            data: {
                labels: ["Basic Attack", "Reso Skill", "Reso Lib", "Echo Skill"],
                datasets: [{
                    label: 'Damage Distribution',
                    data: dataValues,
                    backgroundColor: [
                        'rgba(255, 99, 132, 0.7)',
                        'rgba(54, 162, 235, 0.7)',
                        'rgba(255, 206, 86, 0.7)',
                        'rgba(75, 192, 192, 0.7)'
                    ],
                    borderColor: [
                        'rgba(255, 99, 132, 1)',
                        'rgba(54, 162, 235, 1)',
                        'rgba(255, 206, 86, 1)',
                        'rgba(75, 192, 192, 1)'
                    ],
                    borderWidth: 2
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                layout: {
                    padding: {
                        left: 20,
                        right: 20,
                        top: 20,
                        bottom: 20
                    }
                },
                plugins: {
                    legend: {
                        position: 'top',
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                label += context.parsed.r + '%';
                                return label;
                            }
                        }
                    }
                },
                scales: {
                    r: {
                        beginAtZero: true,
                        min: 0,
                        max: 100,
                        pointLabels: {
                            display: true,
                            font: {
                                size: 14,
                                weight: 'bold'
                            }
                        },
                        ticks: {
                            display: false,
                            backdropColor: 'transparent'
                        },
                        grid: {
                            color: 'rgba(0, 0, 0, 0.1)'
                        },
                        angleLines: {
                            color: 'rgba(0, 0, 0, 0.1)'
                        }
                    }
                }
            },
            plugins: [{
                id: 'percentOnTop',
                afterDatasetsDraw(chart) {
                    const { ctx, data } = chart;
                    ctx.save();
                    
                    const meta = chart.getDatasetMeta(0);
                    
                    data.datasets[0].data.forEach((datapoint, index) => {
                        const element = meta.data[index];
                        
                        const x = element.x;
                        const y = element.y;
                        
                        ctx.font = 'bold 12px Arial';
                        ctx.fillStyle = '#939393';
                        ctx.textAlign = 'center';
                        ctx.textBaseline = 'bottom';
                        
                        ctx.fillText(percentages[index], x, y - 4);
                    });
                    
                    ctx.restore();
                }
            }]
        });
    });
</script>

Kembali ke [[QINNN/NOTES/WAWA/RESONATOR/BUILD/HAVOC/CHISA/CHISA GUIDE\|Chisa Build]]


