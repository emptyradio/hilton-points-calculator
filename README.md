<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hilton Honors Points Calculator</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        
        .container {
            background-color: #ffffff;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            width: 100%;
            max-width: 700px;
            overflow: hidden;
        }

        .header {
            background-color: #002F5B; /* Hilton-like blue */
            color: white;
            padding: 20px 30px;
        }
        .header h1 {
            margin: 0;
            font-size: 24px;
        }
        .calculator-body {
            padding: 30px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        .form-group {
            display: flex;
            flex-direction: column;
        }
        .form-group label {
            font-weight: 600;
            margin-bottom: 6px;
            font-size: 14px;
            color: #333;
        }

        /* Base styles for inputs (EXCLUDING checkboxes/radios) and selects */
        .form-group input:not([type="checkbox"]):not([type="radio"]),
        .form-group select {
            padding: 10px 12px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
            font-family: inherit;
            background-color: #fff;
            width: 100%;
            box-sizing: border-box;
            -webkit-appearance: none;
            appearance: none;
        }

        /* Add a custom dropdown arrow to SELECT elements */
        .form-group select {
            background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23666666%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-13%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2013l128%20127.9c3.6%203.6%207.8%205.4%2013%205.4s9.4-1.8%2013-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-13%200-5-1.9-9.2-5.4-12.6z%22%2F%3E%3C%2Fsvg%3E');
            background-repeat: no-repeat;
            background-position: right 12px center;
            background-size: 10px;
            padding-right: 35px;
        }

        /* Remove spinners from number inputs */
        .form-group input[type="number"]::-webkit-inner-spin-button,
        .form-group input[type="number"]::-webkit-outer-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        .form-group input[type="number"] {
            -moz-appearance: textfield;
        }
        
        /* --- Styles for Radio/Checkbox groups --- */
        .option-group-item {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 5px;
        }
        .option-group-item input[type="radio"],
        .option-group-item input[type="checkbox"] {
            width: auto;
            margin: 0;
            flex-shrink: 0;
        }
        .option-group-item label {
            font-weight: 500;
            font-size: 15px;
            color: #333;
            margin-bottom: 0;
        }
        .option-group-item a {
            color: #002F5B;
            text-decoration: none;
            font-weight: 600;
        }
        .option-group-item a:hover {
            text-decoration: underline;
        }

        .full-width {
            grid-column: 1 / -1;
        }
        
        .clear-button {
            padding: 10px;
            font-size: 15px;
            font-weight: 600;
            color: #333;
            background-color: #f0f0f0;
            border: 1px solid #ccc;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.2s;
            width: 100%;
        }
        .clear-button:hover {
            background-color: #e0e0e0;
        }

        .results {
            background-color: #f9f9f4;
            padding: 30px;
            border-top: 1px solid #eee;
        }
        .results h2 {
            margin-top: 0;
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
        }
        .result-item {
            display: flex;
            justify-content: space-between;
            font-size: 16px;
            padding: 12px 0;
            border-bottom: 1px solid #eee;
        }
        .result-item strong {
            font-weight: 600;
            color: #000;
        }
        .result-item span {
            font-weight: 500;
            color: #d32f2f;
        }
        .result-explainer {
            font-size: 13px;
            color: #666;
            margin-top: 8px;
            text-align: right;
            border-bottom: none;
            padding: 0;
        }
        
        @media (max-width: 600px) {
            .calculator-body {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <div class="header">
            <h1>Hilton Honors Points Calculator</h1>
        </div>

        <div class="calculator-body">
            <div class="form-group">
                <label for="baseCost">Total Cost (excl. Tax) in USD</label>
                <input type="number" id="baseCost" >
            </div>
            <div class="form-group">
                <label for="totalCost">Total Cost (incl. Tax) in USD</label>
                <input type="number" id="totalCost">
            </div>

            <div class="form-group">
                <label for="status">Hilton Honors Status</label>
                <select id="status">
                    <option value="0" selected>Member (0% Bonus)</option>
                    <option value="20">Silver (20% Bonus)</option>
                    <option value="80">Gold (80% Bonus)</option>
                    <option value="100" >Diamond (100% Bonus)</option>
                </select>
            </div>
            <div class="form-group">
                <label for="creditCard">Credit Card</label>
                <select id="creditCard">
                    <option value="0" selected>None (0 pts/$)</option>
                    <option value="7">Hilton Honors (7 pts/$)</option>
                    <option value="12">Hilton Surpass (12 pts/$)</option>
                    <option value="14">Hilton Aspire (14 pts/$)</option>
                </select>
            </div>
            
            <div class="form-group full-width">
                <label for="pointValue">Your Point Value (e.g., 0.005)</label>
                <input type="number" id="pointValue" step="0.001" value="0.005">
            </div>

            <div class="form-group full-width" style="border-top: 1px solid #eee; padding-top: 20px;">
                <label>Hotel Brand</label>
                <div class="option-group-item">
                    <input type="radio" name="brand" id="brandStandard" value="10,1000" checked>
                    <label for="brandStandard">Standard brands (10 pts/$ + 1,000 diamond pts)</label>
                </div>
                <div class="option-group-item">
                    <input type="radio" name="brand" id="brandTru" value="5,0">
                    <label for="brandTru">Tru / Home2 (5 pts/$)</label>
                </div>
                <div class="option-group-item">
                    <input type="radio" name="brand" id="brandEmbassy" value="10,0">
                    <label for="brandEmbassy">AutoCamp / Embassy Suites / Garden Inn / Hampton / Homewood Suites / SLH / Spark (10 pts/$)</label>
                </div>
                <div class="option-group-item">
                    <input type="radio" name="brand" id="brandLivSmart" value="10,250">
                    <label for="brandLivSmart">LivSmart Studios (10 pts/$ + 250 diamond pts)</label>
                </div>
                <div class="option-group-item">
                    <input type="radio" name="brand" id="brandTempo" value="10,500">
                    <label for="brandTempo">Tempo (10 pts/$ + 500 diamond pts)</label>
                </div>
                <div class="option-group-item">
                    <input type="radio" name="brand" id="brandGrand" value="10,2000">
                    <label for="brandGrand">Grand Vacations (10 pts/$ + 2,000 diamond pts)</label>
                </div>
            </div>

            

            <div class="form-group full-width" style="margin-top: -10px;">
                <label>Current promotions</label>
                 <div class="option-group-item">
                    <input type="radio" name="currentPromo" id="promoNone" value="0">
                    <label for="promoNone">None</label>
                </div>
                <div class="option-group-item">
                    <input type="radio" name="currentPromo" id="promoQ4" value="1500" checked>
                    <label for="promoQ4">1,500 bonus points per stay between Oct 1 and Dec 23, 2025. Register <a href="#" target="https://www.hiltonhonors.com/en_US/2025-hh3-season-to-stay/landing/">here</a></label>
                </div>
            </div>
            <div class="form-group full-width" style="border-top: 1px solid #eee; padding-top: 20px;">
                <label for="promoPoints">Other Promotional Bonus Points</label>
                <input type="number" id="promoPoints" value="0">
            </div>

       

            <div class="form-group full-width" style="margin-top: 20px;">
                <button id="clearButton" class="clear-button">Clear All Inputs</button>
            </div>
        </div>
        
        <div class="results">
            <h2>Calculation Results</h2>
            <div class="result-item">
                <strong>Base Points:</strong>
                <span id="resBasePoints">0</span>
            </div>
            <div class="result-item">
                <strong>Status Bonus:</strong>
                <span id="resStatusBonus">0</span>
            </div>
            <div class="result-item">
                <strong>CC Bonus:</strong>
                <span id="resCcBonus">0</span>
            </div>
            <div class="result-item">
                <strong>Welcome Bonus:</strong>
                <span id="resWelcomeBonus">0</span>
            </div>
            <div class="result-item">
                <strong>Promotion Points:</strong>
                <span id="resPromoPoints">0</span>
            </div>
            <div class="result-item" style="border-bottom: 2px solid #ccc;">
                <strong>Total Points Earned:</strong>
                <span id="resTotalPoints" style="font-weight: 700; font-size: 18px;">0</span>
            </div>
            <div class="result-item">
                <strong>Total Cash Price (incl. tax):</strong>
                <span id="resTotalCash">$0.00</span>
            </div>
            <div class="result-item">
                <strong>Value of Points Earned (Rebate):</strong>
                <span id="resPointsValue">$0.00</span>
            </div>
            <div class="result-item" style="border-bottom: 2px solid #ccc;">
                <strong>Net Cost (After Rebate):</strong>
                <span id="resNetCost" style="font-weight: 700; font-size: 18px;">$0.00</span>
            </div>
            <div class="result-item" style="border-bottom: none;">
                <strong>Breakeven Points Price:</strong>
                <span id="resBreakeven">0 points</span>
            </div>
            
            <div class="result-explainer">
                If the points price is lower than the breakeven price, you choose to pay points, if higher, pay cash.
            </div>

        </div>
    </div>

    <script>
        function calculatePoints() {
            // 1. Get all input values.
            const baseCost = parseFloat(document.getElementById('baseCost').value) || 0;
            const totalCost = parseFloat(document.getElementById('totalCost').value) || 0;
            const statusBonusPct = parseFloat(document.getElementById('status').value) || 0;
            const ccRate = parseFloat(document.getElementById('creditCard').value) || 0;
            const pointValue = parseFloat(document.getElementById('pointValue').value) || 0.005;
            
            // 2. Get Brand Base Rate and Welcome Bonus
            const brandRadio = document.querySelector('input[name="brand"]:checked');
            const brandValue = brandRadio ? brandRadio.value.split(',') : [0, 0];
            const baseMultiplier = parseFloat(brandValue[0]) || 0;
            let welcomeBonusRaw = parseFloat(brandValue[1]) || 0;
            
            // Logic: Welcome bonus is only applied if Diamond (100%) is selected, per screenshot text
            let welcomeBonusPts = 0;
            if (statusBonusPct === 100 && welcomeBonusRaw > 0) {
                welcomeBonusPts = welcomeBonusRaw;
            }

            // 3. Get Promotions
            const otherPromoPoints = parseFloat(document.getElementById('promoPoints').value) || 0;
            const currentPromoPts = parseFloat(document.querySelector('input[name="currentPromo"]:checked').value) || 0;
            const totalPromoPoints = otherPromoPoints + currentPromoPts;

            // 4. Calculate Base and Status Points
            let basePoints = baseCost * baseMultiplier;
            let statusBonus = basePoints * (statusBonusPct / 100);

            // 5. Handle Special 2x Rate
            const isLuxury2x = document.getElementById('specialLuxury').checked;
            if (isLuxury2x) {
                basePoints *= 2;
                statusBonus *= 2;
            }
            
            // 6. Calculate CC Bonus (based on baseCost)
            const ccBonus = baseCost * ccRate;

            // 7. Calculate Totals
            const totalPoints = basePoints + statusBonus + ccBonus + welcomeBonusPts + totalPromoPoints;
            const pointsValueCash = totalPoints * pointValue;
            const netCost = totalCost - pointsValueCash;
            const breakevenPoints = (pointValue > 0) ? (netCost / pointValue) : 0;


            // 8. Display Results
            const formatNum = (num) => num.toLocaleString(undefined, { maximumFractionDigits: 0 });
            const formatCurrency = (num) => num.toLocaleString('en-US', { style: 'currency', currency: 'USD' });

            document.getElementById('resBasePoints').innerText = formatNum(basePoints);
            document.getElementById('resStatusBonus').innerText = formatNum(statusBonus);
            document.getElementById('resCcBonus').innerText = formatNum(ccBonus);
            document.getElementById('resWelcomeBonus').innerText = formatNum(welcomeBonusPts);
            document.getElementById('resPromoPoints').innerText = formatNum(totalPromoPoints);
            document.getElementById('resTotalPoints').innerText = formatNum(totalPoints);

            document.getElementById('resTotalCash').innerText = formatCurrency(totalCost);
            document.getElementById('resPointsValue').innerText = formatCurrency(pointsValueCash);
            document.getElementById('resNetCost').innerText = formatCurrency(netCost);
            document.getElementById('resBreakeven').innerText = `${formatNum(breakevenPoints)} points`;
        }

        function clearInputs() {
            // Reset number inputs
            document.getElementById('baseCost').value = "";
            document.getElementById('totalCost').value = "";
            document.getElementById('promoPoints').value = "";
            document.getElementById('pointValue').value = "0.005";

            // Reset dropdowns to defaults
            document.getElementById('status').selectedIndex = 3; // Diamond
            document.getElementById('creditCard').selectedIndex = 3; // Aspire

            // Reset radio buttons to defaults
            document.getElementById('brandStandard').checked = true;
            document.getElementById('promoQ4').checked = true;

            // Reset checkboxes
            document.getElementById('specialLuxury').checked = false;

            // After clearing, re-run the calculation
            calculatePoints();
        }

        // Add event listeners to all input/select fields to auto-calculate
        const inputs = [
            'baseCost', 'totalCost', 'status', 'creditCard', 'pointValue',
            'promoPoints', 'specialLuxury'
        ];
        inputs.forEach(id => {
            const el = document.getElementById(id);
            const event = (el.type === 'checkbox') ? 'change' : 'input';
            if (el.tagName === 'SELECT') {
                el.addEventListener('change', calculatePoints);
            } else {
                el.addEventListener(event, calculatePoints);
            }
        });

        // Add listeners for radio groups
        document.querySelectorAll('input[name="brand"]').forEach(radio => {
            radio.addEventListener('change', calculatePoints);
        });
        document.querySelectorAll('input[name="currentPromo"]').forEach(radio => {
            radio.addEventListener('change', calculatePoints);
        });
        
        document.getElementById('clearButton').addEventListener('click', clearInputs);
        
        // Run the calculation on page load with default values
        window.onload = calculatePoints;
    </script>

</body>
</html>
