int merah[]  = {2, 5, 8, 11};
int kuning[] = {3, 6, 9, 12};
int hijau[]  = {4, 7, 10, 13};

void setup() {
  for (int i = 0; i < 4; i++) {
    pinMode(merah[i], OUTPUT);
    pinMode(kuning[i], OUTPUT);
    pinMode(hijau[i], OUTPUT);
  }
}

void loop() {
  for (int i = 0; i < 4; i++) {
    aktifkanSimpang(i);
  }
}


// SEMUA MERA
void setSemuaMerah() {
  for (int i = 0; i < 4; i++) {
    digitalWrite(merah[i], HIGH);
    digitalWrite(kuning[i], LOW);
    digitalWrite(hijau[i], LOW);
  }
}

// LOGIC PER SIMPANG
void aktifkanSimpang(int i) {

  // Default semua merah
  setSemuaMerah();

  // HIJAU 5 DETIK
  digitalWrite(merah[i], LOW);
  digitalWrite(hijau[i], HIGH);
  delay(5000);

  // KUNING KEDIP 3x (±2 detik)
  digitalWrite(hijau[i], LOW);

  for (int j = 0; j < 3; j++) {
    digitalWrite(kuning[i], HIGH);
    delay(333);
    digitalWrite(kuning[i], LOW);
    delay(333);
  }

  // BALIK MERAH LAGI
  digitalWrite(merah[i], HIGH);
}
