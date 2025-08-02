# COMPTE WAIL BADOULI

<html lang="fr" >
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Compte Trading - Waïl Badouli</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      margin: 0;
      font-family: 'SF Pro Display', sans-serif;
      background: #06080f;
      color: white;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }
    header {
      width: 100%;
      max-width: 430px;
      text-align: center;
      padding: 16px 10px;
      background: rgba(30, 20, 50, 0.9);
      box-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
      position: sticky;
      top: 0;
      z-index: 1000;
      user-select: none;
    }
    h1 {
      color: #00e5ff;
      margin: 0;
      font-size: 1.5rem;
      line-height: 1.2;
    }
    .balance {
      font-size: 1.2rem;
      color: #00e676;
      margin-top: 6px;
      font-weight: 600;
      letter-spacing: 0.03em;
    }
    .marquee {
      width: 100%;
      max-width: 430px;
      background: #0c101a;
      overflow: hidden;
      white-space: nowrap;
      box-shadow: 0 0 10px rgba(0, 255, 255, 0.2);
      padding: 5px 0;
      margin: 8px 0;
      user-select: none;
    }
    .marquee span {
      display: inline-block;
      padding-left: 100%;
      animation: marquee 20s linear infinite;
      color: #00e5ff;
      font-weight: 600;
      font-size: 0.85rem;
    }
    @keyframes marquee {
      0% {
        transform: translateX(0);
      }
      100% {
        transform: translateX(-100%);
      }
    }

    main {
      width: 100%;
      max-width: 430px;
      padding: 16px 12px 60px;
      flex: 1 0 auto;
      box-sizing: border-box;
    }
    h2 {
      color: #ff4081;
      margin-bottom: 12px;
      font-size: 1.3rem;
      font-weight: 600;
    }

    .balance-chart-container {
      width: 100%;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 15px;
      padding: 10px 15px;
      margin-bottom: 20px;
      box-shadow: 0 0 20px rgba(0, 255, 255, 0.15);
      backdrop-filter: blur(10px);
    }

    .crypto-forex {
      display: flex;
      flex-direction: column;
      gap: 20px;
      align-items: center;
    }
    .chart-container {
      width: 100%;
      max-width: 400px;
      height: 280px;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 15px;
      padding: 14px;
      box-shadow: 0 0 20px rgba(255, 0, 255, 0.15);
      backdrop-filter: blur(10px);
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .table-container {
      overflow-x: auto;
      margin-top: 30px;
      background: rgba(255, 255, 255, 0.85);
      border-radius: 15px;
      padding: 12px;
      box-shadow: 0 0 15px rgba(0, 255, 255, 0.15);
    }
    .table-container table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9rem;
      min-width: 600px;
      color: black;
    }
    .table-container th,
    .table-container td {
      padding: 12px 8px;
      text-align: center;
      color: black;
    }
    .table-container th {
      background: #d0d0d0;
      color: black;
      text-transform: uppercase;
    }
    .table-container tr:nth-child(even) {
      background: #f0f0f0;
    }
    .pos {
      color: #008000;
      font-weight: 700;
    }
    .neg {
      color: #b22222;
      font-weight: 700;
    }
    .fee {
      color: #daa520;
      font-weight: 700;
    }

    @media (max-width: 600px) {
      main {
        padding: 16px 8px 60px;
      }
      .chart-container,
      .balance-chart-container {
        max-width: 100%;
        height: 250px;
      }
      h2 {
        font-size: 1.1rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Solde actuel</h1>
    <div class="balance" id="balance">114 576.78 USD</div>
  </header>

  <div class="marquee">
    <span
      >EUR/USD +0.02% | ETH +1.2% | SOL -0.5% | XRP +0.4% | ADA +0.9% | FOREX:
      GBP/JPY -0.12%</span
    >
  </div>

  <main>
    <div class="balance-chart-container">
      <h2>Évolution du solde</h2>
      <canvas id="balanceChart"></canvas>
    </div>

    <h2>Portefeuille Crypto & Forex</h2>
    <div class="crypto-forex">
      <div class="chart-container">
        <canvas id="cryptoChart"></canvas>
      </div>
      <div class="chart-container">
        <canvas id="forexChart"></canvas>
      </div>
    </div>

    <h2>Historique Transactions</h2>
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Date</th>
            <th>Type</th>
            <th>Instrument</th>
            <th>Montant</th>
            <th>Solde Après</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>19 Juil 2025</td>
            <td>Retrait</td>
            <td>Compte</td>
            <td class="neg">-1 500 €</td>
            <td>114 576 €</td>
          </tr>
          <tr>
            <td>05 Juil 2025</td>
            <td>Virement Entrant</td>
            <td>Global Connect</td>
            <td class="pos">+1 225 €</td>
            <td>116 076 €</td>
          </tr>
          <tr>
            <td>28 Juin 2025</td>
            <td>Virement Sortant</td>
            <td>ICT Bank</td>
            <td class="neg">-1 225 €</td>
            <td>114 851 €</td>
          </tr>
          <tr>
            <td>12 Juin 2025</td>
            <td>Achat Crypto</td>
            <td>ETH</td>
            <td class="neg">-5 000 €</td>
            <td>114 076 €</td>
          </tr>
          <tr>
            <td>01 Juin 2025</td>
            <td>Clôture Forex</td>
            <td>EUR/USD</td>
            <td class="pos">+425 €</td>
            <td>119 076 €</td>
          </tr>
          <tr>
            <td>18 Mai 2025</td>
            <td>Vente Crypto</td>
            <td>SOL</td>
            <td class="pos">+2 800 €</td>
            <td>118 651 €</td>
          </tr>
          <tr>
            <td>15 Mai 2025</td>
            <td>Frais</td>
            <td>Plateforme</td>
            <td class="fee">-15 €</td>
            <td>115 851 €</td>
          </tr>
          <tr>
            <td>02 Mai 2025</td>
            <td>Virement Entrant</td>
            <td>David</td>
            <td class="pos">+321 €</td>
            <td>115 866 €</td>
          </tr>
          <tr>
            <td>01 Mai 2025</td>
            <td>Virement Sortant</td>
            <td>David</td>
            <td class="neg">-547 €</td>
            <td>115 545 €</td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>

  <script>
    // Fluctuation légère du solde
    let balance = 114576.78;
    const balanceEl = document.getElementById("balance");
    setInterval(() => {
      const fluctuation = (Math.random() * 6 - 3).toFixed(2);
      balance += parseFloat(fluctuation);
      balanceEl.textContent =
        balance.toLocaleString("fr-FR", {
          minimumFractionDigits: 2,
          maximumFractionDigits: 2,
        }) + " USD";
    }, 3000);

    // Graphique évolution solde
    const ctxBalanceChart = document.getElementById("balanceChart").getContext("2d");
    const balanceData = Array.from({ length: 20 }, () => 114000 + Math.random() * 600);
    const balanceChart = new Chart(ctxBalanceChart, {
      type: "line",
      data: {
        labels: Array.from({ length: 20 }, () => ""),
        datasets: [
          {
            label: "Solde en USD",
            data: balanceData,
            borderColor: "#00e5ff",
            backgroundColor: "rgba(0, 229, 255, 0.1)",
            tension: 0.3,
            fill: true,
            pointRadius: 0,
          },
        ],
      },
      options: {
        responsive: true,
        animation: false,
        scales: {
          x: { display: false },
          y: {
            beginAtZero: false,
            ticks: {
              color: "black",
            },
            grid: {
              color: "rgba(0,0,0,0.1)",
            },
          },
        },
        plugins: {
          legend: { labels: { color: "black" } },
          tooltip: {
            enabled: true,
            mode: "nearest",
            intersect: false,
          },
        },
      },
    });

    // Mise à jour régulière du graphique d'évolution du solde
    setInterval(() => {
      balanceData.push(balance);
      balanceData.shift();
      balanceChart.data.datasets[0].data = balanceData;
      balanceChart.update();
    }, 3000);

    // Graphique crypto
    new Chart(document.getElementById("cryptoChart"), {
      type: "doughnut",
      data: {
        labels: [
          "ETH",
          "SOL",
          "XRP",
          "ADA",
          "MATIC",
          "DOT",
          "AVAX",
          "LINK",
          "LTC",
          "DOGE",
        ],
        datasets: [
          {
            data: [30, 25, 20, 15, 10, 8, 6, 5, 4, 3],
            backgroundColor: [
              "#00e5ff",
              "#ff4081",
              "#00e676",
              "#ffca28",
              "#7c4dff",
              "#e641c7",
              "#e84142",
              "#2a5ada",
              "#a6a9aa",
              "#c2a633",
            ],
          },
        ],
      },
      options: {
        responsive: true,
        plugins: { legend: { labels: { color: "white" } } },
      },
    });

    // Graphique forex
    new Chart(document.getElementById("forexChart"), {
      type: "doughnut",
      data: {
        labels: ["EUR/USD", "GBP/JPY", "USD/CHF", "AUD/NZD", "CAD/JPY"],
        datasets: [
          {
            data: [35, 25, 15, 13, 12],
            backgroundColor: [
              "#00e5ff",
              "#ff4081",
              "#00e676",
              "#ffca28",
              "#7c4dff",
            ],
          },
        ],
      },
      options: {
        responsive: true,
        plugins: { legend: { labels: { color: "white" } } },
      },
    });
  </script>
</body>
</html>

