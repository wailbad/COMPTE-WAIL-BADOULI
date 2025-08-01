# wail-dashboard1

<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Compte de Waïl Badouli</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      margin: 0;
      font-family: 'SF Pro Display', 'Segoe UI', sans-serif;
      background: linear-gradient(160deg, #000000, #0a0f1f, #111827);
      color: #e5e7eb;
      overflow-x: hidden;
    }
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 20px;
      background: rgba(17, 24, 39, 0.8);
      backdrop-filter: blur(15px);
      border-bottom: 1px solid rgba(255,255,255,0.1);
    }
    header img {
      height: 40px;
    }
    h1 {
      font-size: 1.1rem;
      margin: 0;
      color: #f3f4f6;
    }
    main {
      padding: 20px;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }
    .card {
      background: rgba(31, 41, 55, 0.7);
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 0 30px rgba(0,0,0,0.7);
      backdrop-filter: blur(15px);
      animation: fadeIn 0.5s ease-in-out;
    }
    @keyframes fadeIn { 
      from { opacity:0; transform: translateY(20px);} 
      to{opacity:1; transform: translateY(0);} 
    }
    .balance {
      font-size: 2rem;
      color: #22c55e;
      margin: 10px 0 0 0;
      text-shadow: 0 0 10px rgba(34,197,94,0.5);
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
      font-size: 0.9rem;
    }
    th, td {
      padding: 8px;
      border-bottom: 1px solid rgba(255,255,255,0.05);
    }
    th {
      color: #9ca3af;
      font-weight: normal;
      text-align: left;
    }
    .positive { color: #22c55e; }
    .negative { color: #ef4444; }
    canvas {
      margin-top: 10px;
    }
  </style>
</head>
<body>
<header>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/MetaTrader_4_logo.png/240px-MetaTrader_4_logo.png" alt="MetaTrader 4">
  <h1>Compte de Waïl Badouli</h1>
</header>

<main>
  <!-- Solde principal animé -->
  <div class="card">
    <p>Solde actuel</p>
    <p class="balance" id="balance">114 576.78 USD</p>
  </div>

  <!-- Historique transactions -->
  <div class="card">
    <h2>Historique des transactions</h2>
    <table id="transactions">
      <tr><th>Date</th><th>Description</th><th>Montant</th></tr>
      <tr><td>19/07/2025</td><td>Retrait en euros</td><td class="negative">-1 500 €</td></tr>
      <tr><td>05/07/2025</td><td>Virement à David</td><td class="negative">-547 USD</td></tr>
      <tr><td>02/07/2025</td><td>Virement reçu de David</td><td class="positive">+321 USD</td></tr>
      <tr><td>01/07/2025</td><td>Frais de maintenance</td><td class="negative">-15 USD</td></tr>
      <tr><td>25/06/2025</td><td>Virement Global Connect Services</td><td class="positive">+1 225 €</td></tr>
      <tr><td>26/06/2025</td><td>Virement à ICT BANK</td><td class="negative">-1 225 €</td></tr>
      <tr><td>21/06/2025</td><td>Achat crypto – Ethereum</td><td class="negative">-1 000 USD</td></tr>
      <tr><td>19/06/2025</td><td>Vente crypto – Solana</td><td class="positive">+650 USD</td></tr>
    </table>
  </div>

  <!-- Portefeuille crypto avec camembert -->
  <div class="card">
    <h2>Portefeuille Crypto</h2>
    <canvas id="cryptoChart"></canvas>
    <table>
      <tr><th>Crypto</th><th>Quantité</th><th>Valeur (USD)</th></tr>
      <tr><td>Ethereum (ETH)</td><td>12</td><td>38 400</td></tr>
      <tr><td>Solana (SOL)</td><td>180</td><td>27 000</td></tr>
      <tr><td>Cardano (ADA)</td><td>10 000</td><td>19 200</td></tr>
      <tr><td>Polkadot (DOT)</td><td>500</td><td>7 500</td></tr>
    </table>
  </div>
</main>

<script>
  // Animation du solde
  let balanceEl = document.getElementById("balance");
  let balance = 114576.78;
  setInterval(()=>{
    let variation = (Math.random()-0.5)*50;
    balance += variation;
    balanceEl.textContent = balance.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, " ") + " USD";
    balanceEl.style.color = variation>=0 ? "#22c55e" : "#ef4444";
  }, 4000);

  // Camembert crypto
  const ctx = document.getElementById('cryptoChart').getContext('2d');
  new Chart(ctx, {
    type: 'doughnut',
    data: {
      labels: ['Ethereum', 'Solana', 'Cardano', 'Polkadot'],
      datasets: [{
        data: [38400, 27000, 19200, 7500],
        backgroundColor: ['#6366f1', '#10b981', '#f59e0b', '#ec4899'],
        borderWidth: 0
      }]
    },
    options: {
      plugins: { legend: { labels: { color: 'white' } } }
    }
  });
</script>
</body>
</html>
