# Lab: Bob Premium for Z Skill'i - COBOL Üretimi ve Doğrulaması

## Hedef

Bu lab, **Bob Premium for Z** skill'ini kullanarak CICS ile IBM Enterprise COBOL for z/OS standartlarına uygun COBOL programları oluşturmayı, ardından **Z Open Editor** ile sözdizimini otomatik olarak doğrulamayı gösterir. Z Open Editor'de, oluşturulan dosyayı açabilir ve sözdizimini doğrudan editörde doğrulayabilirsiniz. zCodeScan kurallarını yapılandırarak sözdizimi kurallarını değiştirme olanağınız vardır (https://www.ibm.com/docs/en/developer-for-zos/17.0.x?topic=overview-linting-zcodescan).

## Ön Koşullar

- Z Open Editor kurulu VS Code
- CBSA workspace'i açık

## Kodlama standartlarının tanımlanması

Skill'i oluşturmadan önce, mevcut koddan COBOL dili için kodlama standartlarını tanımlayacağız.

### Bob Prompt'u
```text
Mevcut COBOL programlarını analiz ederek COBOL kodlama standartlarını tanımla.
```
### Sonuç
**docs/GLOBAL-docu-standards-cobol.md**'de tanımlanan COBOL kodlama standartları.

BNKMENU, BNK1CAC, CREACC, ABNDPROC ve BANKDATA programlarının analizinden türetilen standartlar
Program yapısı, adlandırma, copybook'lar, CICS/SQL yönetimi, abend'ler, doğrulamalar ve veri erişimi hakkında resmileştirilmiş kurallar



## Skill'in Oluşturulması
COBOL programı oluşturacak ve kodlama standartlarına göre doğrulayacak ve Z Open Editor ile sözdizimini doğrulayacak bir Bob Premium for Z skill'i oluşturmak için skill builder'ı kullanacağız.


### Bob Prompt'u

```text
Skill builder'ı kullanarak şunları yapan bir Bob Premium for Z skill'i oluştur:
- docs/GLOBAL-docu-standards-cobol.md'de tanımlanan kodlama standartlarına uyan bir COBOL programı oluştur
- ardından Z Open Editor kullanarak oluşturulan COBOL'un sözdizimini ve standardını doğrula. Sözdizimi hataları Bob tarafından düzeltilmelidir.
```
### Sonuç

Bob, `.bob/skills/` içinde `cobol-generator-validator` skill'ini oluşturmak için `coding-standards-skill-builder` skill'ini kullanacaktır:
- `skill.yaml`: skill yapılandırması
- `skill.py`: üretim ve doğrulama mantığı
- `templates/`: COBOL kod şablonları
- `requirements.txt`: bağımlılıklar


## Skill'in Etkinleştirilmesi

Skill, şu ifadelerle otomatik olarak etkinleşir:
- "Bir COBOL programı oluştur"
- "Bir COBOL oluştur"
- "COBOL'u doğrula"
- "Bob Premium for Z"

## Örnek 1: Basit Bir Programın Oluşturulması

### İstek

```
Telefon numarasından bir müşterinin hesabını bulan bir COBOL programı oluştur
```

### Beklenen Sonuç

Bob şunları yapacak:

1. **Telefon ile arama programının gereksinimlerini analiz etmek**
2. **Telefon alanı için CUSTOMER copybook yapısını kontrol etmek**
3. **IBM standartlarına uygun COBOL programı oluşturmak**
4. **Z Open Editor ile doğrulamak**
5. **Tespit edilen hataları düzeltmek**



## Örnek 2: BMS Map ile CICS Programı

### İstek

```
Bob Premium for Z ile banka hesabı bilgilerini görüntülemek ve güncellemek için bir BMS map kullanan bir COBOL programı oluştur.
Program UPDTACCT olarak adlandırılmalı ve pseudo-conversational kalıbı kullanmalıdır.
```

### Beklenen Sonuç

Bob, şunlarla tam bir program oluşturur:
- Pseudo-conversational kalıp (COMMAREA)
- BMS map yönetimi (SEND/RECEIVE)
- Kullanıcı girişlerinin doğrulanması
- MAPFAIL hata yönetimi
- DISPLAY-MODE ve UPDATE-MODE yapısı

## Uygulanan Standartlar

### 1. Derleme Direktifleri

**CICS Standardı:**
```cobol
PROCESS CICS,NODYNAM,NSYMBOL(NATIONAL),TRUNC(STD)
CBL CICS('SP,EDF')
```

**CICS + DB2:**
```cobol
PROCESS CICS,NODYNAM,NSYMBOL(NATIONAL),TRUNC(STD)
CBL CICS('SP,EDF')
CBL SQL
```

**CICS + DLI:**
```cobol
PROCESS CICS,NODYNAM,NSYMBOL(NATIONAL),TRUNC(STD)
CBL CICS('SP,EDF,DLI')
```

### 2. Adlandırma Sözleşmeleri

| Öğe | Sözleşme | Örnek |
|---------|-----------|---------|
| WS değişkenleri | `WS-` + açıklayıcı | `WS-CUSTOMER-ID` |
| Paragraflar | Fiil + nesne | `PROCESS-CUSTOMER-RECORD` |
| Koşul adları | Açıklayıcı durum | `VALID-CUSTOMER` |
| Sabitler | Büyük harf + tireler | `MAX-RECORDS` |

### 3. CICS Hata Yönetimi

**Zorunlu Kalıp:**
```cobol
EXEC CICS [COMMAND]
    [PARAMETERS]
    RESP(WS-CICS-RESP)
    RESP2(WS-CICS-RESP2)
END-EXEC.

IF WS-CICS-RESP NOT = DFHRESP(NORMAL)
    MOVE '[OPERATION]' TO WS-ERROR-OPERATION
    PERFORM HANDLE-CICS-ERROR
END-IF.
```



## Sonuç

**Bob Premium for Z** skill'i, IBM Enterprise COBOL for z/OS standartlarına uygun CICS ile COBOL programlarının üretim ve doğrulama sürecini tamamen otomatikleştirir.

**Ana avantajlar:**
- ✅ Standartlara uygun otomatik üretim
- ✅ Z Open Editor ile doğrulama
- ✅ Hataların otomatik düzeltilmesi
- ✅ Tam dokümantasyon
- ✅ Üretime hazır kod

**Başlamak için:**
Sadece "Bob Premium for Z ile bir COBOL programı oluştur" deyin ve talimatları izleyin!

---

**Sürüm**: 1.0.0  
**Tarih**: 2026-05-12  
**Yazar**: Bob for Z Ekibi