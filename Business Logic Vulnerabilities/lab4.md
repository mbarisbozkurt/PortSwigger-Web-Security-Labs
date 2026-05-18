# Flawed enforcement of business rules

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu lab’de kupon kullanımında mantık hatası var. Aynı kupon arka arkaya kullanılamıyor ama iki farklı kupon sırayla kullanıldığında tekrar uygulanabiliyor.

## 3. Exploitation Steps

1. Önce pahalı ürünü sepete ekledim.
2. Sayfanın üstünde verilen `NEWCUST5` kuponunu uyguladım.
3. Daha sonra sitede başka bir kupon olan `SIGNUP30` kuponunu buldum.
4. `NEWCUST5` ve `SIGNUP30` kuponlarını sırayla uyguladım.
5. Bu işlemi birkaç kere tekrar edince toplam fiyat `0` oldu ve siparişi tamamladım.

## 4. Impact

Kullanıcı kuponları sırayla tekrar kullanarak ürünleri ücretsiz veya çok ucuza alabilir.

## 5. Remediation

Kupon kullanımı server tarafında kontrol edilmeli. Aynı kuponun bir kullanıcı veya sepet için tekrar kullanılmasına izin verilmemeli.
