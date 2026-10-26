# 🌌 Novacore Launcher (Prism Architecture) v1.5.0

<p align="center">
  <img src="NovacoreLauncher/Assets/logo_hd.png" alt="Novacore Launcher Logo" width="130" />
</p>

<p align="center">
  <strong>Prism mimarisi üzerine kurulu; ultra hızlı, modern, bağımsız mod motoru ve resmi Mojang CDN bağlantılı yeni nesil Minecraft başlatıcısı.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-v1.5.0-7952D8?style=for-the-badge&logo=minecraft" alt="Version" />
  <img src="https://img.shields.io/badge/Platform-Windows_10_|_11_(64--Bit)-00E5FF?style=for-the-badge&logo=windows" alt="Platform" />
  <img src="https://img.shields.io/badge/Mod_Loaders-Fabric_|_Forge_|_Vanilla-00D2A0?style=for-the-badge&logo=curseforge" alt="Mod Loaders" />
  <img src="https://img.shields.io/badge/Java-Java_8_to_25_Auto--Detect-FF7043?style=for-the-badge&logo=openjdk" alt="Java Support" />
  <img src="https://img.shields.io/badge/License-Free_%26_Open-BB86FC?style=for-the-badge" alt="License" />
</p>

---

## 📑 İçindekiler (Table of Contents)

