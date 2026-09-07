# DiskHealth – USB'den çalışan disk sağlık kontrol aracı

USB belleğe kopyalanır, Windows 7/8/8.1/10/11'de **kurulum yapmadan** çalışır, her disk için tek bakışta karar verir:

**KULLANILABİLİR · KOŞULLU KULLANILABİLİR · KULLANILAMAZ · KARAR VERİLEMEDİ**

Karar iki kanıta dayanır: hızlı S.M.A.R.T. taraması (saniyeler) ve isteğe bağlı **derin test** (diskten gerçek okuma + diskin kendi disk içi testi, 2-5 dk). S.M.A.R.T. uyarısı vermeden bozulan diskleri derin test yakalar; her kararın yanında güven seviyesi ("Hızlı kontrol" / "Kısmen doğrulandı" / "Doğrulandı") yazar.

## Kullanım
1. Bu depoyu indirin (Code → Download ZIP) ve klasörü USB belleğe kopyalayın. Kullanım sonrası `Reports\` klasöründeki raporlar makine adı ve disk seri numarası içerir; USB'yi başkasına verirken boşaltın.
2. Kontrol edilecek bilgisayarda `DiskHealth.exe` dosyasına çift tıklayın. UAC (yönetici izni) sorusuna **Evet** deyin.
3. **Tara** düğmesine basın; diskler ve kararları birkaç saniyede listelenir.
4. Kesin karar için bir disk seçip **Derin test** düğmesine basın (veri silinmez, bilgisayar kullanılmaya devam edilebilir).
5. Diske tıklayınca sağda "Kolay özet" sekmesinde hızlı tarama ve derin test bulguları, her biri için "Ne yapmalı" açıklaması görünür. Rapor (HTML + JSON) `Reports\` klasörüne otomatik kaydedilir.

## Desteklenen sistemler
Windows 7 SP1, 8, 8.1, 10, 11 (32/64 bit). Kurulum gerekmez:
- `DiskHealth.exe` küçük bir başlatıcıdır ve her Windows'ta açılır. .NET Framework 4.5+ varsa (Windows 8 ve sonrası, güncel Windows 7) modern arayüzü (`DiskHealth.Wpf.exe`) açar.
- Güncelleme almamış Windows 7'de otomatik olarak `win7\DiskHealth.Classic.exe` (.NET 3.5) sürümünü açar.

## Dosyalar
| Dosya | Açıklama |
|---|---|
| `DiskHealth.exe` | Başlatıcı: .NET sürümüne göre doğru programı açar |
| `DiskHealth.Wpf.exe` | Ana program (WPF, .NET Framework 4.5) |
| `win7\` | Windows 7 için .NET 3.5 sürümü |
| `rules.json` | Karar kuralları ve eşik değerleri (programdaki Ayarlar → Karar eşikleri ile düzenlenir) |
| `settings.json` | Ayarlar (rapor klasörü, derin test boyutu, disk içi test bekleme süresi vb.; Ayarlar penceresinden düzenlenir) |
| `tools\` | smartmontools 7.5 `smartctl.exe` (GPL v2, `COPYING.txt`, kaynak notu `SOURCE.txt`) |
| `Reports\` | Raporlar |

## Komut satırı
```
DiskHealth.exe /auto          pencere açmadan tarar, raporu kaydeder; çıkış kodu 0 kullanılabilir, 1 koşullu, 2 kullanılamaz, 3 kablo/soğutma, 4 karar verilemedi, 10 hata
DiskHealth.exe /auto /deep    önce her diske derin test uygular
```

## Notlar
- "Kullanılabilir" yalnızca "bu taramada arıza belirtisi yok" demektir; hiçbir test %100 garanti vermez, yedek almanın yerini tutmaz.
- "Kullanılamaz" diskin kendi arıza kanıtına dayanır (S.M.A.R.T. başarısız, bozuk sektörler, okuma hatası, başarısız disk içi test). Kablo ve sıcaklık sorunları "koşullu" olarak ayrı gösterilir; disk değişimi gerekçesi değildir.
- Antivirüs `smartctl.exe` dosyasını engellerse beyaz listeye ekleyin. USB salt okunursa raporlar `Ortak Belgeler\DiskHealth\Reports` klasörüne yazılır.
