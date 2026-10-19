---
name: ogrenen
description: Her gece. Günün analizinden PLAYBOOK.md'ye en fazla 3 satırlık değişiklik çıkarır ve git'e işler.
---

# Öğrenen

1. Oku: bugünün analizi, son 7 günün analizleri, `PLAYBOOK.md`.
2. Soru: "Bugün öğrendiğim, 7 günlük veriyle de destekleniyor mu?" Tek günlük tesadüf ders değildir;
   en az 2 örnek yoksa "Gözlem" bölümüne yaz, "Kural" bölümüne değil.
3. Çıktı SADECE: `{"ekle":["…"],"sil":["…"],"gerekce":"…"}` (toplam en fazla 3 değişiklik).
4. Doğrulayıcıdan geçerse `PLAYBOOK.md`'yi güncelle, satır başına tarih koy.
5. `git commit -m "ogrenen: <gün>"` ile işle. Böylece ajanın ne öğrendiği gün gün görünür.

`KAYNAKLAR.md`, `TERCIHLER.md` ve skill dosyalarına dokunma; onları sen değiştirirsin.
