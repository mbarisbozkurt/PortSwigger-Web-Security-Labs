# Excessive trust in client-side controls

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu lab’de ürünü sepete eklerken `price` bilgisini kullanıcıdan aldığı için zafiyet var.

## 3. Exploitation Steps

1. Ürünü sepete eklerken “add to cart” butonuna tıkladıktan sonra giden isteği görmek için isteği intercept ile yakaladım ve Repeater’a attım.
2. Repeater’da `price` değerinin kullanıcıdan alındığı görülüyor. Browser’da fiyat `1337$` görünüyor. Son 2 sayıyı decimal olarak alıyor. Basitçe `price` değerini `1` olarak değiştirdim.
3. Normalde fiyatı `1337$` olan ürün `0.01$` oldu.

## 4. Impact

Price yani fiyat bilgisi kullanıcıdan alındığı için kullanıcı istediği ürünü ucuza alabilir.

## 5. Remediation

Fiyat bilgisi kullanıcıdan alınmamalı. Backend’de veritabanından çekilmeli.
