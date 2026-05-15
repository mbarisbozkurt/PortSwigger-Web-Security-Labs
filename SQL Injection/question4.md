# SQL injection attack, querying the database type and version on MySQL and Microsoft

## 1. Lab Bilgisi

**Difficulty:** Practitioner

## 2. Vulnerability Özeti

Bu lab da kategori filtresi üzerinden ilerliyordu. Ama bu kez hedef Oracle değil, MySQL veya Microsoft SQL Server tarafında versiyon bilgisini almaktı.

## 3. Exploitation Steps

1. İlk olarak kategori parametresine tek tırnak ekleyip sorgunun kırılıp kırılmadığını kontrol ettim.
2. Ardından `UNION SELECT` ile kolon sayısını denedim.
3. İki kolonla sonuç alabildiğimi görünce versiyon bilgisini ekrana bastırmaya çalıştım.
4. Kullandığım deneme şu şekildeydi:

```sql
' UNION SELECT @@version,NULL--
```

5. Bazı MySQL yorum satırı durumlarında `--` sonrasında boşluk gerekebiliyor. Takılırsa aynı mantıkla `#` yorum karakteri de denenebilir:

```sql
' UNION SELECT @@version,NULL#
```

6. Versiyon bilgisi ürün listesinin içinde görününce lab çözülmüş oldu.

## 4. Impact

Burada önemli olan şey sadece versiyon bilgisini görmek değil. Uygulamanın, kullanıcının verdiği değeri sorguya doğrudan koyduğunu anlamış oluyoruz. Bu da veri sızıntısına ve daha ileri SQL injection saldırılarına kapı açabilir.

## 5. Remediation

Backend tarafında parametreli sorgu kullanılmalı. Veritabanı hata ve versiyon bilgileri kullanıcıya yansıtılmamalı.
