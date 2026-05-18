# SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

## 1. Lab Bilgisi

**Difficulty:** Apprentice

## 2. Vulnerability Özeti

Bu labda kategori filtresinin arkasındaki SQL sorgusuyla oynayabildiğimizi gördüm. Normalde sadece seçilen kategoriye ait ürünler gelmesi gerekirken, filtre koşulunu bozunca gizli ürünler de sayfaya düştü.

## 3. Exploitation Steps

1. Önce bir kategoriye tıkladım ve URL'de `category` parametresinin değiştiğini fark ettim.
2. Buradan kategori bilgisinin direkt SQL sorgusuna gidiyor olabileceğini düşündüm.
3. Parametreye tek tırnak ekleyince sayfanın davranışı değişti.
4. Sonra koşulu her zaman doğru yapacak basit bir deneme yaptım:

```sql
' OR '1'='1'--
```

5. Bu denemeden sonra sadece seçili kategori değil, gizli olan ürünler de dahil bütün ürünler listelendi ve lab çözüldü.

## 4. Impact

Kullanıcı, kategori filtresini manipüle ederek normalde görmemesi gereken ürünleri veya verileri görüntüleyebilir.

## 5. Remediation

Kullanıcının gönderdiği kategori değeri SQL sorgusuna direkt eklenmemeli. Backend tarafında parametreli sorgu kullanılmalı ve kategori gibi değerler önceden izin verilen değerlerle kontrol edilmeli.
