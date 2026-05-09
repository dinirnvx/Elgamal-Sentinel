# 🚀 IoT MCP Project - Complete Guide

Sistem monitoring suhu & kelembaban dengan ESP32 + DHT11 yang terintegrasi dengan Gemini AI melalui Telegram.

---

## 📋 Fitur

✅ **Real-time Monitoring** - Suhu & kelembaban setiap 10 detik  
✅ **Gemini AI Integration** - Analisis data dengan AI  
✅ **Telegram Bot** - Interaksi via chat  
✅ **Alert System** - Notifikasi otomatis jika suhu abnormal  
✅ **Database SQLite** - History data tersimpan  
✅ **MCP Architecture** - Tools-based system  

---

## 🛠️ Hardware yang Dibutuhkan

- **ESP32** (1 unit)
- **DHT11** sensor (1 unit)
- **Kabel jumper** (3 pcs)
- **Breadboard** (optional)

### Koneksi Hardware

```
DHT11          ESP32
─────          ─────
VCC    ──────  3.3V
DATA   ──────  GPIO 15
GND    ──────  GND
```

---

## 💻 Software yang Dibutuhkan

- **Python 3.8+** (sudah terinstall)
- **Arduino IDE** (untuk upload code ke ESP32)
- **Telegram App** (di HP Anda)

---

## 📦 Struktur File

```
iot-mcp-complete/
├── .env                    # Konfigurasi (API keys, tokens)
├── server.py               # Main server
├── esp32_dht11.ino        # Arduino code untuk ESP32
├── README.md              # File ini
└── data/                  # Database (auto-created)
    └── sensor.db
```

---

## 🚀 Cara Install & Jalankan

### STEP 1: Persiapan Folder

```bash
cd C:\Users\THINKPAD\Desktop
mkdir iot-mcp-complete
cd iot-mcp-complete
mkdir data
```

### STEP 2: Download File

Download 3 file ini dan taruh di folder `iot-mcp-complete`:
1. `.env`
2. `server.py`
3. `esp32_dht11.ino`

### STEP 3: Install Python Dependencies

```bash
C:\Users\THINKPAD\AppData\Local\Python\pythoncore-3.14-64\python.exe -m pip install flask flask-cors google-generativeai requests python-dotenv
```

### STEP 4: Jalankan Server

```bash
cd C:\Users\THINKPAD\Desktop\iot-mcp-complete

C:\Users\THINKPAD\AppData\Local\Python\pythoncore-3.14-64\python.exe server.py
```

**Expected output:**
```
============================================================
🚀 IoT MCP Server with Gemini AI
============================================================
📡 Server IP: 192.168.92.30:5000
💬 Telegram Bot: 8455077735:AAFUibm...
🤖 Gemini API: AIzaSyBF67Wnhe-qs...
============================================================
✅ Gemini AI ready!
✅ Database ready!
🤖 Telegram bot listener started...

============================================================
✅ Server is running!
============================================================
🌐 Server URL: http://192.168.92.30:5000
📡 ESP32 endpoint: http://192.168.92.30:5000/api/sensor
🤖 Telegram: Listening for messages
📊 Database: data/sensor.db
============================================================
```

### STEP 5: Upload Code ke ESP32

1. Buka **Arduino IDE**
2. **File** → **Open** → Pilih `esp32_dht11.ino`
3. **Tools** → **Board** → Pilih **ESP32 Dev Module**
4. **Tools** → **Port** → Pilih port ESP32 Anda (COM3, COM4, dll)
5. Klik tombol **Upload** (panah kanan atas)
6. Tunggu sampai selesai upload
7. Buka **Serial Monitor** (Ctrl+Shift+M) → Set baud rate **115200**

**Expected output di Serial Monitor:**
```
================================
  IoT MCP Client with Gemini AI
================================
Server: 192.168.92.30:5000
================================

Initializing DHT11 sensor...
✅ DHT11 ready!

Connecting to WiFi: stl
...........
✅ WiFi connected!
IP Address: 192.168.92.XX

================================
Starting to send data...
================================

─────────────────────────────
📊 Temperature: 28°C
💧 Humidity   : 65%
─────────────────────────────
📤 Sending to server... ✅ SUCCESS!
Response: {"status":"success",...}
```

---

## 📱 Cara Menggunakan Telegram Bot

### Perintah Tersedia

```
/start      - Mulai & lihat bantuan
/suhu       - Lihat data suhu terkini
/stats      - Statistik 24 jam terakhir
/help       - Bantuan
```

### Contoh Interaksi

**1. Lihat Suhu Terkini:**
```
Anda: /suhu

Bot: 🌡️ DATA SENSOR TERKINI
     ✅ NORMAL
     
     Suhu: 28°C
     Kelembaban: 65%
     Device: ESP32_DHT11_RUANGAN
     Waktu: 2024-02-03 15:30:00
```

**2. Lihat Statistik:**
```
Anda: /stats

Bot: 📊 STATISTIK 24 JAM TERAKHIR
     
     🌡️ Suhu:
     • Rata-rata: 27.3°C
     • Terendah: 24.1°C
     • Tertinggi: 31.2°C
     
     💧 Kelembaban:
     • Rata-rata: 62.5%
     • Terendah: 55%
     • Tertinggi: 70%
     
     📈 Total data: 144 readings
```

