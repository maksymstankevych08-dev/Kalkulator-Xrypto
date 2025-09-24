<!doctype html>
<html lang="pl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Kalkulator transakcji BTC</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#06b6d4;--muted:#94a3b8;--glass: rgba(255,255,255,0.03)}
    html,body{height:100%;margin:0;font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,'Helvetica Neue',Arial;background:linear-gradient(180deg,#071024 0%,#071428 60%);color:#e6eef6}
    .container{max-width:1100px;margin:32px auto;padding:24px}
    header{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}
    h1{font-size:20px;margin:0}
    p.lead{color:var(--muted);margin:6px 0 0;font-size:13px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:16px;border-radius:12px;box-shadow:0 6px 18px rgba(2,6,23,0.6)}
    table{width:100%;border-collapse:collapse;font-size:13px}
    thead th{font-weight:600;text-align:left;padding:8px 10px;color:#cfe8f2}
    tbody td{padding:8px 10px;border-top:1px solid rgba(255,255,255,0.03)}
    input[type="number"], input[type="date"], input[type="text"]{width:100%;box-sizing:border-box;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit}
    .actions{display:flex;gap:8px;align-items:center}
    button{background:var(--accent);border:none;padding:8px 12px;border-radius:8px;color:#042023;font-weight:600;cursor:pointer}
    button.ghost{background:transparent;border:1px solid rgba(255,255,255,0.04);color:var(--muted);font-weight:600}
    .right{text-align:right}
    .muted{color:var(--muted);font-size:13px}
    .totals{display:flex;gap:12px;flex-wrap:wrap;margin-top:12px}
    .totals .tile{background:var(--glass);padding:12px;border-radius:10px;min-width:140px}
    .green{color:#7ee787}
    .red{color:#ff7b7b}
    .small{font-size:12px;color:var(--muted)}
    .controls{display:flex;gap:10px;align-items:center;margin-bottom:12px}
    @media (max-width:900px){thead th:nth-child(3),td:nth-child(3),thead th:nth-child(5),td:nth-child(5){display:none}}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div>
        <h1>Kalkulator transakcji BTC</h1>
        <p class="lead">Wpisz daty, ceny i ilości — strona policzy kwoty, zysk/stratę i procenty.</p>
      </div>
      <div class="actions">
        <button id="addRow">Dodaj wiersz</button>
        <button id="reset" class="ghost">Wyczyść</button>
      </div>
    </header>

    <div class="card">
      <div class="controls">
        <div class="small muted">Wpisuj ręcznie ceny BTC z momentu zakupu i sprzedaży. Kalkulator policzy resztę.</div>
      </div>

      <table id="txTable">
        <thead>
          <tr>
            <th>Data zakupu</th>
            <th>Cena zakupu (1 BTC)</th>
            <th>Ilość BTC</th>
            <th>Kwota zakupu</th>
            <th>Data sprzedaży</th>
            <th>Cena sprzedaży (1 BTC)</th>
            <th>Kwota sprzedaży</th>
            <th>Zysk/Strata</th>
            <th>%</th>
            <th></th>
          </tr>
        </thead>
        <tbody id="tbody">
        </tbody>
      </table>

      <div class="totals">
        <div class="tile">
          <div class="small">Suma wydatków</div>
          <div id="sumBuy">0</div>
        </div>
        <div class="tile">
          <div class="small">Suma wpływów</div>
          <div id="sumSell">0</div>
        </div>
        <div class="tile">
          <div class="small">Łączny zysk / strata</div>
          <div id="sumProfit">0</div>
        </div>
        <div class="tile">
          <div class="small">Średni % na transakcji</div>
          <div id="avgPct">0%</div>
        </div>
      </div>

    </div>

  </div>

  <script>
    function fmt(num){
      if(num === "" || num === null || isNaN(num)) return '';
      return Number(num).toLocaleString('pl-PL', {minimumFractionDigits:2, maximumFractionDigits:2});
    }

    function createRow(){
      const tr = document.createElement('tr');
      tr.innerHTML = `
        <td><input type="date" class="buyDate"></td>
        <td><input type="number" class="buyPrice" step="0.01" min="0" placeholder="Cena BTC (zakup)"></td>
        <td><input type="number" class="amount" step="0.00000001" min="0" placeholder="Ilość BTC"></td>
        <td class="right buyAmount"></td>
        <td><input type="date" class="sellDate"></td>
        <td><input type="number" class="sellPrice" step="0.01" min="0" placeholder="Cena BTC (sprzedaż)"></td>
        <td class="right sellAmount"></td>
        <td class="right profit"></td>
        <td class="right pct"></td>
        <td class="right"><button class="remove ghost">Usuń</button></td>
      `;

      tr.querySelectorAll('input').forEach(i => i.addEventListener('input', computeAll));
      tr.querySelector('.remove').addEventListener('click', ()=>{ tr.remove(); computeAll(); });

      return tr;
    }

    const tbody = document.getElementById('tbody');
    const addRowBtn = document.getElementById('addRow');
    const resetBtn = document.getElementById('reset');

    addRowBtn.addEventListener('click', ()=>{ tbody.appendChild(createRow()); computeAll(); });
    resetBtn.addEventListener('click', ()=>{ tbody.innerHTML=''; computeAll(); });

    tbody.appendChild(createRow());

    function parseNum(val){
      if(val === null || val === undefined || val === '') return NaN;
      return Number(val);
    }

    function computeAll(){
      let sumBuy = 0, sumSell = 0, sumProfit = 0, pctCount = 0, pctSum = 0;
      [...tbody.querySelectorAll('tr')].forEach(tr => {
        const buyPrice = parseNum(tr.querySelector('.buyPrice').value);
        const amt = parseNum(tr.querySelector('.amount').value);
        const sellPrice = parseNum(tr.querySelector('.sellPrice').value);

        const buyAmountCell = tr.querySelector('.buyAmount');
        const sellAmountCell = tr.querySelector('.sellAmount');
        const profitCell = tr.querySelector('.profit');
        const pctCell = tr.querySelector('.pct');

        const buyAmt = (!isNaN(buyPrice) && !isNaN(amt)) ? (buyPrice * amt) : NaN;
        const sellAmt = (!isNaN(sellPrice) && !isNaN(amt)) ? (sellPrice * amt) : NaN;

        buyAmountCell.textContent = isNaN(buyAmt) ? '' : fmt(buyAmt);
        sellAmountCell.textContent = isNaN(sellAmt) ? '' : fmt(sellAmt);

        let profit = NaN;
        if(!isNaN(buyAmt) && !isNaN(sellAmt)){
          profit = sellAmt - buyAmt;
          profitCell.textContent = fmt(profit);
          profitCell.classList.toggle('green', profit>0);
          profitCell.classList.toggle('red', profit<0);
        } else {
          profitCell.textContent = '';
          profitCell.classList.remove('green','red');
        }

        let pct = NaN;
        if(!isNaN(profit) && !isNaN(buyAmt) && buyAmt !== 0){
          pct = (profit / buyAmt) * 100;
          pctCell.textContent = pct.toFixed(2) + '%';
          pctCell.classList.toggle('green', pct>0);
          pctCell.classList.toggle('red', pct<0);
          pctSum += pct;
          pctCount += 1;
        } else {
          pctCell.textContent = '';
          pctCell.classList.remove('green','red');
        }

        if(!isNaN(buyAmt)) sumBuy += buyAmt;
        if(!isNaN(sellAmt)) sumSell += sellAmt;
        if(!isNaN(profit)) sumProfit += profit;
      });

      document.getElementById('sumBuy').textContent = fmt(sumBuy);
      document.getElementById('sumSell').textContent = fmt(sumSell);
      const sp = document.getElementById('sumProfit');
      sp.textContent = fmt(sumProfit);
      sp.classList.toggle('green', sumProfit>0);
      sp.classList.toggle('red', sumProfit<0);

      const avgPct = (pctCount===0) ? 0 : (pctSum/pctCount);
      document.getElementById('avgPct').textContent = avgPct.toFixed(2) + '%';
    }

    computeAll();
  </script>
</body>
</html>
