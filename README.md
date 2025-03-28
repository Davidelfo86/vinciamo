<!DOCTYPE html>
<html>
<head>
    <title>Corse Cavalli</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border: 1px solid #ddd;
        }

        table th:nth-child(3),
        table th:nth-child(4),
        table th:nth-child(5),
        table td:nth-child(3),
        table td:nth-child(4),
        table td:nth-child(5) {
            width: 10%;
        }

        table th:nth-child(1),
        table td:nth-child(1) {
            width: 5%;
        }

        table th:nth-child(2),
        table td:nth-child(2) {
            width: 32%;
        }

        input, select {
            width: 90%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }

        table td:nth-child(3) input,
        table td:nth-child(4) input,
        table td:nth-child(5) input,
        table td:nth-child(3) select,
        table td:nth-child(4) select,
        table td:nth-child(5) select {
            width: 60%;
        }

        button {
            padding: 10px 20px;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin: 10px 5px;
        }

        .btn-salva {
            background-color: #4CAF50;
        }

        .btn-cerca {
            background-color: #2196F3;
        }

        .alert {
            padding: 15px;
            margin: 10px 0;
            border-radius: 4px;
            color: white;
        }

        .alert-warning {
            background-color: #f44336;
        }

        .alert-info {
            background-color: #2196F3;
        }

        .tris-row {
            background-color: #f8f9fa;
            font-weight: bold;
        }

        .button-container {
            margin: 20px 0;
        }

        select {
            background-color: white;
        }
    </style>
