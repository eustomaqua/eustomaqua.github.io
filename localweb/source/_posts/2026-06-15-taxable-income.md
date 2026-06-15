---
title: 个人所得税申报
date: 2026-06-14
updated: 2026-06-14
categories:
  - 俗世红尘
tags:
---


<!--
<!DOCTYPE html>
<html>
<head>
<style>
  .calc-table {
    width: 100%;
    border-collapse: collapse;
    font-family: sans-serif;
  }
  .calc-table th, .calc-table td {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
  }
  .calc-table input {
    width: 80%;
    padding: 5px;
    box-sizing: border-box;
  }
</style>
</head>
<body>

<table class="calc-table">
  <thead>
    <tr>
      <th>输入值 A</th>
      <th>输入值 B</th>
      <th>计算逻辑 $(A \times 2) + B$</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <input type="number" id="inputA" value="0" oninput="calculate()">
      </td>
      <td>
        <input type="number" id="inputB" value="0" oninput="calculate()">
      </td>
      <td>
        <span id="result">0</span>
      </td>
    </tr>
  </tbody>
</table>

<script>
  function calculate() {
    let a = parseFloat(document.getElementById('inputA').value) || 0;
    let b = parseFloat(document.getElementById('inputB').value) || 0;
    let result = (a * 2) + b;
    document.getElementById('result').innerText = result;
  }
</script>

</body>
</html>
-->



<!DOCTYPE html>
<html>
<head>
<!-- .tax-calculator {font-family: sans-serif;} -->
<style>
  .calc-table {
    width: 100%;
    border-collapse: collapse;
    font-family: sans-serif;
  }
  .calc-table th, .calc-table td {
    border: 1px solid #ccc;
    padding: 7px;
    text-align: center;
  }
  .calc-table input {
    width: 80%;
    padding: 4px;
    box-sizing: border-box;
  }

  .calc-table input.modern-input {
    width: 250px;
    padding: 7px;
    background-color: #f0f2f5;
    border: 2px solid transparent;
    border-radius: 30px;
    outline: none;
    transition: all 0.3s ease;
  }
  .calc-table input.modern-input:focus {
    background-color: #ffffff;
    border-color: #1890ff;
    box-shadow: 0 0 8px rgba(24, 144, 255, 0.2);
  }
  #tax-result {
    margin-top: 10px;
    font-weight: bold;
    white-space: pre-line;
  }
</style>
</head>

<body>
<label for="year-select">Which year are you choosing? </label>
<select id="year-select" onchange="getExchangeRate()">
    <option value="">---</option>
    <option value="2025">2025 </option>
    <option value="2024">2024 </option>
    <option value="2023">2023 </option>
</select>

<!-- 国家 汇率 计算逻辑 $(A \times 2) + B$ /to pay (in total)-->
<!-- Currency rate /exchange rate, foreign exchange, Deductible-->
<table class="calc-table">
  <thead>
    <tr>
      <th>Country</th>
      <th>FX</th>
      <th>Salary</th>
      <th>Tax prepaid</th>
      <th>Deductible</th>
      <th>*calc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>P.R. China</td>
      <td>1.0000</td>
      <td><input type="number" id="inputA" value="0" oninput="calculate()"></td>
      <td><input type="number" id="inputB" value="0" oninput="calculate()"></td>
      <td><span id="result">0</span></td>
      <td><span id="self-cn">0</span></td>
    </tr>
    <tr>
      <td></td><td>1.0000</td><td>
        <input class="modern-input" type="number" id="inputC" value="-78000" oninput="calculate()">
      </td><td>spec deductions (neg)</td><td></td><td></td> <!-- other -->
    </tr>
    <tr>
      <td>United States</td>
      <td><span type="number" id="rate-us"></td>
      <td><input type="number" oninput="calculate()" id="sal-us"></td>
      <td><input type="number" oninput="calculate()" id="taxed-us"></td>
      <td><span id="ded-us"></span></td>
      <td><span id="self-us"></span></td>
    </tr>
    <tr>
      <td>Singapore</td>
      <td><span type="number" id="rate-sg"></td>
      <td><input type="number" oninput="calculate()" id="sal-sg"></td>
      <td><input type="number" oninput="calculate()" id="taxed-sg"></td>
      <td><span id="ded-sg"></span></td>
      <td><span id="self-sg"></span></td>
    </tr>
    <tr>
      <td>Denmark</td>
      <td><span type="number" id="rate-dk"></td>
      <td><input type="number" oninput="calculate()" id="sal-dk"></td>
      <td><input type="number" oninput="calculate()" id="taxed-dk"></td>
      <td><span id="ded-dk"></span></td>
      <td><span id="self-dk"></span></td>
    </tr>
    <tr>
      <td>Poland</td>
      <td><span type="number" id="rate-pl"></td>
      <td><input type="number" oninput="calculate()" id="sal-pl"></td>
      <td><input type="number" oninput="calculate()" id="taxed-pl"></td>
      <td><span id="ded-pl"></span></td>
      <td><span id="self-pl"></span></td>
    </tr>
  </tbody>
