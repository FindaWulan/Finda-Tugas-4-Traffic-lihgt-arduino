# Finda-Tugas-4-Traffic-lihgt-arduino
# Simulasi Lampu Lalu Lintas 4 Simpang (Arduino)

Proyek ini adalah simulasi sistem kendali lampu lalu lintas untuk perempatan jalan (4 simpang: Utara, Timur, Selatan, Barat) menggunakan Arduino Uno. Simulasi ini dibuat menggunakan platform **Tinkercad**.

# Daftar Isi
- [Komponen](#komponen)
- [Skema Rangkaian (Wiring)](#skema-rangkaian-wiring)
- [Fitur Utama](#fitur-utama)
- [Cara Kerja](#cara-kerja)
- [Penjelasan Kode (Source Code)](#penjelasan-kode-source-code)

---

# Komponen
| Komponen | Jumlah |
| Arduino Uno R3 | 1 |
| LED (Merah, Kuning, Hijau) | 12 (4 per warna) |
| Resistor 220Ω | 12 |
| Breadboard | 1 |
| Kabel Jumper | Secukupnya |

---

# Skema Rangkaian (Wiring)
Semua LED menggunakan konfigurasi **Common Ground** (Katoda terhubung ke GND Arduino). Anoda (+) setiap LED terhubung ke pin digital melalui resistor 220 Ohm.

**Alokasi Pin:**
- **Utara:** Merah (2), Kuning (3), Hijau (4)
- **Timur:** Merah (5), Kuning (6), Hijau (7)
- **Selatan:** Merah (8), Kuning (9), Hijau (10)
- **Barat:** Merah (11), Kuning (12), Hijau (13)

---

# Fitur Utama
1. **Array Based:** Menggunakan array untuk pengelolaan pin yang lebih ringkas.
2. **Safe Mode:** Fungsi `setSemuaMerah()` memastikan tidak ada bentrokan hijau antar simpang.
3. **Realistic Yellow:** Lampu kuning berkedip (blink) sebagai peringatan sebelum kembali ke merah.

---

## 🔄 Cara Kerja
1. Sistem akan menjalankan simpang secara berurutan: **Utara -> Timur -> Selatan -> Barat**.
2. Saat satu simpang aktif (Hijau), tiga simpang lainnya dipaksa dalam kondisi Merah.
3. Durasi Lampu Hijau: **5 Detik**.
4. Durasi Lampu Kuning: **2 Detik** (dengan efek kedip 3x).

---

## 💻 Penjelasan Kode (Source Code)
// Definisi PIN untuk setiap warna (Indeks: 0=Utara, 1=Timur, 2=Selatan, 3=Barat)
int merah[]  = {2, 5, 8, 11}; 
int kuning[] = {3, 6, 9, 12};
int hijau[]  = {4, 7, 10, 13};

void setup() {
  // Loop untuk mengatur semua 12 pin menjadi OUTPUT secara otomatis
  for (int i = 0; i < 4; i++) {
    pinMode(merah[i], OUTPUT);
    pinMode(kuning[i], OUTPUT);
    pinMode(hijau[i], OUTPUT);
  }
}

void loop() {
  // Menjalankan fungsi aktifkanSimpang untuk indeks 0 sampai 3 secara berurutan
  for (int i = 0; i < 4; i++) {
    aktifkanSimpang(i);
  }
}

// Fungsi untuk me-reset semua lampu ke kondisi aman (Merah menyala)
void setSemuaMerah() {
  for (int i = 0; i < 4; i++) {
    digitalWrite(merah[i], HIGH);  // Semua Merah NYALA
    digitalWrite(kuning[i], LOW);   // Semua Kuning MATI
    digitalWrite(hijau[i], LOW);    // Semua Hijau MATI
  }
}

// Logika kendali untuk satu simpang yang sedang mendapat giliran jalan
void aktifkanSimpang(int i) {
  setSemuaMerah();                 // Reset semua ke Merah dulu

  // FASE HIJAU
  digitalWrite(merah[i], LOW);     // Matikan lampu merah di simpang aktif
  digitalWrite(hijau[i], HIGH);    // Nyalakan lampu hijau
  delay(5000);                     // Tunggu 5 detik

  // FASE KUNING (KEDIP)
  digitalWrite(hijau[i], LOW);     // Matikan lampu hijau
  for (int j = 0; j < 3; j++) {    // Ulangi 3 kali:
    digitalWrite(kuning[i], HIGH); // Kuning Nyala
    delay(333);                    // Tunggu 0.3 detik
    digitalWrite(kuning[i], LOW);  // Kuning Mati
    delay(333);                    // Tunggu 0.3 detik
  }

  // KEMBALI KE MERAH
  digitalWrite(merah[i], HIGH);    // Nyalakan kembali merah sebelum pindah simpang
}

link tinkercad : https://www.tinkercad.com/things/knCZ7SrjtzU-mighty-bombul-uusam/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard

Nama: Finda Wulan Febrianti 
NIM H1H024055

