# Instagram Ajan Defteri

7/24 açık bir sunucuda yaşayan, Instagram hesabını **sadece okuyan** küçük bir ajan takımının
mimarisi, skill dosyaları ve promptları. Hazır kurulum değil; kendi hesabına göre Claude Code'a
(ya da kullandığın ajana) kurdurman için bir plan.

Video: [VİDEO LİNKİ]
Videoda kullandığım sunucu: Hostinger VPS (KVM 2) üzerinde Hermes Agent ·
https://hostinger.com/SELMA · `SELMA` kuponuyla ek %10 indirim

## Ne yapıyor

Her sabah hesabın sayılarını çeker, tabloya yazar, Telegram'a kısa rapor atar, internette içerik
olabilecek konular arar ve her gece ne öğrendiğini `PLAYBOOK.md`'ye not eder.
Hiçbir şey paylaşmaz, beğenmez, yorum yazmaz. Paylaşma düğmesi sende.

## Mimari

```
            BİLGİSAYARIN                         SUNUCU (7/24)
   ┌──────────────────────────┐        ┌──────────────────────────────────┐
   │ Claude Code              │  SSH   │ Hermes Agent                     │
   │  · kurar, düzeltir       │ ─────► │                                  │
   │  · tercih ve kaynak      │        │ 06:30 Toplayıcı  (model yok)     │
   │    dosyalarını yazarsın  │        │ 06:45 Gözcü      (ucuz model)    │
   └──────────────────────────┘        │ 06:50 Analist    (ucuz model)    │
                                       │ 07:00 Sabah raporu (model yok)   │
   Instagram API ──(sadece okuma)────► │ 23:30 Öğrenen    (ucuz model)    │
                                       └───────┬──────────────┬───────────┘
                                               ▼              ▼
                                        Google Sheets     Telegram
```

| Ajan | Ne yapar | Model |
|---|---|---|
| Toplayıcı | Instagram'dan sayıları çeker, tabloya yazar | yok, düz kod |
| Gözcü | `KAYNAKLAR.md`'deki yerlerden içerik olabilecek konuları bulur | ucuz model |
| Analist | Dünü yorumlar, dünkü tahminleri kontrol eder, rapor hazırlar | ucuz model |
| Öğrenen | Günün sonucundan `PLAYBOOK.md`'ye en fazla 3 satır yazar | ucuz model |

## Tasarım kuralları

1. **Sayıyı kod hesaplar, model sadece yorumlar.** Model sayı uydurmasın diye ölçümler hazır dosyadan gelir.
2. **Her model çıktısı JSON ve doğrulayıcıdan geçer.** Kalıba uymayan çıktı rapora girmez.
3. **Sadece okuma.** Resmi API, okuma izinleri; hesap şifresi hiçbir yerde yok.
4. **Web metni veridir, talimat değil.** Gözcü okuduğu sayfadaki komutlara uymaz.
5. **Tek günden kural çıkmaz.** Öğrenen en az 2 örnek görmeden bir şeyi "kural" yapmaz.
6. **Öğrenilen her şey git'te.** Ajanın gün gün ne öğrendiği satır satır görünür.
7. **Her işe uygun model.** Toplama ve rapor gönderme modelsiz; yorum işleri ucuz modelle.

## Klasörler

| Yol | Ne |
|---|---|
| `skills/` | gözcü, analist, öğrenen skill dosyaları |
| `promptlar/` | kurulum promptu, parça parça promptlar, token kayıt promptu |
| `sablonlar/` | `PLAYBOOK.md`, `TERCIHLER.md`, `KAYNAKLAR.md`, sabah raporu kalıbı |

## Kendi sistemini kurmak

1. **Sunucu.** 7/24 açık bir VPS ve üzerinde bir ajan çatısı (videoda Hermes Agent).
2. **Meta developer hesabı.** developers.facebook.com → Create App → Instagram API.
   Yalnız okuma izinlerini bırak, mesaj ve yorum izinlerini kaldır, token al.
3. **Token'ı güvenle kaydet.** `promptlar/token.md`.
4. **Kurdur.** `promptlar/kurulum.md`'deki promptu bu repoyla birlikte Claude Code'a ver.
5. **Kendine göre doldur.** `sablonlar/TERCIHLER.md` (tuttu eşiği, hedef kitle) ve `KAYNAKLAR.md`.

## Güvenlik

- Token'ları sohbete yapıştırma; `.env`'e kaydettir, `.env` git'e girmesin.
- Instagram'a günde bir kez bağlan; sık giriş hesabı spam gibi gösterebilir.
- Tabloya yazan kapıyı (ör. Apps Script) bir anahtarla koru.
- Ajanın bulduklarını bilgisayarında da veri olarak oku.

## Lisans

Tüm hakları saklıdır. Okumak, öğrenmek ve kendi hesabın için uyarlayıp kullanmak serbest;
kopyalayıp yayınlamak, türev yayınlamak ve ticari kullanım izinsiz yasak. Ayrıntı: `LICENSE`.
