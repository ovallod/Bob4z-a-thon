# Bob Premium for Z İleri Düzey Alıştırmalar
## Alıştırma 1: Coding Standard Skill | Alıştırma 2: VSAM'dan DB2'ye Yeniden Düzenleme

**Tahmini Süre:** 1-2 saat  
**Seviye:** İleri  
**Ön Koşullar:** COBOL ve CICS bilgisi

---

## 📋 İçindekiler

1. [Alıştırma 1: Özelleştirilmiş Coding Standard Skill Oluşturma](#alıştırma-1--özelleştirilmiş-coding-standard-skill-oluşturma)
2. [Alıştırma 2: VSAM'dan DB2'ye Yeniden Düzenleme](#alıştırma-2--vsamdan-db2ye-yeniden-düzenleme)

---

## Alıştırma 1: Özelleştirilmiş Coding Standard Skill Oluşturma

### 🎯 Hedef

Mevcut COBOL kodunuzu analiz eden ve tüm ekipte kod tutarlılığını garanti etmek için yeniden kullanılabilir dokümante standartlar otomatik olarak oluşturan özelleştirilmiş bir kodlama standardı skill'i oluşturmak.

### 🔧 Kullanılacak Bob Modu

**Mod: 🧰 Z Code**

---

## 📋 Adım Adım Senaryo

### **Adım 1: Skill'in İlk Oluşturulması**

#### 💬 Bob Prompt'u

```
Mevcut COBOL programlarını analiz ederek çalışma alanımda bir kodlama standardı skill'i oluştur
```

#### ⚙️ Bob'un Yaptıkları

Bob şunları yapacak:
1. Workspace'teki tüm COBOL programlarını analiz etmek
2. Tekrarlayan kodlama kalıplarını tanımlamak (adlandırma, yapılar, hata yönetimi)
3. `.bob/` içinde üç dosya oluşturmak:
   - `CBSA-standards-reference.md`: Standartların dokümantasyonu
   - `CBSA-example.md`: Uyumlu kod örnekleri
   - `skills.md`: Skill tanımı

#### ✅ Beklenen Sonuç

Bob, şunları dokümante eden üç dosya oluşturur:
- Adlandırma sözleşmeleri (programlar, değişkenler, paragraflar)
- Standart program yapısı
- Hata yönetimi (0-9 kodları)
- CICS ve SQL kalıpları
- Kod kalitesi kuralları

---

### **Adım 2: Standardın Özelleştirilmesi (İsteğe Bağlı)**

#### 💬 Bob Prompt'u

```
CBSA-standards-reference.md dosyasını aşağıdaki kuralları eklemek için değiştir:
- Sayaç değişkenleri CTR- ile başlamalıdır
- Doğrulama paragrafları -VALIDATION ile bitmelidir
- Loglama standartları hakkında bir bölüm ekle
```

#### ⚙️ Bob'un Yaptıkları

Bob, referans dosyasını özel kurallarınızla günceller ve yeni sözleşmeleri skill'e entegre eder.

---

### **Adım 3: Standartla Kod Üretimi**

#### 💬 Bob Prompt'u

```
Şunları yapan bir COBOL programı oluştur:
- E-postasıyla bir müşteri arar
- E-posta formatını doğrular
- Bulunursa müşteri bilgilerini döndürür
- Tüm olası hataları yönetir

Yapı ve sözleşmeler için CBSA-standards-reference.md'yi takip et
```

#### ⚙️ Bob'un Yaptıkları

Bob şunları yapacak:
1. `CBSA-standards-reference.md` dosyasını okumak
2. Tüm dokümante edilmiş standartları uygulamak
3. Tam ve uyumlu bir COBOL programı oluşturmak (örn: `BNKINQE.cbl`)
4. Kodu uygun yorumlarla dokümante etmek

---

## 💡 Katma Değer

| Yön | Skill Olmadan | Skill ile |
|--------|-----------|-----------|
| Standart analizi | 2-3 gün | 2 dakika |
| Dokümantasyon | Eksik | Kapsamlı |
| Kod üretimi | Değişken standartlar | Garantili standartlar |
| Tutarlılık | Değişken | %100 |
| Başlangıç | 2-3 hafta | 1-2 gün |

**Global kazanç: %95 süre azalması**

---

## 📋 Kullanım Durumları

1. **Başlangıç**: Yeni geliştiriciler için standartların net referansı
2. **Modernizasyon**: Eskiyle tutarlı yeni kod üretimi
3. **Harmonizasyon**: Tüm organizasyon için birleşik standartlar
4. **Denetim**: Dokümante edilmiş ve izlenebilir standartlar

---

## 🎓 Hatırlanması Gereken Ana Noktalar

### ✅ Avantajlar

- **Otomasyon**: Bob kalıpları otomatik olarak çıkarır
- **Yeniden Kullanılabilirlik**: Skill tüm gelecekteki geliştirmelerinize uygulanır
- **Tutarlılık**: Kod tekdüzeliğini garanti eder
- **Evrimsel**: Skill zaman içinde güncellenebilir

### ⚠️ Dikkat Noktaları

1. İlk oluşturmada tespit edilen standartları kontrol edin
2. Oluşturulan dosyaları özel ihtiyaçlarınıza göre uyarlayın
3. Standartlarınız evrimleştiğinde skill'i güncelleyin
4. Skill'i tüm ekiple paylaşın

---

## Alıştırma 2: VSAM'dan DB2'ye Yeniden Düzenleme

### 🎯 Hedef

VSAM dosyaları kullanan mevcut bir COBOL programını DB2 kullanacak şekilde yeniden düzenlemek, fonksiyonel uyumluluğu korurken ve performansı iyileştirmek.

### 🔧 Kullanılacak Bob Modu

**Mod: 📐 Z Architect**

---

## 📋 Adım Adım Senaryo

### **Adım 0: extractionGoal.md Belgesinin Oluşturulması**

#### 💬 Bob Prompt'u

```
VSAM'dan DB2'ye geçiş için yeniden düzenleme ilkelerini tanımlayan bir extractionGoal.md belgesi oluştur, şunları içerecek şekilde:

1. Fonksiyonelliğin Korunması
2. VSAM İşlemlerinin SQL'e Eşlenmesi
3. İşlemsel Yönetim
4. Sıralı Geçişlerin Optimizasyonu
5. Sağlam Hata Yönetimi
6. Host Değişkenlerinin Kullanımı
7. Performans Optimizasyonu
8. Yapı ve Modülerlik
9. Uyumluluk ve Aşamalı Geçiş
10. Dokümantasyon ve İzlenebilirlik

Ayrıca bir yeniden düzenleme kontrol listesi ve başarı kriterlerini de dahil et.
```

#### ⚙️ Bob'un Yaptıkları

Bob, şunları içeren `extractionGoal.md` dosyasını (485 satır) oluşturur:
- COBOL örnekleriyle 10 detaylı ilke
- VSAM→DB2 karşılık tabloları
- 3 aşamada kontrol listesi
- Ölçülebilir başarı kriterleri

---

### **Adım 1: Mevcut VSAM Programının Analizi**

#### 💬 Bob Prompt'u

```
VSAM dosyaları kullanan BNKCUST programını analiz et ve şunları tanımla:
- Kullanılan VSAM işlemleri (READ, WRITE, REWRITE, DELETE, STARTBR, READNEXT)
- İşlenen veri yapıları
- Erişim anahtarları ve indeksler
- Veri erişim kalıpları
- Geçiş için karmaşıklık noktaları
```

#### ⚙️ Bob'un Yaptıkları

Bob şunları yapacak:
1. Tüm CICS VSAM komutlarını tanımlamak için COBOL kodunu analiz etmek
2. Veri yapılarını çıkarmak (copybook'lar, working-storage)
3. Kullanılan birincil ve ikincil anahtarları tanımlamak
4. Erişim kalıplarını dokümante etmek
5. Her işlem için geçiş karmaşıklığını değerlendirmek

#### ✅ Beklenen Sonuç

Bob, şunlarla detaylı bir analiz raporu oluşturur:
- Kullanılan VSAM dosyaları (tür, anahtarlar, uzunluk)
- Tanımlanan işlemler (READ, STARTBR/READNEXT, REWRITE, WRITE, DELETE)
- Geçiş karmaşıklığı tablosu
- Öneriler (DB2 tablosu oluştur, işlemleri değiştir, indeks ekle)

---

### **Adım 2: DB2 Veri Modelinin Tasarımı**

#### 💬 Bob Prompt'u

```
CUSTOMER VSAM dosyasını değiştirmek için bir DB2 veri modeli öner, şunları içerecek şekilde:
- Tablonun DDL tanımı
- Gerekli indeksler
- Bütünlük kısıtlamaları
- Performans değerlendirmeleri
```

#### ⚙️ Bob'un Yaptıkları

Bob şunları yapacak:
1. Mevcut VSAM yapısını analiz etmek
2. Optimal DB2 şemasını tasarlamak
3. DDL scriptlerini oluşturmak (CREATE TABLE, INDEX, CONSTRAINTS)
4. Uygun indeksleri önermek
5. Tasarım kararlarını dokümante etmek

#### ✅ Beklenen Sonuç

Bob şunları oluşturur:
- CUSTOMER tablosu için tam DDL scriptleri
- Birincil ve ikincil anahtarlar üzerinde indeksler
- CHECK ve DEFAULT kısıtlamaları
- Tasarım kararlarının dokümantasyonu

---

### **Adım 3: Skill Komutuyla Etkileşimli Yeniden Düzenleme**

#### 💬 Bob Prompt'u (Mod 🧰 Z Code)

```
/refactor BNKCUST.cbl extractionGoal.md
```

**Açıklama**:
- `/refactor`: Etkileşimli yeniden düzenleme skill'inin komutu
- `BNKCUST.cbl`: Yeniden düzenlenecek kaynak dosya
- `extractionGoal.md`: İlkeleri içeren belge

#### ⚙️ Bob'un Yaptıkları

Bob, 4 aşamada **etkileşimli yeniden düzenleme iş akışını** başlatır:

**Aşama 1 - Analiz**:
- Tüm VSAM işlemlerini tespit eder
- extractionGoal.md'den ilkeleri yükler
- Bir yeniden düzenleme planı önerir

**Aşama 2 - Doğrulama**:
- Her VSAM→SQL dönüşümünü sunar
- Kullanıcı onayı ister

**Aşama 3 - Üretim**:
- Yeniden düzenlenmiş kodu aşamalı olarak oluşturur
- READ'i SELECT ile, STARTBR/READNEXT'i CURSOR ile vb. değiştirir
- İşlemsel yönetim ekler (COMMIT/ROLLBACK)

**Aşama 4 - Nihai Rapor**:
- ÖNCE/SONRA karşılaştırma raporu oluşturur
- Tüm değişiklikleri dokümante eder

#### ✅ Beklenen Sonuç

Şunlarla yeniden düzenlenmiş COBOL programı:
- Tüm VSAM işlemleri SQL ile değiştirilmiş
- Sıralı geçişler için DB2 cursor'ları
- Tam işlemsel yönetim
- Sağlam SQL hata yönetimi
- COMMAREA uyumluluğu korunmuş

---

### **Adım 4: Geçiş Planı ve Testler**

#### 💬 Bob Prompt'u

```
VSAM'dan DB2'ye geçmek için tam bir geçiş planı oluştur, şunları içerecek şekilde:
- Geçiş adımları
- Test stratejisi
- Geri alma planı
- Performans değerlendirmeleri
- Doğrulama kontrol listesi
```

#### ⚙️ Bob'un Yaptıkları

Bob, 5 aşamada detaylı bir geçiş planı oluşturur:

1. **Hazırlık**: DB2 ortamı oluşturma, veri geçişi
2. **Geliştirme**: Kod yeniden düzenleme, birim testleri
3. **Entegrasyon Testleri**: Fonksiyonel, performans, yük testleri
4. **Dağıtım**: Geçiş, dağıtım sonrası doğrulama
5. **Stabilizasyon**: İzleme, optimizasyon

Ayrıca şunları içerir:
- Geri alma planı (2 senaryo)
- Risk ve azaltma matrisi
- Nihai doğrulama kontrol listesi

---

## 💡 Katma Değer

| Yön | Manuel Yaklaşım | Bob ile |
|--------|-------------------|----------|
| VSAM analizi | 2-3 gün | 10 dakika |
| DB2 tasarımı | 3-5 gün | 15 dakika |
| Kod yeniden düzenleme | 1-2 hafta | 30 dakika |
| Geçiş planı | 3-5 gün | 20 dakika |

**Global kazanç: %90-95 süre azalması**

---

## 📋 Kullanım Durumları

1. **Aşamalı Modernizasyon**: VSAM dosyalarının aşamalı geçişi
2. **Performans İyileştirme**: DB2 ile daha hızlı karmaşık sorgular
3. **Modern Entegrasyon**: Web/mobil uygulamalardan veri erişimi
4. **Uyumluluk ve Denetim**: Garantili referans bütünlüğü

---

## 🎓 Hatırlanması Gereken Ana Noktalar

### ✅ Geçişin Avantajları

- **Performans**: Karmaşık sorgular için optimize edilmiş DB2
- **Bütünlük**: Kısıtlamalar ve ACID işlemleri
- **Esneklik**: Standart SQL, birleştirmeler, toplamalar
- **Entegrasyon**: Diğer sistemlerden kolaylaştırılmış erişim

### ⚠️ Dikkat Noktaları

1. Üretimden önce gerçek yük altında test edin
2. Mevcut COMMAREA arayüzünü koruyun
3. COMMIT/ROLLBACK'i doğru yönetin
4. Geçişten sonra DB2'yi izleyin
5. Ekibi SQL ve DB2 konusunda eğitin

### 💡 İyi Uygulamalar

- **Kapsamlı testler**: Tüm senaryoları doğrulayın
- **Aşamalı geçiş**: Bir seferde bir program
- **Sürekli izleme**: DB2 performansını izleyin
- **Geri alma hazır**: Test edilmiş yedek plan

---

## 🚀 Ana Prompt'ların Özeti

### Alıştırma 1 - Kodlama Standartları

```
1. Mevcut COBOL programlarını analiz ederek çalışma alanımda bir kodlama standardı skill'i oluştur

2. CBSA-standards-reference.md dosyasını aşağıdaki kuralları eklemek için değiştir: [...]

3. [...] yapan bir COBOL programı oluştur CBSA-standards-reference.md'yi takip et
```

### Alıştırma 2 - VSAM→DB2 Yeniden Düzenleme

```
1. VSAM'dan DB2'ye geçiş için yeniden düzenleme ilkelerini tanımlayan bir extractionGoal.md belgesi oluştur [...]

2. VSAM dosyaları kullanan BNKCUST programını analiz et ve şunları tanımla: [...]

3. CUSTOMER VSAM dosyasını değiştirmek için bir DB2 veri modeli öner [...]

4. /refactor BNKCUST.cbl extractionGoal.md

5. VSAM'dan DB2'ye geçmek için tam bir geçiş planı oluştur [...]
```

---

## 📊 Ölçülebilir Kazançlar

| Alıştırma | Görev | Bob Olmadan | Bob ile | Kazanç |
|----------|-------|----------|----------|------|
| **1** | Kodlama Standartları | 2-3 gün | 2 dakika | %99.9 |
| **2** | VSAM→DB2 Geçişi | 3-4 hafta | 75 dakika | %99.5 |

---

**Sürüm**: 1.0  
**Tarih**: 2 Haziran 2026  
**Yazar**: Bob Premium for Z Ekibi

**Mainframe ile çalışma şeklinizi dönüştürün! 🚀**