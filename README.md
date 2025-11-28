# SmartLibrary - Akıllı Kütüphane Yönetim Sistemi

Bu proje, **Nesneye Yönelik Programlama (OOP)** dersi kapsamında geliştirilmiş, Java tabanlı masaüstü konsol uygulamasıdır. **JDBC** ve **SQLite** kullanılarak veri kalıcılığı sağlanmış, kütüphane işlemlerinin (kitap, öğrenci, ödünç alma) yönetimi simüle edilmiştir.

## Proje Hakkında

**SmartLibrary**, üniversite kütüphanesindeki temel iş akışlarını dijitalleştirmeyi amaçlar. Sistem; kitapların kaydını tutar, öğrencileri sisteme ekler, silebilir ve kitap ödünç alma/iade etme süreçlerini tarih bazlı olarak takip eder.

### Kullanılan Teknolojiler ve Araçlar

* **Dil:** Java (JDK 17 / 8 uyumlu)
* **IDE:** Visual Studio Code
* **Veritabanı:** SQLite
* **Kütüphane:** SQLite JDBC Driver (`sqlite-jdbc-xxxx.jar`)
* **Mimari:** Katmanlı Mimari (Entities, Repositories, Database Access)

---

## Özellikler (Beklenenler ve Karşılananlar)

Bu proje, ders gereksinimlerinde belirtilen teknik şartları tam olarak sağlar:

* **Sınıf ve Nesne Yapısı:** `Book`, `Student`, `Loan` sınıfları ile veri modellemesi.
* **Encapsulation (Kapsülleme):** Private değişkenler ve Getter/Setter kullanımı.
* **Repository Pattern:** Veri tabanı işlemleri (Ekleme, Listeleme, Silme) `Repository` sınıfları içinde ayrıştırılmıştır.
* **JDBC & SQLite:** Veriler uçucu bellekte değil, `smartlibrary.db` dosyasında saklanır.
* **Koleksiyonlar:** Veriler listelenirken `ArrayList` yapısı kullanılmıştır.
* **Otomatik Tablo Oluşturma:** Uygulama ilk açıldığında veritabanı tabloları yoksa otomatik oluşturur.
* **Kontrol Mekanizmaları:** Bir kitap ödünçteyken başkasına verilmesi engellenir.

---

## Proje Yapısı

Proje dosyaları aşağıdaki gibi yapılandırılmıştır:

```text
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
├── BookRepository.java      # Kitap işlemleri (Ekle, Sil, Listele)
├── StudentRepository.java   # Öğrenci işlemleri (Ekle, Sil, Listele)
└── LoanRepository.java      # Ödünç alma/verme işlemleri
````

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

## Kullanım Senaryosu ve Menü

1.  **Kitap Ekle:** Kütüphaneye yeni kitap eklenir.
2.  **Kitapları Listele:** Tüm kitaplar listelenir.
3.  **Öğrenci Ekle:** Yeni öğrenci kaydı yapılır.
4.  **Öğrencileri Listele:** Tüm öğrenciler listelenir.
5.  **Kitap Ödünç Ver:** Kitap ID ve Öğrenci ID ile işlem yapılır.
      * *Not: Eğer kitap zaten başkasındaysa sistem uyarı verecektir.*
6.  **Ödünç Listesini Görüntüle:** Kim hangi kitabı almış listelenir.
7.  **Kitap Geri Teslim Al:** Kitap iade tarihi girilerek süreç tamamlanır.
8.  **Kitap Sil:** ID numarası girilen kitap veritabanından silinir.
9.  **Öğrenci Sil:** ID numarası girilen öğrenci veritabanından silinir.

-----

**Geliştirici:** Ömer Faruk Sağlam
**Ders:** Nesne Dayalı Programlama II
**Tarih:** Kasım 2025
