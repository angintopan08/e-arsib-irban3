<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Arsip Irban 3</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
        }
        .container-card {
            background-color: #ffffff;
            border-radius: 1.5rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            padding: 2.5rem;
            max-width: 90vw;
            margin-left: auto;
            margin-right: auto;
            margin-top: 2rem;
            margin-bottom: 2rem;
        }
        .form-input {
            width: 100%;
            padding: 0.75rem 1rem;
            border: 1px solid #d1d5db;
            border-radius: 0.5rem;
            transition: all 0.2s ease-in-out;
        }
        .form-input:focus {
            outline: 2px solid transparent;
            outline-offset: 2px;
            border-color: #2563eb;
            box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.25);
        }
        .button {
            padding: 0.75rem 2rem;
            font-weight: 600;
            border-radius: 0.5rem;
            transition: background-color 0.3s;
        }
        .button-primary {
            background-color: #2563eb;
            color: #ffffff;
        }
        .button-primary:hover {
            background-color: #1d4ed8;
        }
        .button-secondary {
            background-color: #e5e7eb;
            color: #4b5563;
        }
        .button-secondary:hover {
            background-color: #d1d5db;
        }
        .table-container {
            overflow-x: auto;
        }
        .table-striped tbody tr:nth-child(odd) {
            background-color: #f9fafb;
        }
        .loading-spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-left-color: #2563eb;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .suggestion-box {
            background-color: #f0f4f8;
            border-left: 4px solid #3b82f6;
            padding: 1rem;
            margin-top: 1rem;
            border-radius: 0.5rem;
        }
        .suggestion-box h4 {
            font-weight: bold;
            color: #1e40af;
        }
        @media (min-width: 768px) {
            .grid-cols-2 {
                grid-template-columns: repeat(2, minmax(0, 1fr));
            }
        }
    </style>
