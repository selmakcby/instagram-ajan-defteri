# Kurulum promptu

Videoda Claude Code'a verdiğim prompt. Köşeli parantezleri kendine göre değiştir.

```
Her gün [video] üretiyorum. Bazılarını paylaşıyorum, bazılarını paylaşmıyorum.
Hangisinin tuttuğunu takip edecek, 7/24 açık bir sunucuda yaşayan bir ajan istiyorum.
Her sabah [Instagram] hesabımın sayılarını çeksin.
Bir tabloya yazsın.
Bana [Telegram]'dan kısa bir rapor atsın.
İnternette içerik olabilecek konular bulsun.
Her gece ne öğrendiğini bir dosyaya not etsin.
Kısıtlar: Hiçbir şey paylaşmasın, beğenmesin, yorum yazmasın. Sadece okusun. Paylaşma düğmesi bende.
```

Bu prompttan sonra Claude Code'a şu dosyaları da göster ki aynı mimariyle kursun:
`README.md` (mimari), `skills/` ve `sablonlar/`.

## Parça parça istemek istersen

**Toplayıcı (modelsiz script):**
```
Instagram Graph API'den, sadece okuma izniyle, son 7 günün içeriklerini ve her birinin
izlenme, beğeni, kaydetme sayılarını çeken bir script yaz. Model kullanma, düz kod olsun.
Sonucu tarihli bir JSON dosyasına yaz, ayrıca tabloya satır olarak ekle.
Token'ı .env'den oku, hiçbir yere basma. Günde bir kez çalışacak.
```

**Doğrulayıcı:**
```
Ajanların JSON çıktısını kontrol eden küçük bir doğrulayıcı yaz. Her çıktı türü için
beklenen alanlar ve tipler belli olsun (skills/ klasöründeki JSON kalıpları).
Alan eksikse, tip yanlışsa, metin çok uzunsa ya da link https değilse çıktıyı reddetsin.
Reddedilen çıktı rapora ve PLAYBOOK'a girmesin.
```

**Zamanlama:**
```
Bu dört işi sunucuda zamanla: toplayıcı 06:30, gözcü 06:45, analist 06:50,
sabah raporu 07:00, öğrenen 23:30. Her işin logu ayrı dosyaya düşsün.
```
