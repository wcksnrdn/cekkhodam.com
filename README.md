<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cek Khodam Online</title>
    <link rel="stylesheet" href="cekkhodam.css">
</head>
<body>
    <div class="main-container">
        <div class="container">
            <div class="judul">
                <h1>Cek Khodam</h1>
            </div>
            <input type="text" id="name" placeholder="Masukkan Nama Anda">
            <button onclick="generateKhodam()" class="btn">
                <svg height="24" width="24" fill="#FFFFFF" viewBox="0 0 24 24" data-name="Layer 1" id="Layer_1" class="sparkle">
                    <path d="M10,21.236,6.755,14.745.264,11.5,6.755,8.255,10,1.764l3.245,6.491L19.736,11.5l-6.491,3.245ZM18,21l1.5,3L21,21l3-1.5L21,18l-1.5-3L18,18l-3,1.5ZM19.333,4.667,20.5,7l1.167-2.333L24,3.5,21.667,2.333,20.5,0,19.333,2.333,17,3.5Z"></path>
                </svg>
                <span class="text">Generate</span>
            </button>
            <div class="loading" id="loading">
                <div class="loader">
                    <svg viewBox="0 0 80 80">
                        <circle id="test" cx="40" cy="40" r="32"></circle>
                    </svg>
                </div>
                <div class="loader triangle">
                    <svg viewBox="0 0 86 80">
                        <polygon points="43 8 79 72 7 72"></polygon>
                    </svg>
                </div>
                <div class="loader">
                    <svg viewBox="0 0 80 80">
                        <rect x="8" y="8" width="64" height="64"></rect>
                    </svg>
                </div>
            </div>
            <div class="result-container">
                <h1>Here for the Result!</h1>
                <div class="result" id="result">
                    <div class="result-name" id="resultName"></div>
                    <div class="result-khodam" id="resultKhodam"></div>
                </div>
            </div>
    </div>
    <div class="history" id="history">
        <h2>History</h2>
        <div class="history-container">
            <ul id="historyList"></ul>
        </div>
        <button class="clear-history" onclick="clearHistory()">Hapus History</button>
    </div>
</div>
    <script>
        function generateKhodam() {
            const name = document.getElementById('name').value;
            const khodams = [
                "Naga", "Macan", "Garuda", "Kuda", "Harimau", "Elang", "Kerbau", "Gajah", "Lembu", "Burung Phoenix",
                "Singa", "Ular", "Katak", "Kancil", "Buaya", "Kijang", "Angsa", "Kupu-kupu", "Serigala", "Kelelawar",
                "Kadal", "Landak", "Bebek", "Kepiting", "Kanguru", "Badak", "Kucing", "Panda", "Cendrawasih", "Kucing hutan",
                "Gorila", "Zebra", "Kuda nil", "Banteng", "Kerbau air", "Lumba-lumba", "Penyu", "Kura-kura", "Jerapah",
                "Ikan paus", "Hiu", "Belut", "Burung hantu", "Merak", "Kekuatan Setan", "Syaitan", "Iblis", "Jin Jahat",
                "Setan Merah", "Sihir Hitam", "Iblis Neraka", "Sihir Sihir", "Guna Guna", "Santet Kejam", "Pukau Pukau", "Genderuwo"
            ];
            const randomIndex = Math.floor(Math.random() * khodams.length);
            const resultNameDiv = document.getElementById('resultName');
            const resultKhodamDiv = document.getElementById('resultKhodam');
            const loadingDiv = document.getElementById('loading');
            const historyList = document.getElementById('historyList');

            if (name.trim() === "") {
                resultNameDiv.innerHTML = "Silakan masukkan nama Anda!";
                resultKhodamDiv.innerHTML = "";
                return;
            }

            resultNameDiv.innerHTML = "";
            resultKhodamDiv.innerHTML = "";
            loadingDiv.style.display = "block";

            setTimeout(() => {
                loadingDiv.style.display = "none";
                const khodam = khodams[randomIndex];
                resultNameDiv.innerHTML = `Nama Anda: ${name}`;
                resultKhodamDiv.innerHTML = `Khodam Anda: ${khodam}`;

                // Save to history
                const historyItem = document.createElement('li');
                historyItem.textContent = `Nama: ${name} - Khodam: ${khodam}`;
                historyList.insertBefore(historyItem, historyList.firstChild); // Insert as first child

                // Save to localStorage
                const history = JSON.parse(localStorage.getItem('khodamHistory')) || [];
                history.unshift({ name, khodam }); // Insert at the beginning of array
                localStorage.setItem('khodamHistory', JSON.stringify(history));
            }, 2000);
        }

        function clearHistory() {
            const historyList = document.getElementById('historyList');
            historyList.innerHTML = ''; // Clear the history in the DOM

            localStorage.removeItem('khodamHistory'); // Clear the history in localStorage
        }

        // Load history from localStorage on page load
        window.onload = () => {
            const history = JSON.parse(localStorage.getItem('khodamHistory')) || [];
            const historyList = document.getElementById('historyList');
            // Reverse loop to display latest first
            for (let i = history.length - 1; i >= 0; i--) {
                const historyItem = document.createElement('li');
                historyItem.textContent = `Nama: ${history[i].name} - Khodam: ${history[i].khodam}`;
                historyList.appendChild(historyItem);
            }
        }
    </script>
</body>
</html>
