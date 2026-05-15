# SQL injection attack, querying the database type and version on Oracle

## 1. Lab Bilgisi

**Difficulty:** Practitioner

## 2. Vulnerability Özeti

Bu labda SQL injection üzerinden veritabanının Oracle olduğunu ve versiyon bilgisini çıkarmak gerekiyordu. Yine kategori filtresi üzerinden ilerledim.

## 3. Exploitation Steps

1. Kategori parametresine ufak denemeler yaparak başladım.
2. Tek tırnakla hata alınca buranın SQL sorgusuna temas ettiğini anladım.
3. Sonra `UNION SELECT` ile sayfanın kaç kolon beklediğini bulmaya çalıştım.
4. Oracle tarafında boş `SELECT` atılamadığı için `dual` tablosunu kullanmak gerekti. İki kolonla sayfa düzgün cevap verdi:

```sql
' UNION SELECT NULL,NULL FROM dual--
```

5. Bundan sonra versiyon bilgisini basmak için Oracle'ın versiyon bilgisini tuttuğu yerden veri çektim:

```sql
' UNION SELECT banner,NULL FROM v$version--
```

6. Sayfada veritabanı banner bilgisi görününce lab tamamlandı.

## 4. Impact

Bu zafiyet saldırgana veritabanı hakkında teknik bilgi verir. Tek başına bile değerli bir bilgi sızıntısıdır, çünkü sonraki adımlarda veritabanına özel payload hazırlamayı kolaylaştırır.

## 5. Remediation

Kullanıcı girdisi SQL'e direkt eklenmemeli ve parametreli sorgular kullanılmalı. Ayrıca uygulama kullanıcısının gereksiz sistem tablolarına erişimi olmamalı.
