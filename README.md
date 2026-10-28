<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interest Calculator</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #e8f0ff, #f7f9fc);
      color: #1e293b;
      min-height: 100vh;
      padding: 30px 15px;
    }

    .container {
      max-width: 850px;
      margin: auto;
    }

    header {
      text-align: center;
      margin-bottom: 28px;
    }

    header h1 {
      color: #1747b0;
      font-size: 32px;
      margin-bottom: 10px;
    }

    header p {
      color: #64748b;
      line-height: 1.6;
    }

    .calculator {
      background: white;
      padding: 28px;
      border-radius: 20px;
      box-shadow: 0 12px 35px rgba(25, 50, 100, 0.10);
    }

    .field {
      margin-bottom: 20px;
    }

    label {
      display: block;
      font-weight: 600;
      margin-bottom: 9px;
      font-size: 14px;
    }

    input, select {
      width: 100%;
      padding: 13px;
      border: 1px solid #cbd5e1;
      border-radius: 10px;
      font-size: 16px;
      background: white;
      color: #1e293b;
      outline: none;
    }

    input:focus, select:focus {
      border-color: #2563eb;
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12);
    }

    .grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 18px;
    }

    .duration {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }

    .buttons {
      display: flex;
      gap: 12px;
      margin-top: 8px;
    }

    button {
      flex: 1;
      padding: 14px;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: 0.2s;
    }

    .calculate {
      background: #2563eb;
      color: white;
    }

    .calculate:hover {
      background: #1747b0;
    }

    .reset {
      background: #e2e8f0;
      color: #334155;
    }

    .reset:hover {
      background: #cbd5e1;
    }

    .results {
      display: none;
      margin-top: 25px;
      border-radius: 16px;
      overflow: hidden;
      border: 1px solid #dbeafe;
    }

    .result-header {
      background: #1747b0;
      color: white;
      padding: 22px;
      text-align: center;
    }

    .result-header p {
      font-size: 14px;
      opacity: 0.9;
      margin-bottom: 8px;
    }

    .result-header h2 {
      font-size: 34px;
      overflow-wrap: anywhere;
    }

    .result-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1px;
      background: #e2e8f0;
    }

    .result-item {
      padding: 20px;
      background: #f8fafc;
    }

    .result-item p {
      color: #64748b;
      font-size: 13px;
      margin-bottom: 8px;
    }

    .result-item h3 {
      font-size: 21px;
      overflow-wrap: anywhere;
    }

    .breakdown {
      padding: 20px;
      background: white;
    }

    .breakdown h3 {
      margin-bottom: 15px;
      color: #1747b0;
    }

    .breakdown-row {
      display: flex;
      justify-content: space-between;
      gap: 15px;
      padding: 11px 0;
      border-bottom: 1px solid #e2e8f0;
      font-size: 14px;
    }

    .breakdown-row span:last-child {
      font-weight: 600;
      text-align: right;
    }

    .note {
      color: #64748b;
      font-size: 12px;
      line-height: 1.6;
      margin-top: 15px;
    }

    .error {
      display: none;
      color: #b91c1c;
      background: #fef2f2;
      border: 1px solid #fecaca;
      border-radius: 8px;
      padding: 12px;
      margin-top: 15px;
      font-size: 14px;
    }

    footer {
      text-align: center;
      color: #64748b;
      font-size: 13px;
      margin-top: 25px;
    }

    @media (max-width: 550px) {
      body {
        padding: 20px 12px;
      }

      header h1 {
        font-size: 27px;
      }

      .calculator {
        padding: 19px;
      }

      .grid {
        grid-template-columns: 1fr;
        gap: 0;
      }

      .result-header h2 {
        font-size: 28px;
      }

      .result-item {
        padding: 14px;
      }

      .result-item h3 {
        font-size: 18px;
      }

      .buttons {
        flex-direction: column;
      }
    }
  </style>
</head>

