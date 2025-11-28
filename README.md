-----

# SmartLibrary - Akıllı Kütüphane Yönetim Sistemi

Bu proje, **Nesneye Yönelik Programlama (OOP)** dersi kapsamında geliştirilmiş, Java tabanlı masaüstü konsol uygulamasıdır. **JDBC** ve **SQLite** kullanılarak veri kalıcılığı sağlanmış, kütüphane işlemlerinin (kitap, öğrenci, ödünç alma) yönetimi simüle edilmiştir.

## Proje Hakkında

**SmartLibrary**, üniversite kütüphanesindeki temel iş akışlarını dijitalleştirmeyi amaçlar. Sistem; kitapların kaydını tutar, öğrencileri sisteme ekler ve kitap ödünç alma/iade etme süreçlerini tarih bazlı olarak takip eder.

### Kullanılan Teknolojiler ve Araçlar

  * **Dil:** Java (JDK 17 / 8 uyumlu)
  * **IDE:** Visual Studio Code
  * **Veritabanı:** SQLite
  * **Kütüphane:** SQLite JDBC Driver (`sqlite-jdbc-xxxx.jar`)
  * **Mimari:** Katmanlı Mimari (Entities, Repositories, Database Access)

-----

## Özellikler (Beklenenler ve Karşılananlar)

Bu proje, ders gereksinimlerinde belirtilen aşağıdaki teknik şartları tam olarak sağlar:

  * **Sınıf ve Nesne Yapısı:** `Book`, `Student`, `Loan` sınıfları ile veri modellemesi.
  * **Encapsulation (Kapsülleme):** Private değişkenler ve Getter/Setter kullanımı.
  * **Repository Pattern:** Veri tabanı işlemleri (CRUD) `Repository` sınıfları içinde ayrıştırılmıştır.
  * **JDBC & SQLite:** Veriler uçucu bellekte değil, `smartlibrary.db` dosyasında saklanır.
  * **Koleksiyonlar:** Veriler listelenirken `ArrayList` yapısı kullanılmıştır.
  * **Otomatik Tablo Oluşturma:** Uygulama ilk açıldığında veritabanı tabloları yoksa otomatik oluşturur.
  * **Kontrol Mekanizmaları:** Bir kitap ödünçteyken başkasına verilmesi engellenir.

-----

## Proje Yapısı

Proje dosyaları aşağıdaki gibi yapılandırılmıştır:

```
SmartLibrary/
│
├── smartlibrary.db          # Proje çalışınca otomatik oluşan veritabanı dosyası
├── sqlite-jdbc-3.46.0.0.jar # Veritabanı bağlantısı için gerekli sürücü
├── README.md                # Proje dokümantasyonu
│
├── Main.java                # Uygulamanın giriş noktası ve menü yönetimi
├── Database.java            # SQLite bağlantısı ve tablo oluşturma işlemleri
│
├── Book.java                # Kitap nesnesi (Entity)
├── Student.java             # Öğrenci nesnesi (Entity)
├── Loan.java                # Ödünç alma işlemi nesnesi (Entity)
│
├── BookRepository.java      # Kitap tablosu CRUD işlemleri
├── StudentRepository.java   # Öğrenci tablosu CRUD işlemleri
└── LoanRepository.java      # Ödünç alma/verme işlemleri
```

-----

## Kurulum ve Çalıştırma (Visual Studio Code)

Projeyi bilgisayarınızda çalıştırmak için aşağıdaki adımları izleyin:

### 1\. Gereksinimler

  * Bilgisayarınızda **JDK (Java Development Kit)** yüklü olmalıdır.
  * **Visual Studio Code** ve **Extension Pack for Java** eklentisi kurulu olmalıdır.

### 2\. Projeyi Açma

1.  Projeyi indirin ve klasörü **Visual Studio Code** ile açın (`File > Open Folder`).

### 3\. JDBC Sürücüsünü Tanıtma (ÖNEMLİ ADIM)

SQLite bağlantısının çalışması için `.jar` dosyasının projeye referans olarak eklenmesi gerekir:

1.  `sqlite-jdbc-xxxx.jar` dosyasını proje klasörüne atın.
2.  VS Code sol panelde **"JAVA PROJECTS"** sekmesini bulun.
3.  **Referenced Libraries** kısmındaki **+ (Artı)** butonuna tıklayın.
4.  Proje klasöründeki `.jar` dosyasını seçip ekleyin.

### 4\. Çalıştırma

  * `Main.java` dosyasını açın.
  * Sağ üstteki **Play (▷)** butonuna basın veya `F5` tuşunu kullanın.
  * Terminal ekranında menü belirecektir.

-----

## Veritabanı Şeması

Uygulama arka planda aşağıdaki SQLite tablolarını kullanır:

**1. Books (Kitaplar)**
| id (PK) | title | author | year |
|---|---|---|---|
| Auto Inc | Kitap Adı | Yazar | Basım Yılı |

**2. Students (Öğrenciler)**
| id (PK) | name | department |
|---|---|---|
| Auto Inc | Ad Soyad | Bölüm |

**3. Loans (Ödünç İşlemleri)**
| id (PK) | bookId (FK) | studentId (FK) | dateBorrowed | dateReturned |
|---|---|---|---|---|
| Auto Inc | Kitap ID | Öğrenci ID | Alınan Tarih | Teslim Tarihi (Null olabilir) |

-----

## Kullanım Senaryosu

1.  **Kitap Ekle:** Menüden 1'i seçin, kitap bilgilerini girin.
2.  **Öğrenci Ekle:** Menüden 3'ü seçin, öğrenci bilgilerini girin.
3.  **Listeleme:** 2 ve 4 ile kayıtlı verileri görebilirsiniz (ID numaralarına dikkat edin).
4.  **Ödünç Ver:** Menüden 5'i seçin. Kitap ID ve Öğrenci ID girerek işlemi tamamlayın.
      * *Not: Eğer kitap zaten başkasındaysa sistem uyarı verecektir.*
5.  **İade Al:** Menüden 7'yi seçin. Kitap ID ve iade tarihini girerek kaydı kapatın.

-----

**Geliştirici:** Ömer Faruk Sağlam
**Ders:** Nesneye Yönelik Programlama - II
**Tarih:** Kasım 2025
