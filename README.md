# tidyteam
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tidy Team - Reinigungsvertrag</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2em;
            margin-bottom: 10px;
        }
        
        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }
        
        .form-content {
            padding: 40px;
        }
        
        .section {
            margin-bottom: 35px;
            padding-bottom: 25px;
            border-bottom: 2px solid #f0f0f0;
        }
        
        .section:last-child {
            border-bottom: none;
        }
        
        .section-title {
            font-size: 1.4em;
            color: #667eea;
            margin-bottom: 20px;
            font-weight: 600;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }
        
        @media (max-width: 768px) {
            .form-row {
                grid-template-columns: 1fr;
            }
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 500;
        }
        
        input[type="text"],
        input[type="email"],
        input[type="tel"],
        input[type="number"],
        input[type="date"],
        input[type="time"],
        textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s;
        }
        
        input:focus,
        textarea:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .checkbox-group {
            display: flex;
            gap: 30px;
            align-items: center;
            margin-top: 10px;
        }
        
        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        input[type="radio"],
        input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .signature-container {
            margin-top: 20px;
        }
        
        #signatureCanvas {
            border: 2px solid #667eea;
            border-radius: 8px;
            cursor: crosshair;
            display: block;
            width: 100%;
            max-width: 500px;
            height: 200px;
            background: #fafafa;
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        button {
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 600;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }
        
        .btn-secondary {
            background: #f0f0f0;
            color: #333;
        }
        
        .btn-secondary:hover {
            background: #e0e0e0;
        }
        
        .submit-section {
            margin-top: 40px;
            padding-top: 30px;
            border-top: 2px solid #f0f0f0;
            text-align: center;
        }
        
        .footer {
            background: #f8f9fa;
            padding: 20px;
            text-align: center;
            color: #666;
            font-size: 0.9em;
        }
        
        .success-message {
            display: none;
            background: #4caf50;
            color: white;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .error-message {
            display: none;
            background: #f44336;
            color: white;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🧹 Tidy Team</h1>
            <p>Reinigungsvertrag mit Abgabegarantie</p>
        </div>
        
        <div class="form-content">
            <div id="successMessage" class="success-message"></div>
            <div id="errorMessage" class="error-message"></div>
            
            <form id="cleaningForm">
                <!-- Besichtigungstermin & Kundendaten -->
                <div class="section">
                    <h2 class="section-title">📋 Besichtigungstermin & Kundendaten</h2>
                    
                    <div class="form-group">
                        <label for="besichtigungstermin">Besichtigungstermin:</label>
                        <input type="date" id="besichtigungstermin" name="besichtigungstermin">
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="vorname">Vorname:</label>
                            <input type="text" id="vorname" name="vorname" required>
                        </div>
                        <div class="form-group">
                            <label for="name">Name:</label>
                            <input type="text" id="name" name="name" required>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="adresse">Adresse / Ort:</label>
                        <input type="text" id="adresse" name="adresse" required>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="telefon">Telefon:</label>
                            <input type="tel" id="telefon" name="telefon">
                        </div>
                        <div class="form-group">
                            <label for="email">E-Mail:</label>
                            <input type="email" id="email" name="email" required>
                        </div>
                    </div>
                </div>
                
                <!-- Wohnungsdaten -->
                <div class="section">
                    <h2 class="section-title">🏠 Wohnungsdaten</h2>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="zimmeranzahl">Zimmeranzahl:</label>
                            <input type="number" id="zimmeranzahl" name="zimmeranzahl" min="1" step="0.5">
                        </div>
                        <div class="form-group">
                            <label for="wohnflaeche">Wohnfläche (m²):</label>
                            <input type="number" id="wohnflaeche" name="wohnflaeche" min="1">
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="stockwerk">Stockwerk:</label>
                            <input type="text" id="stockwerk" name="stockwerk">
                        </div>
                        <div class="form-group">
                            <label>Lift vorhanden:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="lift_ja" name="lift" value="Ja">
                                    <label for="lift_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="lift_nein" name="lift" value="Nein">
                                    <label for="lift_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="preis">Preis (CHF):</label>
                        <input type="number" id="preis" name="preis" min="0" step="0.01">
                    </div>
                </div>
                
                <!-- Termine -->
                <div class="section">
                    <h2 class="section-title">📅 Reinigungstermin & Abgabetermin</h2>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="reinigungstermin">Reinigungstermin (Datum):</label>
                            <input type="date" id="reinigungstermin" name="reinigungstermin">
                        </div>
                        <div class="form-group">
                            <label for="abgabetermin">Abgabetermin (Datum):</label>
                            <input type="date" id="abgabetermin" name="abgabetermin">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="uhrzeit">Uhrzeit:</label>
                        <input type="time" id="uhrzeit" name="uhrzeit">
                    </div>
                </div>
                
                <!-- Leistungen -->
                <div class="section">
                    <h2 class="section-title">✨ Leistungen</h2>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>Storen / Lamellen:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="storen_ja" name="storen" value="Ja">
                                    <label for="storen_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="storen_nein" name="storen" value="Nein">
                                    <label for="storen_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label for="fenster">Fenster (Stk.):</label>
                            <input type="number" id="fenster" name="fenster" min="0">
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>WC / Bad:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="wcbad_ja" name="wcbad" value="Ja">
                                    <label for="wcbad_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="wcbad_nein" name="wcbad" value="Nein">
                                    <label for="wcbad_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>Waschmaschine / Tumbler:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="waschmaschine_ja" name="waschmaschine" value="Ja">
                                    <label for="waschmaschine_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="waschmaschine_nein" name="waschmaschine" value="Nein">
                                    <label for="waschmaschine_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>Küche:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="kueche_ja" name="kueche" value="Ja">
                                    <label for="kueche_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="kueche_nein" name="kueche" value="Nein">
                                    <label for="kueche_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label for="balkon">Balkon (Anzahl):</label>
                            <input type="number" id="balkon" name="balkon" min="0">
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>Wintergarten:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="wintergarten_ja" name="wintergarten" value="Ja">
                                    <label for="wintergarten_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="wintergarten_nein" name="wintergarten" value="Nein">
                                    <label for="wintergarten_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>Kärcher:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="kaercher_ja" name="kaercher" value="Ja">
                                    <label for="kaercher_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="kaercher_nein" name="kaercher" value="Nein">
                                    <label for="kaercher_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>Teppich:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="teppich_ja" name="teppich" value="Ja">
                                    <label for="teppich_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="teppich_nein" name="teppich" value="Nein">
                                    <label for="teppich_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>Keller:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="keller_ja" name="keller" value="Ja">
                                    <label for="keller_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="keller_nein" name="keller" value="Nein">
                                    <label for="keller_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>Estrich:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="estrich_ja" name="estrich" value="Ja">
                                    <label for="estrich_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="estrich_nein" name="estrich" value="Nein">
                                    <label for="estrich_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>Garage:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="garage_ja" name="garage" value="Ja">
                                    <label for="garage_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="garage_nein" name="garage" value="Nein">
                                    <label for="garage_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>Briefkasten:</label>
                        <div class="checkbox-group">
                            <div class="checkbox-item">
                                <input type="radio" id="briefkasten_ja" name="briefkasten" value="Ja">
                                <label for="briefkasten_ja">Ja</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="radio" id="briefkasten_nein" name="briefkasten" value="Nein">
                                <label for="briefkasten_nein">Nein</label>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Extras -->
                <div class="section">
                    <h2 class="section-title">💳 Extras</h2>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label>Bezahlung:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="bezahlung_bar" name="bezahlung" value="Bar">
                                    <label for="bezahlung_bar">Bar</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="bezahlung_twint" name="bezahlung" value="Twint">
                                    <label for="bezahlung_twint">Twint</label>
                                </div>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <label>Übergabe dabei:</label>
                            <div class="checkbox-group">
                                <div class="checkbox-item">
                                    <input type="radio" id="uebergabe_ja" name="uebergabe" value="Ja">
                                    <label for="uebergabe_ja">Ja</label>
                                </div>
                                <div class="checkbox-item">
                                    <input type="radio" id="uebergabe_nein" name="uebergabe" value="Nein">
                                    <label for="uebergabe_nein">Nein</label>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>Vollmacht:</label>
                        <div class="checkbox-group">
                            <div class="checkbox-item">
                                <input type="radio" id="vollmacht_ja" name="vollmacht" value="Ja">
                                <label for="vollmacht_ja">Ja</label>
                            </div>
                            <div class="checkbox-item">
                                <input type="radio" id="vollmacht_nein" name="vollmacht" value="Nein">
                                <label for="vollmacht_nein">Nein</label>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Unterschrift -->
                <div class="section">
                    <h2 class="section-title">✍️ Unterschrift Kunde</h2>
                    
                    <div class="form-group">
                        <label for="datum">Datum:</label>
                        <input type="date" id="datum" name="datum" required>
                    </div>
                    
                    <div class="signature-container">
                        <label>Unterschrift:</label>
                        <canvas id="signatureCanvas" width="500" height="200"></canvas>
                        <div class="button-group">
                            <button type="button" class="btn-secondary" onclick="clearSignature()">Unterschrift löschen</button>
                        </div>
                    </div>
                </div>
                
                <!-- Submit -->
                <div class="submit-section">
                    <div class="button-group" style="justify-content: center;">
                        <button type="submit" class="btn-primary">📄 PDF erstellen & per E-Mail versenden</button>
                    </div>
                </div>
            </form>
        </div>
        
        <div class="footer">
            <p><strong>Tidy Team GmbH</strong></p>
            <p>Freiestrasse 38, 8580 Amriswil</p>
            <p>Tel: 078 737 97 16 | info@tidy-team.ch | tidy-team.ch</p>
            <p>UBS IBAN: CH84 0020 3203 1111 7301 A</p>
        </div>
    </div>
    
    <script>
        // Signature Canvas Setup
        const canvas = document.getElementById('signatureCanvas');
        const ctx = canvas.getContext('2d');
        let isDrawing = false;
        let lastX = 0;
        let lastY = 0;
        
        // Set canvas size properly
        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
        }
        
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        // Drawing functions
        function startDrawing(e) {
            isDrawing = true;
            const rect = canvas.getBoundingClientRect();
            [lastX, lastY] = [e.clientX - rect.left, e.clientY - rect.top];
        }
        
        function draw(e) {
            if (!isDrawing) return;
            
            const rect = canvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            ctx.strokeStyle = '#000';
            ctx.lineWidth = 2;
            ctx.lineCap = 'round';
            ctx.lineJoin = 'round';
            
            ctx.beginPath();
            ctx.moveTo(lastX, lastY);
            ctx.lineTo(x, y);
            ctx.stroke();
            
            [lastX, lastY] = [x, y];
        }
        
        function stopDrawing() {
            isDrawing = false;
        }
        
        // Touch support
        function getTouchPos(e) {
            const rect = canvas.getBoundingClientRect();
            const touch = e.touches[0];
            return {
                x: touch.clientX - rect.left,
                y: touch.clientY - rect.top
            };
        }
        
        canvas.addEventListener('mousedown', startDrawing);
        canvas.addEventListener('mousemove', draw);
        canvas.addEventListener('mouseup', stopDrawing);
        canvas.addEventListener('mouseout', stopDrawing);
        
        canvas.addEventListener('touchstart', (e) => {
            e.preventDefault();
            const pos = getTouchPos(e);
            isDrawing = true;
            [lastX, lastY] = [pos.x, pos.y];
        });
        
        canvas.addEventListener('touchmove', (e) => {
            e.preventDefault();
            if (!isDrawing) return;
            const pos = getTouchPos(e);
            
            ctx.strokeStyle = '#000';
            ctx.lineWidth = 2;
            ctx.lineCap = 'round';
            ctx.lineJoin = 'round';
            
            ctx.beginPath();
            ctx.moveTo(lastX, lastY);
            ctx.lineTo(pos.x, pos.y);
            ctx.stroke();
            
            [lastX, lastY] = [pos.x, pos.y];
        });
        
        canvas.addEventListener('touchend', () => {
            isDrawing = false;
        });
        
        function clearSignature() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }
        
        // Form submission
        document.getElementById('cleaningForm').addEventListener('submit', async function(e) {
            e.preventDefault();
            
            // Check if signature exists
            const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
            const hasSignature = imageData.data.some(channel => channel !== 0);
            
            if (!hasSignature) {
                showError('Bitte fügen Sie eine Unterschrift hinzu.');
                return;
            }
            
            // Generate PDF
            try {
                await generatePDF();
            } catch (error) {
                showError('Fehler beim Erstellen des PDFs: ' + error.message);
            }
        });
        
        async function generatePDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // Get form data
            const formData = new FormData(document.getElementById('cleaningForm'));
            const data = Object.fromEntries(formData.entries());
            
            // Header
            doc.setFontSize(20);
            doc.setTextColor(102, 126, 234);
            doc.text('Tidy Team GmbH', 105, 20, { align: 'center' });
            
            doc.setFontSize(14);
            doc.text('Reinigungsvertrag mit Abgabegarantie', 105, 28, { align: 'center' });
            
            // Reset color
            doc.setTextColor(0, 0, 0);
            doc.setFontSize(10);
            
            let y = 40;
            
            // Section: Besichtigungstermin & Kundendaten
            doc.setFontSize(12);
            doc.setFont(undefined, 'bold');
            doc.text('Besichtigungstermin & Kundendaten', 20, y);
            y += 8;
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Besichtigungstermin: ${data.besichtigungstermin || '-'}`, 20, y);
            y += 6;
            doc.text(`Name / Vorname: ${data.name || ''} ${data.vorname || ''}`, 20, y);
            y += 6;
            doc.text(`Adresse / Ort: ${data.adresse || '-'}`, 20, y);
            y += 6;
            doc.text(`Telefon: ${data.telefon || '-'}`, 20, y);
            y += 6;
            doc.text(`E-Mail: ${data.email || '-'}`, 20, y);
            y += 10;
            
            // Section: Wohnungsdaten
            doc.setFontSize(12);
            doc.setFont(undefined, 'bold');
            doc.text('Wohnungsdaten', 20, y);
            y += 8;
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Zimmeranzahl: ${data.zimmeranzahl || '-'}`, 20, y);
            y += 6;
            doc.text(`Wohnfläche: ${data.wohnflaeche || '-'} m²`, 20, y);
            y += 6;
            doc.text(`Stockwerk: ${data.stockwerk || '-'}`, 20, y);
            y += 6;
            doc.text(`Lift: ${data.lift || '-'}`, 20, y);
            y += 6;
            doc.text(`Preis: CHF ${data.preis || '-'}`, 20, y);
            y += 10;
            
            // Section: Termine
            doc.setFontSize(12);
            doc.setFont(undefined, 'bold');
            doc.text('Reinigungstermin & Abgabetermin', 20, y);
            y += 8;
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Reinigungstermin: ${data.reinigungstermin || '-'}`, 20, y);
            y += 6;
            doc.text(`Abgabetermin: ${data.abgabetermin || '-'}`, 20, y);
            y += 6;
            doc.text(`Uhrzeit: ${data.uhrzeit || '-'}`, 20, y);
            y += 10;
            
            // Section: Leistungen
            doc.setFontSize(12);
            doc.setFont(undefined, 'bold');
            doc.text('Leistungen', 20, y);
            y += 8;
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            
            const leistungen = [
                ['Storen / Lamellen', data.storen || '-'],
                ['Fenster (Stk.)', data.fenster || '-'],
                ['WC / Bad', data.wcbad || '-'],
                ['Waschmaschine / Tumbler', data.waschmaschine || '-'],
                ['Küche', data.kueche || '-'],
                ['Balkon (Anzahl)', data.balkon || '-'],
                ['Wintergarten', data.wintergarten || '-'],
                ['Kärcher', data.kaercher || '-'],
                ['Teppich', data.teppich || '-'],
                ['Keller', data.keller || '-'],
                ['Estrich', data.estrich || '-'],
                ['Garage', data.garage || '-'],
                ['Briefkasten', data.briefkasten || '-']
            ];
            
            leistungen.forEach(([label, value]) => {
                doc.text(`${label}: ${value}`, 20, y);
                y += 6;
            });
            
            y += 4;
            
            // Section: Extras
            doc.setFontSize(12);
            doc.setFont(undefined, 'bold');
            doc.text('Extras', 20, y);
            y += 8;
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Bezahlung: ${data.bezahlung || '-'}`, 20, y);
            y += 6;
            doc.text(`Übergabe dabei: ${data.uebergabe || '-'}`, 20, y);
            y += 6;
            doc.text(`Vollmacht: ${data.vollmacht || '-'}`, 20, y);
            y += 10;
            
            // Signature
            doc.setFontSize(12);
            doc.setFont(undefined, 'bold');
            doc.text('Unterschrift Kunde', 20, y);
            y += 8;
            
            doc.setFontSize(10);
            doc.setFont(undefined, 'normal');
            doc.text(`Datum: ${data.datum || '-'}`, 20, y);
            y += 10;
            
            // Add signature image
            const signatureData = canvas.toDataURL('image/png');
            doc.addImage(signatureData, 'PNG', 20, y, 80, 30);
            y += 35;
            
            // Footer
            doc.setFontSize(8);
            doc.setTextColor(100, 100, 100);
            const footerY = 280;
            doc.text('Tidy Team GmbH - Freiestrasse 38, 8580 Amriswil', 105, footerY, { align: 'center' });
            doc.text('Tel: 078 737 97 16 - info@tidy-team.ch - tidy-team.ch', 105, footerY + 4, { align: 'center' });
            doc.text('UBS IBAN: CH84 0020 3203 1111 7301 A', 105, footerY + 8, { align: 'center' });
            
            // Save PDF
            doc.save(`Reinigungsvertrag_${data.name}_${data.vorname}_${data.datum}.pdf`);
            
            // Prepare email
            const emailSubject = `Reinigungsvertrag - ${data.name} ${data.vorname}`;
            const emailBody = `Sehr geehrte Damen und Herren,

anbei finden Sie den ausgefüllten Reinigungsvertrag.

Kundendaten:
- Name: ${data.name} ${data.vorname}
- Adresse: ${data.adresse}
- Telefon: ${data.telefon}
- E-Mail: ${data.email}

Reinigungstermin: ${data.reinigungstermin || '-'}
Abgabetermin: ${data.abgabetermin || '-'}

Mit freundlichen Grüssen
Tidy Team`;
            
            // Hinweistext anzeigen
            showSuccess(`PDF wurde erfolgreich erstellt und heruntergeladen!<br><br>
                <strong>E-Mail-Versand:</strong><br>
                Bitte öffnen Sie Ihr E-Mail-Programm und senden Sie das PDF an:<br>
                <strong>info@tidy-team.ch</strong><br><br>
                <em>Hinweis: Der automatische E-Mail-Versand direkt aus dem Browser ist aus Sicherheitsgründen eingeschränkt. 
                Sie können das heruntergeladene PDF manuell per E-Mail versenden.</em>`);
            
            // Versuch, E-Mail-Client zu öffnen
            const mailtoLink = `mailto:info@tidy-team.ch?subject=${encodeURIComponent(emailSubject)}&body=${encodeURIComponent(emailBody)}`;
            window.location.href = mailtoLink;
        }
        
        function showSuccess(message) {
            const successDiv = document.getElementById('successMessage');
            successDiv.innerHTML = message;
            successDiv.style.display = 'block';
            document.getElementById('errorMessage').style.display = 'none';
            
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
        
        function showError(message) {
            const errorDiv = document.getElementById('errorMessage');
            errorDiv.textContent = message;
            errorDiv.style.display = 'block';
            document.getElementById('successMessage').style.display = 'none';
            
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
        
        // Set today's date as default
        document.getElementById('datum').valueAsDate = new Date();
    </script>
</body>
</html>
