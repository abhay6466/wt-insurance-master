# wt-insurance-master
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ShieldSure — Systematic Architecture</title>
<style>
  :root {
    --color-primary: #0B1D3A;
    --color-accent: #C9973A;
    --color-bg: #F9F6F0;
    --color-surface: #FFFFFF;
    --color-text: #1A1A2E;
    --color-text-muted: #6B7280;
    --color-border: #E5E7EB;
    
    --space-sm: 8px;
    --space-md: 16px;
    --space-lg: 24px;
    --space-xl: 32px;
    
    --radius-md: 8px;
    --radius-lg: 12px;
    --shadow-md: 0 4px 16px rgba(11,29,58,0.08);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: system-ui, -apple-system, sans-serif; background: var(--color-bg); color: var(--color-text); line-height: 1.5; }

  .header { background: var(--color-primary); color: var(--color-surface); padding: var(--space-md) var(--space-xl); display: flex; justify-content: space-between; align-items: center; }
  .header__logo { color: var(--color-accent); font-size: 1.5rem; font-weight: 700; }
  
  .hero { background: var(--color-primary); color: var(--color-surface); padding: 60px 20px; text-align: center; }
  .hero__title { color: var(--color-accent); font-size: 2.5rem; margin-bottom: var(--space-sm); }
  
  .main-container { max-width: 1000px; margin: 0 auto; padding: var(--space-xl) var(--space-md); }

  .tabs { display: flex; gap: var(--space-sm); border-bottom: 2px solid var(--color-border); margin-bottom: var(--space-xl); }
  .tabs__btn { padding: var(--space-md) var(--space-xl); border: none; background: transparent; font-size: 1rem; color: var(--color-text-muted); cursor: pointer; border-bottom: 3px solid transparent; margin-bottom: -2px; font-weight: 600; transition: 0.2s ease; }
  .tabs__btn:hover { color: var(--color-primary); }
  .tabs__btn.is-active { color: var(--color-primary); border-bottom-color: var(--color-accent); }

  .calc-section { display: none; animation: fadeIn 0.3s ease; }
  .calc-section.is-active { display: grid; grid-template-columns: 1fr 1fr; gap: var(--space-xl); }
  @media (max-width: 768px) { .calc-section.is-active { grid-template-columns: 1fr; } }
  
  .card { background: var(--color-surface); padding: var(--space-xl); border-radius: var(--radius-lg); box-shadow: var(--shadow-md); }
  .card__title { margin-bottom: var(--space-lg); color: var(--color-primary); border-bottom: 2px solid var(--color-accent); padding-bottom: var(--space-sm); display: inline-block; }

  .form__group { margin-bottom: var(--space-md); }
  .form__row { display: grid; grid-template-columns: 1fr 1fr; gap: var(--space-md); }
  .form__label { display: block; font-size: 0.85rem; font-weight: 600; color: var(--color-text-muted); margin-bottom: 4px; text-transform: uppercase; letter-spacing: 0.5px; }
  .form__control { width: 100%; padding: 12px; border: 1.5px solid var(--color-border); border-radius: var(--radius-md); font-size: 1rem; transition: border-color 0.2s; }
  .form__control:focus { border-color: var(--color-accent); outline: none; }

  .btn { width: 100%; padding: 14px; background: var(--color-primary); color: var(--color-surface); border: none; border-radius: var(--radius-md); font-size: 1rem; font-weight: 600; cursor: pointer; transition: background 0.2s; margin-top: var(--space-sm); }
  .btn:hover { background: var(--color-accent); color: var(--color-primary); }

  .result-box { background: var(--color-primary); color: var(--color-surface); padding: var(--space-lg); border-radius: var(--radius-md); margin-top: var(--space-lg); text-align: center; display: none; }
  .result-box.is-visible { display: block; }
  .result-box__value { color: var(--color-accent); font-size: 2.5rem; font-weight: 700; margin: var(--space-sm) 0; }

  @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
</style>
</head>
<body>

<header class="header">
  <div class="header__logo">ShieldSure</div>
  <button class="btn" style="width: auto; margin: 0; padding: 8px 16px;">Contact</button>
</header>

<section class="hero">
  <h1 class="hero__title">Systematic Protection</h1>
  <p>Data-driven, modular insurance calculations.</p>
</section>

