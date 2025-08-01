# wail-dashboard1
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard Waïl Badouli</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
  body {
    margin: 0;
    font-family: 'SF Pro Display', sans-serif;
    background: radial-gradient(circle at top, #0b0f1a 0%, #06080f 100%);
    color: white;
    overflow-x: hidden;
  }
  header {
    position: sticky;
    top: 0;
    text-align: center;
    padding: 20px;
    background: rgba(20,25,40,0.8);
    backdrop-filter: blur(12px);
    box-shadow: 0 0 20px rgba(0,255,100,0.2);
  }
  #balance {
    font-size: 2em;
    color: #4caf50;
    transition: color 0.3s ease;
  }
  main {
    padding: 20px;
  }
  .charts {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
  }
  .chart-box {
    background: rgba(255,255,255,0.05);
    border-radius: 15px;
    backdrop-filter: blur(10px);
    padding: 15px;
    flex: 1 1 300px;
    min-width: 300px;
  }
  h2 {
    margin-top: 0;
    font-weight: 600;
    color: #4cafef;
  }
  .card {
    background: rgba(255,255,255,0.05);
    border-radius: 12px;
    padding: 12px;
    margin: 8px 0;
    backdrop-filter: blur(6px);
  }
  .ticker {
    width: 100%;
    background: rgba(20,25,40,0.9);
    color: #4cafef;
    position: fixed;
    bottom: 0;
    white-space: nowrap;
    overflow: hidden;
    height: 40px;
    line-height: 40px;
    font-size: 0.9em;
  }
  .ticker-content {
    display: inline-block;
    padding-left: 100%;
    animation: scroll 20s linear infinite;
  }
  @keyframes scroll {
    0% { transform: translateX(0); }
    100% { transform: translateX(-100%); }
  }
</style>
</head>
<body>
<header>
  <div><b>Compte de Waïl Badouli</b></div>
  <div id="balance">114,576.78 USD</div>
</header>

<main>
  <div class="charts">
    <div class="chart-box">
      <h2>Évolution du Compte</h2>
      <canvas id="balanceChart" height="200"></canvas>
    </div>
    <div class="chart-box">
      <h2>Portefeuille Crypto</h2>
      <canvas id="cryptoChart" height="200"></canvas>
    </div>
  </div>

  <h2>Transactions Récentes</h2>
  <div id="transactions">
    <!-- 25 transactions dynamiques -->
  </div>
</main>

<!-- Bandeau Forex -->
<div class="ticker">
  <div class="ticker-content" id="forexTicker">
    EUR/USD 1.098 ▲0.12% | GBP/JPY 182.44 ▼0.08% | USD/CHF 0.882 ▲0.05% | AUD/NZD 1.072 ▲0.15% | CAD/JPY 111.24 ▼0.10%
  </div>
</div>

<script>
  // --- Variables ---
  let balance = 114576.78;
  const transactions = [
    "19 Juil 2025 – Retrait – 1,500 EUR",
    "05 Juil 2025 – Virement Global Connect Services +1,225 EUR",
    "28 Juin 2025 – Virement vers ICT Bank –1,225 EUR",
    "12 Juin 2025 – Achat Crypto ETH –5,000 USD",
    "01 Juin 2025 – Clôture ordre Forex EUR/USD +425 USD",
    "18 Mai 2025 – Vente Crypto SOL +2,800 USD",
    "02 Mai 2025 – Virement reçu de David +321 USD",
    "01 Mai 2025 – Virement vers David –547 USD",
    "25 Avr 2025 – Achat Crypto ADA –2,000 USD",
    "15 Avr 2025 – Frais plateforme –15 USD",
    "05 Avr 2025 – Ordre Forex GBP/USD –250 USD",
    "01 Avr 2025 – Virement Global Connect Services +1,225 EUR",
    "28 Mar 2025 – Virement vers ICT Bank –1,225 EUR",
    "15 Mar 2025 – Achat Crypto DOT –1,000 USD",
    "02 Mar 2025 – Frais plateforme –12 USD",
    "20 Fév 2025 – Clôture Forex USD/JPY +375 USD",
    "10 Fév 2025 – Vente Crypto SOL +1,500 USD",
    "05 Fév 2025 – Ordre Forex EUR/GBP –180 USD",
    "25 Jan 2025 – Achat Crypto ETH –2,000 USD",
    "15 Jan 2025 – Virement reçu de David +321 USD",
    "05 Jan 2025 – Virement vers David –547 USD",
    "01 Jan 2025 – Virement Global Connect Services +1,225 EUR",
    "28 Déc 2024 – Virement vers ICT Bank –1,225 EUR",
    "20 Déc 2024 – Achat Crypto ADA –1,500 USD",
    "10 Déc 2024 – Frais plateforme –10 USD"
  ];

  // --- Inject transactions ---
  const txContainer = document.getElementById('transactions');
  transactions.forEach(tx => {
    const div = document.createElement('div');
    div.className = 'card';
    div.textContent = tx;
    txContainer.appendChild(div);
  });

  // --- Solde fluctuant ---
  setInterval(() => {
    const change = (Math.random() - 0.5) * 100;
    balance += change;
    const balElem = document.getElementById('balance');
    balElem.textContent = balance.toFixed(2) + ' USD';
    balElem.style.color = change >= 0 ? '#4caf50' : '#f44336';
  }, 2000);

  // --- Chart.js : Evolution balance ---
  const ctxBalance = document.getElementById('balanceChart');
  const balanceChart = new Chart(ctxBalance, {
    type: 'line',
    data: {
      labels: Array.from({length: 20}, (_, i) => i),
      datasets: [{
        label: 'Évolution USD',
        data: Array.from({length: 20}, () => 114000 + Math.random()*1000),
        borderColor: '#4caf50',
        backgroundColor: 'rgba(76, 175, 80, 0.1)',
        tension: 0.3
      }]
    },
    options: { plugins: { legend: { display: false } }, scales: { x: { display: false } } }
  });
  setInterval(() => {
    balanceChart.data.datasets[0].data.push(balance);
    balanceChart.data.datasets[0].data.shift();
    balanceChart.update();
  }, 2000);

  // --- Chart.js : Crypto camembert ---
  const ctxCrypto = document.getElementById('cryptoChart');
  new Chart(ctxCrypto, {
    type: 'doughnut',
    data: {
      labels: ['Ethereum', 'Solana', 'Cardano', 'Polkadot'],
      datasets: [{
        data: [34500, 32000, 28000, 20076],
        backgroundColor: ['#627EEA', '#14F195', '#0033AD', '#E6007A']
      }]
    }
  });
</script>
</body>
</html>