</head>
<body>

    <div class="container-card">
        <h1 class="text-3xl font-bold text-center text-gray-800 mb-6">E-Arsip Irban 3</h1>
        <p class="text-center text-gray-500 mb-8">Masukkan data surat masuk dengan mudah dan terstruktur.</p>

        <form id="formSurat" class="grid grid-cols-1 md:grid-cols-2 gap-x-8 gap-y-6">

            <!-- Kolom Kiri -->
            <div>
                <div class="mb-4">
                    <label for="nomorSurat" class="block text-sm font-medium text-gray-700">Nomor Surat</label>
                    <input type="text" id="nomorSurat" class="form-input mt-1" placeholder="Masukkan nomor surat">
                </div>
                <div class="mb-4">
                    <label for="pengirim" class="block text-sm font-medium text-gray-700">Asal Surat</label>
                    <input type="text" id="pengirim" class="form-input mt-1" placeholder="Masukkan asal surat">
                </div>
                <div class="mb-4">
                    <label for="tanggalSurat" class="block text-sm font-medium text-gray-700">Tanggal Surat</label>
                    <input type="date" id="tanggalSurat" class="form-input mt-1">
                </div>
                <div class="mb-4">
                    <label for="perihal" class="block text-sm font-medium text-gray-700">Perihal</label>
                    <textarea id="perihal" rows="3" class="form-input mt-1" placeholder="Jelaskan perihal surat"></textarea>
                    <button type="button" id="btnSummarize" class="button button-secondary text-sm px-3 py-1 mt-2">Ringkas Perihal ✨</button>
                    <div id="summaryResult" class="suggestion-box hidden">
                        <h4 class="text-sm">Ringkasan:</h4>
                        <p id="summaryText" class="text-gray-700 mt-1 text-sm"></p>
                    </div>
                </div>
            </div>

            <!-- Kolom Kanan -->
            <div>
                <div class="mb-4">
                    <label for="kepada" class="block text-sm font-medium text-gray-700">Kepada</label>
                    <input type="text" id="kepada" class="form-input mt-1" placeholder="Tujuan surat">
                </div>
                <div class="mb-4">
                    <label for="disposisiSetda" class="block text-sm font-medium text-gray-700">Disposisi Setda Asisten</label>
                    <input type="text" id="disposisiSetda" class="form-input mt-1" placeholder="Disposisi Setda Asisten">
                    <button type="button" id="btnSuggestSetda" class="button button-secondary text-sm px-3 py-1 mt-2">Saran Disposisi ✨</button>
                </div>
                <div class="mb-4">
                    <label for="disposisiInspektur" class="block text-sm font-medium text-gray-700">Disposisi Inspektur Sekretaris</label>
                    <input type="text" id="disposisiInspektur" class="form-input mt-1" placeholder="Disposisi Inspektur Sekretaris">
                    <button type="button" id="btnSuggestInspektur" class="button button-secondary text-sm px-3 py-1 mt-2">Saran Disposisi ✨</button>
                </div>
                <div class="mb-4">
                    <label for="disposisiIrban" class="block text-sm font-medium text-gray-700">Disposisi Irban</label>
                    <input type="text" id="disposisiIrban" class="form-input mt-1" placeholder="Disposisi Irban">
                    <button type="button" id="btnSuggestIrban" class="button button-secondary text-sm px-3 py-1 mt-2">Saran Disposisi ✨</button>
                </div>
                <div class="mb-4">
                    <label for="namaTTD" class="block text-sm font-medium text-gray-700">Nama TTD</label>
                    <input type="text" id="namaTTD" class="form-input mt-1" placeholder="Nama yang menandatangani">
                </div>
                <div class="mb-4">
                    <label for="tanggalTerima" class="block text-sm font-medium text-gray-700">Tanggal Diterima</label>
                    <input type="date" id="tanggalTerima" class="form-input mt-1">
                </div>
                <div class="mb-4">
                    <label for="fileUpload" class="block text-sm font-medium text-gray-700">Unggah File</label>
                    <input type="file" id="fileUpload" class="form-input mt-1">
                </div>
            </div>

            <!-- Tombol Aksi -->
            <div class="md:col-span-2 flex justify-center gap-4 mt-4">
                <button type="button" id="btnSimpan" class="button button-primary">Simpan Data</button>
                <button type="button" id="btnReset" class="button button-secondary">Reset Formulir</button>
            </div>
        </form>

        <!-- Bagian Tabel untuk menampilkan data -->
        <div class="mt-12 table-container">
            <h2 class="text-xl font-bold text-gray-800 mb-4 text-center">Data Surat Masuk</h2>
            <table class="min-w-full divide-y divide-gray-200 rounded-lg overflow-hidden shadow-sm table-striped">
                <thead class="bg-gray-50">
                    <tr>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">No.</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Nomor Surat</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Asal Surat</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Tgl. Surat</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Perihal</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Kepada</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Disposisi Setda Asisten</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Disposisi Inspektur Sekretaris</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Disposisi Irban</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Nama TTD</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">Tgl. Diterima</th>
                        <th class="px-6 py-3 text-left text-xs font-bold text-gray-500 uppercase tracking-wider">File</th>
                    </tr>
                </thead>
                <tbody id="dataTableBody" class="bg-white divide-y divide-gray-200">
                    <!-- Data akan ditambahkan di sini oleh JavaScript -->
                </tbody>
            </table>
        </div>
    </div>

    <!-- Modal untuk menampilkan pesan error atau notifikasi lainnya -->
    <div id="messageModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full hidden">
        <div class="relative top-20 mx-auto p-5 border w-96 shadow-lg rounded-md bg-white">
            <div class="mt-3 text-center">
                <h3 class="text-lg leading-6 font-medium text-gray-900">Perhatian</h3>
                <div class="mt-2 px-7 py-3">
                    <p id="modalMessage" class="text-sm text-gray-500"></p>
                </div>
                <div class="items-center px-4 py-3">
                    <button id="closeModalButton" class="px-4 py-2 bg-blue-500 text-white text-base font-medium rounded-md w-full shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500">
                        OK
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const form = document.getElementById('formSurat');
            const btnSimpan = document.getElementById('btnSimpan');
            const btnReset = document.getElementById('btnReset');
            const fileUpload = document.getElementById('fileUpload');
            const dataTableBody = document.getElementById('dataTableBody');
            const perihalInput = document.getElementById('perihal');
            const btnSummarize = document.getElementById('btnSummarize');
            const summaryResult = document.getElementById('summaryResult');
            const summaryText = document.getElementById('summaryText');
            const btnSuggestSetda = document.getElementById('btnSuggestSetda');
            const btnSuggestInspektur = document.getElementById('btnSuggestInspektur');
            const btnSuggestIrban = document.getElementById('btnSuggestIrban');
            const disposisiSetdaInput = document.getElementById('disposisiSetda');
            const disposisiInspekturInput = document.getElementById('disposisiInspektur');
            const disposisiIrbanInput = document.getElementById('disposisiIrban');
            const messageModal = document.getElementById('messageModal');
            const modalMessage = document.getElementById('modalMessage');
            const closeModalButton = document.getElementById('closeModalButton');
            
            let dataSurat = [];
            const API_URL = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent';
            const API_KEY = ""; // Canvas will provide this

            // Function to show a custom modal message
            function showMessage(message) {
                modalMessage.textContent = message;
                messageModal.classList.remove('hidden');
            }

            // Function to close the modal
            closeModalButton.addEventListener('click', () => {
                messageModal.classList.add('hidden');
            });

            // Memuat data dari localStorage saat aplikasi pertama kali dibuka
            const storedData = localStorage.getItem('dataSurat');
            if (storedData) {
                dataSurat = JSON.parse(storedData);
                renderTable();
            }

            // Fungsi untuk merender tabel data
            function renderTable() {
                dataTableBody.innerHTML = ''; // Kosongkan tabel
                dataSurat.forEach((data, index) => {
                    const row = document.createElement('tr');
                    const fileName = data.file ? data.file.name : 'Tidak ada file';
                    const fileLink = data.file ? `<a href="${data.file.data}" download="${fileName}" class="text-blue-600 hover:text-blue-800 underline">Unduh File</a>` : 'Tidak ada file';
                    
                    row.innerHTML = `
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${index + 1}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${data.nomorSurat}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${data.pengirim}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${data.tanggalSurat}</td>
                        <td class="px-6 py-4 text-sm text-gray-500">${data.perihal}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${data.kepada}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${data.disposisiSetda}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${data.disposisiInspektur}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${data.disposisiIrban}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${data.namaTTD}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${data.tanggalTerima}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${fileLink}</td>
                    `;
                    dataTableBody.appendChild(row);
                });
            }

            // Fungsi untuk menyimpan data
            btnSimpan.addEventListener('click', () => {
                const reader = new FileReader();
                const file = fileUpload.files[0];

                // Memeriksa apakah file diunggah
                if (file) {
                    reader.onloadend = () => {
                        const data = {
                            nomorSurat: document.getElementById('nomorSurat').value,
                            pengirim: document.getElementById('pengirim').value,
                            tanggalSurat: document.getElementById('tanggalSurat').value,
                            perihal: document.getElementById('perihal').value,
                            kepada: document.getElementById('kepada').value,
                            disposisiSetda: document.getElementById('disposisiSetda').value,
                            disposisiInspektur: document.getElementById('disposisiInspektur').value,
                            disposisiIrban: document.getElementById('disposisiIrban').value,
                            namaTTD: document.getElementById('namaTTD').value,
                            tanggalTerima: document.getElementById('tanggalTerima').value,
                            file: {
                                name: file.name,
                                data: reader.result // Base64 string dari file
                            }
                        };
                        saveData(data);
                    };
                    reader.readAsDataURL(file);
                } else {
                    const data = {
                        nomorSurat: document.getElementById('nomorSurat').value,
                        pengirim: document.getElementById('pengirim').value,
                        tanggalSurat: document.getElementById('tanggalSurat').value,
                        perihal: document.getElementById('perihal').value,
                        kepada: document.getElementById('kepada').value,
                        disposisiSetda: document.getElementById('disposisiSetda').value,
                        disposisiInspektur: document.getElementById('disposisiInspektur').value,
                        disposisiIrban: document.getElementById('disposisiIrban').value,
                        namaTTD: document.getElementById('namaTTD').value,
                        tanggalTerima: document.getElementById('tanggalTerima').value,
                        file: null
                    };
                    saveData(data);
                }
            });

            function saveData(data) {
                // Validasi data
                if (Object.values(data).slice(0, 10).some(val => val === '')) {
                    showMessage('Mohon lengkapi semua data kecuali file!');
                    return;
                }
                
                dataSurat.push(data);
                localStorage.setItem('dataSurat', JSON.stringify(dataSurat));
                renderTable();
                resetForm();
            }

            // Fungsi untuk mereset formulir
            btnReset.addEventListener('click', () => {
                resetForm();
            });

            function resetForm() {
                form.reset();
                document.getElementById('tanggalTerima').valueAsDate = new Date();
                document.getElementById('nomorSurat').focus();
                summaryResult.classList.add('hidden');
                summaryText.textContent = '';
                disposisiSetdaInput.value = '';
                disposisiInspekturInput.value = '';
                disposisiIrbanInput.value = '';
            }

            // Mengisi tanggal saat ini secara default
            document.getElementById('tanggalTerima').valueAsDate = new Date();

            // === GEMINI API INTEGRATIONS ===

            // Function to generate content using Gemini API
            async function generateContent(prompt) {
                try {
                    const response = await fetch(`${API_URL}?key=${API_KEY}`, {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                        },
                        body: JSON.stringify({
                            contents: [{
                                parts: [{ text: prompt }]
                            }]
                        })
                    });

                    if (!response.ok) {
                        const error = await response.json();
                        throw new Error(`API Error: ${response.status} - ${error.error.message}`);
                    }

                    const result = await response.json();
                    return result.candidates[0].content.parts[0].text;
                } catch (error) {
                    console.error('Error calling Gemini API:', error);
                    showMessage('Terjadi kesalahan saat menghubungi layanan AI. Silakan coba lagi.');
                    return null;
                }
            }

            // Feature 1: Summarize Perihal
            btnSummarize.addEventListener('click', async () => {
                const perihal = perihalInput.value.trim();
                if (perihal === '') {
                    showMessage('Mohon masukkan perihal surat terlebih dahulu.');
                    return;
                }
                
                btnSummarize.innerHTML = `<span class="loading-spinner"></span> Merangkum...`;
                btnSummarize.disabled = true;

                const prompt = `Ringkas teks berikut dalam satu kalimat yang padat dan informatif:\n"${perihal}"`;
                const summary = await generateContent(prompt);

                btnSummarize.innerHTML = `Ringkas Perihal ✨`;
                btnSummarize.disabled = false;

                if (summary) {
                    summaryText.textContent = summary;
                    summaryResult.classList.remove('hidden');
                }
            });

            // Feature 2: Suggest Disposisi
            async function suggestDisposisi(targetRole, inputElement) {
                const perihal = perihalInput.value.trim();
                if (perihal === '') {
                    showMessage('Mohon masukkan perihal surat terlebih dahulu.');
                    return;
                }

                // Temporary loading state
                const originalText = inputElement.nextElementSibling.textContent;
                inputElement.nextElementSibling.innerHTML = `<span class="loading-spinner"></span> Menganalisis...`;
                inputElement.nextElementSibling.disabled = true;

                const prompt = `Berdasarkan perihal surat berikut: "${perihal}". Berikan satu kalimat disposisi singkat dan relevan untuk ${targetRole}. Jangan sertakan judul seperti "Untuk Setda Asisten" atau sejenisnya. Langsung berikan isi disposisi.`;
                const suggestion = await generateContent(prompt);

                // Restore button state
                inputElement.nextElementSibling.innerHTML = originalText;
                inputElement.nextElementSibling.disabled = false;

                if (suggestion) {
                    inputElement.value = suggestion.trim();
                }
            }

            btnSuggestSetda.addEventListener('click', () => suggestDisposisi('Setda Asisten', disposisiSetdaInput));
            btnSuggestInspektur.addEventListener('click', () => suggestDisposisi('Inspektur Sekretaris', disposisiInspekturInput));
            btnSuggestIrban.addEventListener('click', () => suggestDisposisi('Irban', disposisiIrbanInput));

        });
    </script>

</body>
</html>