- [Öne Çıkan Özellikler](#-öne-çıkan-özellikler)
- [Mod Merkezi & Otomatik Sürüm Filtreleme](#-mod-merkezi--otomatik-sürüm-filtreleme)
- [Fabric KnotClient Mod Motoru](#-fabric-knotclient-mod-motoru)
- [Upgrader & Veri Koruma (Preserve Data)](#-upgrader--veri-koruma)
- [Proje Mimarisi](#-proje-mimarisi)
- [Kurulum & Çalıştırma Dosyaları](#-kurulum--çalıştırma-dosyaları)
- [Sistem Gereksinimleri](#-sistem-gereksinimleri)
- [Sıkça Sorulan Sorular](#-sıkça-sorulan-sorular)
- [Yasal Uyarı](#-yasal-uyarı)

---

## 🌟 Öne Çıkan Özellikler

### 1. ⚡ Doğrudan Mojang Piston CDN Pipeline
- Mojang'ın resmi manifestosundan (`piston-meta.mojang.com`) 26.2, 26.3, 1.21.1 ve klasik sürümleri ışık hızında indirir.
- **Snapshot Desteği:** Deneysel sürümleri tek tıkla listeleyin ve kurun.
- Eksik kütüphaneleri ve asset dosyalarını paralel, takılma yapmayan asenkron motorla otomatik tamamlar.

### 2. 🧩 Dahili Modrinth & CurseForge Entegrasyonu
- Tarayıcı açmaya gerek kalmadan client içinden binlerce modu arayın (Sodium, Iris, Mod Menu, Lithium, JEI vb.).
- **Orijinal Marka Rozetleri:** Modrinth ve CurseForge doğrulanmış ikonları ve gerçek mod kapak afişleri.
- **Akıllı Sürüm Filtreleme:** Profilinizin tam sürümünü (`26.2`, `Fabric`) algılar ve sadece o sürüme uygun `.jar` dosyalarını kurar.

### 3. 🔄 Tek Tıkla "Tüm Modları Güncelle" (Update All Mods)
- Kurulu modlarınızı otomatik tarar; hedef Minecraft sürümünüzle uyumlu en son sürümleri Modrinth üzerinden çekip tek seferde günceller.
- Eski veya uyumsuz `.jar` dosyalarını çakışma olmaması için klasörden temizler.

### 4. 🚀 Fabric Loader & KnotClient Çalışma Zamanı
- Fabric modları için `net.fabricmc.loader.impl.launch.knot.KnotClient` ana sınıfını ve Fabric kütüphanelerini otomatik enjekte eder.
- `instances/<profil>/mods/` dizinindeki tüm modları tarar ve Minecraft'a aktarır.

### 5. 🛡️ Upgrader & Veri Koruma (Preserve Data)
- **Bağımsız Upgrader (`NovacoreLauncher_Updater.exe`):** Launcher'ı baştan kurmaya gerek kalmadan günceller.
- **Veri Koruma:** Güncelleme veya kaldırma sırasında kullanıcı dünyalarını, profillerini ve modlarını asla silmez.

### 6. 🌓 Çift Tema & İki Dil Desteği
- Koyu (Novacore Dark) ve Açık (Clean Light) temalar arasında anında geçiş.
- 🇹🇷 Türkçe ve 🇬🇧 İngilizce tam yerelleştirme.

---

## 🧩 Mod Merkezi & Otomatik Sürüm Filtreleme

Novacore Launcher, mod indirme karmaşasını tamamen ortadan kaldırır:

```
[Kullanıcı Profili: 26.2 Fabric]
       │
       ▼
[Mod Arama: "Sodium"] ──► Modrinth API (facets: versions:26.2, categories:fabric)
       │
       ▼
[Doğru Sürüm Eşleşti] ──► sodium-fabric-0.9.2+mc26.2.jar
       │
       ▼
[Eski Sürüm Temizlendi] ──► Uyumsuz 26.3/26.4 kalıntıları silindi
       │
       ▼
[Kurulum Tamamlandı] ──► instances/26.2/mods/ dizinine yerleştirildi
```

---

## 🏗️ Proje Mimarisi

```
Novacore Launcher/
├── Files/                                # Hazır derlenmiş ikili dosyalar (Release)
├── NovacoreLauncher/                     # Ana WPF Başlatıcı Kaynak Kodları (.NET 10)
│   ├── Assets/                           # İkonlar ve marka logoları
│   ├── Models/                           # Profil, hesap ve ayar modelleri
│   ├── Services/                         # LaunchService, MojangService, ModBrowseService...
│   └── MainWindow.xaml                   # Modern karanlık arayüz
├── NovacoreInstaller/                    # Bağımsız Kurulum Sihirbazı (Setup.exe)
├── NovacoreUpgrader/                     # Otomatik Güncelleyici (Updater.exe)
├── NovacoreUninstaller/                  # Veri korumalı Kaldırıcı (Uninstall.exe)
└── NovacoreLauncher_Website/             # Resmi HTML5/CSS3/JS Web Sitesi (GitHub Pages)
    ├── assets/                           # Web görselleri ve logolar
    ├── downloads/                        # Doğrudan Setup indirme dosyası
    ├── index.html                        # Ana sayfa
    ├── styles.css                        # Glassmorphism karanlık neon tema
    └── script.js                         # Dil ve interaktif maket betiği
```

---

## 📦 Kurulum & Çalıştırma Dosyaları

| Amaç | Kısayol / Dosya | Açıklama |
| :--- | :--- | :--- |
| **Resmi Web Sitesini Aç** | [`Baslat_WebSitesi.bat`](Baslat_WebSitesi.bat) | Tanıtım sitesini varsayılan tarayıcıda açar |
| **Başlatıcıyı Çalıştır** | [`Baslat_NovacoreLauncher.bat`](Baslat_NovacoreLauncher.bat) | Novacore Launcher'ı doğrudan başlatır |
| **Kurulum Sihirbazı** | [`Kurulum_Yap_NovacoreLauncher.bat`](Kurulum_Yap_NovacoreLauncher.bat) | `NovacoreLauncher_Setup.exe` kurulumunu çalıştırır |
| **Yükseltici (Upgrader)** | [`Upgrader_Calistir_NovacoreLauncher.bat`](Upgrader_Calistir_NovacoreLauncher.bat) | `NovacoreLauncher_Updater.exe` ile sürüm yeniler |
| **Kaldırıcı (Uninstaller)**| [`Uninstall_Yap_NovacoreLauncher.bat`](Uninstall_Yap_NovacoreLauncher.bat) | Verileri koruyarak başlatıcıyı sistemden kaldırır |

---

## 💻 Sistem Gereksinimleri

| Bileşen | Minimum | Önerilen |
| :--- | :--- | :--- |
| **İşletim Sistemi** | Windows 10 (64-Bit) | Windows 11 (64-Bit En Güncel) |
| **İşlemci (CPU)** | Intel Core i3 / AMD FX Serisi | Intel Core i5 / AMD Ryzen 5 veya üstü |
| **Bellek (RAM)** | 2 GB Tahsis | 4 GB - 8 GB Tahsis (Modlu oyunlar için) |
| **Java Sürümü** | Java 8 veya Java 17 | Java 21 / Java 25 (Otomatik Algılanır) |
| **Ekran Kartı** | OpenGL 3.3 Uyumlu GPU | NVIDIA RTX / AMD Radeon (OpenGL 4.5+) |

---

## ❓ Sıkça Sorulan Sorular

**S: Novacore Launcher ücretsiz mi?**  
C: Evet, Novacore Launcher tamamen ücretsiz ve açık mimarilidir. Reklam veya ücretli kısıtlama içermez.

**S: Modlar Minecraft sürümümle uyumlu iner mi?**  
C: Kesinlikle. Akıllı sürüm ve yükleyici filtresi sayesinde profilinizin sürümüne (örn: 26.2 Fabric) tam uyan modlar indirilir.

**S: Android sürümü var mı?**  
C: Hayır. Novacore Launcher, masaüstü bilgisayarlarda en yüksek kare hızını (FPS) ve gelişmiş Java optimizasyonunu sağlamak için yalnızca Windows PC platformuna odaklanmıştır.

---

## ⚖️ Yasal Uyarı (Disclaimer)

Novacore Launcher, **Mojang AB** veya **Microsoft** ile ilişkili değildir ve onlar tarafından onaylanmamıştır.  
Minecraft, **Mojang Synergies AB**'nin tescilli ticari markasıdır.