</table>

<div id="tax-result" style="margin-top: 10px; font-weight: bold;"></div>



<script>
    const rate_usd = {"2025": 7.0288, "2024": 7.1884, "2023": 7.0827, };
    const rate_eur = {"2025": 8.2355, "2024": 7.5257, "2023": 7.8592, };
    const rate_gbp = {"2025": 9.4346, "2024": 9.0765, "2023": 9.0411, };
    const rate_aud = {"2025": 4.6892, "2024": 4.5070, "2023": 4.8484, };
    const rate_nzd = {"2025": 4.0520, "2024": 4.0955, "2023": 4.4991, };
    const rate_sgd = {"2025": 5.4586, "2024": 5.3214, "2023": 5.3772, }
    const rate_chf = {"2025": 8.8510, "2024": 7.9977, "2023": 8.4184, };
    const rate_cad = {"2025": 5.1142, "2024": 5.0498, "2023": 5.3673, };
    const rate_pln = {"2025": 1/0.51289, "2024": 1/0.56827, "2023": 1/0.55227, };
    const rate_dkk = {"2025": 1/0.9076, "2024": 1/0.9917, "2023": 0.9491, };
    const rate_sek = {"2025": 1/1.3129, "2024": 1/1.5233, "2023": 1.4065, };
    const rate_nok = {"2025": 1/1.4351, "2024": 1/1.5658, "2023": 1.4362, };

  const rates = {us: rate_usd, sg: rate_sgd, dk: rate_dkk, pl: rate_pln};
  function input2num(id) {
    return parseFloat(document.getElementById(id).value) || 0;
  }
  function setText(id, value) {
    document.getElementById(id).innerText = Number(value).toFixed(2);
  }

  function calculate() {
    const year = document.getElementById("year-select").value;
    if (!year) {
      document.getElementById("tax-result").innerText = "Please choose a year first.";
      return;
    }

    let a = parseFloat(document.getElementById('inputA').value) || 0;
    let b = parseFloat(document.getElementById('inputB').value) || 0;
    let c = parseFloat(document.getElementById('inputC').value) || 0;
    // let result = (a * 2) + b;
    // document.getElementById('result').innerText = result;
    // document.getElementById("inputA").addEventListener("input", calculate);

    const salary_us = input2num('sal-us') * rates.us[year];
    const salary_sg = input2num('sal-sg') * rates.sg[year];
    const salary_dk = input2num('sal-dk') * rates.dk[year];
    const salary_pl = input2num('sal-pl') * rates.pl[year];
    let income_ovs = salary_us + salary_sg + salary_dk + salary_pl;
    let income_cny = a + income_ovs;
    let tax_cny = updateAnnualTax(income_cny + c);
    // document.getElementById('result').value = b.toFixed(2);
    setText('result', b);
    setText('self-cn', updateAnnualTax(a + c)); //updateAnnualTax(income_cny));
    setText('self-sg', calc_sgTax(input2num('sal-sg') - 1000));
    // setText('self-dk', calc_dkTax(input2num('sal-dk')));

    const taxed_us = input2num('taxed-us') * rates.us[year];
    const taxed_sg = input2num('taxed-sg') * rates.sg[year];
    const taxed_dk = input2num('taxed-dk') * rates.dk[year];
    const taxed_pl = input2num('taxed-pl') * rates.pl[year];
    let deduct_us = tax_cny * salary_us / income_ovs;
    let deduct_sg = tax_cny * salary_sg / income_ovs;
    let decuct_dk = tax_cny * salary_dk / income_ovs;
    let decuct_pl = tax_cny * salary_pl / income_ovs;
    let pay_cny = b + Math.min(deduct_us, taxed_us) + Math.min(
      deduct_sg, taxed_sg) + Math.min(
      decuct_dk, taxed_dk) + Math.min(decuct_pl, taxed_pl);
    setText('ded-us', deduct_us);
    setText('ded-sg', deduct_sg);
    setText('ded-dk', decuct_dk);
    setText('ded-pl', decuct_pl);
    let credit = tax_cny - pay_cny;

    let text_icm = "Total income gained:"   //.padEnd(22, " ")
    let text_tax = "Overall tax payable :"  // .padStart(22, " ")
    let text_todo = "Remaining tax to pay:"
    document.getElementById('tax-result').innerText = `\n ${text_icm} ${income_cny.toFixed(2)} \n ${text_tax} ${tax_cny.toFixed(2)} \n ${text_todo} ${credit.toFixed(2)}`;
  }

  function updateAnnualTax(taxable_income) {
    const brackets = [[0, 0.00, 0],
                      [36000, 0.03, 0],
                      [144000, 0.10, 2520],
                      [300000, 0.20, 16920],
                      [420000, 0.25, 31920],
                      [660000, 0.30, 52920],
                      [960000, 0.35, 85920],
                      [Infinity, 0.45, 181920]];
    const bracket = brackets.find(([limit]) => taxable_income <= limit);
    return taxable_income * bracket[1] - bracket[2];
  }

  function calc_sgTax(taxable) {
    if (taxable <= 20000) {
      return 0;
    } else if (taxable <= 30000) {
      return (taxable - 20000) * 0.02;
    } else if (taxable <= 40000) {
      return 10000*0.02 + (taxable - 30000) * 3.5/100;
    } else if (taxable <= 80000) {
      return 200 + 10000*0.035 + (taxable - 40000)*0.07;
    } else if (taxable <= 120000) {
      return 200 + 350 + 40000*0.07 + (taxable - 80000)*11.5/100;
    } else if (taxable <= 160000) {
      return 200 + 350 + 2800 + (taxable - 120000)*15/100;
    } else if (taxable <= 200000) { 
      return 200 + 350 + 2800 + 6000 + (taxable - 160000) * 18/100;
    }
  }
  function calc_dkTax(income) {
    let labour = (income - income * 18.7/100) * 0.08;
    let employ = Math.min((income - labour) * 12.75/100, 63300)
    let base_taxable = income - labour - 54100 - employ;
    if (base_taxable <= 696000) {
      return base_taxable * 0.42;
    } else if (base_taxable <= 845000) {
      return 696000 * 0.42 + (base_taxable - 696000) * 0.49;
    } else if (base_taxable <= 2818000) {
      return 292320 + 149000*0.49 + (base_taxable - 845000) * 0.56;
    } else {
      return 292320 + 73010 + 1973000*0.56 + (base_taxable - 2818000)*0.61;
    }
  }

  function getExchangeRate() {
    // const year = document.getElementById("year-select").value;
    // const resultDiv = document.getElementById("result");
    // // 模拟的汇率数据（实际应用中可在此处调用 API 获取如 USD/CNY 的汇率）
    // const rates = {
    //     "2023": "1 USD = 7.05 CNY",
    //     "2024": "1 USD = 7.12 CNY",
    //     "2025": "1 USD = 7.15 CNY",
    //     "2026": "1 USD = 7.20 CNY"
    // };
    // if (year) {
    //     resultDiv.innerHTML = `该年份的平均汇率约为：${rates[year]}`;
    // } else {
    //     resultDiv.innerHTML = "";
    // }

    // https://www.pbc.gov.cn/zhengcehuobisi/125207/125217/125925/2025123109021714424/index.html
    // https://www.pbc.gov.cn/zhengcehuobisi/125207/125217/125925/5548334/index.html
    // https://www.pbc.gov.cn/zhengcehuobisi/125207/125217/125925/5184576/index.html
    // `${rates_us[year]}`;
    const year = document.getElementById("year-select").value;
    
    if (year) {
      document.getElementById("rate-us").innerText = `${rate_usd[year]}`;
      document.getElementById("rate-sg").innerText = `${rate_sgd[year]}`;
      document.getElementById("rate-dk").innerText = `${rate_dkk[year].toFixed(4)}`;
      document.getElementById("rate-pl").innerText = `${rate_pln[year].toFixed(4)}`;
    } else {
      document.getElementById("rate-us").innerText = "";
    }
  }
</script>



</body>
</html>

