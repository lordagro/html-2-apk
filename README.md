<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lotd Agro Limited - Order Form</title>
    <script>
        function calculateTotal() {
            let total = 0;
            let rows = document.querySelectorAll(".order-row");
            rows.forEach(row => {
                let qty = parseFloat(row.querySelector(".qty").value) || 0;
                let tp = parseFloat(row.querySelector(".tp").textContent) || 0;
                let amount = qty * tp;
                row.querySelector(".amount").textContent = amount.toFixed(2);
                total += amount;
            });
            document.getElementById("totalAmount").textContent = total.toFixed(2);
            document.getElementById("amountInWords").textContent = numberToWords(total);
        }

        function numberToWords(num) {
            const a = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"];
            const b = ["", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"];

            if (num < 20) return a[num];
            if (num < 100) return b[Math.floor(num / 10)] + " " + a[num % 10];
            if (num < 1000) return a[Math.floor(num / 100)] + " Hundred " + numberToWords(num % 100);
            return num;
        }

        function downloadForm() {
            window.print();
        }

        function saveAsHTML() {
            let content = document.documentElement.outerHTML;
            let blob = new Blob([content], { type: "text/html" });
            let a = document.createElement("a");
            a.href = URL.createObjectURL(blob);
            a.download = "order-form.html";
            a.click();
        }
    </script>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        table { width: 100%; border-collapse: collapse; }
        th, td { border: 1px solid black; padding: 8px; text-align: left; }
        .form-container { display: flex; justify-content: space-between; }

        @media print {
            button {
                display: none;
            }
        }
    </style>
</head>
<body>
    <h2>Lord Agro Limited</h2>
    <h3>Order Form</h3>
    <div class="form-container">
        <div>
            <label>Customer Name: <input type="text"></label><br>
            <label>Customer ID: <input type="text"></label><br>
            <label>Mobile Number: <input type="text"></label><br>
            <label>Address: <input type="text"></label><br>
        </div>
        <div>
            <label>Officer Name: <input type="text"></label><br>
            <label>Territory: <input type="text"></label><br>
            <label>Mobile No: <input type="text"></label><br>
            <label>Date: <input type="date"></label><br>
            <label>Cash/Credit: <select><option>Cash</option><option>Credit</option></select></label>
        </div>
    </div>
    <br>
    <table>
        <tr>
            <th>Sl</th>
            <th>Item Details</th>
            <th>Pack Size</th>
            <th>TP (Tk)</th>
            <th>Qty</th>
            <th>Amount</th>
            <th>Free</th>
        </tr>
        <script>
            let items = [
                ["OXY-FORTE", "1kg", 510],
                ["ANTI-BACK", "500ml", 1065],
                ["ANTI-BACK", "100ml", 245],
                ["AMM-REMOVER", "500ml", 1120],
                ["AMM-REMOVER", "100ml", 255],
                ["MICRO-BIOTIC", "100gm", 680],
                ["POND-GURD", "100gm", 590],
                ["TOXIN PRO", "500ml", 1490],
                ["TOXIN PRO", "100ml", 340],
                ["ACUA-VIT C", "500gm", 565],
                ["ENERGY PLUS", "1kg", 145],
                ["HEPATIC BOOSTER", "500ml", 440],
                ["SUPER ZYME", "500gm", 520],
                ["VITA MIX", "500ml", 640],
                ["BACTO-KILLER", "500gm", 1380],
                ["AMMO-NILL", "500gm", 1465],
                ["VITA CARE", "1kg", 1240],
                ["NUTRI-GROW", "56kg", 1240],
                ["TOXIN", "500ml", 1180],
                ["TOXIN", "100ml", 280]
            ];
            document.write(items.map((item, index) => `
                <tr class="order-row">
                    <td>${index + 1}</td>
                    <td>${item[0]}</td>
                    <td>${item[1]}</td>
                    <td class="tp">${item[2]}</td>
                    <td><input type="number" class="qty" oninput="calculateTotal()" min="0"></td>
                    <td class="amount">0.00</td>
                    <td>
                        <select class="free-option">
                            ${Array.from({ length: 11 }, (_, i) => `<option value="${i}">${i}</option>`).join("")}
                        </select>
                    </td>
                </tr>`).join(""));
        </script>
    </table>
    <br>
    <strong>Total Amount: Tk <span id="totalAmount">0.00</span></strong><br>
    <strong>Amount in Words: <span id="amountInWords"></span></strong><br><br>
    <button onclick="downloadForm()">Download as PDF</button>
    <button onclick="saveAsHTML()">Save as HTML</button>
</body>
</html>
