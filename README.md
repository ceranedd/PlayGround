# Jalan Kabut — Chronicles of the Verdant Realm

**Prototipe playable Wuxia action-RPG · Bab I: Jalur Cemara**

Jalan Kabut adalah IP orisinal tentang para pengembara di Provinsi Qinghe. Identitasnya berpusat pada ilmu yang diwariskan lewat laku, reputasi yang dibentuk oleh tindakan, dan pertarungan yang menekankan jarak, timing, serta pilihan aliran. Ini bukan remake: nama, dunia, karakter, visual, dan implementasi dibuat mandiri.

## Mainkan

Buka `index.html` pada browser modern atau jalankan server statis dari root proyek, misalnya `python3 -m http.server 8000`, lalu kunjungi `http://localhost:8000`.

- Klik **Mulai Perjalanan**.
- **WASD / tombol panah** bergerak, **J** menyerang, **F** memakai jurus Tapak Awan (18 Qi), **Space** dash, **E** bicara.
- Tombol di HUD membuka peta, jurnal, dan perguruan. Pada layar sentuh tersedia joystick dan tombol serang/jurus/dash.
- Dekati Guru Shen di dusun, kalahkan tiga bandit di jalur utara, lalu kembali untuk menuntaskan tugas.

Ini vertical slice 2D berbasis Canvas yang bisa langsung dimainkan tanpa instalasi, aset eksternal, atau backend. Pertarungan, musuh, quest, Qi/health, minimap, suasana, kontrol keyboard/touch, dan UI adalah implementasi nyata; multiplayer, persistensi akun, crafting penuh, dan dunia luas belum dibuat. Prototipe tidak menyimpan progres setelah halaman ditutup.

## 1. Konsep & pilar desain

**Genre:** third-person action martial-arts RPG dengan aspirasi MMORPG. **Pemain:** pengembara tanpa perguruan yang tiba di Qinghe. **Fantasi inti:** menjadi ahli silat lewat latihan dan pengalaman, bukan sekadar menaikkan angka level.

Pilar yang menjadi pagar scope:

1. **Pertarungan terbaca dan responsif** — telegraph jelas, parry/dash memberi jawaban, skill punya biaya dan cooldown.
2. **Dunia bereaksi** — reputasi, kriminalitas, rutinitas NPC, serta konflik perguruan punya konsekuensi yang terlihat.
3. **Kemajuan horizontal** — mastery, teknik, gear, dan hubungan membuka opsi, bukan membuat angka damage terus tak terkendali.
4. **Dunia persilatan yang berakar** — tempat, dialog, silat, dan simbol visual baru; inspirasi genre umum, bukan salinan IP lain.
5. **Scope kecil dahulu** — satu area yang selesai dan menyenangkan sebelum menambah konten atau pemain serentak.

## 2. Mekanik inti

Loop sesi: **jelajah → amati ancaman / rutinitas → bertarung atau berinteraksi → dapatkan bahan/reputasi/mastery → pilih latihan atau kerajinan → buka pilihan baru**.

- **Kontrol:** gerak analog/keyboard, dash, serangan ringan, jurus Qi, interaksi kontekstual.
- **Senjata (rencana):** pedang (seimbang), dao (tekanan), tombak (jangkauan), tongkat (kontrol), tangan kosong (counter), senjata rahasia (jarak/utility). Tiap senjata menggunakan moveset dan animasi sendiri.
- **Neigong:** resource untuk jurus, stance, dan teknik pasif; regenerasi/risiko dikendalikan stance serta keadaan bertarung.
- **Qinggong:** dash saat ini adalah placeholder gerak. Versi selanjutnya menambahkan lompatan, vault, wall-run terbatas, stamina dan validasi server.
- **Counter/parry:** sistem target: input dalam jendela telegraph musuh memotong serangan dan membuka punish singkat. Hindari auto-target yang menghilangkan positioning.
- **Kehidupan:** gathering, masak, smithing, tailoring, medicine, fishing dan trading dimasukkan setelah combat + satu loop ekonomi terbukti.

## 3. Dunia & lore

**Provinsi Qinghe** adalah provinsi perbatasan yang hidup dari jalur dagang di kaki Pegunungan Giok. Kabut musim semi mengganggu perjalanan; tiga bandit di Jalur Cemara adalah krisis kecil yang memperkenalkan dunia dan Guru Shen. Biara Awan Hening, Paviliun Pedang, Aula Emei, serta Pengembara Sungai adalah nama fiksi orisinal dalam setting ini.

### Peta roadmap

- **Jalur Cemara (vertical slice):** dusun, jalur dagang, tutorial, bandit, Guru Shen.
- **Hutan Seribu Pinus:** gathering, gua/dungeon kecil, event cuaca dan elite.
- **Dusun & Dermaga Qinghe:** pasar pemain tahap lanjut, fishing, life skills, rumah.
- **Biara Awan Hening / Paviliun Pedang:** quest perguruan, mentor, teknik unik.
- **Pegunungan Giok:** ekspedisi, world event dan boss setelah combat/netcode stabil.