</head>
<body>
    <h1>Corse Cavalli</h1>
    
    <div id="messageBox"></div>

    <table id="mainTable">
        <tr>
            <th></th>
            <th>Cavalli</th>
            <th>1°posto</th>
            <th>2°posto</th>
            <th>3°posto</th>
        </tr>
        <tr>
            <td>1</td>
            <td><input type="text" class="cavalli-input"></td>
            <td><input type="text" class="primo-input"></td>
            <td><input type="text" class="secondo-input"></td>
            <td><input type="text" class="terzo-input"></td>
        </tr>
        <tr>
            <td>2</td>
            <td><input type="text" class="cavalli-input"></td>
            <td><input type="text" class="primo-input"></td>
            <td><input type="text" class="secondo-input"></td>
            <td><input type="text" class="terzo-input"></td>
        </tr>
        <tr>
            <td>3</td>
            <td><input type="text" class="cavalli-input"></td>
            <td><input type="text" class="primo-input"></td>
            <td><input type="text" class="secondo-input"></td>
            <td><input type="text" class="terzo-input"></td>
        </tr>
        <tr>
            <td>4</td>
            <td><input type="text" class="cavalli-input"></td>
            <td><input type="text" class="primo-input"></td>
            <td><input type="text" class="secondo-input"></td>
            <td><input type="text" class="terzo-input"></td>
        </tr>
        <tr>
            <td>5</td>
            <td><input type="text" class="cavalli-input"></td>
            <td><input type="text" class="primo-input"></td>
            <td><input type="text" class="secondo-input"></td>
            <td><input type="text" class="terzo-input"></td>
        </tr>
        <tr>
            <td>6</td>
            <td><input type="text" class="cavalli-input"></td>
            <td><input type="text" class="primo-input"></td>
            <td><input type="text" class="secondo-input"></td>
            <td><input type="text" class="terzo-input"></td>
        </tr>
        <tr class="tris-row">
            <td></td>
            <td>Tris vincente</td>
            <td>
                <select id="primoTris" style="width: 60%">
                    <option value="">-</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                    <option value="6">6</option>
                </select>
            </td>
            <td>
                <select id="secondoTris" style="width: 60%">
                    <option value="">-</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                    <option value="6">6</option>
                </select>
            </td>
            <td>
                <select id="terzoTris" style="width: 60%">
                    <option value="">-</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5</option>
                    <option value="6">6</option>
                </select>
            </td>
        </tr>
    </table>

    <div class="button-container">
        <button onclick="cercaGara()" class="btn-cerca">Cerca Gara</button>
        <button onclick="salvaDati()" class="btn-salva">Salva Corsa</button>
    </div>

    <h3>Log Dati</h3>
    <div id="logDati"></div>
    <script>
        let corse = JSON.parse(localStorage.getItem('corse')) || [];
        const SHEETS_URL = 'https://script.google.com/macros/s/AKfycbxLFkI2fU329vYO1Q73rsorW3SLIt8lKO4PpvxyuHZZuZOnHm5BsY2Jg92lRxhxXsf5/exec';

        function cercaGara() {
            const righe = document.querySelectorAll('#mainTable tr');
            const cavalliAttuali = [];

            // Raccogli i nomi dei cavalli inseriti
            for (let i = 1; i < 7; i++) {
                const riga = righe[i];
                const cavalloInput = riga.querySelectorAll('input')[0];
                if (cavalloInput.value.trim()) {
                    cavalliAttuali.push(cavalloInput.value.trim());
                }
            }

            if (cavalliAttuali.length === 0) {
                mostraMessaggio('⚠️ Inserisci almeno un cavallo prima di cercare', 'warning');
                return;
            }

            // Cerca nelle corse salvate
            let trovata = false;
            for (let corsa of corse) {
                let cavalliCorsa = corsa.dati
                    .filter(d => d.cavalli.trim())
                    .map(d => d.cavalli.trim());

                if (JSON.stringify(cavalliCorsa) === JSON.stringify(cavalliAttuali)) {
                    mostraMessaggio(`🎯 Corsa trovata! La tris vincente era: ${corsa.trisVincente}`, 'info');
                    trovata = true;
                    break;
                }
            }

            if (!trovata) {
                mostraMessaggio('🔍 Nessuna corsa simile trovata nel database', 'warning');
            }
        }

        async function salvaInGoogleSheets(corsa) {
            try {
                const response = await fetch(SHEETS_URL, {
                    method: 'POST',
                    mode: 'no-cors',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        ...corsa,
                        trisVincente: "'" + corsa.trisVincente // Aggiunge l'apostrofo per forzare il formato testo
                    })
                });
                return true;
            } catch (error) {
                console.error('Errore nel salvataggio:', error);
                return false;
            }
        }

        function mostraMessaggio(messaggio, tipo) {
            const messageBox = document.getElementById('messageBox');
            messageBox.innerHTML = `<div class="alert alert-${tipo}">${messaggio}</div>`;
            setTimeout(() => {
                messageBox.innerHTML = '';
            }, 5000);
        }

        async function salvaDati() {
            const primo = document.getElementById('primoTris').value;
            const secondo = document.getElementById('secondoTris').value;
            const terzo = document.getElementById('terzoTris').value;

            if (!primo || !secondo || !terzo) {
                mostraMessaggio('⚠️ Seleziona tutti i numeri della tris!', 'warning');
                return;
            }

            const data = new Date().toLocaleDateString('it-IT', {
                day: '2-digit',
                month: '2-digit',
                year: 'numeric'
            });
            
            const corsa = {
                id: Date.now(),
                data: data,
                trisVincente: `${primo}-${secondo}-${terzo}`,
                dati: []
            };

            // Raccoglie i dati dalla tabella
            for (let i = 1; i < 7; i++) {
                const riga = document.querySelectorAll('#mainTable tr')[i];
                const inputs = riga.querySelectorAll('input');
                const numero = riga.cells[0].textContent;
                corsa.dati.push({
                    numero: numero,
                    cavalli: inputs[0].value,
                    primo: inputs[1].value,
                    secondo: inputs[2].value,
                    terzo: inputs[3].value
                });
            }

            if (corsa.dati.every(riga => !riga.cavalli)) {
                mostraMessaggio('⚠️ Inserisci almeno un cavallo!', 'warning');
                return;
            }

            mostraMessaggio('⌛ Salvataggio in corso...', 'info');

            // Salva in Google Sheets
            const salvataggioOk = await salvaInGoogleSheets(corsa);
            
            if (salvataggioOk) {
                corse.push(corsa);
                localStorage.setItem('corse', JSON.stringify(corse));
                aggiornaLogDati();
                pulisciForm();
                mostraMessaggio('✅ Corsa salvata con successo!', 'info');
            }
        }

        function aggiornaLogDati() {
            const logDiv = document.getElementById('logDati');
            logDiv.innerHTML = '';
            
            corse.forEach(corsa => {
                const corsaDiv = document.createElement('div');
                corsaDiv.style.marginBottom = '20px';
                corsaDiv.style.borderBottom = '1px solid #ccc';
                
                corsaDiv.innerHTML = `
                    <p><strong>Data: ${corsa.data}</strong> | Tris: ${corsa.trisVincente}</p>
                    <table style="width: 100%; margin-bottom: 10px;">
                        <tr>
                            <th>Numero</th>
                            <th>Cavalli</th>
                            <th>1°posto</th>
                            <th>2°posto</th>
                            <th>3°posto</th>
                        </tr>
                        ${corsa.dati.map(riga => `
                            <tr>
                                <td>${riga.numero}</td>
                                <td>${riga.cavalli}</td>
                                <td>${riga.primo}</td>
                                <td>${riga.secondo}</td>
                                <td>${riga.terzo}</td>
                            </tr>
                        `).join('')}
                    </table>
                    <button onclick="eliminaCorsa(${corsa.id})">Elimina</button>
                `;
                logDiv.appendChild(corsaDiv);
            });
        }

        function eliminaCorsa(id) {
            corse = corse.filter(corsa => corsa.id !== id);
            localStorage.setItem('corse', JSON.stringify(corse));
            aggiornaLogDati();
        }

        function pulisciForm() {
            const inputs = document.querySelectorAll('#mainTable input');
            inputs.forEach(input => input.value = '');
            document.getElementById('primoTris').value = '';
            document.getElementById('secondoTris').value = '';
            document.getElementById('terzoTris').value = '';
        }

        window.onload = aggiornaLogDati;
    </script>
</body>
</html>
