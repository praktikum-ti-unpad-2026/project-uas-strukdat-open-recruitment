# Dungeon Escape

> *Sebuah game labirin berbasis terminal yang menantang logika, strategi, dan refleks pemain untuk menemukan jalan keluar dari penjara bawah tanah yang penuh bahaya.*

---

## Latar Belakang

Dalam dunia pengembangan perangkat lunak, pemahaman terhadap struktur data bukan hanya sekadar teori — ia adalah fondasi dari setiap sistem yang efisien dan responsif. Namun, konsep seperti **Graph**, **Stack**, **Queue**, **Linked List**, dan **Tree** seringkali terasa abstrak dan sulit dipahami hanya melalui pembelajaran konvensional.

**Dungeon Escape** hadir sebagai solusi: sebuah game dungeon berbasis labirin yang mengintegrasikan struktur data secara langsung ke dalam mekanisme permainan. Pemain tidak hanya bermain — mereka secara tidak langsung *merasakan* bagaimana struktur data bekerja di balik layar.

Permasalahan yang diangkat:
- Sulitnya visualisasi konsep struktur data secara konkret dan menarik
- Minimnya media pembelajaran interaktif yang menggabungkan teori dan praktik
- Kurangnya motivasi belajar struktur data pada mahasiswa/pelajar pemrograman

---

## Tujuan dan Manfaat

### Tujuan
- Membangun game labirin yang fungsional dengan mekanisme gameplay berbasis struktur data nyata
- Mengimplementasikan Graph, Stack, Queue, Linked List, dan Binary Tree dalam konteks permainan yang kohesif
- Menyajikan pengalaman bermain yang menantang sekaligus edukatif

### Manfaat
| Manfaat | Deskripsi |

|    Edukatif   | Pemain memahami cara kerja struktur data melalui gameplay langsung |

|    Kognitif   | Melatih kemampuan berpikir logis dan strategi melalui navigasi labirin |

|    Teknis     | Demonstrasi nyata penerapan struktur data dalam proyek perangkat lunak |

|    Hiburan    | Pengalaman bermain yang menarik dengan sistem enemy, trap, dan inventory |

---

##  Penjelasan Aplikasi

**Dungeon Escape** adalah game berbasis terminal (CLI) di mana pemain berperan sebagai petualang yang terperangkap di dalam penjara bawah tanah. Tujuan utama adalah menemukan jalan keluar labirin sambil menghindari musuh, menjebak trap, dan mengelola item inventory.

### Fitur Utama

####  Sistem Labirin — *Graph*
- Setiap ruangan direpresentasikan sebagai **node** dalam graph
- Jalur antar ruangan sebagai **edge** (bisa satu atau dua arah)
- Pemain bisa menjelajahi ruangan yang saling terhubung secara bebas

####  Backtracking & Riwayat — *Stack*
- Pemain dapat **undo** langkah terakhir dengan menekan perintah `undo`
- Sistem menyimpan **riwayat perjalanan** secara LIFO (Last In, First Out)
- Backtracking otomatis ketika pemain menemui jalan buntu

####  Pergerakan Musuh & Event — *Queue*
- Enemy bergerak menggunakan sistem **antrian (FIFO)** — enemy yang lebih dulu muncul lebih dulu bergerak
- Event seperti trap dan jebakan diproses secara berurutan melalui Queue
- Simulasi giliran yang adil dan terprediksi

####  Sistem Inventory — *Linked List*
- Item yang dikumpulkan pemain tersimpan dalam **Linked List dinamis**
- Penambahan dan penghapusan item O(1) di head/tail
- Mendukung operasi: ambil item, gunakan item, buang item

####  Sistem Upgrade & Keputusan — *Binary Tree*
- Percabangan jalan di labirin dimodelkan sebagai **Binary Tree** (kiri atau kanan)
- Sistem upgrade skill/item menggunakan struktur pohon
- Decision tree untuk interaksi NPC dan pilihan cerita

### Pemetaan Struktur Data

```
Dungeon Escape
├── Graph       → Peta labirin (node = ruangan, edge = jalur)
├── Stack       → Undo langkah & backtracking
├── Queue       → Giliran enemy & antrian event/trap
├── Linked List → Inventory item pemain
└── Binary Tree → Percabangan jalan & sistem upgrade
```

---

## Gambaran Awal Rancangan Antarmuka

### 1. Layar Utama (Main Menu)

```
╔══════════════════════════════════════════════════════╗
║                                                      ║
║                  ═══ ESCAPE ═══                      ║
║                                                      ║
║              [ 1 ] New Game                          ║
║              [ 2 ] Load Game                         ║
║              [ 3 ] How to Play                       ║
║              [ 4 ] Exit                              ║
║                                                      ║
║          "Find the exit... if you dare."             ║
╚══════════════════════════════════════════════════════╝
```

### 2. Layar Gameplay Utama

```
╔══════════════════╦═══════════════════════════════════╗
║  MAP OVERVIEW    ║  CURRENT ROOM: Chamber of Shadows ║
║                  ╠═══════════════════════════════════╣
║  [?]─[?]─[ ]     ║                                   ║
║   │       │      ║   You stand in a dimly lit room.  ║
║  [★]─[!]─[X]     ║   The air smells of damp stone.  ║
║   │              ║   You hear footsteps nearby...    ║
║  [E]─[?]─[?]     ║                                   ║
║                  ╠═══════════════════════════════════╣
║  ★ = You here    ║  EXITS:  [N] North  [E] East      ║
║  E = Exit        ║          [S] Blocked              ║
║  ! = Danger      ╠═══════════════════════════════════╣
║  ? = Unknown     ║  > _                              ║
╠══════════════════╩═══════════════════════════════════╣
║ HP: ████████░░  20/25  │  STEPS: 14  │  SCORE: 320   ║
╚══════════════════════════════════════════════════════╝
```