Satu zona awal harus kecil, padat, punya landmark navigasi, encounter singkat, serta jalur kembali yang bermakna. Tambahkan waktu dinamis dan cuaca sebagai modul simulasi setelah kebutuhan streaming dan server dipahami.

## 4. Combat & progression

**Target combat:** lock-on opsional; arah serangan terlihat; recovery dan stamina membuat keputusan penting; musuh punya telegraph; hitbox konsisten. Aksi yang mengubah state (serangan, dodge, skill, parry) diproses server dalam MMORPG. Client hanya memprediksi gerak kosmetik/respons cepat.

**Progression:** tidak ada keharusan level karakter sebagai gerbang utama. Track terpisah: (a) atribut dasar dan kondisi, (b) mastery per weapon/technique dari penggunaan, (c) skill tree/talent dengan trade-off, (d) cultivation/neigong membuka gaya bermain, (e) gear dengan sifat situasional, (f) reputasi perguruan/faksi. Batasi bonus stat agar PvP tetap sehat; berikan scaling/gear normalization untuk duel dan perang.

Prototype saat ini hanya memiliki HP, Qi, satu jurus, basic attack, dash, dan satu quest. Ini sengaja merupakan vertical slice mekanik, bukan klaim bahwa sistem MMORPG lengkap sudah tersedia.

## 5. Rekomendasi engine & tim

**Rekomendasi untuk tim kecil yang menarget PC + mobile: Unity LTS, C#**, karena build multi-platform, toolchain animasi/asset, profiling mobile, dan ekosistem server/client luas. Jaga core gameplay independen dari vendor agar opsi dedicated server tetap terbuka. Alternatif: **Godot 4** untuk tim kecil dengan kemampuan engineering kuat dan prioritas biaya/kontrol; evaluasi kebutuhan dedicated-server, tooling produksi, dan pipeline konten sebelum mengunci.

Web Canvas yang ada adalah prototipe distribusi cepat, bukan fondasi MMO 3D. Jangan memindahkan networking persisten ke browser atau menjadikan client otoritatif.

Tim awal realistis: 1 gameplay/generalist programmer, 1 technical artist/3D generalist, 1 designer/producer, 1 backend/network engineer (paruh waktu pada awalnya), QA/playtest internal. Scope art harus mendukung modular reuse; outsource hanya setelah style guide dan ukuran aset terkunci.

## 6. Arsitektur MMORPG (tahap online)

Mulai dari **single-player prototype**, lalu dua client dalam satu arena, baru zonal MMO. Bentuk akhir: client tipis; gateway/auth; service akun dan karakter; world/zone servers authoritative; persistence service; chat/social; match/instance service; admin/telemetry. Pisahkan simulasi zona dan service ekonomi/akun agar kegagalan satu tidak menjatuhkan semua shard. Mulai satu region dan satu zone server sebelum autoscaling.

```text
[Unity PC/Mobile]
   ├── HTTPS: Auth / Character / Inventory / Marketplace
   └── UDP reliable sequenced: Gateway → Zone server (authoritative combat/movement)
                                  ├── PostgreSQL (akun, karakter, inventory, ekonomi)
                                  ├── Redis (presence, cache, rate limit; bukan sumber kebenaran)
                                  └── Event queue → telemetry / audit / analytics
```

Gunakan fixed simulation tick (mis. 20 Hz untuk zona), snapshot/interpolation, server-side movement/combat validation, sequence number, reconnect token, rate limit, dan interest management per area. Jangan kirim seluruh dunia ke setiap client. Chat dan transaksi punya jalur terpisah serta audit. Hindari microservices dini: modular monolith + zone process lebih hemat operasional sampai metrik membenarkan pemisahan.

**Keamanan dasar:** server authoritative untuk posisi final, cooldown, damage, loot, crafting, transaksi, dan reputasi; validasi input; idempotency key untuk ekonomi; log transaksi append-only; backup dan migration test. Jangan percaya nilai inventory/hasil hit dari client.

## 7. Data & networking

Entitas persisten awal: `Account`, `Character`, `CharacterStats`, `TechniqueMastery`, `InventoryItem`, `QuestProgress`, `Reputation`, `Guild`, `Listing`, `Transaction`. Pisahkan data konfigurasi (moveset/item/NPC) dari state pemain. Gunakan UUID, timestamp UTC, optimistic version pada update karakter, dan transaksi DB untuk perdagangan.

Contoh skema sederhana (PostgreSQL, versi produksi perlu constraint/index/migrasi):

```sql
CREATE TABLE characters (
  id UUID PRIMARY KEY, account_id UUID NOT NULL, name TEXT NOT NULL UNIQUE,
  region_id TEXT NOT NULL, x REAL NOT NULL, y REAL NOT NULL,
  hp SMALLINT NOT NULL, qi SMALLINT NOT NULL, version INTEGER NOT NULL DEFAULT 1,
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE TABLE inventory_items (
  character_id UUID NOT NULL REFERENCES characters(id), slot SMALLINT NOT NULL,
  item_id TEXT NOT NULL, quantity INTEGER NOT NULL CHECK (quantity >= 0),
  PRIMARY KEY (character_id, slot)
);
```

