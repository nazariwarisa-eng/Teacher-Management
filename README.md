<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EduPulse - Bank Data & Integrasi Google Form</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome untuk Icon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-slate-50 font-sans text-slate-800 antialiased">

    <div class="flex h-screen overflow-hidden">
        
        <!-- SIDEBAR -->
        <aside class="w-64 bg-slate-900 text-slate-300 flex flex-col justify-between hidden md:flex border-r border-slate-800">
            <div>
                <!-- Logo & Brand -->
                <div class="h-16 flex items-center px-6 bg-slate-950 border-b border-slate-800">
                    <div class="flex items-center space-x-3">
                        <div class="bg-indigo-600 text-white p-2 rounded-lg shadow-md">
                            <i class="fa-solid fa-graduation-cap text-lg"></i>
                        </div>
                        <span class="text-xl font-bold tracking-wide text-white">EduPulse</span>
                    </div>
                </div>

                <!-- Menu Navigasi -->
                <nav class="p-4 space-y-1">
                    <a href="#dashboard" onclick="switchTab('dashboard')" id="nav-dashboard" class="flex items-center space-x-3 px-4 py-3 rounded-xl text-white bg-indigo-600 shadow-md font-medium transition-all">
                        <i class="fa-solid fa-chart-pie w-5"></i>
                        <span>Ringkasan Kelas</span>
                    </a>
                    <a href="#nilai" onclick="switchTab('nilai')" id="nav-nilai" class="flex items-center space-x-3 px-4 py-3 rounded-xl hover:bg-slate-800 hover:text-white transition-all text-slate-400 font-medium">
                        <i class="fa-solid fa-book-open w-5"></i>
                        <span>Bank Data & Nilai</span>
                    </a>
                    <a href="#integrasi" onclick="switchTab('integrasi')" id="nav-integrasi" class="flex items-center space-x-3 px-4 py-3 rounded-xl hover:bg-slate-800 hover:text-white transition-all text-slate-400 font-medium">
                        <i class="fa-solid fa-link w-5"></i>
                        <span>Sinkronisasi G-Form</span>
                    </a>
                    <a href="#kehadiran" onclick="switchTab('kehadiran')" id="nav-kehadiran" class="flex items-center space-x-3 px-4 py-3 rounded-xl hover:bg-slate-800 hover:text-white transition-all text-slate-400 font-medium">
                        <i class="fa-solid fa-calendar-check w-5"></i>
                        <span>Rekap Kehadiran</span>
                    </a>
                </nav>
            </div>

            <!-- User Info di Bawah Sidebar -->
            <div class="p-4 border-t border-slate-800 bg-slate-950/50">
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-full bg-indigo-500/20 text-indigo-400 flex items-center justify-center font-bold">
                        BU
                    </div>
                    <div>
                        <p class="text-sm font-semibold text-white">Budi Utomo, S.Pd</p>
                        <p class="text-xs text-slate-400">Guru Mata Pelajaran</p>
                    </div>
                </div>
            </div>
        </aside>

        <!-- KONTEN UTAMA -->
        <main class="flex-1 flex flex-col h-screen overflow-y-auto">
            
            <!-- Top Navbar -->
            <header class="h-16 bg-white border-b border-slate-200 flex items-center justify-between px-6 sticky top-0 z-20 shadow-xs">
                <div class="flex items-center space-x-4">
                    <h1 id="page-title" class="text-xl font-bold text-slate-800">Ringkasan Kelas</h1>
                </div>
                <div class="flex items-center space-x-4">
                    <select id="kelas-select" onchange="gantiKelas()" class="bg-slate-100 border border-slate-300 text-slate-700 text-sm rounded-lg px-3 py-2 font-medium focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                        <option value="X-IPA-1">Kelas X - IPA 1</option>
                        <option value="X-IPA-2">Kelas X - IPA 2</option>
                        <option value="XI-IPS-1">Kelas XI - IPS 1</option>
                    </select>
                </div>
            </header>

            <!-- Workspace Body -->
            <div class="p-6 md:p-8 space-y-6 max-w-7xl mx-auto w-full">

                <!-- TAB 1: DASHBOARD / RINGKASAN -->
                <div id="tab-dashboard" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                        <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-xs flex items-center justify-between">
                            <div>
                                <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Total Siswa</p>
                                <h3 id="stat-total-siswa" class="text-2xl font-bold text-slate-800 mt-1">32 Siswa</h3>
                            </div>
                            <div class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-xl flex items-center justify-center text-xl">
                                <i class="fa-solid fa-users"></i>
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-xs flex items-center justify-between">
                            <div>
                                <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Rata-Rata Kelas</p>
                                <h3 id="stat-rata-rata" class="text-2xl font-bold text-emerald-600 mt-1">82.4</h3>
                            </div>
                            <div class="w-12 h-12 bg-emerald-50 text-emerald-600 rounded-xl flex items-center justify-center text-xl">
                                <i class="fa-solid fa-chart-line"></i>
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-xs flex items-center justify-between">
                            <div>
                                <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Kehadiran Rata-Rata</p>
                                <h3 class="text-2xl font-bold text-blue-600 mt-1">96.5%</h3>
                            </div>
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-xl flex items-center justify-center text-xl">
                                <i class="fa-solid fa-user-check"></i>
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-xs flex items-center justify-between">
                            <div>
                                <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Status Sinkronisasi</p>
                                <h3 class="text-2xl font-bold text-purple-600 mt-1">Aktif</h3>
                            </div>
                            <div class="w-12 h-12 bg-purple-50 text-purple-600 rounded-xl flex items-center justify-center text-xl">
                                <i class="fa-solid fa-rotate"></i>
                            </div>
                        </div>
                    </div>

                    <!-- Panel Banner -->
                    <div class="bg-gradient-to-r from-indigo-900 to-slate-900 rounded-2xl p-6 text-white shadow-md flex flex-col md:flex-row items-center justify-between">
                        <div class="space-y-2 mb-4 md:mb-0">
                            <span class="bg-indigo-500/30 text-indigo-300 text-xs font-semibold px-3 py-1 rounded-full uppercase tracking-wide">Fitur Unggulan</span>
                            <h2 class="text-2xl font-bold">Sinkronisasi Otomatis Google Form</h2>
                            <p class="text-slate-300 text-sm max-w-2xl">
                                Bagikan link tugas via Google Form ke siswa. Begitu siswa mengumpulkan, Anda dapat langsung menarik datanya ke sistem ini untuk mengisi nilai Tugas 1 atau Tugas 2 secara otomatis!
                            </p>
                        </div>
                        <button onclick="switchTab('integrasi')" class="bg-white text-indigo-900 px-5 py-3 rounded-xl font-semibold shadow hover:bg-slate-100 transition whitespace-nowrap">
                            <i class="fa-solid fa-link mr-2"></i> Hubungkan G-Form
                        </button>
                    </div>
                </div>

                <!-- TAB 2: BANK DATA & NILAI -->
                <div id="tab-nilai" class="hidden space-y-6">
                    <div class="bg-white rounded-2xl border border-slate-200 shadow-xs overflow-hidden">
                        <div class="p-6 border-b border-slate-200 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                            <div>
                                <h3 class="text-lg font-bold text-slate-800">Daftar Nilai Siswa (<span id="label-kelas-aktif">X - IPA 1</span>)</h3>
                                <p class="text-sm text-slate-500">Nilai di bawah dapat diisi manual atau ditarik otomatis dari Google Form.</p>
                            </div>
                            <div class="flex items-center space-x-3">
                                <button onclick="tambahSiswaModal()" class="bg-indigo-600 hover:bg-indigo-700 text-white text-sm font-semibold px-4 py-2.5 rounded-xl transition shadow-xs flex items-center space-x-2">
                                    <i class="fa-solid fa-user-plus"></i>
                                    <span>Tambah Siswa</span>
                                </button>
                                <button onclick="simpanData()" class="bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-semibold px-4 py-2.5 rounded-xl transition shadow-xs flex items-center space-x-2">
                                    <i class="fa-solid fa-floppy-disk"></i>
                                    <span>Simpan</span>
                                </button>
                            </div>
                        </div>

                        <!-- Tabel Nilai -->
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="bg-slate-50 text-slate-600 text-xs font-bold uppercase tracking-wider border-b border-slate-200">
                                        <th class="py-4 px-6">No</th>
                                        <th class="py-4 px-6">Nama Siswa</th>
                                        <th class="py-4 px-6 text-center">Tugas 1 (G-Form)</th>
                                        <th class="py-4 px-6 text-center">Tugas 2</th>
                                        <th class="py-4 px-6 text-center">UTS</th>
                                        <th class="py-4 px-6 text-center">UAS</th>
                                        <th class="py-4 px-6 text-center">Nilai Akhir</th>
                                        <th class="py-4 px-6">Catatan Guru</th>
                                    </tr>
                                </thead>
                                <tbody id="tabel-nilai-body" class="divide-y divide-slate-200 text-sm">
                                    <!-- Dinamis -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- TAB 3: INTEGRASI GOOGLE FORM (BARU) -->
                <div id="tab-integrasi" class="hidden space-y-6">
                    <div class="bg-white rounded-2xl border border-slate-200 shadow-xs p-6 md:p-8 space-y-6">
                        <div>
                            <span class="bg-purple-100 text-purple-700 text-xs font-semibold px-3 py-1 rounded-full uppercase tracking-wide">Otomatisasi Nilai</span>
                            <h2 class="text-xl font-bold text-slate-800 mt-2">Sinkronisasi Google Form Tugas</h2>
                            <p class="text-sm text-slate-500 mt-1">
                                Masukkan link Google Form tugas atau tempel data respons kuis siswa. Sistem akan otomatis mencocokkan nama dan memasukkan nilainya ke kolom <strong>Tugas 1</strong>.
                            </p>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 pt-2">
                            <!-- Kolom Kiri: Input Link & Target -->
                            <div class="space-y-4 bg-slate-50 p-5 rounded-xl border border-slate-200">
                                <h3 class="font-bold text-slate-700 text-sm"><i class="fa-solid fa-link text-indigo-600 mr-2"></i> Konfigurasi Link Form</h3>
                                
                                <div>
                                    <label class="block text-xs font-semibold text-slate-600 mb-1">Link Google Form Tugas</label>
                                    <input type="text" id="gform-link" class="w-full bg-white border border-slate-300 rounded-xl px-4 py-2.5 text-sm focus:ring-2 focus:ring-indigo-500 focus:outline-none" placeholder="https://forms.gle/contohLinkTugas123">
                                </div>

                                <div>
                                    <label class="block text-xs font-semibold text-slate-600 mb-1">Pilih Kolom Nilai Tujuan</label>
                                    <select id="target-kolom-nilai" class="w-full bg-white border border-slate-300 rounded-xl px-4 py-2.5 text-sm focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                                        <option value="t1">Masukkan ke Tugas 1</option>
                                        <option value="t2">Masukkan ke Tugas 2</option>
                                    </select>
                                </div>

                                <div class="pt-2">
                                    <button onclick="simulasiTarikGForm()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-semibold py-3 rounded-xl transition shadow-xs flex items-center justify-center space-x-2">
                                        <i class="fa-solid fa-cloud-arrow-down"></i>
                                        <span>Tarik Data Nilai dari G-Form</span>
                                    </button>
                                </div>
                            </div>

                            <!-- Kolom Kanan: Status & Panduan -->
                            <div class="space-y-4 bg-indigo-50/50 p-5 rounded-xl border border-indigo-100 flex flex-col justify-between">
                                <div>
                                    <h3 class="font-bold text-indigo-900 text-sm mb-2"><i class="fa-solid fa-circle-info text-indigo-600 mr-2"></i> Informasi Cara Kerja</h3>
                                    <ul class="text-xs text-slate-600 space-y-2 list-disc pl-4">
                                        <li>Siswa mengerjakan tugas melalui link Google Form yang Anda bagikan di grup kelas.</li>
                                        <li>Pastikan di Google Form terdapat kolom isian <strong>"Nama Lengkap Siswa"</strong> yang sesuai dengan database nama di aplikasi ini.</li>
                                        <li>Tombol sinkronisasi di samping akan membaca respons jawaban siswa dan mengisikannya secara otomatis ke tabel nilai.</li>
                                    </ul>
                                </div>

                                <div id="log-sinkronisasi" class="bg-white p-3 rounded-lg border border-indigo-200 text-xs text-slate-500 hidden">
                                    <p class="font-semibold text-emerald-600"><i class="fa-solid fa-circle-check mr-1"></i> Berhasil Sinkronisasi!</p>
                                    <p id="log-detail" class="mt-1">Data 5 siswa dari kelas X-IPA-1 telah diperbarui nilainya.</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- TAB 4: REKAP KEHADIRAN -->
                <div id="tab-kehadiran" class="hidden space-y-6">
                    <div class="bg-white rounded-2xl border border-slate-200 shadow-xs p-6">
                        <h3 class="text-lg font-bold text-slate-800 mb-2">Rekapitulasi Kehadiran Kelas</h3>
                        <p class="text-sm text-slate-500 mb-6">Ringkasan total kehadiran siswa selama satu semester berjalan.</p>
                        
                        <div class="overflow-x-auto">
                            <table class="w-full text-left border-collapse">
                                <thead>
                                    <tr class="bg-slate-50 text-slate-600 text-xs font-bold uppercase tracking-wider border-b border-slate-200">
                                        <th class="py-3 px-4">Nama Siswa</th>
                                        <th class="py-3 px-4 text-center text-emerald-600">Hadir (H)</th>
                                        <th class="py-3 px-4 text-center text-blue-600">Sakit (S)</th>
                                        <th class="py-3 px-4 text-center text-amber-600">Izin (I)</th>
                                        <th class="py-3 px-4 text-center text-rose-600">Alpa (A)</th>
                                        <th class="py-3 px-4 text-center">Persentase</th>
                                    </tr>
                                </thead>
                                <tbody id="tabel-kehadiran-body" class="divide-y divide-slate-200 text-sm">
                                    <!-- Dimuat via JS -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

            </div>
        </main>
    </div>

    <!-- MODAL TAMBAH SISWA -->
    <div id="modal-tambah" class="fixed inset-0 bg-slate-900/50 backdrop-blur-xs hidden items-center justify-center z-50 p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-xl space-y-4">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="text-lg font-bold text-slate-800">Tambah Data Siswa Baru</h3>
                <button onclick="tutupModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div class="space-y-3">
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">Nama Lengkap Siswa</label>
                    <input type="text" id="input-nama-siswa" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-4 py-2.5 text-sm focus:ring-2 focus:ring-indigo-500 focus:outline-none" placeholder="Contoh: Siti Rahma">
                </div>
            </div>
            <div class="flex justify-end space-x-3 pt-4 border-t border-slate-100">
                <button onclick="tutupModal()" class="px-4 py-2 rounded-xl text-slate-600 hover:bg-slate-100 text-sm font-medium">Batal</button>
                <button onclick="simpanSiswaBaru()" class="px-5 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-sm font-semibold shadow-xs">Simpan</button>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // Database Mock Data per Kelas
        const databaseNilai = {
            "X-IPA-1": [
                { id: 1, nama: "Ahmad Fauzan", t1: 85, t2: 90, uts: 88, uas: 85, catatan: "Aktif di kelas" },
                { id: 2, nama: "Dewi Lestari", t1: 90, t2: 92, uts: 95, uas: 90, catatan: "Sangat teliti" },
                { id: 3, nama: "Fajar Nugraha", t1: 75, t2: 70, uts: 65, uas: 70, catatan: "Perlu tingkatkan latihan" },
                { id: 4, nama: "Rizky Ramadhan", t1: 80, t2: 85, uts: 82, uas: 80, catatan: "Disiplin" },
                { id: 5, nama: "Siti Aisyah", t1: 95, t2: 90, uts: 92, uas: 94, catatan: "Prestasi sangat baik" }
            ],
            "X-IPA-2": [
                { id: 1, nama: "Budi Santoso", t1: 78, t2: 80, uts: 75, uas: 77, catatan: "Cukup baik" },
                { id: 2, nama: "Citra Kirana", t1: 88, t2: 85, uts: 90, uas: 86, catatan: "Rajin mengumpulkan data" }
            ],
            "XI-IPS-1": [
                { id: 1, nama: "Joko Widodo", t1: 82, t2: 80, uts: 78, uas: 81, catatan: "Aktif berdiskusi" },
                { id: 2, nama: "Mega Puspita", t1: 90, t2: 94, uts: 91, uas: 92, catatan: "Sangat potensial" }
            ]
        };

        let kelasAktif = "X-IPA-1";

        // Fungsi Pindah Tab
        function switchTab(tabId) {
            ['dashboard', 'nilai', 'integrasi', 'kehadiran'].forEach(t => {
                document.getElementById('tab-' + t).classList.add('hidden');
                document.getElementById('nav-' + t).className = "flex items-center space-x-3 px-4 py-3 rounded-xl hover:bg-slate-800 hover:text-white transition-all text-slate-400 font-medium";
            });

            document.getElementById('tab-' + tabId).classList.remove('hidden');
            document.getElementById('nav-' + tabId).className = "flex items-center space-x-3 px-4 py-3 rounded-xl text-white bg-indigo-600 shadow-md font-medium transition-all";

            const titles = {
                'dashboard': 'Ringkasan Kelas',
                'nilai': 'Bank Data & Nilai Siswa',
                'integrasi': 'Sinkronisasi Google Form',
                'kehadiran': 'Rekapitulasi Kehadiran'
            };
            document.getElementById('page-title').innerText = titles[tabId];
        }

        // Ganti Kelas
        function gantiKelas() {
            kelasAktif = document.getElementById('kelas-select').value;
            document.getElementById('label-kelas-aktif').innerText = kelasAktif;
            renderTabelNilai();
            renderTabelKehadiran();
            hitungStatistik();
        }

        // Render Tabel Nilai
        function renderTabelNilai() {
            const tbody = document.getElementById('tabel-nilai-body');
            tbody.innerHTML = '';
            const data = databaseNilai[kelasAktif] || [];

            if(data.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="text-center py-6 text-slate-400">Belum ada data siswa untuk kelas ini.</td></tr>`;
                return;
            }

            data.forEach((siswa, index) => {
                let rata = Math.round((siswa.t1 + siswa.t2 + siswa.uts + siswa.uas) / 4);
                let badgeColor = rata >= 85 ? 'text-emerald-600 bg-emerald-50' : (rata >= 75 ? 'text-blue-600 bg-blue-50' : 'text-amber-600 bg-amber-50');

                let row = `
                    <tr class="hover:bg-slate-50/80 transition">
                        <td class="py-4 px-6 text-slate-500 font-medium">${index + 1}</td>
                        <td class="py-4 px-6 font-semibold text-slate-800">${siswa.nama}</td>
                        <td class="py-4 px-6 text-center"><input type="number" value="${siswa.t1}" onchange="updateNilai(${index}, 't1', this.value)" class="w-16 text-center bg-slate-50 border border-slate-200 rounded-lg py-1 focus:bg-white focus:ring-2 focus:ring-indigo-500 focus:outline-none"></td>
                        <td class="py-4 px-6 text-center"><input type="number" value="${siswa.t2}" onchange="updateNilai(${index}, 't2', this.value)" class="w-16 text-center bg-slate-50 border border-slate-200 rounded-lg py-1 focus:bg-white focus:ring-2 focus:ring-indigo-500 focus:outline-none"></td>
                        <td class="py-4 px-6 text-center"><input type="number" value="${siswa.uts}" onchange="updateNilai(${index}, 'uts', this.value)" class="w-16 text-center bg-slate-50 border border-slate-200 rounded-lg py-1 focus:bg-white focus:ring-2 focus:ring-indigo-500 focus:outline-none"></td>
                        <td class="py-4 px-6 text-center"><input type="number" value="${siswa.uas}" onchange="updateNilai(${index}, 'uas', this.value)" class="w-16 text-center bg-slate-50 border border-slate-200 rounded-lg py-1 focus:bg-white focus:ring-2 focus:ring-indigo-500 focus:outline-none"></td>
                        <td class="py-4 px-6 text-center"><span class="px-3 py-1 rounded-full font-bold text-xs ${badgeColor}">${rata}</span></td>
                        <td class="py-4 px-6"><input type="text" value="${siswa.catatan}" onchange="updateCatatan(${index}, this.value)" class="w-full bg-slate-50 border border-slate-200 rounded-lg px-3 py-1 text-xs focus:bg-white focus:ring-2 focus:ring-indigo-500 focus:outline-none" placeholder="Catatan..."></td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        // Render Tabel Kehadiran
        function renderTabelKehadiran() {
            const tbody = document.getElementById('tabel-kehadiran-body');
            tbody.innerHTML = '';
            const data = databaseNilai[kelasAktif] || [];

            data.forEach((siswa) => {
                let row = `
                    <tr class="hover:bg-slate-50/80 transition">
                        <td class="py-3 px-4 font-semibold text-slate-800">${siswa.nama}</td>
                        <td class="py-3 px-4 text-center font-medium text-emerald-600">28</td>
                        <td class="py-3 px-4 text-center font-medium text-blue-600">1</td>
                        <td class="py-3 px-4 text-center font-medium text-amber-600">1</td>
                        <td class="py-3 px-4 text-center font-medium text-rose-600">0</td>
                        <td class="py-3 px-4 text-center font-bold text-slate-700">96.6%</td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        // Hitung Statistik Dashboard
        function hitungStatistik() {
            const data = databaseNilai[kelasAktif] || [];
            document.getElementById('stat-total-siswa').innerText = data.length + " Siswa";
            
            if(data.length > 0) {
                let totalRata = 0;
                data.forEach(s => {
                    let rataSiswa = (s.t1 + s.t2 + s.uts + s.uas) / 4;
                    totalRata += rataSiswa;
                });
                let finalAvg = (totalRata / data.length).toFixed(1);
                document.getElementById('stat-rata-rata').innerText = finalAvg;
            } else {
                document.getElementById('stat-rata-rata').innerText = "0";
            }
        }

        // Simulasi Sinkronisasi Google Form
        function simulasiTarikGForm() {
            const link = document.getElementById('gform-link').value;
            const targetKolom = document.getElementById('target-kolom-nilai').value;

            if(!link) {
                alert('Silakan masukkan link Google Form terlebih dahulu!');
                return;
            }

            // Simulasi penarikan data otomatis nilai acak/sukses untuk kelas aktif
            const dataSiswa = databaseNilai[kelasAktif];
            dataSiswa.forEach(s => {
                // Berikan nilai random atau nilai tes dari gform (misal antara 80 - 98)
                let nilaiForm = Math.floor(Math.random() * (98 - 80 + 1)) + 80;
                s[targetKolom] = nilaiForm;
            });

            // Tampilkan log berhasil
            const logBox = document.getElementById('log-sinkronisasi');
            const logDetail = document.getElementById('log-detail');
            logBox.classList.remove('hidden');
            logDetail.innerText = `Berhasil menarik respons dari Google Form! Nilai ${dataSiswa.length} siswa di ${kelasAktif} telah dimasukkan ke kolom ${targetKolom.toUpperCase()}.`;

            // Refresh tampilan tabel nilai & statistik
            renderTabelNilai();
            hitungStatistik();

            setTimeout(() => {
                alert('Sinkronisasi Google Form berhasil! Silakan cek menu "Bank Data & Nilai" untuk melihat perubahan nilainya.');
            }, 300);
        }

        // Update Nilai secara Live
        function updateNilai(index, field, value) {
            databaseNilai[kelasAktif][index][field] = Number(value);
            renderTabelNilai();
            hitungStatistik();
        }

        function updateCatatan(index, value) {
            databaseNilai[kelasAktif][index].catatan = value;
        }

        // Modal Tambah Siswa
        function tambahSiswaModal() {
            document.getElementById('modal-tambah').classList.remove('hidden');
            document.getElementById('modal-tambah').classList.add('flex');
        }

        function tutupModal() {
            document.getElementById('modal-tambah').classList.remove('flex');
            document.getElementById('modal-tambah').classList.add('hidden');
            document.getElementById('input-nama-siswa').value = '';
        }

        function simpanSiswaBaru() {
            const nama = document.getElementById('input-nama-siswa').value;
            if(!nama) {
                alert('Nama siswa tidak boleh kosong!');
                return;
            }

            if(!databaseNilai[kelasAktif]) {
                databaseNilai[kelasAktif] = [];
            }

            databaseNilai[kelasAktif].push({
                id: databaseNilai[kelasAktif].length + 1,
                nama: nama,
                t1: 75,
                t2: 75,
                uts: 75,
                uas: 75,
                catatan: "Siswa baru"
            });

            tutupModal();
            renderTabelNilai();
            renderTabelKehadiran();
            hitungStatistik();
            alert('Siswa baru berhasil ditambahkan!');
        }

        function simpanData() {
            alert('Data nilai kelas ' + kelasAktif + ' berhasil disimpan permanen!');
        }

        window.onload = function() {
            renderTabelNilai();
            renderTabelKehadiran();
            hitungStatistik();
        };
    </script>
</body>
</html>
