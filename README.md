<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tabella Presenze Venerdì e Sabato</title>
    <style>
        :root {
            --primary-color: #4a6fa5;
            --secondary-color: #6b8cbc;
            --light-color: #f0f4f8;
            --border-color: #ddd;
            --header-bg: #e9ecef;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            padding: 20px;
            overflow: hidden;
        }
        
        header {
            text-align: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--light-color);
        }
        
        h1 {
            color: var(--primary-color);
            margin-bottom: 10px;
            font-size: 2rem;
        }
        
        .subtitle {
            color: #666;
            font-size: 1.1rem;
        }
        
        .info-box {
            background: linear-gradient(135deg, var(--light-color), #e3f2fd);
            border-left: 5px solid var(--primary-color);
            padding: 20px;
            margin-bottom: 25px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .info-box p {
            margin-bottom: 10px;
        }
        
        .info-box strong {
            color: var(--primary-color);
        }
        
        .add-person-form {
            display: flex;
            gap: 12px;
            margin-bottom: 25px;
            flex-wrap: wrap;
            background: var(--light-color);
            padding: 20px;
            border-radius: 10px;
        }
        
        .add-person-form input {
            padding: 12px 15px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            flex-grow: 1;
            min-width: 250px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        .add-person-form input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(74, 111, 165, 0.1);
        }
        
        .add-person-form button {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .add-person-form button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.15);
        }
        
        .table-container {
            overflow-x: auto;
            margin-bottom: 20px;
            border: 2px solid var(--border-color);
            border-radius: 10px;
            background: white;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 1000px;
        }
        
        th, td {
            border: 1px solid var(--border-color);
            padding: 12px 8px;
            text-align: center;
            transition: background-color 0.2s;
        }
        
        th {
            background: linear-gradient(135deg, var(--header-bg), #e9ecef);
            font-weight: 600;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        
        .person-name {
            font-weight: 700;
            background: linear-gradient(135deg, var(--light-color), #e8f4fd);
            text-align: left;
            position: sticky;
            left: 0;
            z-index: 5;
            min-width: 150px;
        }
        
        .month-header {
            background: linear-gradient(135deg, var(--secondary-color), #5a7bb0);
            color: white;
            font-size: 1.1rem;
        }
        
        .day-header {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            font-weight: 600;
            white-space: nowrap;
        }
        
        .friday {
            background-color: #e8f4fd;
        }
        
        .friday:hover {
            background-color: #d4e9fa;
        }
        
        .saturday {
            background-color: #f0f8ff;
        }
        
        .saturday:hover {
            background-color: #e1f0ff;
        }
        
        input[type="checkbox"] {
            transform: scale(1.4);
            cursor: pointer;
            accent-color: var(--primary-color);
        }
        
        .actions {
            display: flex;
            gap: 15px;
            justify-content: space-between;
            margin-top: 25px;
            flex-wrap: wrap;
        }
        
        .actions button {
            padding: 14px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s;
            flex: 1;
            min-width: 160px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .save-btn {
            background: linear-gradient(135deg, #28a745, #20c997);
            color: white;
        }
        
        .save-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(40, 167, 69, 0.3);
        }
        
        .reset-btn {
            background: linear-gradient(135deg, #dc3545, #e83e8c);
            color: white;
        }
        
        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(220, 53, 69, 0.3);
        }
        
        .share-section {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 2px solid var(--border-color);
        }
        
        .share-btn {
            background: linear-gradient(135deg, #25D366, #128C7E);
            color: white;
            border: none;
            padding: 16px 30px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            transition: all 0.3s;
            box-shadow: 0 4px 6px rgba(37, 211, 102, 0.3);
        }
        
        .share-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 15px rgba(37, 211, 102, 0.4);
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        
        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 1.6rem;
            }
            
            .add-person-form {
                flex-direction: column;
            }
            
            .add-person-form input {
                min-width: 100%;
            }
            
            th, td {
                padding: 8px 6px;
                font-size: 0.85rem;
            }
            
            .actions {
                flex-direction: column;
            }
            
            .actions button {
                min-width: 100%;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
        }
        
        @media (max-width: 480px) {
            h1 {
                font-size: 1.4rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            th, td {
                padding: 6px 4px;
                font-size: 0.8rem;
            }
            
            input[type="checkbox"] {
                transform: scale(1.2);
            }
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #4CAF50;
            color: white;
            padding: 15px 20px;
            border-radius: 8px;
            z-index: 1000;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            transform: translateX(400px);
            transition: transform 0.3s ease;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .loading {
            text-align: center;
            padding: 20px;
            color: #666;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>📅 Tabella Presenze Venerdì e Sabato</h1>
            <p class="subtitle">Dal 17 Ottobre 2025 al 6 Giugno 2026</p>
        </header>
        
        <div class="info-box">
            <p><strong>🚀 Istruzioni:</strong> Inserisci il tuo nome e segna con ✓ i giorni in cui sarai presente.</p>
            <p><strong>📱 Condividi:</strong> Usa il pulsante in fondo per invitare altri a partecipare!</p>
            <p><strong>💾 Salvataggio automatico:</strong> I dati si salvano automaticamente nel tuo browser.</p>
        </div>
        
        <div class="stats" id="statsContainer">
            <div class="stat-card">
                <div class="stat-number" id="totalPeople">0</div>
                <div class="stat-label">Persone Registrate</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="totalDays">38</div>
                <div class="stat-label">Giorni Totali</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="totalPresences">0</div>
                <div class="stat-label">Presenze Totali</div>
            </div>
        </div>
        
        <div class="add-person-form">
            <input type="text" id="personName" placeholder="✏️ Inserisci il tuo nome completo" maxlength="50">
            <button id="addPersonBtn">
                <span>👤 Aggiungi Persona</span>
            </button>
        </div>
        
        <div class="table-container">
            <table id="presenceTable">
                <thead>
                    <!-- Le intestazioni verranno generate dinamicamente con JavaScript -->
                </thead>
                <tbody>
                    <!-- Le righe delle persone verranno aggiunte dinamicamente con JavaScript -->
                </tbody>
            </table>
        </div>
        
        <div class="actions">
            <button id="saveBtn" class="save-btn">
                <span>💾 Salva Dati</span>
            </button>
            <button id="resetBtn" class="reset-btn">
                <span>🔄 Reset Tabella</span>
            </button>
        </div>
        
        <div class="share-section">
            <button id="shareBtn" class="share-btn">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893-.001-3.189-1.248-6.189-3.515-8.453"/>
                </svg>
                <span>Condividi su WhatsApp</span>
            </button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Elementi DOM
            const personNameInput = document.getElementById('personName');
            const addPersonBtn = document.getElementById('addPersonBtn');
            const presenceTable = document.getElementById('presenceTable');
            const tableHead = presenceTable.querySelector('thead');
            const tableBody = presenceTable.querySelector('tbody');
            const saveBtn = document.getElementById('saveBtn');
            const resetBtn = document.getElementById('resetBtn');
            const shareBtn = document.getElementById('shareBtn');
            const statsContainer = document.getElementById('statsContainer');
            const totalPeopleElement = document.getElementById('totalPeople');
            const totalPresencesElement = document.getElementById('totalPresences');
            const totalDaysElement = document.getElementById('totalDays');
            
            // Array per memorizzare le persone e le date
            let people = [];
            let dates = [];
            
            // Genera tutte le date dal 17 ottobre 2025 al 6 giugno 2026
            function generateDates() {
                const startDate = new Date(2025, 9, 17); // Ottobre è 9 (0-indexed)
                const endDate = new Date(2026, 5, 6); // Giugno è 5
                
                let currentDate = new Date(startDate);
                dates = [];
                
                while (currentDate <= endDate) {
                    // Aggiungi solo venerdì (5) e sabato (6)
                    if (currentDate.getDay() === 5 || currentDate.getDay() === 6) {
                        dates.push(new Date(currentDate));
                    }
                    currentDate.setDate(currentDate.getDate() + 1);
                }
                
                totalDaysElement.textContent = dates.length;
            }
            
            // Formatta una data come stringa "GG/MM/AAAA"
            function formatDate(date) {
                const day = String(date.getDate()).padStart(2, '0');
                const month = String(date.getMonth() + 1).padStart(2, '0');
                const year = date.getFullYear();
                return `${day}/${month}/${year}`;
            }
            
            // Crea l'intestazione della tabella con le date
            function createTableHeader() {
                // Pulisci l'intestazione esistente
                tableHead.innerHTML = '';
                
                // Crea la riga principale
                const mainRow = document.createElement('tr');
                
                // Aggiungi la cella per i nomi
                const nameHeader = document.createElement('th');
                nameHeader.textContent = 'Nome';
                nameHeader.rowSpan = 2;
                mainRow.appendChild(nameHeader);
                
                // Raggruppa le date per mese
                const months = {};
                dates.forEach(date => {
                    const monthYear = `${date.getMonth() + 1}/${date.getFullYear()}`;
                    if (!months[monthYear]) {
                        months[monthYear] = [];
                    }
                    months[monthYear].push(date);
                });
                
                // Aggiungi le intestazioni dei mesi
                Object.keys(months).forEach(monthYear => {
                    const monthHeader = document.createElement('th');
                    const [month, year] = monthYear.split('/');
                    const monthNames = ['Gennaio', 'Febbraio', 'Marzo', 'Aprile', 'Maggio', 'Giugno', 
                                       'Luglio', 'Agosto', 'Settembre', 'Ottobre', 'Novembre', 'Dicembre'];
                    monthHeader.textContent = `${monthNames[parseInt(month) - 1]} ${year}`;
                    monthHeader.colSpan = months[monthYear].length;
                    monthHeader.className = 'month-header';
                    mainRow.appendChild(monthHeader);
                });
                
                tableHead.appendChild(mainRow);
                
                // Crea la riga per i giorni
                const daysRow = document.createElement('tr');
                
                // Aggiungi le celle per ogni data
                dates.forEach(date => {
                    const dayHeader = document.createElement('th');
                    const day = date.getDate();
                    const month = date.getMonth() + 1;
                    dayHeader.textContent = `${day}/${month}`;
                    dayHeader.title = formatDate(date); // Tooltip con data completa
                    dayHeader.className = `day-header ${date.getDay() === 5 ? 'friday' : 'saturday'}`;
                    daysRow.appendChild(dayHeader);
                });
                
                tableHead.appendChild(daysRow);
            }
            
            // Aggiorna le statistiche
            function updateStats() {
                totalPeopleElement.textContent = people.length;
                
                // Calcola il totale delle presenze
                let totalPresences = 0;
                const checkboxes = document.querySelectorAll('input[type="checkbox"]');
                checkboxes.forEach(checkbox => {
                    if (checkbox.checked) totalPresences++;
                });
                
                totalPresencesElement.textContent = totalPresences;
            }
            
            // Aggiunge una nuova persona alla tabella
            function addPerson(name) {
                // Verifica che il nome non sia vuoto
                if (!name.trim()) {
                    showNotification('⚠️ Inserisci un nome valido');
                    return;
                }
                
                // Verifica che il nome non esista già
                if (people.includes(name)) {
                    showNotification('⚠️ Questo nome è già presente nella tabella');
                    return;
                }
                
                // Aggiungi la persona all'array
                people.push(name);
                
                // Crea una nuova riga per la persona
                const newRow = document.createElement('tr');
                
                // Aggiungi la cella con il nome
                const nameCell = document.createElement('td');
                nameCell.textContent = name;
                nameCell.className = 'person-name';
                newRow.appendChild(nameCell);
                
                // Aggiungi le checkbox per ogni data
                dates.forEach(date => {
                    const dateCell = document.createElement('td');
                    dateCell.className = date.getDay() === 5 ? 'friday' : 'saturday';
                    
                    const checkbox = document.createElement('input');
                    checkbox.type = 'checkbox';
                    checkbox.dataset.person = name;
                    checkbox.dataset.date = formatDate(date);
                    
                    dateCell.appendChild(checkbox);
                    newRow.appendChild(dateCell);
                });
                
                // Aggiungi la riga al corpo della tabella
                tableBody.appendChild(newRow);
                
                // Pulisci l'input
                personNameInput.value = '';
                
                // Aggiorna le statistiche
                updateStats();
                
                // Salva i dati
                saveData();
                
                showNotification('✅ Persona aggiunta con successo!');
            }
            
            // Mostra una notifica
            function showNotification(message) {
                // Rimuovi notifiche esistenti
                const existingNotification = document.querySelector('.notification');
                if (existingNotification) {
                    existingNotification.remove();
                }
                
                const notification = document.createElement('div');
                notification.className = 'notification';
                notification.textContent = message;
                document.body.appendChild(notification);
                
                // Mostra la notifica
                setTimeout(() => {
                    notification.classList.add('show');
                }, 100);
                
                // Nascondi dopo 3 secondi
                setTimeout(() => {
                    notification.classList.remove('show');
                    setTimeout(() => {
                        if (notification.parentNode) {
                            notification.parentNode.removeChild(notification);
                        }
                    }, 300);
                }, 3000);
            }
            
            // Salva i dati nel localStorage
            function saveData() {
                const data = {
                    people: people,
                    presences: {}
                };
                
                // Raccogli tutte le presenze
                const checkboxes = document.querySelectorAll('input[type="checkbox"]');
                checkboxes.forEach(checkbox => {
                    if (!data.presences[checkbox.dataset.person]) {
                        data.presences[checkbox.dataset.person] = {};
                    }
                    data.presences[checkbox.dataset.person][checkbox.dataset.date] = checkbox.checked;
                });
                
                localStorage.setItem('presenceTableData', JSON.stringify(data));
            }
            
            // Carica i dati dal localStorage
            function loadData() {
                const savedData = localStorage.getItem('presenceTableData');
                if (savedData) {
                    const data = JSON.parse(savedData);
                    people = data.people || [];
                    
                    // Ricrea le righe per ogni persona
                    people.forEach(person => {
                        const newRow = document.createElement('tr');
                        
                        // Aggiungi la cella con il nome
                        const nameCell = document.createElement('td');
                        nameCell.textContent = person;
                        nameCell.className = 'person-name';
                        newRow.appendChild(nameCell);
                        
                        // Aggiungi le checkbox per ogni data
                        dates.forEach(date => {
                            const dateCell = document.createElement('td');
                            dateCell.className = date.getDay() === 5 ? 'friday' : 'saturday';
                            
                            const checkbox = document.createElement('input');
                            checkbox.type = 'checkbox';
                            checkbox.dataset.person = person;
                            checkbox.dataset.date = formatDate(date);
                            
                            // Ripristina lo stato della checkbox se salvato
                            if (data.presences && data.presences[person] && data.presences[person][formatDate(date)]) {
                                checkbox.checked = true;
                            }
                            
                            dateCell.appendChild(checkbox);
                            newRow.appendChild(dateCell);
                        });
                        
                        // Aggiungi la riga al corpo della tabella
                        tableBody.appendChild(newRow);
                    });
                    
                    updateStats();
                }
            }
            
            // Resetta la tabella
            function resetTable() {
                if (confirm('⚠️ Sei sicuro di voler resettare tutta la tabella?\n\nTutti i dati verranno cancellati e questa azione non può essere annullata.')) {
                    people = [];
                    tableBody.innerHTML = '';
                    localStorage.removeItem('presenceTableData');
                    updateStats();
                    showNotification('🔄 Tabella resettata con successo');
                }
            }
            
            // Condividi su WhatsApp
            function shareOnWhatsApp() {
                const url = window.location.href;
                const text = "🗓️ Compila la tabella delle presenze per i venerdì e sabati!\n\nDal 17 Ottobre 2025 al 6 Giugno 2026\n\nInserisci il tuo nome e segna i giorni in cui ci sarai!";
                const whatsappUrl = `https://wa.me/?text=${encodeURIComponent(text + " " + url)}`;
                window.open(whatsappUrl, '_blank');
            }
            
            // Inizializza la tabella
            function initTable() {
                generateDates();
                createTableHeader();
                loadData();
                
                // Mostra messaggio di benvenuto
                setTimeout(() => {
                    if (people.length === 0) {
                        showNotification('👋 Benvenuto! Inizia aggiungendo il tuo nome.');
                    }
                }, 1000);
            }
            
            // Aggiungi event listeners
            addPersonBtn.addEventListener('click', function() {
                addPerson(personNameInput.value);
            });
            
            personNameInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    addPerson(personNameInput.value);
                }
            });
            
            saveBtn.addEventListener('click', function() {
                saveData();
                showNotification('💾 Dati salvati con successo!');
            });
            
            resetBtn.addEventListener('click', resetTable);
            
            shareBtn.addEventListener('click', shareOnWhatsApp);
            
            // Salva automaticamente quando viene cambiata una checkbox
            presenceTable.addEventListener('change', function(e) {
                if (e.target.type === 'checkbox') {
                    saveData();
                    updateStats();
                }
            });
            
            // Inizializza la tabella
            initTable();
        });
    </script>
</body>
</html>