High-level logic vulnerability

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu lab’de ürünü sepete eklerken `quantity` bilgisi eksi değer girilebiliyor ve bu server tarafında kontrol edilmiyor

## 3. Exploitation Steps

1. Ürünü sepete eklerken “add to cart” butonuna tıkladıktan sonra giden isteği görmek için isteği intercept ile yakaladım ve Repeater’a attım.
2. Repeater’da `quantity` değerinin değiştirilebileceği görülüyor. `quantity` değerini -15 yaptım ve isteği gönderdim
3. Toplam fiyat negatif bir değer oldu. Sistem bunu kabul etmediği için diğer ürünlerden ekleyerek toplam fiyatı 0'dan büyük yaptım ve siparişi tamamladım

## 4. Impact

Kullanıcı sepet toplamını düşürerek pahalı ürünleri ucuza alabilir.

## 5. Remediation

Quantity değeri server tarafında kontrol edilmeli. Negatif değer kabul edilmemeli ve toplam fiyat server tarafında hesaplanmalı.