<main class="main-container">
  <nav class="tabs" id="tab-navigation">
    <button class="tabs__btn is-active" data-target="life">Life</button>
    <button class="tabs__btn" data-target="health">Health</button>
    <button class="tabs__btn" data-target="motor">Motor</button>
  </nav>

  <section id="life" class="calc-section is-active">
    <div class="card">
      <h2 class="card__title">Life Details</h2>
      <form id="form-life" onsubmit="event.preventDefault(); App.calculate('life');">
        <div class="form__row">
          <div class="form__group">
            <label class="form__label">Age</label>
            <input type="number" name="age" class="form__control" value="30" required>
          </div>
          <div class="form__group">
            <label class="form__label">Cover Amount</label>
            <select name="cover" class="form__control">
              <option value="5000000">₹50 Lakhs</option>
              <option value="10000000">₹1 Crore</option>
            </select>
          </div>
        </div>
        <div class="form__row">
          <div class="form__group">
            <label class="form__label">Term (Years)</label>
            <select name="term" class="form__control">
              <option value="20">20 Yrs</option>
              <option value="30">30 Yrs</option>
            </select>
          </div>
          <div class="form__group">
            <label class="form__label">Smoker</label>
            <select name="smoker" class="form__control">
              <option value="false">No</option>
              <option value="true">Yes</option>
            </select>
          </div>
        </div>
        <button type="submit" class="btn">Calculate Premium</button>
      </form>
      <div id="result-life" class="result-box">
        <div class="form__label">Estimated Monthly Premium</div>
        <div id="output-life" class="result-box__value">₹0</div>
      </div>
    </div>
  </section>

  <section id="health" class="calc-section">
    <div class="card">
      <h2 class="card__title">Health Details</h2>
      <form id="form-health" onsubmit="event.preventDefault(); App.calculate('health');">
        <div class="form__row">
          <div class="form__group">
            <label class="form__label">Age</label>
            <input type="number" name="age" class="form__control" value="32" required>
          </div>
          <div class="form__group">
            <label class="form__label">Cover Amount</label>
            <select name="cover" class="form__control">
              <option value="500000">₹5 Lakhs</option>
              <option value="1000000">₹10 Lakhs</option>
            </select>
          </div>
        </div>
        <button type="submit" class="btn">Calculate Premium</button>
      </form>
      <div id="result-health" class="result-box">
        <div class="form__label">Estimated Annual Premium</div>
        <div id="output-health" class="result-box__value">₹0</div>
      </div>
    </div>
  </section>

  <section id="motor" class="calc-section">
    <div class="card">
      <h2 class="card__title">Vehicle Details</h2>
      <form id="form-motor" onsubmit="event.preventDefault(); App.calculate('motor');">
        <div class="form__row">
          <div class="form__group">
            <label class="form__label">Vehicle Type</label>
            <select name="type" class="form__control">
              <option value="car">Car</option>
              <option value="bike">Two Wheeler</option>
            </select>
          </div>
          <div class="form__group">
            <label class="form__label">IDV (₹)</label>
            <input type="number" name="idv" class="form__control" value="600000" required>
          </div>
        </div>
        <div class="form__row">
          <div class="form__group">
            <label class="form__label">Coverage</label>
            <select name="coverage" class="form__control">
              <option value="comprehensive">Comprehensive</option>
              <option value="thirdparty">Third Party Only</option>
            </select>
          </div>
          <div class="form__group">
            <label class="form__label">NCB</label>
            <select name="ncb" class="form__control">
              <option value="0">0%</option>
              <option value="20">20%</option>
              <option value="25">25%</option>
              <option value="50">50%</option>
            </select>
          </div>
        </div>
        <button type="submit" class="btn">Calculate Premium</button>
      </form>
      <div id="result-motor" class="result-box">
        <div class="form__label">Estimated Annual Premium</div>
        <div id="output-motor" class="result-box__value">₹0</div>
      </div>
    </div>
  </section>

</main>

<script>
const Utils = {
  formatCurrency: (num) => new Intl.NumberFormat('en-IN', { style: 'currency', currency: 'INR', maximumFractionDigits: 0 }).format(num),
  getFormData: (formId) => Object.fromEntries(new FormData(document.getElementById(formId)).entries())
};

const InsuranceLogic = {
  life: (data) => {
    let baseRate = data.cover * 0.00036;
    if (data.age > 40) baseRate *= 1.4;
    if (data.smoker === 'true') baseRate *= 1.5;
    return (baseRate * (20 / data.term)) / 12;
  },
  
  health: (data) => {
    let baseRate = data.cover * 0.016;
    if (data.age > 45) baseRate *= 1.5;
    return baseRate;
  },

  motor: (data) => {
    let tpPremium = data.type === 'car' ? 2094 : 714;
    let odPremium = data.coverage === 'comprehensive' ? (data.idv * 0.026 * (1 - (data.ncb / 100))) : 0;
    return tpPremium + odPremium;
  }
};

const UI = {
  switchTab: (targetId) => {
    document.querySelectorAll('.tabs__btn').forEach(btn => {
      btn.classList.toggle('is-active', btn.dataset.target === targetId);
    });
    document.querySelectorAll('.calc-section').forEach(sec => {
      sec.classList.toggle('is-active', sec.id === targetId);
    });
  },
  
  renderResult: (type, amount) => {
    document.getElementById(`output-${type}`).textContent = Utils.formatCurrency(amount);
    document.getElementById(`result-${type}`).classList.add('is-visible');
  }
};

const App = {
  init: () => {
    document.getElementById('tab-navigation').addEventListener('click', (e) => {
      if (e.target.classList.contains('tabs__btn')) {
        UI.switchTab(e.target.dataset.target);
      }
    });
  },
  
  calculate: (type) => {
    const rawData = Utils.getFormData(`form-${type}`);
    const parsedData = Object.keys(rawData).reduce((acc, key) => {
      acc[key] = isNaN(rawData[key]) || rawData[key] === '' ? rawData[key] : Number(rawData[key]);
      return acc;
    }, {});

    const premium = InsuranceLogic[type](parsedData);
    UI.renderResult(type, premium);
  }
};

document.addEventListener('DOMContentLoaded', App.init);
</script>
</body>
</html>