<body>
  <div class="container">

    <header>
      <h1>💰 Interest Calculator</h1>
      <p>Calculate interest and maturity amount with years and months.</p>
    </header>

    <main class="calculator">

      <form id="interestForm">

        <div class="field">
          <label for="principal">Principal Amount (₹)</label>
          <input
            type="number"
            id="principal"
            min="0.01"
            step="any"
            placeholder="Example: 50000"
            required
          >
        </div>

        <div class="grid">
          <div class="field">
            <label for="rate">Annual Interest Rate (%)</label>
            <input
              type="number"
              id="rate"
              min="0"
              max="1000"
              step="any"
              placeholder="Example: 8.5"
              required
            >
          </div>

          <div class="field">
            <label for="type">Interest Type</label>
            <select id="type">
              <option value="simple">Simple Interest</option>
              <option value="compound">Compound Interest</option>
            </select>
          </div>
        </div>

        <div class="field">
          <label>Duration</label>
          <div class="duration">
            <div>
              <input
                type="number"
                id="years"
                min="0"
                max="1000"
                step="1"
                value="1"
                placeholder="Years"
                aria-label="Years"
                required
              >
              <small>Years</small>
            </div>

            <div>
              <input
                type="number"
                id="months"
                min="0"
                max="11"
                step="1"
                value="0"
                placeholder="Months"
                aria-label="Months"
                required
              >
              <small>Months (0–11)</small>
            </div>
          </div>
        </div>

        <div class="buttons">
          <button type="submit" class="calculate">
            Calculate Interest
          </button>

          <button type="reset" class="reset">
            Reset
          </button>
        </div>

        <div id="error" class="error" role="alert"></div>
      </form>

      <section id="results" class="results" aria-live="polite">

        <div class="result-header">
          <p>Total Maturity Amount</p>
          <h2 id="total">₹0.00</h2>
        </div>

        <div class="result-grid">
          <div class="result-item">
            <p>Principal Amount</p>
            <h3 id="principalResult">₹0.00</h3>
          </div>

          <div class="result-item">
            <p>Total Interest</p>
            <h3 id="interestResult">₹0.00</h3>
          </div>

          <div class="result-item">
            <p>Interest Rate</p>
            <h3 id="rateResult">0%</h3>
          </div>

          <div class="result-item">
            <p>Total Duration</p>
            <h3 id="durationResult">0 months</h3>
          </div>
        </div>

        <div class="breakdown">
          <h3>Calculation Breakdown</h3>

          <div class="breakdown-row">
            <span>Interest Method</span>
            <span id="methodResult">Simple Interest</span>
          </div>

          <div class="breakdown-row">
            <span>Principal</span>
            <span id="breakPrincipal">₹0.00</span>
          </div>

          <div class="breakdown-row">
            <span>Interest Earned / Payable</span>
            <span id="breakInterest">₹0.00</span>
          </div>

          <div class="breakdown-row">
            <span>Final Amount</span>
            <span id="breakTotal">₹0.00</span>
          </div>

          <p class="note" id="formulaNote"></p>
        </div>

      </section>
    </main>

    <footer>
      Interest Calculator · Free to use · No data is uploaded
    </footer>

  </div>

  <script>
    const form = document.getElementById("interestForm");
    const results = document.getElementById("results");
    const errorBox = document.getElementById("error");

    const money = new Intl.NumberFormat("en-IN", {
      style: "currency",
      currency: "INR",
      minimumFractionDigits: 2,
      maximumFractionDigits: 2
    });

    function formatMoney(value) {
      return money.format(value);
    }

    form.addEventListener("submit", function (event) {
      event.preventDefault();

      errorBox.style.display = "none";
      results.style.display = "none";

      const principal = Number(document.getElementById("principal").value);
      const rate = Number(document.getElementById("rate").value);
      const years = Number(document.getElementById("years").value);
      const months = Number(document.getElementById("months").value);
      const type = document.getElementById("type").value;

      if (
        !Number.isFinite(principal) ||
        !Number.isFinite(rate) ||
        !Number.isInteger(years) ||
        !Number.isInteger(months) ||
        principal <= 0 ||
        rate < 0 ||
        rate > 1000 ||
        years < 0 ||
        years > 1000 ||
        months < 0 ||
        months > 11 ||
        years + months === 0
      ) {
        errorBox.textContent =
          "Enter a positive principal, a valid rate, and a duration greater than zero. Months must be between 0 and 11.";
        errorBox.style.display = "block";
        return;
      }

      const totalMonths = years * 12 + months;
      const timeInYears = totalMonths / 12;

      let interest;
      let total;
      let formulaNote;

      if (type === "simple") {
        // Simple Interest = Principal × Rate × Time / 100
        interest = principal * rate * timeInYears / 100;
        total = principal + interest;

        formulaNote =
          "Simple Interest = Principal × Annual Rate × Duration in Years ÷ 100. " +
          "The duration is calculated using total months ÷ 12.";
      } else {
        // Monthly compounding, using the annual nominal rate divided by 12.
        const monthlyRate = rate / 100 / 12;
        total = principal * Math.pow(1 + monthlyRate, totalMonths);
        interest = total - principal;

        formulaNote =
          "Compound Amount = Principal × (1 + Annual Rate ÷ 1200) ^ Total Months. " +
          "Interest is compounded monthly, with no additional deposits or withdrawals.";
      }

      if (!Number.isFinite(total) || !Number.isFinite(interest)) {
        errorBox.textContent =
          "The result is too large to calculate. Please use smaller values.";
        errorBox.style.display = "block";
        return;
      }

      document.getElementById("total").textContent =
        formatMoney(total);

      document.getElementById("principalResult").textContent =
        formatMoney(principal);

      document.getElementById("interestResult").textContent =
        formatMoney(interest);

      document.getElementById("rateResult").textContent =
        rate + "% per year";

      document.getElementById("durationResult").textContent =
        years + (years === 1 ? " year " : " years ") +
        months + (months === 1 ? " month" : " months");

      document.getElementById("methodResult").textContent =
        type === "simple"
          ? "Simple Interest"
          : "Compound Interest (Monthly)";

      document.getElementById("breakPrincipal").textContent =
        formatMoney(principal);

      document.getElementById("breakInterest").textContent =
        formatMoney(interest);

      document.getElementById("breakTotal").textContent =
        formatMoney(total);

      document.getElementById("formulaNote").textContent =
        formulaNote;

      results.style.display = "block";
    });

    form.addEventListener("reset", function () {
      results.style.display = "none";
      errorBox.style.display = "none";
    });
  </script>
</body>
</html>
