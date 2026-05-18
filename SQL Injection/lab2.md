# SQL injection vulnerability allowing login bypass

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu labda login formundaki kullanıcı adı alanı SQL injection'a açıktı. Bu yüzden parola kontrolünü devre dışı bırakıp admin hesabına şifreyi bilmeden giriş yapmak mümkün oldu.

## 3. Exploitation Steps

1. Login ekranında önce normal birkaç deneme yaptım.
2. Sonra kullanıcı adı alanına tek tırnak koyunca input'un sorguda doğrudan kullanıldığını düşündüren bir davranış aldım.
3. Admin kullanıcısını hedefleyip sorgunun geri kalanını yorum satırına almaya çalıştım:

```sql
administrator'--
```

4. Şifre alanına rastgele bir şey yazdım.
5. Sorguda parola kısmı çalışmadığı için uygulama beni `administrator` olarak içeri aldı.
6. Lab tamamlandı.

## 4. Impact

Saldırgan, parola bilmeden yönetici hesabına giriş yapabilir. Bu da doğrudan hesap ele geçirme ve yetkisiz erişim anlamına gelir.

## 5. Remediation

Login sorgusu string birleştirme ile kurulmamalı. Kullanıcı adı ve şifre mutlaka parametreli sorguyla kontrol edilmeli. Ayrıca login tarafındaki hata mesajları da gereksiz ipucu vermemeli.
