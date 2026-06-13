# Basic SSRF against the local server

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu labda ürün stok kontrolü için kullanılan `stockApi` parametresi, sunucu tarafında verilen URL'e istek atıyor. Uygulama bu parametreyi yeterli şekilde doğrulamadığı için isteği dış bir stok servisi yerine local server üzerindeki admin paneline yönlendirebildim. `http://localhost/admin` üzerinden admin paneline erişip `carlos` kullanıcısını silerek labı çözdüm.

## 3. Kullanılan Payload

```http
stockApi=http://localhost/admin
```

Carlos kullanıcısını silmek için kullanılan endpoint:

```http
stockApi=http://localhost/admin/delete?username=carlos
```

## 4. Exploitation Steps

1. İlk olarak ürün detay sayfasında stok kontrolü fonksiyonunu tespit ettim.

![Ürün detay sayfasındaki stok kontrolü](images/lab1/1.png)

2. `Check stock` isteğini Burp Suite ile yakaladım. İstek içinde `stockApi` parametresinin backend tarafından çağrılan URL'i taşıdığını gördüm.

![stockApi parametresinin yakalanması](images/lab1/2.png)

3. `stockApi` değerini local server üzerindeki admin panelini gösterecek şekilde değiştirdim.

```http
stockApi=http://localhost/admin
```

![stockApi değerinin localhost admin paneline değiştirilmesi](images/lab1/3.png)

4. İsteği gönderdiğimde response içinde local server üzerindeki admin paneli döndü. Bu sayede SSRF ile normalde dışarıdan erişilemeyen admin paneline sunucu üzerinden erişmiş oldum.

![Local admin panelinin response içinde görüntülenmesi](images/lab1/4.png)

5. Admin panelindeki delete endpoint'ini kullanarak `carlos` kullanıcısını silmek için `stockApi` parametresini aşağıdaki şekilde güncelledim.

```http
stockApi=http://localhost/admin/delete?username=carlos
```

![Carlos kullanıcısını silen SSRF isteği](images/lab1/5.png)

6. İstek gönderildikten sonra `carlos` kullanıcısı silindi ve lab başarıyla çözüldü.

![Lab solved](images/lab1/6.png)

## 5. Impact

SSRF zafiyeti sayesinde saldırgan, uygulama sunucusunu kendi adına istek yapan bir aracı gibi kullanabilir. Bu durumda dışarıdan erişilemeyen internal servisler, local admin panelleri veya metadata servisleri hedeflenebilir. Yetki kontrolü zayıf olan internal endpoint'ler üzerinden kullanıcı silme gibi kritik işlemler yapılabilir.

## 6. Remediation

Sunucu tarafında kullanıcıdan gelen URL'ler doğrudan çağrılmamalıdır. `stockApi` gibi parametrelerde allowlist yaklaşımı uygulanmalı, yalnızca beklenen host ve path değerlerine izin verilmelidir. `localhost`, private IP aralıkları, link-local adresler ve internal domain'lere giden istekler engellenmelidir. Ayrıca admin endpoint'leri yalnızca network konumuna güvenmemeli; her istekte güçlü authentication ve authorization kontrolleri yapmalıdır.
