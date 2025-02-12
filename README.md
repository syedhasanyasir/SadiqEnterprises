<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Login & Billing System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #ffffff; /* White Background */
      color: #000000; /* Black Text */
    }
    .container {
      padding: 10px;
    }
    .login-container, .billing-container {
      display: none;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 20px;
    }
    .login-container {
      display: flex; /* Show login page initially */
    }
    .login-box {
      width: 100%;
      max-width: 400px;
      background-color: #d3d3d3; /* Light Grey */
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      text-align: center;
    }
    .login-box h1 {
      margin-bottom: 20px;
      color: #000000; /* Black Text */
    }
    .login-box input {
      width: 100%;
      padding: 12px;
      margin-bottom: 15px;
      background-color: #ffffff; /* White Input Background */
      color: #000000; /* Black Text */
      border: 1px solid #d3d3d3; /* Light Grey Border */
      border-radius: 4px;
    }
    .login-box input:focus {
      outline: none;
      border-color: #a9a9a9; /* Darker Grey */
    }
    .login-box button {
      width: 100%;
      padding: 12px;
      background-color: #ffffff; /* White Button */
      color: #000000; /* Black Text */
      border: 2px solid #d3d3d3; /* Light Grey Border */
      border-radius: 5px;
      cursor: pointer;
      font-weight: bold;
    }
    .login-box button:hover {
      background-color: #d3d3d3; /* Light Grey Button */
      color: #000000; /* Black Text */
    }
    .billing-container {
      display: none;
      flex-direction: column;
      align-items: stretch;
      padding: 20px;
    }
    .billing-container h1 {
      text-align: center;
      color: #000000; /* Black Text */
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
      overflow-x: auto;
    }
    th, td {
      padding: 10px;
      text-align: left;
      border: 1px solid #d3d3d3; /* Light Grey Border */
    }
    th {
      background-color: #d3d3d3; /* Light Grey Background */
      color: #000000; /* Black Text */
    }
    .total-section {
      margin-top: 20px;
      text-align: right;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .total-section label {
      font-weight: bold;
      margin-right: 10px;
    }
    .total-section span {
      color: #000000; /* Black Text */
      font-weight: bold;
    }
    .total-section input {
      width: 100px;
      padding: 8px;
      border: 1px solid #d3d3d3; /* Light Grey Border */
      border-radius: 4px;
    }
    button {
      background-color: #d3d3d3; /* Light Grey Button */
      color: #000000; /* Black Text */
      border: none;
      padding: 12px;
      margin-top: 20px;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #a9a9a9; /* Darker Grey Button */
    }

    /* Responsive Design */
    @media (max-width: 768px) {
      table, th, td {
        font-size: 12px;
      }
      .login-box {
        padding: 15px;
      }
      .login-box h1 {
        font-size: 20px;
      }
      .login-box button {
        padding: 10px;
      }
    }
    @media (max-width: 480px) {
      .login-box input, .login-box button {
        padding: 8px;
        font-size: 14px;
      }
      .total-section input {
        width: 80px;
      }
    }
  </style>
</head>
<body>
  <!-- Login Page -->
  <div class="login-container" id="loginPage">
    <div class="login-box">
      <h1>SADIQ ENTERPRISES PVT. (LTD)</h1>
      <input type="text" id="username" placeholder="Enter Username" required>
      <input type="password" id="password" placeholder="Enter Password" required>
      <button onclick="login()">Login</button>
    </div>
  </div>

  <!-- Billing System -->
  <div class="billing-container" id="billingPage">
    <h1>SADIQ ENTERPRISES PVT. (LTD) - Billing System</h1>
    <table>
      <thead>
        <tr>
          <th>Serial No.</th>
          <th>Item</th>
          <th>Rate (Editable)</th>
          <th>Quantity</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody id="billTableBody">
        <!-- Rows will be dynamically added -->
      </tbody>
    </table>
    <button onclick="addRow()">Add Row</button>

    <div class="total-section">
      <label>Subtotal:</label>
      <span id="subtotal">0</span><br>
      <label>Discount (%):</label>
      <input type="number" id="discount" value="0" onchange="calculateTotal()">
      <br>
      <label>Total:</label>
      <span id="finalTotal">0</span>
    </div>
  </div>

  <script>
    const validUsername = "admin";
    const validPassword = "12345";

    function login() {
      const username = document.getElementById("username").value;
      const password = document.getElementById("password").value;

      if (username === validUsername && password === validPassword) {
        document.getElementById("loginPage").style.display = "none";
        document.getElementById("billingPage").style.display = "block";
      } else {
        alert("Invalid username or password!");
      }
    }

    const items = [
      { name: "Fuel Pipe CD 70", rate: 32.44 },
      { name: "Blow Pipe (Old Model) CD 70", rate: 45.58 },
      { name: "Battery Pipe CD 70", rate: 26.61 },
      { name: "Blow Pipe (New Model) CD 70", rate: 60.84 },
      { name: "Z Pipe CD 70", rate: 27.45 },
      { name: "L Pipe CD 70", rate: 13.67 },
      { name: "Fuel Pipe CG 125", rate: 35.72 },
      { name: "Blow Pipe (Old Model) CG 125", rate: 46.53 },
      { name: "Battery Pipe CG 125", rate: 29.47 },
      { name: "ASV Control CG 125", rate: 53.42 },
      { name: "Blow Pipe (New Model) CG 125", rate: 85.01 },
      { name: "B Breather (Hockey) CG 125", rate: 73.46 },
      { name: "Section Pipe CG 125", rate: 110.03 },
      { name: "150 Pipe CG 125", rate: 29.47 },
      { name: "Fuel Pipe CG 125 DLX", rate: 37.52 },
      { name: "Blow Pipe CG 125 DLX", rate: 61.27 },
      { name: "Battery Pipe CG 125 DLX", rate: 26.08 },
      { name: "Fuel Pipe CD 100", rate: 29.36 },
      { name: "Blow Pipe CD 100", rate: 34.77 },
      { name: "Battery Pipe CD 100", rate: 27.67 },
      { name: "Over Flow Pipe Carburetor CD 70", rate: 18.44 },
      { name: "Over Flow Pipe Carburetor CG 125", rate: 25.65 },
      { name: "Air Cleaner CG 125", rate: 37.21 },
      { name: "Oil Gauge O Ring CD 70", rate: 4.35 },
      { name: "Under Rubber Handle CD 100", rate: 7.53 },
      { name: "Rubber Handle Cushion CD 100", rate: 9.12 },
      { name: "Cushion Front Fuel Tank CG 125 DLX", rate: 14.63 },
      { name: "Rubber Muffler Mount 125 DLX", rate: 12.72 },
      { name: "Grommet Side Cover CG 125 DLX", rate: 7.53 },
      { name: "Grommet A Rear Cover CG 125 OLX", rate: 4.77 },
      { name: "Plug Rubber CD 70/CD 100", rate: 7.53 },
      { name: "Drum Rubber CD 70", rate: 117.02 },
      { name: "Bulb Holder CD 70", rate: 43.35 },
      { name: "Drum Rubber 150", rate: 304.75 },
      { name: "Seat Rubber A CD-70", rate: 9.12 },
      { name: "Seat Rubber B CD-70", rate: 12.83 },
      { name: "Seat Rubber C CD-70", rate: 9.75 },
      { name: "Tapit O-Ring CD-70", rate: 14.63 },
      { name: "Meter Harness CD 70", rate: 79.29 },
      { name: "Meter Harness CG 125", rate: 97.52 },
      { name: "Meter Harness CD-100", rate: 170.66 },
      { name: "C-12 Holder", rate: 11.24 },
      { name: "Read Vol Tube", rate: 75.58 },
    ];

    function addRow() {
      const tableBody = document.getElementById('billTableBody');
      const row = document.createElement('tr');

      row.innerHTML = `
        <td>${tableBody.children.length + 1}</td>
        <td>
          <select onchange="updateRate(this)">
            <option value="">Select Item</option>
            ${items.map(item => `<option value="${item.rate}">${item.name}</option>`).join('')}
          </select>
        </td>
        <td><input type="number" placeholder="Rate" onchange="calculateRow(this)"></td>
        <td><input type="number" placeholder="Quantity" onchange="calculateRow(this)"></td>
        <td class="total">0</td>
      `;

      tableBody.appendChild(row);
    }

    function updateRate(select) {
      const rateInput = select.parentElement.nextElementSibling.children[0];
      rateInput.value = select.value;
      calculateRow(rateInput);
    }

    function calculateRow(input) {
      const row = input.parentElement.parentElement;
      const rate = parseFloat(row.children[2].children[0].value) || 0;
      const quantity = parseFloat(row.children[3].children[0].value) || 0;
      const totalCell = row.children[4];

      totalCell.textContent = (rate * quantity).toFixed(2);
      calculateSubtotal();
    }

    function calculateSubtotal() {
      const totals = document.querySelectorAll('.total');
      let subtotal = 0;

      totals.forEach(cell => {
        subtotal += parseFloat(cell.textContent) || 0;
      });

      document.getElementById('subtotal').textContent = subtotal.toFixed(2);
      calculateTotal();
    }

    function calculateTotal() {
      const subtotal = parseFloat(document.getElementById('subtotal').textContent) || 0;
      const discount = parseFloat(document.getElementById('discount').value) || 0;
      const finalTotal = subtotal - (subtotal * discount / 100);

      document.getElementById('finalTotal').textContent = finalTotal.toFixed(2);
    }
  </script>
</body>
</html>