### 3. Panel Inventory (Linked List View)

```
╔══════════════════════════════════════════════════════╗
║                     INVENTORY                        ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  HEAD →  [Health Potion] → [Iron Key] → [Torch] → ∅  ║
║                                                      ║
╠══════════════════════════════════════════════════════╣
║  [U] Use Item    [D] Drop Item    [ESC] Close        ║
╚══════════════════════════════════════════════════════╝
```

### 4. Layar Skill/Upgrade Tree (Binary Tree)

```
╔══════════════════════════════════════════════════════╗
║                  SKILL UPGRADE TREE                  ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║                   [Combat Arts]                      ║
║                  /             \                     ║
║           [Sword Mastery]   [Shield Wall]            ║
║            /        \                   \            ║
║      [Slash+2]  [Critical Hit]      [Block+3]        ║
║                                                      ║
╠══════════════════════════════════════════════════════╣
║  Skill Points: 3    [ENTER] Select    [ESC] Back     ║
╚══════════════════════════════════════════════════════╝
```

### 5. Layar Enemy Encounter (Queue System)

```
╔══════════════════════════════════════════════════════╗
║                  ENEMY ENCOUNTER!                    ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Enemy Queue:  [Goblin]  → [Skeleton] → [Orc] → ...  ║
║                                                      ║
║  NOW FIGHTING:    Goblin  (HP: 8/10)                 ║
║  YOUR HP:      ████████░░ (20/25)                    ║
║                                                      ║
╠══════════════════════════════════════════════════════╣
║  [A] Attack  [D] Defend  [R] Run  [I] Use Item       ║
╚══════════════════════════════════════════════════════╝
```

### 6. Layar Game Over / Victory

```
╔══════════════════════════════════════════════════════╗
║                                                      ║
║                  YOU ESCAPED!                        ║
║                                                      ║
║         ════════════════════════════                 ║
║              FINAL STATISTICS                        ║
║         ════════════════════════════                 ║
║                                                      ║
║   Total Steps     :  47                              ║
║   Enemies Defeated:   5                              ║
║   Items Collected :   8                              ║
║   Rooms Explored  :  12 / 18                         ║
║   Final Score     :  1,250 pts                       ║
║                                                      ║
║         ════════════════════════════                 ║
║                                                      ║
║          [ R ] Play Again    [ Q ] Quit              ║
╚══════════════════════════════════════════════════════╝
```

---

## Teknologi yang Digunakan

- **Bahasa**: C++
- **Antarmuka**: Terminal / CLI
- **Tools**: VS Code / Dev C++, GitHub

---

##  Rancangan Pengerjaan Proyek

Proyek ini dikerjakan oleh **2 orang anggota yaitu Rafi Abdul Hikam dan Raffa Pasha Hidayat** dengan pendekatan pembagian berdasarkan lapisan sistem: satu anggota fokus pada **core engine & struktur data**, dan satu anggota fokus pada **gameplay & antarmuka**. Keduanya saling berkoordinasi agar setiap komponen dapat terintegrasi dengan baik.

### Pembagian Tugas

| Komponen | Rafi (Backend & Engine) | Raffa (Gameplay & UI) |
|---|---|---|
| Graph (peta labirin) |  Implementasi struktur & algoritma BFS/DFS | Desain layout ruangan & koneksi jalur |
| Stack (backtracking) |  Implementasi push/pop & undo sistem | Integrasi dengan input pemain |
| Queue (enemy & event) | Implementasi antrian musuh & trap | Desain pola gerakan & spawn enemy |
| Linked List (inventory) |  Implementasi node & operasi list | Desain UI tampilan inventory |
| Binary Tree (upgrade/keputusan) |  Implementasi tree & traversal | Desain konten skill & percabangan cerita |
| Main loop & game state |  Mengelola alur permainan utama | Mengelola input/output & tampilan layar |
| Testing & debugging | Bersama | Bersama |
| Dokumentasi & README | Bersama | Bersama |

### Alur Koordinasi

```
Minggu 1: Perencanaan & Desain
├── [Berdua]  Finalisasi fitur dan struktur data yang digunakan
├── [Berdua]  Menentukan format data antar modul (struct, class)
└── [Berdua]  Setup repository GitHub & struktur folder proyek

Minggu 2–3: Implementasi Inti
├── [Rafi]  Implementasi Graph, Stack, Queue, Linked List, Binary Tree
└── [Raffa]  Implementasi sistem input, tampilan CLI, dan loop game

Minggu 4: Integrasi & Gameplay
├── [Berdua]  Menggabungkan modul backend dengan frontend CLI
├── [Rafi]  Optimasi performa & logika struktur data
└── [Raffa]  Penyempurnaan UI, spawn enemy, dan sistem skor

Minggu 5: Testing & Finalisasi
├── [Berdua]  Uji coba gameplay end-to-end & perbaikan bug
├── [Berdua]  Melengkapi dokumentasi & komentar kode
└── [Berdua]  Persiapan presentasi
```

### Alat Koordinasi

- **GitHub** — version control, branching per fitur, pull request untuk review kode
- **WhatsApp** — komunikasi harian & diskusi cepat