**3. Tanya Bebas dengan AI:**
```
Anda: Berapa suhu sekarang?

Bot: ⏳ Menganalisis dengan AI...

Bot: Berdasarkan data sensor terkini, 
     suhu saat ini adalah 28°C dengan 
     kelembaban 65%. Suhu dalam kondisi 
     normal dan nyaman untuk aktivitas 
     di dalam ruangan.
```

```
Anda: Kenapa suhu naik siang hari?

Bot: Kenaikan suhu di siang hari adalah 
     hal yang wajar karena intensitas 
     sinar matahari lebih tinggi. Jika 
     sensor berada di dalam ruangan, 
     pastikan tidak terkena sinar langsung 
     dan ventilasi udara cukup baik.
```

---

## 🔧 Troubleshooting

### Problem 1: WiFi tidak connect di ESP32

**Symptoms:**
```
Connecting to WiFi: stl
.......................
❌ WiFi connection failed!
```

**Solution:**
1. Cek SSID benar: `stl`
2. Cek password benar: `12345678`
3. Pastikan router WiFi menyala
4. Pastikan ESP32 dalam jangkauan WiFi

---

### Problem 2: Server tidak terima data dari ESP32

**Symptoms:**
```
📤 Sending to server... ❌ Connection failed!
```

**Solution:**
1. Pastikan server Python sedang running
2. Cek IP laptop dengan `ipconfig` → harus `192.168.92.30`
3. Jika IP berbeda, ganti di file `.ino` baris:
   ```cpp
   const char* SERVER_URL = "http://192.168.92.30:5000/api/sensor";
   ```
4. Pastikan ESP32 dan laptop di WiFi yang sama

---

### Problem 3: Telegram bot tidak respond

**Symptoms:**
- Kirim `/suhu` tidak ada balasan

**Solution:**
1. Cek server Python masih running
2. Cek internet connection
3. Restart server Python
4. Kirim `/start` dulu untuk reset bot

---

### Problem 4: DHT11 baca error

**Symptoms:**
```
❌ DHT11 read failed!
```

**Solution:**
1. Cek koneksi kabel:
   - VCC → 3.3V
   - DATA → GPIO 15
   - GND → GND
2. Pastikan DHT11 tidak rusak
3. Coba ganti ke pin lain (update di code)

---

### Problem 5: Gemini AI error

**Symptoms:**
```
❌ Maaf, terjadi error: 429 Resource Exhausted
```

**Solution:**
1. API quota habis (free tier limit)
2. Tunggu 1 menit
3. Coba lagi

---

## 📊 Arsitektur Sistem

```
┌──────────────┐
│   ESP32      │
│   DHT11      │  ← Baca suhu & kelembaban setiap 10 detik
└──────┬───────┘
       │
       │ HTTP POST (JSON)
       ▼
┌──────────────────────┐
│   LAPTOP/PC          │
│   Python Server      │
│   (server.py)        │
│                      │
│   Components:        │
│   • Flask API        │  ← Terima data dari ESP32
│   • SQLite DB        │  ← Simpan history
│   • Gemini AI        │  ← Analisis data
│   • Telegram Bot     │  ← Kirim notifikasi & chat
└──────┬───────────────┘
       │
       │ Telegram Bot API
       ▼
┌─────────────┐
│ TELEGRAM    │
│ (HP Anda)   │  ← Interaksi dengan user via chat
└─────────────┘
```

---

## 🔐 Keamanan

**PENTING:** File `.env` berisi API keys dan tokens yang **sensitif**!

**Jangan:**
- ❌ Upload ke GitHub public
- ❌ Share ke orang lain
- ❌ Screenshot dengan API key visible

**Sebaiknya:**
- ✅ Tambahkan `.env` ke `.gitignore`
- ✅ Regenerate API key jika tercopy orang lain
- ✅ Gunakan environment variables

---

## 📈 Fitur Lanjutan (Opsional)

### 1. Tambah Sensor Lain

Edit `esp32_dht11.ino`, tambahkan sensor baru:
```cpp
#define LDR_PIN 34
int lightLevel = analogRead(LDR_PIN);
```

### 2. Kirim Email Alert

Edit `server.py`, tambahkan SMTP:
```python
import smtplib
# ... kirim email saat suhu tinggi
```

### 3. Web Dashboard

Buat file `dashboard.html` untuk visualisasi grafik real-time.

---

## 📞 Support

Jika ada masalah atau pertanyaan:

1. Cek troubleshooting section di atas
2. Lihat Serial Monitor ESP32 untuk log error
3. Lihat output server Python untuk error log

---

## 📜 License

MIT License - Free to use for educational purposes

---

## 🎓 Credits

- **MCP Architecture** - Model Context Protocol
- **Gemini AI** - Google AI
- **Telegram Bot API** - Telegram
- **ESP32** - Espressif Systems
- **DHT11** - Aosong Electronics

---

**Selamat mencoba! 🚀**
