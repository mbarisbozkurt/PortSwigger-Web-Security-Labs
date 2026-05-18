# Inconsistent handling of exceptional input

## 1. Lab Bilgisi

**Difficulty:** Practitioner

## 2. Vulnerability Özeti

Email alanı uzun girildiğinde sistem emaili bir yerde kesiyor. Bu yüzden emailin sonu `@dontwannacry.com` gibi görünecek şekilde ayarlanabiliyor ve admin yetkisi alınabiliyor.

## 3. Exploitation Steps

1. Register isteğini Burp ile yakaladım ve Repeater’a attım.
2. Email kısmına uzun bir değer girdim. Sonuna da `@dontwannacry.com.exploit-server.net` ekledim.
3. `A` sayısını değiştirerek My account kısmında görünen emailin `@dontwannacry.com` ile bitmesini sağladım.
4. Email client üzerinden gelen doğrulama linkine tıkladım ve hesabı aktif ettim.
5. Hesaba giriş yaptıktan sonra admin paneline erişebildiğimi gördüm.
6. Admin panelinden `carlos` kullanıcısını sildim ve lab tamamlandı.

## 4. Impact

Kullanıcı email alanındaki kesme hatasını kullanarak admin yetkisi alabilir.

## 5. Remediation

Email uzunluğu ve formatı server tarafında doğru kontrol edilmeli. Farklı yerlerde farklı uzunlukta email saklanmamalı ve yetki kontrolü sadece email domainine göre yapılmamalı.
