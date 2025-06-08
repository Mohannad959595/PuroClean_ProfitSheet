<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PuroClean - Profit Sheet</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-red: #d2232a;
            --dark-red: #7d1519;
            --light-red: #f9d7d8;
            --accent-blue: #0077b6;
            --light-blue: #e6f2ff;
            --dark-gray: #333;
            --medium-gray: #666;
            --light-gray: #f5f5f7;
            --border-radius: 8px;
            --box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            --transition: all 0.3s ease;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--light-gray);
            color: var(--dark-gray);
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            overflow: hidden;
        }
        
        /* Header Styles */
        .header {
            background: linear-gradient(135deg, var(--primary-red) 0%, var(--dark-red) 100%);
            color: white;
            padding: 25px 30px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
        }
        
        .header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 8px;
            position: relative;
            letter-spacing: 0.5px;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }
        
        .header .subtitle {
            font-size: 1.25rem;
            font-weight: 400;
            opacity: 0.9;
            position: relative;
            margin-top: 5px;
        }
        
        .header .logo {
            position: absolute;
            top: 20px;
            left: 30px;
            font-size: 2.5rem;
            opacity: 0.8;
        }
        
        /* Info Section */
        .info-section {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            padding: 25px;
            background: var(--light-gray);
            border-bottom: 1px solid #e0e0e0;
        }
        
        .info-item {
            position: relative;
        }
        
        .info-item label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            color: var(--medium-gray);
            font-size: 0.9rem;
        }
        
        .info-item input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: var(--border-radius);
            font-size: 1rem;
            transition: var(--transition);
            background: white;
        }
        
        .info-item input:focus {
            border-color: var(--primary-red);
            outline: none;
            box-shadow: 0 0 0 3px rgba(210, 35, 42, 0.1);
        }
        
        /* Section Styling */
        .section {
            margin: 25px;
            border: 1px solid #eaeaea;
            border-radius: var(--border-radius);
            overflow: hidden;
            background: white;
            box-shadow: 0 2px 6px rgba(0,0,0,0.04);
        }
        
        .section-title {
            background: linear-gradient(to right, var(--primary-red), var(--dark-red));
            color: white;
            padding: 15px 20px;
            font-size: 1.25rem;
            font-weight: 600;
            display: flex;
            align-items: center;
        }
        
        .section-title i {
            margin-right: 10px;
            font-size: 1.1rem;
        }
        
        /* Table Styling */
        .table-container {
            padding: 20px;
            overflow-x: auto;
        }
        
        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            min-width: 1000px;
        }
        
        th {
            background-color: var(--light-blue);
            color: var(--accent-blue);
            font-weight: 600;
            text-align: center;
            padding: 14px 10px;
            border-bottom: 2px solid #d0e0f0;
        }
        
        td {
            padding: 12px 10px;
            border-bottom: 1px solid #eee;
            text-align: center;
        }
        
        tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        
        tr:hover {
            background-color: #f0f8ff;
        }
        
        .column-header {
            background-color: #e0ecf9;
            font-weight: 600;
            color: #0056b3;
            font-size: 0.95rem;
        }
        
        input {
            width: 100%;
            padding: 8px 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            text-align: center;
            transition: var(--transition);
            font-size: 0.95rem;
        }
        
        input:focus {
            border-color: var(--primary-red);
            outline: none;
            box-shadow: 0 0 0 2px rgba(210, 35, 42, 0.1);
        }
        
        .date-input {
            width: 120px;
        }
        
        .amount-input {
            width: 100px;
            text-align: center;
            font-weight: 500;
        }
        
        /* Buttons */
        .btn-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px 20px;
        }
        
        .btn-group {
            display: flex;
            gap: 12px;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: var(--border-radius);
            font-size: 0.95rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .btn-calculate {
            background: linear-gradient(to right, #28a745, #218838);
            color: white;
        }
        
        .btn-export {
            background: linear-gradient(to right, #007bff, #0069d9);
            color: white;
        }
        
        .add-row-btn {
            background: linear-gradient(to right, #ff9800, #e68a00);
            color: white;
            padding: 10px 20px;
            margin: 0 20px 20px;
            border: none;
            border-radius: var(--border-radius);
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .add-row-btn:hover {
            background: linear-gradient(to right, #e68a00, #cc7a00);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .delete-btn {
            background-color: #e74c3c;
            color: white;
            border: none;
            border-radius: 4px;
            padding: 5px 10px;
            cursor: pointer;
            transition: var(--transition);
        }
        
        .delete-btn:hover {
            background-color: #c0392b;
        }
        
        /* Summary Table */
        .summary-table {
            width: 100%;
            margin: 20px 0;
            border-collapse: collapse;
            background: white;
            border-radius: var(--border-radius);
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        }
        
        .summary-table td {
            padding: 12px 20px;
            border: none;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        
        .summary-table tr:last-child td {
            border-bottom: none;
        }
        
        .summary-table tr:nth-child(odd) {
            background-color: #fafafa;
        }
        
        .summary-value {
            text-align: right;
            font-weight: 600;
            color: var(--dark-gray);
            font-family: 'Courier New', monospace;
        }
        
        .highlight-row {
            background-color: var(--light-blue) !important;
            font-weight: 600;
        }
        
        .profit-positive {
            color: #28a745;
        }
        
        .profit-negative {
            color: #e74c3c;
        }
        
        /* Footer */
        .footer {
            text-align: center;
            padding: 20px;
            color: var(--medium-gray);
            font-size: 0.9rem;
            border-top: 1px solid #eee;
            background: var(--light-gray);
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .header .subtitle {
                font-size: 1.1rem;
            }
            
            .btn-container {
                flex-direction: column;
                gap: 15px;
            }
            
            .btn-group {
                width: 100%;
                justify-content: center;
            }
            
            .section {
                margin: 15px;
            }
        }
        
        @media (max-width: 480px) {
            .info-section {
                grid-template-columns: 1fr;
            }
            
            .header {
                padding: 20px 15px;
            }
            
            .header h1 {
                font-size: 1.7rem;
            }
            
            .btn {
                padding: 10px 15px;
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo">
                <i class="fas fa-broom"></i>
            </div>
            <h1>PuroClean</h1>
            <div class="subtitle">Profit Sheet</div>
        </div>
        
        <div class="info-section">
            <div class="info-item">
                <label for="claim-number"><i class="fas fa-file-invoice"></i> Claim Number</label>
                <input type="text" id="claim-number" placeholder="Enter claim number">
            </div>
            <div class="info-item">
                <label for="address"><i class="fas fa-map-marker-alt"></i> Address</label>
                <input type="text" id="address" value="161 Ascot Street 374">
            </div>
            <div class="info-item">
                <label for="insured-name"><i class="fas fa-user"></i> Insured Name</label>
                <input type="text" id="insured-name" placeholder="Enter insured name">
            </div>
            <div class="info-item">
                <label for="insurance-company"><i class="fas fa-building"></i> Insurance Company</label>
                <input type="text" id="insurance-company" placeholder="Enter insurance company">
            </div>
        </div>
        
        <div class="section">
            <div class="section-title">
                <i class="fas fa-fire-extinguisher"></i> Emergency: Work Costs
            </div>
            <div class="table-container">
                <table id="emergency-costs">
                    <thead>
                        <tr class="column-header">
                            <td colspan="3">Basic Expenses</td>
                            <td colspan="1"></td>
                            <td colspan="4">Reimbursed Amounts</td>
                        </tr>
                        <tr>
                            <th>Vendor</th>
                            <th>Invoice</th>
                            <th>Issue Date</th>
                            <th>Amount ($)</th>
                            <th>PuroClean Invoice</th>
                            <th>Issue Date</th>
                            <th>Amount ($)</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><input type="text" class="vendor" placeholder="Vendor name"></td>
                            <td><input type="text" class="invoice" placeholder="Invoice #"></td>
                            <td><input type="date" class="date-input issue-date"></td>
                            <td><input type="number" step="0.01" class="amount-input amount" placeholder="0.00"></td>
                            <td><input type="text" class="puro-inv" placeholder="Invoice #"></td>
                            <td><input type="date" class="date-input puro-issue-date"></td>
                            <td><input type="number" step="0.01" class="amount-input puro-amount" placeholder="0.00"></td>
                            <td><button class="delete-btn" onclick="deleteRow(this)"><i class="fas fa-trash"></i></button></td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <button class="add-row-btn" onclick="addEmergencyRow()">
                <i class="fas fa-plus-circle"></i> Add Emergency Row
            </button>
            
            <table class="summary-table">
                <tr>
                    <td>Total Work Expenses:</td>
                    <td class="summary-value" id="emergency-total-expenses">0.00</td>
                </tr>
                <tr>
                    <td>Royalty 12%:</td>
                    <td class="summary-value" id="emergency-royalties-incl">0.00</td>
                </tr>
                <tr class="highlight-row">
                    <td>Total Expenses (Job Costs + Royalty):</td>
                    <td class="summary-value" id="emergency-total-all">0.00</td>
                </tr>
                <tr>
                    <td colspan="2"><div style="height: 15px;"></div></td>
                </tr>
                <tr>
                    <td>Emergency Revenue:</td>
                    <td class="summary-value" id="emergency-revenue">0.00</td>
                </tr>
                <tr>
                    <td>Revenue (excl tax):</td>
                    <td class="summary-value" id="emergency-revenue-excl">0.00</td>
                </tr>
                <tr>
                    <td colspan="2"><div style="height: 15px;"></div></td>
                </tr>
                <tr>
                    <td>Profit (Revenue excl tax - Total Expenses incl tax):</td>
                    <td class="summary-value" id="emergency-profit">0.00</td>
                </tr>
                <tr>
                    <td>Profit Percentage of Revenue (Profit/Revenue incl tax):</td>
                    <td class="summary-value" id="emergency-profit-percent">0.00%</td>
                </tr>
            </table>
        </div>
        
        <div class="section">
            <div class="section-title">
                <i class="fas fa-hammer"></i> Rebuild: Work Costs
            </div>
            <div class="table-container">
                <table id="rebuild-costs">
                    <thead>
                        <tr class="column-header">
                            <td colspan="3">Basic Expenses</td>
                            <td colspan="1"></td>
                            <td colspan="4">Reimbursed Amounts</td>
                        </tr>
                        <tr>
                            <th>Vendor</th>
                            <th>Invoice</th>
                            <th>Issue Date</th>
                            <th>Amount ($)</th>
                            <th>PuroClean Invoice</th>
                            <th>Issue Date</th>
                            <th>Amount ($)</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><input type="text" class="vendor" placeholder="Vendor name"></td>
                            <td><input type="text" class="invoice" placeholder="Invoice #"></td>
                            <td><input type="date" class="date-input issue-date"></td>
                            <td><input type="number" step="0.01" class="amount-input amount" placeholder="0.00"></td>
                            <td><input type="text" class="puro-inv" placeholder="Invoice #"></td>
                            <td><input type="date" class="date-input puro-issue-date"></td>
                            <td><input type="number" step="0.01" class="amount-input puro-amount" placeholder="0.00"></td>
                            <td><button class="delete-btn" onclick="deleteRow(this)"><i class="fas fa-trash"></i></button></td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <button class="add-row-btn" onclick="addRebuildRow()">
                <i class="fas fa-plus-circle"></i> Add Rebuild Row
            </button>
            
            <table class="summary-table">
                <tr>
                    <td>Total Work Expenses:</td>
                    <td class="summary-value" id="rebuild-total-expenses">0.00</td>
                </tr>
                <tr>
                    <td>Royalty 5%:</td>
                    <td class="summary-value" id="rebuild-royalties-incl">0.00</td>
                </tr>
                <tr class="highlight-row">
                    <td>Total Expenses (Job Costs + Royalty):</td>
                    <td class="summary-value" id="rebuild-total-all">0.00</td>
                </tr>
                <tr>
                    <td colspan="2"><div style="height: 15px;"></div></td>
                </tr>
                <tr>
                    <td>Rebuild Revenue:</td>
                    <td class="summary-value" id="rebuild-revenue">0.00</td>
                </tr>
                <tr>
                    <td>Revenue (excl tax):</td>
                    <td class="summary-value" id="rebuild-revenue-excl">0.00</td>
                </tr>
                <tr>
                    <td colspan="2"><div style="height: 15px;"></div></td>
                </tr>
                <tr>
                    <td>Profit (Revenue excl tax - Total Expenses incl tax):</td>
                    <td class="summary-value" id="rebuild-profit">0.00</td>
                </tr>
                <tr>
                    <td>Profit Percentage of Revenue (Profit/Revenue incl tax):</td>
                    <td class="summary-value" id="rebuild-profit-percent">0.00%</td>
                </tr>
            </table>
        </div>
        
        <div class="btn-container">
            <div class="btn-group">
                <button class="btn btn-calculate" onclick="calculateAll()">
                    <i class="fas fa-calculator"></i> Calculate All
                </button>
                <button class="btn btn-export" onclick="exportToPDF()">
                    <i class="fas fa-file-pdf"></i> Export to PDF
                </button>
            </div>
            <div>
                <button class="btn" style="background: linear-gradient(to right, #6c757d, #5a6268); color: white;" onclick="resetForm()">
                    <i class="fas fa-sync-alt"></i> Reset Form
                </button>
            </div>
        </div>
        
        <div class="footer">
            <p>PuroClean Profit Sheet &copy; 2025 | Designed for Financial Analysis</p>
        </div>
    </div>

    <script>
        const { jsPDF } = window.jspdf;
        
        // Add rows to tables with delete functionality
        function addEmergencyRow() {
            const tbody = document.querySelector('#emergency-costs tbody');
            const newRow = document.createElement('tr');
            newRow.innerHTML = `
                <td><input type="text" class="vendor" placeholder="Vendor name"></td>
                <td><input type="text" class="invoice" placeholder="Invoice #"></td>
                <td><input type="date" class="date-input issue-date"></td>
                <td><input type="number" step="0.01" class="amount-input amount" placeholder="0.00"></td>
                <td><input type="text" class="puro-inv" placeholder="Invoice #"></td>
                <td><input type="date" class="date-input puro-issue-date"></td>
                <td><input type="number" step="0.01" class="amount-input puro-amount" placeholder="0.00"></td>
                <td><button class="delete-btn" onclick="deleteRow(this)"><i class="fas fa-trash"></i></button></td>
            `;
            tbody.appendChild(newRow);
        }
        
        function addRebuildRow() {
            const tbody = document.querySelector('#rebuild-costs tbody');
            const newRow = document.createElement('tr');
            newRow.innerHTML = `
                <td><input type="text" class="vendor" placeholder="Vendor name"></td>
                <td><input type="text" class="invoice" placeholder="Invoice #"></td>
                <td><input type="date" class="date-input issue-date"></td>
                <td><input type="number" step="0.01" class="amount-input amount" placeholder="0.00"></td>
                <td><input type="text" class="puro-inv" placeholder="Invoice #"></td>
                <td><input type="date" class="date-input puro-issue-date"></td>
                <td><input type="number" step="0.01" class="amount-input puro-amount" placeholder="0.00"></td>
                <td><button class="delete-btn" onclick="deleteRow(this)"><i class="fas fa-trash"></i></button></td>
            `;
            tbody.appendChild(newRow);
        }
        
        // Delete row
        function deleteRow(button) {
            const row = button.closest('tr');
            row.remove();
            calculateAll();
        }
        
        // Reset form
        function resetForm() {
            if (confirm('Are you sure you want to reset the entire form? All data will be lost.')) {
                document.getElementById('claim-number').value = '';
                document.getElementById('insured-name').value = '';
                document.getElementById('insurance-company').value = '';
                
                // Reset emergency table
                const emergencyTbody = document.querySelector('#emergency-costs tbody');
                emergencyTbody.innerHTML = '';
                addEmergencyRow();
                
                // Reset rebuild table
                const rebuildTbody = document.querySelector('#rebuild-costs tbody');
                rebuildTbody.innerHTML = '';
                addRebuildRow();
                
                calculateAll();
            }
        }
        
        // Calculate all values
        function calculateAll() {
            calculateEmergency();
            calculateRebuild();
        }
        
        function calculateEmergency() {
            // Calculate expenses
            const amountInputs = document.querySelectorAll('#emergency-costs .amount');
            let totalAmount = 0;
            amountInputs.forEach(input => {
                totalAmount += parseFloat(input.value) || 0;
            });
            document.getElementById('emergency-total-expenses').textContent = totalAmount.toFixed(2);
            
            // Calculate PuroClean amounts
            const puroAmountInputs = document.querySelectorAll('#emergency-costs .puro-amount');
            let totalPuroAmount = 0;
            puroAmountInputs.forEach(input => {
                totalPuroAmount += parseFloat(input.value) || 0;
            });
            document.getElementById('emergency-revenue').textContent = totalPuroAmount.toFixed(2);
            
            // Calculate reimbursed amounts (without tax)
            const reimbursedAmount = totalPuroAmount / 1.13;
            document.getElementById('emergency-revenue-excl').textContent = reimbursedAmount.toFixed(2);
            
            // Calculate royalties
            const royaltiesExcl = reimbursedAmount * 0.12;
            const royaltiesIncl = royaltiesExcl * 1.13;
            document.getElementById('emergency-royalties-incl').textContent = royaltiesIncl.toFixed(2);
            
            // Calculate totals (Job Costs + Royalty including tax)
            const totalExpensesInclTax = totalAmount + royaltiesIncl;
            document.getElementById('emergency-total-all').textContent = totalExpensesInclTax.toFixed(2);
            
            // Calculate profit
            const profit = reimbursedAmount - totalExpensesInclTax;
            const profitElement = document.getElementById('emergency-profit');
            profitElement.textContent = profit.toFixed(2);
            profitElement.className = profit >= 0 ? 'summary-value profit-positive' : 'summary-value profit-negative';
            
            // Calculate profit percentage
            const profitPercent = (profit / totalPuroAmount) * 100 || 0;
            const percentElement = document.getElementById('emergency-profit-percent');
            percentElement.textContent = profitPercent.toFixed(2) + '%';
            percentElement.className = profitPercent >= 0 ? 'summary-value profit-positive' : 'summary-value profit-negative';
        }
        
        function calculateRebuild() {
            // Calculate expenses
            const amountInputs = document.querySelectorAll('#rebuild-costs .amount');
            let totalAmount = 0;
            amountInputs.forEach(input => {
                totalAmount += parseFloat(input.value) || 0;
            });
            document.getElementById('rebuild-total-expenses').textContent = totalAmount.toFixed(2);
            
            // Calculate PuroClean amounts
            const puroAmountInputs = document.querySelectorAll('#rebuild-costs .puro-amount');
            let totalPuroAmount = 0;
            puroAmountInputs.forEach(input => {
                totalPuroAmount += parseFloat(input.value) || 0;
            });
            document.getElementById('rebuild-revenue').textContent = totalPuroAmount.toFixed(2);
            
            // Calculate reimbursed amounts (without tax)
            const reimbursedAmount = totalPuroAmount / 1.13;
            document.getElementById('rebuild-revenue-excl').textContent = reimbursedAmount.toFixed(2);
            
            // Calculate royalties
            const royaltiesExcl = reimbursedAmount * 0.05;
            const royaltiesIncl = royaltiesExcl * 1.13;
            document.getElementById('rebuild-royalties-incl').textContent = royaltiesIncl.toFixed(2);
            
            // Calculate totals (Job Costs + Royalty including tax)
            const totalExpensesInclTax = totalAmount + royaltiesIncl;
            document.getElementById('rebuild-total-all').textContent = totalExpensesInclTax.toFixed(2);
            
            // Calculate profit
            const profit = reimbursedAmount - totalExpensesInclTax;
            const profitElement = document.getElementById('rebuild-profit');
            profitElement.textContent = profit.toFixed(2);
            profitElement.className = profit >= 0 ? 'summary-value profit-positive' : 'summary-value profit-negative';
            
            // Calculate profit percentage
            const profitPercent = (profit / totalPuroAmount) * 100 || 0;
            const percentElement = document.getElementById('rebuild-profit-percent');
            percentElement.textContent = profitPercent.toFixed(2) + '%';
            percentElement.className = profitPercent >= 0 ? 'summary-value profit-positive' : 'summary-value profit-negative';
        }
        
        // Export to PDF
        function exportToPDF() {
            calculateAll();
            
            const doc = new jsPDF({
                orientation: 'portrait',
                unit: 'mm',
                format: 'a4'
            });
            
            // Add header with logo and title
            doc.setFillColor(210, 35, 42); // PuroClean red
            doc.rect(0, 0, doc.internal.pageSize.width, 25, 'F');
            doc.setTextColor(255, 255, 255);
            doc.setFontSize(18);
            doc.setFont('helvetica', 'bold');
            doc.text('PuroClean', 105, 12, { align: 'center' });
            doc.setFontSize(14);
            doc.setFont('helvetica', 'normal');
            doc.text('Profit Sheet', 105, 18, { align: 'center' });
            
            // Reset text color
            doc.setTextColor(0, 0, 0);
            
            // Add claim information
            doc.setFontSize(11);
            doc.text(`Date: ${new Date().toLocaleDateString()}`, 15, 35);
            doc.text(`Claim Number: ${document.getElementById('claim-number').value}`, 15, 40);
            doc.text(`Address: ${document.getElementById('address').value}`, 15, 45);
            doc.text(`Insured Name: ${document.getElementById('insured-name').value}`, 15, 50);
            doc.text(`Insurance Company: ${document.getElementById('insurance-company').value}`, 15, 55);
            
            // Emergency section
            doc.setFontSize(14);
            doc.setFont('helvetica', 'bold');
            doc.text('Emergency: Work Costs', 15, 65);
            doc.setFont('helvetica', 'normal');
            
            // Emergency table data
            const emergencyTable = document.getElementById('emergency-costs');
            const emergencyData = [];
            const emergencyRows = emergencyTable.querySelectorAll('tbody tr');
            
            emergencyRows.forEach(row => {
                const rowData = [
                    row.querySelector('.vendor').value,
                    row.querySelector('.invoice').value,
                    row.querySelector('.issue-date').value,
                    row.querySelector('.amount').value || '0.00',
                    row.querySelector('.puro-inv').value,
                    row.querySelector('.puro-issue-date').value,
                    row.querySelector('.puro-amount').value || '0.00'
                ];
                emergencyData.push(rowData);
            });
            
            // Add emergency table to PDF
            doc.autoTable({
                startY: 70,
                head: [['Vendor', 'Invoice', 'Issue Date', 'Amount', 'PuroClean Invoice', 'Issue Date', 'Amount']],
                body: emergencyData,
                margin: { left: 15 },
                styles: { 
                    fontSize: 9, 
                    cellPadding: 3,
                    valign: 'middle'
                },
                headStyles: { 
                    fillColor: [0, 119, 182], // blue
                    textColor: [255, 255, 255],
                    fontStyle: 'bold'
                },
                alternateRowStyles: {
                    fillColor: [240, 248, 255] // light blue
                }
            });
            
            // Emergency summary
            const emergencySummaryData = [
                ['Total Work Expenses:', document.getElementById('emergency-total-expenses').textContent],
                ['Royalty 12%:', document.getElementById('emergency-royalties-incl').textContent],
                ['Total Expenses (Job Costs + Royalty):', document.getElementById('emergency-total-all').textContent],
                ['Emergency Revenue:', document.getElementById('emergency-revenue').textContent],
                ['Revenue (excl tax):', document.getElementById('emergency-revenue-excl').textContent],
                ['Profit:', document.getElementById('emergency-profit').textContent],
                ['Profit Percentage:', document.getElementById('emergency-profit-percent').textContent]
            ];
            
            doc.autoTable({
                startY: doc.lastAutoTable.finalY + 10,
                body: emergencySummaryData,
                margin: { left: 15 },
                columnStyles: {
                    0: { cellWidth: 120, fontStyle: 'bold' },
                    1: { cellWidth: 40, halign: 'right' }
                },
                styles: { 
                    fontSize: 10, 
                    cellPadding: 4
                },
                tableWidth: 'wrap',
                head: [['Emergency Summary', 'Value']],
                headStyles: {
                    fillColor: [210, 35, 42], // red
                    textColor: [255, 255, 255],
                    fontStyle: 'bold'
                }
            });
            
            // Rebuild section (new page)
            doc.addPage();
            doc.setFontSize(14);
            doc.setFont('helvetica', 'bold');
            doc.text('Rebuild: Work Costs', 15, 20);
            doc.setFont('helvetica', 'normal');
            
            // Rebuild table data
            const rebuildTable = document.getElementById('rebuild-costs');
            const rebuildData = [];
            const rebuildRows = rebuildTable.querySelectorAll('tbody tr');
            
            rebuildRows.forEach(row => {
                const rowData = [
                    row.querySelector('.vendor').value,
                    row.querySelector('.invoice').value,
                    row.querySelector('.issue-date').value,
                    row.querySelector('.amount').value || '0.00',
                    row.querySelector('.puro-inv').value,
                    row.querySelector('.puro-issue-date').value,
                    row.querySelector('.puro-amount').value || '0.00'
                ];
                rebuildData.push(rowData);
            });
            
            // Add rebuild table to PDF
            doc.autoTable({
                startY: 25,
                head: [['Vendor', 'Invoice', 'Issue Date', 'Amount', 'PuroClean Invoice', 'Issue Date', 'Amount']],
                body: rebuildData,
                margin: { left: 15 },
                styles: { 
                    fontSize: 9, 
                    cellPadding: 3,
                    valign: 'middle'
                },
                headStyles: { 
                    fillColor: [0, 119, 182], // blue
                    textColor: [255, 255, 255],
                    fontStyle: 'bold'
                },
                alternateRowStyles: {
                    fillColor: [240, 248, 255] // light blue
                }
            });
            
            // Rebuild summary
            const rebuildSummaryData = [
                ['Total Work Expenses:', document.getElementById('rebuild-total-expenses').textContent],
                ['Royalty 5%:', document.getElementById('rebuild-royalties-incl').textContent],
                ['Total Expenses (Job Costs + Royalty):', document.getElementById('rebuild-total-all').textContent],
                ['Rebuild Revenue:', document.getElementById('rebuild-revenue').textContent],
                ['Revenue (excl tax):', document.getElementById('rebuild-revenue-excl').textContent],
                ['Profit:', document.getElementById('rebuild-profit').textContent],
                ['Profit Percentage:', document.getElementById('rebuild-profit-percent').textContent]
            ];
            
            doc.autoTable({
                startY: doc.lastAutoTable.finalY + 10,
                body: rebuildSummaryData,
                margin: { left: 15 },
                columnStyles: {
                    0: { cellWidth: 120, fontStyle: 'bold' },
                    1: { cellWidth: 40, halign: 'right' }
                },
                styles: { 
                    fontSize: 10, 
                    cellPadding: 4
                },
                tableWidth: 'wrap',
                head: [['Rebuild Summary', 'Value']],
                headStyles: {
                    fillColor: [210, 35, 42], // red
                    textColor: [255, 255, 255],
                    fontStyle: 'bold'
                }
            });
            
            // Footer
            const pageCount = doc.internal.getNumberOfPages();
            for(let i = 1; i <= pageCount; i++) {
                doc.setPage(i);
                doc.setFontSize(10);
                doc.setTextColor(100);
                doc.text(`Page ${i} of ${pageCount}`, doc.internal.pageSize.width - 20, doc.internal.pageSize.height - 10, {align: 'right'});
                doc.text('PuroClean Profit Sheet', 20, doc.internal.pageSize.height - 10);
            }
            
            // Save PDF file
            doc.save('PuroClean_Profit_Sheet.pdf');
        }
        
        // Initialize some default data
        window.onload = function() {
            // Add a few rows to each section
            addEmergencyRow();
            addEmergencyRow();
            addRebuildRow();
            addRebuildRow();
            
            // Set today's date in date fields
            const today = new Date().toISOString().split('T')[0];
            document.querySelectorAll('input[type="date"]').forEach(input => {
                input.value = today;
            });
            
            // Add sample data
            document.getElementById('claim-number').value = 'CL-2025-00123';
            document.getElementById('insured-name').value = 'John D. Smith';
            document.getElementById('insurance-company').value = 'StateFarm Insurance';
            
            // Calculate initial values
            calculateAll();
        };
    </script>
</body>
</html>
