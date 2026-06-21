# Lab: Bob for Z ile CBSA Uygulamasının Tam Analizi

## Lab'a Genel Bakış

Bu lab, **Bob for Z** yapay zeka asistanını kullanarak **CICS Banking Sample Application (CBSA)** uygulamasının tam analizinde size rehberlik eder.
**LabDiscoverCBSA**'ya ek olarak, bu lab ayrıca front-end kısmını (Java, React, API,....) entegre eder.
Bob'un farklı modlarını kullanmayı ve detaylı analizler, dokümantasyon ve mimari diyagramlar elde etmek için etkili prompt'lar formüle etmeyi öğreneceksiniz.

---

## Ön Koşullar

- ✅ **IBM Bob Premium Package for Z** uzantısı kurulu VSCode
- ✅ Yerel olarak klonlanmış CBSA projesi (**LabDiscoverCBSA**'ya bakın)
- ✅ Bob'un **Z Code** moduna erişim
- ✅ COBOL, JCL ve mainframe mimarisi temel bilgisi (önerilir ancak zorunlu değildir)

---

## Tahmini Süre

**Toplam süre: 2-3 saat**

---

## İçindekiler

0. [Hazırlık 0: Uygulamanın Front-end'ini Alma](#hazırlık-0)  
1. [Alıştırma 1: Başlatma ve AGENTS.md Dosyasının Oluşturulması](#alıştırma-1)
2. [Alıştırma 2: Veri Sözlüğünün Oluşturulması](#alıştırma-2)
3. [Alıştırma 3: COBOL Programlarının Envanteri](#alıştırma-3)
4. [Alıştırma 4: Frontend Envanteri](#alıştırma-4)
5. [Alıştırma 5: Mimari Diyagramlar](#alıştırma-5)
6. [Alıştırma 6: Fonksiyonel Analiz - Yerel Transfer](#alıştırma-6)
7. [Alıştırma 7: Kullanıcı Kılavuzu](#alıştırma-7)
8. [Alıştırma 8: Teknik Analiz - Credit Score](#alıştırma-8)

---



<a name="Hazırlık-0"></a>
## Hazırlık 0: Uygulamanın Front-end'ini Alma

## 🎯 Hedef

CBSA uygulamasının front-end kısmının kaynak kodunu GitHub'dan almak ve lab için workspace'i hazırlamak.

### 🔧 Kullanılacak Bob Modu

**Mod: 💻 Code**

Code modu, sistem komutlarını çalıştırmaya ve dosyaları manipüle etmeye olanak tanır.

### 📝 Bağlam

Analize başlamadan önce, CBSA uygulamasının kaynak kodunu resmi GitHub deposundan almanız gerekir. Bu hazırlığı otomatikleştirmek için Bob'u kullanacağız. 
Bob'u açın, **File>Open Folder** menüsüne tıklayın ve ~/CBSA dizinini seçin.


### 💬 Bob Prompt'u 

```
"src/bank-application-frontend", "src/webui", "src/Z-OS-Connect-Customer-Services-Interface", "src/Z-OS-Connect-Payment-Interface", "src/Z-OS-Connect-Payment-Interface" ve "src/zosconnect_artefacts" adlı dizinleri GitHub deposu https://github.com/cicsdev/cics-banking-sample-application-cbsa.git'ten al ve bu workspace'e yerleştir.
```

### ✅ Beklenen Sonuç 

Bob aşağıdaki komutları çalıştırır:

```bash
# Depoyu geçici bir dizine klonla
rm -rf /tmp/cbsa-temp && git clone --depth 1 --filter=blob:none --sparse https://github.com/cicsdev/cics-banking-sample-application-cbsa.git /tmp/cbsa-temp
cd /tmp/cbsa-temp && git sparse-checkout set src/bank-application-frontend src/webui src/Z-OS-Connect-Customer-Services-Interface src/Z-OS-Connect-Payment-Interface src/zosconnect_artefacts

mkdir -p ./src && cp -r /tmp/cbsa-temp/src/bank-application-frontend /tmp/cbsa-temp/src/webui /tmp/cbsa-temp/src/Z-OS-Connect-Customer-Services-Interface /tmp/cbsa-temp/src/Z-OS-Connect-Payment-Interface /tmp/cbsa-temp/src/zosconnect_artefacts ./src/

```

**Çıktı konsolu**:
```
Aşağıdaki 5 dizin GitHub deposundan alındı ve workspace'e yerleştirildi:
1.	bank-application-frontend/ - Bankacılık frontend uygulaması
2.	webui/ - Web kullanıcı arayüzü
3.	Z-OS-Connect-Customer-Services-Interface/ - Müşteri hizmetleri için z/OS Connect arayüzü
4.	Z-OS-Connect-Payment-Interface/ - Ödemeler için z/OS Connect arayüzü
5.	zosconnect_artefacts/ - z/OS Connect yapıtları


```



### 🎓 Öğrendikleriniz

- **Otomasyon**: Bob, Git ve sistem komutlarını çalıştırabilir
- **Workspace hazırlığı**: Bob, lab için dosyaları düzenleyebilir
- **Doğrulama**: Bob, her şeyin yerinde olduğunu doğrulayabilir
- **Zaman kazancı**: Manuel olarak 15-20 dakika yerine 5 dakika

### ✅ Teknik Ön Koşullar

Lab'a başlamadan önce, sahip olduğunuzdan emin olun:

- **IBM Z Open Editor** uzantısı ile kurulmuş **Bob**
- Bob'da etkinleştirilmiş **Bob Premium for Z**
- Sisteminizde kurulu **Git**
- Depoyu klonlamak için **İnternet erişimi**

### 🎯 Hazırsınız!

Workspace Bob ile hazırlandıktan sonra, bu çalışma alanında LabDicoverCBSA'yı zaten yaptıysanız, doğrudan <a name="alıştırma-4">Alıştırma 4 Frontend Envanteri</a>'ne başlayabilirsiniz.
Aksi takdirde Alıştırma 1'den başlayın.

<a name="alıştırma-1"></a>
## Alıştırma 1: Başlatma ve AGENTS.md Dosyasının Oluşturulması


### Hedef
Proje yapısını, build komutlarını, kodlama standartlarını ve Bob'u gelecekteki analizlerinde yönlendirmek için ana konumları dokümante eden bir AGENTS.md dosyası oluşturmak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Önerilen Prompt
```
/init
```

### Bob'un Yapacakları
1. Projenin tam yapısını analiz etmek
2. Kullanılan dilleri tespit etmek (COBOL, JCL, Java, vb.)
3. Build komutlarını tanımlamak (Maven, shell scriptleri)
4. Veri sözlüğünü bulmak (bobz/DD.json)
5. COBOL programlarını teknik dokümantasyonlarına eşlemek
6. Tüm bu bilgilerle AGENTS.md dosyasını oluşturmak

### Beklenen Sonuç
**Oluşturulan dosya:** `AGENTS.md`

**Beklenen içerik:**
- Workspace türü (IBM Enterprise COBOL for z/OS)
- Tespit edilen diller (COBOL, JCL, BMS, Java 17)
- Build komutları (build.sh, Maven)
- Dizin yapısı
- Veri sözlüğünün konumu
- COBOL programlarının dokümantasyona eşlemesi
- Dokümantasyon kuralları (varsayılan olarak Türkçe dil)

### Doğrulama
✅ AGENTS.md dosyası proje kökünde mevcut  
✅ "Workspace Type" bölümü içeriyor  
✅ "Build Commands" bölümü içeriyor  
✅ COBOL → Dokümantasyon eşleme tablosu içeriyor  
✅ Veri sözlüğünün konumunu belirtiyor

### Tahmini Süre
⏱️ 5-10 dakika

---

<a name="alıştırma-2"></a>
## Alıştırma 2: Veri Sözlüğünün Oluşturulması

### Hedef
Mainframe kodunun anlaşılmasını kolaylaştırmak için COBOL değişkenlerini Türkçe açıklamalarla dokümante eden bir veri sözlüğü oluşturmak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Önerilen Prompt
```
BNKMENU programı için bir veri sözlüğü oluştur
```

### Bob'un Yapacakları
1. Bir sözlüğün zaten var olup olmadığını kontrol etmek
2. BNKMENU.cbl COBOL programını taramak
3. En önemli değişkenleri çıkarmak (ilk 15)
4. Her değişken için Türkçe açıklamalar oluşturmak
5. bobz/DD.json dosyasını oluşturmak
6. AGENTS.md'yi sözlüğün konumuyla güncellemek

### Beklenen Sonuç
**Oluşturulan dosya:** `bobz/DD.json`

**Beklenen içerik:**
```json
{
  "version": "2.0.0",
  "entries": [
    {
      "name": "COMM-EYE",
      "type": "variable",
      "shortDescription": "İletişim Eyecatcher",
      "longDescription": "İletişim alanı için kontrol tanımlayıcısı...",
      "origin": "AI",
      "scope": [{"programName": "BNKMENU"}]
    },
    ...
  ]
}
```

**Giriş sayısı:** 15 dokümante edilmiş değişken

### Doğrulama
✅ bobz/DD.json dosyası mevcut  
✅ En az 15 giriş içeriyor  
✅ Her giriş Türkçe kısa ve uzun açıklamaya sahip  
✅ "scope" alanı "BNKMENU" içeriyor  
✅ AGENTS.md sözlüğün konumuyla güncellendi

### Tahmini Süre
⏱️ 10-15 dakika

---

<a name="alıştırma-3"></a>
## Alıştırma 3: COBOL Programlarının Envanteri

### Hedef
Tüm COBOL programlarının bağımlılıkları, sınıflandırmaları ve ilişkileriyle tam envanterini oluşturmak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Önerilen Prompt
```
Tüm COBOL programlarının envanterini çıkar
```

### Bob'un Yapacakları
1. Tüm COBOL programlarını taramak (29 program)
2. Bağımlılıkları analiz etmek (copybook'lar, Db2 tabloları, VSAM dosyaları)
3. Programları sınıflandırmak (BMS, hizmetler, yardımcı programlar, batch)
4. Bağımlılık matrisleri oluşturmak
5. Bağımlılık ağacı oluşturmak
6. Her programı rolüyle dokümante etmek

### Beklenen Sonuç
**Oluşturulan dosya:** `docs/COBOL_INVENTORY.md`

**Beklenen içerik:**
- Genel bakış (29 program)
- Türe göre sınıflandırma:
  - BMS programları (11)
  - Hizmet programları (13)
  - Yardımcı programlar (4)
  - Batch programı (1)
- Her program için detaylı bağımlılıklar:
  - Kullanılan copybook'lar
  - Erişilen Db2 tabloları (READ/WRITE)
  - Erişilen VSAM dosyaları
  - Çağrılan programlar
- Bağımlılık matrisleri
- Bağımlılık ağacı
- Program başına detaylı dokümantasyon

### Doğrulama
✅ docs/COBOL_INVENTORY.md dosyası mevcut  
✅ 29 COBOL programını listeler  
✅ Her programın bağımlılıkları dokümante edilmiş  
✅ Erişim türleri (READ/WRITE) belirtilmiş  
✅ Bağımlılık matrisleri mevcut

### Tahmini Süre
⏱️ 15-20 dakika

---

<a name="alıştırma-4"></a>
## Alıştırma 4: Frontend Envanteri

### Hedef
REST API'leri, JSON modelleri ve veri erişim katmanlarını içeren tam frontend mimarisini dokümante etmek.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Önerilen Prompt
```
Front-end'in envanterini çıkar
```

### Bob'un Yapacakları
1. REST JAX-RS kaynaklarını analiz etmek (5 kaynak)
2. HTTP yöntemleriyle tüm endpoint'leri dokümante etmek
3. JSON modellerini analiz etmek (13 sınıf)
4. Veri erişim katmanını dokümante etmek (8 sınıf)
5. COBOL arayüzlerini tanımlamak (8 sınıf)
6. Tam yapılandırılmış dokümantasyon oluşturmak

### Beklenen Sonuç
**Oluşturulan dosya:** `docs/FRONTEND_INVENTORY.md`

**Beklenen içerik:**

**1. REST Kaynakları (5):**
- AccountsResource: 5 endpoint
- CustomerResource: 5 endpoint
- ProcessedTransactionResource: 3 endpoint
- CompanyNameResource: 1 endpoint
- SortCodeResource: 1 endpoint

**2. JSON Modelleri (13):**
- AccountJSON, DebitCreditAccountJSON, TransferLocalJSON
- CustomerJSON
- ProcessedTransactionJSON (6 varyant)
- CreditScore, CreditScoreCICS540

**3. Veri erişim katmanı (8):**
- Account.java, AccountList.java (Db2)
- Customer.java, CustomerList.java (VSAM)
- GetUserSortCode.java
- HBankDataAccess.java

**4. COBOL Arayüzleri (8):**
- CRECUST.java, CUSTOMER.java, PROCTRAN.java
- GetCompany.java, GetSortCode.java
- NewAccountNumber.java, NewCustomerNumber.java
- CustomerControl.java

### Doğrulama
✅ docs/FRONTEND_INVENTORY.md dosyası mevcut  
✅ 5 REST kaynağı tüm endpoint'leriyle dokümante edilmiş  
✅ 13 JSON modeli nitelikleriyle listelenmiş  
✅ 8 veri erişim sınıfı dokümante edilmiş  
✅ 8 COBOL arayüzü listelenmiş  
✅ Mimari kalıplar açıklanmış

### Tahmini Süre
⏱️ 15-20 dakika

---

<a name="alıştırma-5"></a>
## Alıştırma 5: Mimari Diyagramlar

### Hedef
Global mimariyi ve frontend'in detaylı mimarisini görselleştiren Draw.io diyagramları oluşturmak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Alıştırma 5A: Global Mimari Diyagramı

#### Önerilen Prompt
```
Uygulamanın farklı katmanlarını ayırt ederek front-end ve backend'i entegre eden global bir diyagram (draw.io'da) oluştur
```

#### Beklenen Sonuç
**Oluşturulan dosya:** `docs/CBSA_Architecture_Diagram.drawio`

**Beklenen içerik:**
- Renk kodlarıyla 5 farklı katman:
  1. **Sunum Katmanı** (Mavi): BMS 3270, Carbon React UI, Spring Boot UI, Mobil
  2. **REST API Katmanı** (Sarı): 5 JAX-RS kaynağı, z/OS Connect
  3. **İş Mantığı Katmanı** (Pembe): 29 COBOL programı
  4. **Veri Erişim Katmanı** (Mor): Db2, VSAM, COBOL Arayüzleri
  5. **Depolama Katmanı** (Yeşil): Db2 Tabloları, VSAM Dosyaları, BMS Map'leri
- Katmanlar arası veri akışlarını gösteren oklar
- Tam açıklama
- Teknik notlar

#### Doğrulama
✅ Dosya Draw.io'da doğru açılıyor  
✅ 5 katman görünür ve farklı  
✅ Veri akışları oklarla temsil ediliyor  
✅ Açıklama mevcut ve tam

### Alıştırma 5B: Detaylı Frontend Diyagramı

#### Önerilen Prompt
```
Front-end kısmının detaylı bir diyagramını yap
```

#### Beklenen Sonuç
**Oluşturulan dosya:** `docs/CBSA_Frontend_Detailed_Diagram.drawio`

**Beklenen içerik:**
- Tam detaylarla 5 katman:
  1. **İstemci**: 4 arayüz türü
  2. **REST API**: Tüm endpoint'ler detaylı
  3. **JSON Modelleri**: Niteliklerle 13 sınıf
  4. **Veri Erişimi**: Yöntemlerle 8 sınıf
  5. **COBOL Backend**: Sınıflandırılmış 29 program
- HTTP/REST, JCICS LINK, SQL/VSAM akışları
- Kullanılan teknolojiler (JAX-RS, JCICS, Carbon Design System)
- Tam istatistikler

#### Doğrulama
✅ Dosya Draw.io'da doğru açılıyor  
✅ Tüm REST endpoint'leri listeleniyor  
✅ 13 JSON modeli temsil ediliyor  
✅ İletişim akışları net  
✅ Teknolojiler dokümante edilmiş

### Tahmini Süre
⏱️ 20-25 dakika (diyagram başına 10-12 dk)

---

<a name="alıştırma-6"></a>
## Alıştırma 6: Fonksiyonel Analiz - Yerel Transfer

### Hedef
Yerel fon transfer işleminin işleyişini derinlemesine anlamak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Önerilen Prompt
```
Transfer local işlemi nedir?
```

### Bob'un Yapacakları
1. Kaynak dosyaları okumak (TransferLocalJSON.java, XFRFUN.cbl, BNK1TFN.cbl)
2. İşlem akışını analiz etmek
3. Yapılan doğrulamaları tanımlamak
4. Hata yönetimini dokümante etmek
5. Anti-deadlock stratejisini açıklamak
6. Güvenlik mekanizmalarını detaylandırmak (SYNCPOINT, ROLLBACK)

### Beklenen Sonuç
**Bob'un yanıtı içerir:**

**1. İlgili Bileşenler:**
- TransferLocalJSON.java (model)
- BNK1TFN.cbl (BMS arayüzü)
- XFRFUN.cbl (iş mantığı)

**2. İşlem Akışı:**
- İlk doğrulama (tutar > 0, farklı hesaplar)
- Güncelleme sırası (deadlock önleme)
- Kaynak hesap güncellemesi (borç)
- Hedef hesap güncellemesi (alacak)
- Denetim kaydı (PROCTRAN)

**3. Hata Yönetimi:**
- Kod '1': Kaynak hesap bulunamadı
- Kod '2': Hedef hesap bulunamadı
- Kod '3': Beklenmeyen hata
- Kod '4': Geçersiz tutar

**4. Güvenlik Mekanizmaları:**
- Atomik işlem (ACID)
- SYNCPOINT ROLLBACK
- Deadlock önleme
- Tam denetim izi

### Doğrulama
✅ Açıklama 3 ana bileşeni kapsıyor  
✅ İşlem akışı adım adım detaylandırılmış  
✅ 4 hata kodu açıklanmış  
✅ Güvenlik mekanizmaları dokümante edilmiş  
✅ Anti-deadlock stratejisi açıklanmış

### Tahmini Süre
⏱️ 10-15 dakika

---

<a name="alıştırma-7"></a>
## Alıştırma 7: Kullanıcı Kılavuzu

### Hedef
Son kullanıcılara yönelik yerel transfer fonksiyonu için tam bir kullanıcı kılavuzu oluşturmak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Önerilen Prompt
```
Yerel transferin kullanıcı kılavuzunu yap.
```

### Bob'un Yapacakları
1. Profesyonel kılavuz yapısı oluşturmak
2. Ön koşulları dokümante etmek
3. 3 arayüz üzerinden erişimi açıklamak (BMS, Web, API)
4. Adım adım prosedürü detaylandırmak
5. Çözümlerle tüm hata mesajlarını listelemek
6. Pratik örnekler sağlamak
7. SSS ve güvenlik tavsiyeleri eklemek

### Beklenen Sonuç
**Oluşturulan dosya:** `docs/GUIDE_UTILISATEUR_TRANSFERT_LOCAL.md`

**Beklenen içerik (500 satır):**

**1. Ana Bölümler:**
- Genel bakış
- Ön koşullar
- Fonksiyona erişim (BMS 3270, Web, REST API)
- Transfer prosedürü (4 detaylı adım)
- Doğrulama ve onay
- Hata mesajları (6 tür)
- Pratik örnekler (3 senaryo)
- Sık sorulan sorular (8 soru)
- Güvenlik tavsiyeleri

**2. Görsel Öğeler:**
- Simüle edilmiş BMS ekran görüntüleri
- REST API istek örnekleri
- Klavye kısayol tabloları
- Bakiye hesaplama örnekleri

**3. Teknik Bilgiler:**
- İlgili COBOL programları
- Veritabanı tabloları
- CICS işlem kodları

### Doğrulama
✅ Dosya yaklaşık 500 satır  
✅ 3 arayüz dokümante edilmiş (BMS, Web, API)  
✅ Prosedür 4 adımda detaylandırılmış  
✅ 6 hata mesajı çözümlerle açıklanmış  
✅ 3 pratik örnek sağlanmış  
✅ SSS en az 8 soru içeriyor  
✅ Güvenlik tavsiyeleri mevcut

### Tahmini Süre
⏱️ 15-20 dakika

---

<a name="alıştırma-8"></a>
## Alıştırma 8: Teknik Analiz - Credit Score

### Hedef
Kredi puanlama sistemini ve asenkron JCICS API ile teknik uygulamasını anlamak.

### Kullanılacak Bob Modu
🧰 **Z Code**

### Alıştırma 8A: Genel İşleyiş

#### Önerilen Prompt
```
Credit Score fonksiyonu ne yapar?
```

#### Beklenen Sonuç
**Bob'un yanıtı içerir:**

**1. Mimari:**
- CreditScore.java (giriş noktası)
- CreditScoreCICS540.java (gelişmiş uygulama)
- CRDTAGY1-5.cbl (5 simüle edilmiş ajans)

**2. Süreç:**
- 5 asenkron işlemin başlatılması
- Her ajans 1-999 arası puan üretir
- Ajans başına 0-3 saniye rastgele gecikme
- getAny() ile sonuçların toplanması
- Puanların ortalamasının hesaplanması

**3. Özellikler:**
- Paralellik (Async JCICS API)
- Dayanıklılık (bir ajans başarısız olursa devam eder)
- Yedek (CICS < 5.4 ise yedek mod)
- Performans (sıralı 15 sn yerine maks 3 sn)

### Alıştırma 8B: Değer Ölçeği

#### Önerilen Prompt
```
Kredi puanlarının değer ölçeği nedir?
```

#### Beklenen Sonuç
**Bob'un yanıtı içerir:**

**1. Değer Aralığı:**
- Minimum: 1
- Maksimum: 999
- Tür: Tam sayı

**2. Hesaplama:**
```
Nihai Puan = (Puan1 + Puan2 + Puan3 + Puan4 + Puan5) / 5
```

**3. Önerilen Yorumlama:**
- 1-199: Çok Düşük
- 200-399: Düşük
- 400-599: Orta
- 600-799: İyi
- 800-999: Mükemmel

**4. Karşılaştırma:**
- CBSA: 1-999 (kurgusal)
- FICO: 300-850 (ABD)
- Experian: 0-999 (İngiltere)

### Doğrulama
✅ 3 seviyeli mimari açıklanmış  
✅ Asenkron süreç detaylandırılmış  
✅ 1-999 ölçeği dokümante edilmiş  
✅ Hesaplama formülü sağlanmış  
✅ Puanların yorumlaması önerilmiş  
✅ Gerçek sistemlerle karşılaştırma yapılmış

### Tahmini Süre
⏱️ 15-20 dakika (alt alıştırma başına 7-10 dk)

---

## Çıktıların Özeti

Bu lab'ın sonunda, aşağıdaki dosyaları oluşturmuş olacaksınız:

| # | Dosya | Tür | Boyut |
|---|---------|------|--------|
| 1 | AGENTS.md | Dokümantasyon | ~150 satır |
| 2 | bobz/DD.json | Sözlük | 15 giriş |
| 3 | docs/COBOL_INVENTORY.md | Envanter | ~800 satır |
| 4 | docs/FRONTEND_INVENTORY.md | Envanter | ~600 satır |
| 5 | docs/CBSA_Architecture_Diagram.drawio | Diyagram | 5 katman |
| 6 | docs/CBSA_Frontend_Detailed_Diagram.drawio | Diyagram | 5 katman |
| 7 | docs/GUIDE_UTILISATEUR_TRANSFERT_LOCAL.md | Kılavuz | ~500 satır |

**Toplam: CBSA uygulamasını tamamen dokümante eden 7 dosya**

---

## Kazanılan Beceriler

Bu lab'ın sonunda, şunları bileceksiniz:

✅ Bob ile bir mainframe projesi başlatmak  
✅ Bir veri sözlüğü oluşturmak ve sürdürmek  
✅ COBOL kodunun tam envanterlerini oluşturmak  
✅ Frontend/backend mimarilerini dokümante etmek  
✅ Profesyonel mimari diyagramlar oluşturmak  
✅ Karmaşık CICS işlemlerini analiz etmek  
✅ Detaylı kullanıcı kılavuzları yazmak  
✅ Asenkron JCICS API'sini anlamak  
✅ Bob'un farklı modlarını etkili kullanmak  
✅ Kesin ve etkili prompt'lar formüle etmek

---

## Başarı İçin Tavsiyeler

### 1. Prompt Formülasyonu
- ✅ **Kesin olun**: "Analiz kodu" yerine "Frontend'in envanterini çıkar"
- ✅ **Türkçe kullanın**: Bob Türkçe yanıt verecek şekilde yapılandırılmış
- ✅ **Bir seferde bir görev**: Birden fazla karmaşık isteği birleştirmeyin

### 2. Modların Kullanımı
- 🧰 **Z Code**: Tüm mainframe analizleri ve dokümantasyon üretimi için
- 📐 **Z Architect**: Mimari ve tasarım analizleri için (bu lab'da kullanılmadı)
- ❓ **Ask**: Kod değişikliği olmadan sorular için

### 3. Sonuçların Doğrulanması
- ✅ Dosyaların oluşturulduğunu her zaman kontrol edin
- ✅ İçeriklerini doğrulamak için dosyaları açın
- ✅ Draw.io diyagramlarını editörde test edin
- ✅ Bağlamı anlamak için Bob'un açıklamalarını okuyun

### 4. Zaman Yönetimi
- ⏱️ Her alıştırma için tahmini süreleri takip edin
- ⏱️ Uzun alıştırmalar arasında molalar verin
- ⏱️ Bob'dan açıklama istemekten çekinmeyin

---

## Sorun Giderme

### Sorun: Bob yanıt vermiyor
**Çözüm:** Z Code modunda olduğunuzu ve projenin VSCode'da açık olduğunu kontrol edin

### Sorun: Dosya oluşturulmadı
**Çözüm:** Yazma izinlerini ve kullanılabilir disk alanını kontrol edin

### Sorun: Draw.io diyagramı açılmıyor
**Çözüm:** VSCode'da Draw.io Integration uzantısını kurun

### Sorun: Bob İngilizce içerik üretiyor
**Çözüm:** Bob'a hatırlatın: "Lütfen Türkçe yanıtla"

---

## Ek Kaynaklar

- **CBSA Dokümantasyonu**: `doc/CBSA_Architecture_guide.md`
- **Kurulum Kılavuzu**: `etc/install/base/doc/README.md`
- **BMS Kullanıcı Kılavuzu**: `etc/usage/base/doc/CBSA_BMS_User_Guide.md`
- **Bob Dokümantasyonu**: IBM Bob Premium Package for Z Uzantısı

---

## Sonuç

Bu lab, karmaşık mainframe uygulamalarının analizi ve dokümantasyonunda Bob for Z'nin gücünü keşfetmenizi sağladı. Şunları öğrendiniz:

- Kesin sonuçlar elde etmek için farklı prompt türlerini kullanmak
- Otomatik olarak profesyonel dokümantasyon oluşturmak
- Görsel mimari diyagramlar oluşturmak
- Karmaşık CICS işlemlerini anlamak
- REST API'leri ve veri modellerini dokümante etmek

**Sonraki Adımlar:**
- Bu teknikleri kendi mainframe projelerinize uygulayın
- Bob'un diğer modlarını keşfedin (Z Architect, Ask)
- Skill-builder ile kendi özel becerilerinizi oluşturun
- Keşiflerinizi ekibinizle paylaşın

---

**Lab Sürümü:** 1.0  
**Oluşturma Tarihi:** 12 Mayıs 2026  
**Yazar:** Bob - IBM Z için Yapay Zeka Asistanı  
**Toplam Süre:** 2-3 saat

---

© 2026 IBM - CICS Banking Sample Application Lab