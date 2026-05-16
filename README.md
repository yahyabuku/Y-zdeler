<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Özel Yüzde Hesaplayıcı</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; display: flex; justify-content: center; padding: 20px; background: #eef2f7; margin: 0; }
        .card { background: white; padding: 25px; border-radius: 16px; box-shadow: 0 4px 20px rgba(0,0,0,0.08); width: 100%; max-width: 400px; }
        h2 { text-align: center; color: #2c3e50; margin-bottom: 20px; font-size: 1.2rem; }
        .input-group { margin-bottom: 15px; position: relative; }
        label { display: block; font-size: 0.9rem; color: #666; margin-bottom: 8px; }
        input { width: 100%; padding: 15px; border: 2px solid #dfe6e9; border-radius: 12px; box-sizing: border-box; font-size: 20px; outline: none; transition: all 0.3s; }
        input:focus { border-color: #3498db; box-shadow: 0 0 8px rgba(52, 152, 219, 0.2); }
        
        .clear-btn { 
            width: 100%; margin-top: 10px; padding: 12px; border: none; border-radius: 10px; 
            background: #ff7675; color: white; font-weight: bold; cursor: pointer; 
            font-size: 16px; transition: background 0.3s;
        }
        .clear-btn:active { background: #d63031; transform: scale(0.98); }

        .results-bar { margin-top: 20px; background: #f8f9fa; border-radius: 12px; padding: 15px; display: none; border-left: 5px solid #3498db; animation: slideDown 0.3s ease-out; }
        .res-item { display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid #eee; }
        .res-item:last-child { border-bottom: none; }
        .res-label { font-weight: 600; color: #555; }
        .res-value { color: #2ecc71; font-weight: bold; font-family: monospace; font-size: 1.2rem; }

        @keyframes slideDown { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>
    <div class="card">
        <h2>Yüzde Hesaplayıcı</h2>
        <div class="input-group">
            <label>Hesaplanacak Sayı</label>
            <input type="number" id="sayi" placeholder="Sayıyı girin..." oninput="ozelHesapla()" inputmode="decimal">
            <button class="clear-btn" onclick="temizle()">Temizle</button>
        </div>
        
        <div id="resultsBar" class="results-bar">
            <div class="res-item"><span class="res-label">%85:</span> <span class="res-value" id="r85">0</span></div>
            <div class="res-item"><span class="res-label">%70:</span> <span class="res-value" id="r70">0</span></div>
            <div class="res-item"><span class="res-label">%55:</span> <span class="res-value" id="r55">0</span></div>
            <div class="res-item"><span class="res-label">%40:</span> <span class="res-value" id="r40">0</span></div>
            <div class="res-item"><span class="res-label">%30:</span> <span class="res-value" id="r30">0</span></div>
        </div>
    </div>

    <script>
        function ozelYuvarla(num) {
            // 1.004 -> 1.00 | 1.005 -> 1.01 kuralı
            return (Math.round((num + Number.EPSILON) * 100) / 100).toFixed(2);
        }

        function ozelHesapla() {
            const s = parseFloat(document.getElementById('sayi').value);
            const bar = document.getElementById('resultsBar');
            
            if (!isNaN(s)) {
                bar.style.display = 'block';
                [85, 70, 55, 40, 30].forEach(y => {
                    let sonuc = (s * y) / 100;
                    document.getElementById('r' + y).innerText = ozelYuvarla(sonuc);
                });
            } else {
                bar.style.display = 'none';
            }
        }

        function temizle() {
            document.getElementById('sayi').value = '';
            document.getElementById('resultsBar').style.display = 'none';
            document.getElementById('sayi').focus(); // Tekrar yazmaya hazır hale getir
        }
    </script>
</body>
</html>
