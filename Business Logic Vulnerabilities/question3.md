# Inconsistent security controls

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu lab’de admin paneline erişim için email kontrol ediliyor. Ama kullanıcı kayıt olduktan sonra email adresini değiştirebildiği için bu kontrol bypass edilebiliyor.

## 3. Exploitation Steps

1. Önce kendi exploit server email adresimle yeni bir hesap oluşturdum.
2. Email client üzerinden gelen doğrulama mailine tıklayıp hesabı aktif ettim.
3. Hesaba giriş yaptıktan sonra My account kısmından email adresimi `@dontwannacry.com` domaini ile değiştirdim.
4. Email değiştikten sonra admin paneline erişebildiğimi gördüm.
5. Admin panelinden `carlos` kullanıcısını sildim ve lab tamamlandı.

## 4. Impact

Kullanıcı sadece email adresini değiştirerek admin yetkisi alabilir ve admin paneline erişebilir.

## 5. Remediation

Yetki kontrolü email domainine göre yapılmamalı. Kullanıcı rolleri server tarafında tutulmalı ve email değişince yetki otomatik verilmemeli.