Contoh pesan command (bukan implementasi netcode dalam prototipe):

```json
{"seq":184,"tick":9220,"input":{"moveX":0.7,"moveY":0,"sprint":false,"action":"light_attack"}}
```

Server memeriksa sequence/tick, kecepatan legal, stamina, cooldown, dan jarak hit; kemudian broadcast event/snapshot. Simpan quest progress dan transaksi penting secara durable, tetapi jangan menulis setiap frame posisi ke database. Gunakan checkpoint/autosave dan snapshot berkala.

## 8. UI/UX

HUD prototipe memperlihatkan HP/Qi, objektif, minimap, cuaca/waktu, lokasi, interaksi, dan aksi. Untuk produksi: UI dapat diskalakan, safe area mobile, remapping key, ukuran teks, warna yang aksesibel, mode low-motion, indikator cooldown/telegraph dengan ikon + bentuk (tidak hanya warna), opsi kamera/aim assist, serta tutorial bertahap. Marketplace/trading wajib menampilkan konfirmasi, riwayat, pajak, dan sumber item.

## 9. Kebutuhan aset & animasi

Untuk vertical slice 3D berikutnya: 1 karakter pemain humanoid rigged, 3 variasi bandit berbagi rig, 1 mentor NPC; locomotion idle/walk/run/turn; attack chain 3 hit; skill; hit-react; guard/parry; knockdown; dash/jump/land; interaction; facial/hand polish belakangan. Buat hitbox/socket weapon, root-motion policy, retarget guide, naming convention, LOD, collider, material budget, dan import preset sebelum produksi konten.

Lingkungan awal: modular dusun (rumah, kios, gerbang, jembatan), pohon pinus, batu, jalur, kabut, prop interaktif dan landmark perguruan. Prioritas readability, siluet, pencahayaan dan performa mobile; targetkan device budget lebih dulu. Aset placeholder prototipe Canvas dibuat dari bentuk procedural; tidak memakai aset komersial eksternal.

## 10. Roadmap, gate, dan risiko

| Tahap | Hasil yang bisa diuji | Gate sebelum lanjut |
|---|---|---|
| 0. Playable slice (sekarang) | Jalur Cemara, kontrol, pertarungan, 1 quest, HUD | 10 menit bermain tanpa blocker; kontrol desktop/touch jelas |
| 1. Combat prototype (2–4 minggu tim kecil) | Greybox 3D, 1 weapon, 2 musuh, telegraph/parry, kamera | Playtest membuktikan hit terbaca dan input responsif |
| 2. Vertical slice (6–10 minggu) | 1 zona mini, quest, NPC jadwal sederhana, loot/mastery/save lokal | 20–30 menit loop menyenangkan; target performa device disepakati |
| 3. Network spike (3–5 minggu) | Dedicated zone server, 2–8 pemain, movement/combat server-authoritative | Uji latency, reconnect, exploit dasar, biaya server terukur |
| 4. Closed alpha | 1–2 zona, party, dungeon, crafting terbatas, telemetry/moderation | Load test, backup/restore, ekonomi dan anti-cheat dasar |
| 5. Beta & release bertahap | Konten berulang, social, guild, marketplace, live ops | SLO, support, incident response, privasi dan ekonomi siap |

**Urutan penting:** jangan membangun perkawinan, perang faksi, housing, marketplace, dan world boss sebelum core combat + save + server authority terbukti. Batasi feature count tiap milestone; playtest mingguan dan ukur completion, death reason, latency, frame time, serta crash. Rencanakan PC lebih dahulu atau mobile lebih dahulu berdasarkan uji kontrol/performa, bukan mengejar dua platform penuh sekaligus.

**Risiko utama:** scope MMO melampaui tim; combat terasa tidak adil karena latency; ekonomi bot/dupe; biaya konten/hosting; kompatibilitas input mobile; kualitas animasi. Mitigasi: vertical slice sempit, simulasi lokal lalu dedicated server awal, transaksi idempotent/audit, content tools modular, budget device nyata, dan tidak menjanjikan fitur yang belum playable.

## Struktur proyek prototipe

```text
index.html       # HUD, menu, modal, canvas
style.css        # presentasi responsif desktop/mobile
game.js          # render Canvas, simulasi, input, quest (prototipe lokal)
README.md        # visi, rancangan teknis, rencana milestone
```

Struktur yang disarankan saat migrasi Unity:

```text
Assets/Game/{Core,Combat,Characters,World,Quests,UI,Audio}
Assets/Content/{Data,Prefabs,Animations,Materials,Environment}
Assets/Tests/{EditMode,PlayMode}
Server/{Gateway,Zone,Persistence,Contracts}
Ops/{Docker,Metrics,Migrations,Runbooks}
```

Jaga `game.js` sekarang sebagai demonstrasi mandiri. Saat menambah fitur pada prototipe, pecah menjadi modul `world`, `combat`, `actors`, `ui`, dan `input`; untuk production pindahkan simulasi authoritative ke server dan pakai data-driven definitions untuk jurus/item.
