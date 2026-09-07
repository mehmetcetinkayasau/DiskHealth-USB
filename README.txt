DiskHealth 2.0 - Disk Saglik Kontrol Araci (USB'den calisir, kurulum gerektirmez)
==================================================================================

KULLANIM
  1. Bu klasoru (icindeki her sey ile birlikte) USB bellege kopyalayin. Kopyalamadan once Reports
     klasorunu bosaltin: raporlar makine adi ve disk seri numarasi icerir.
  2. Kontrol edilecek bilgisayarda DiskHealth.exe dosyasini cift tiklayin. Program .NET surumune bakar:
     - Windows 8/8.1/10/11 ve guncel Windows 7: modern arayuz (DiskHealth.Wpf.exe) acilir.
     - Guncelleme almamis Windows 7 (.NET 4.5 yok): win7\DiskHealth.Classic.exe acilir. Kurulum gerekmez.
     Windows "yonetici izni" (UAC) sorar, Evet deyin. SMART verisi icin yonetici yetkisi gerekir.
  3. "Tara" dugmesine basin. Birkac saniye icinde her diskin kartinda KARAR gorunur:
        KULLANILABILIR              (yesil)   Ariza belirtisi yok.
        KOSULLU KULLANILABILIR      (sari)    Izlenmeli: bozuk sektor gibi risk isareti var ya da
                                              kablo/sogutma sorunu var; nedeni giderip tekrar test edin.
        KULLANILAMAZ                (kirmizi) Diskin kendi ariza kaniti var. Yedek alin, degistirin.
        KARAR VERILEMEDI            (gri)     SMART verisi alinamadi (RAID, USB kutu, sanal makine).
  4. Her diskin yaninda GUVEN seviyesi yazar:
        Hizli kontrol      = yalnizca SMART sayaclarina dayanir. Diskler SMART uyarisi vermeden de bozulabilir.
        Kismen dogrulandi  = Derin testin tek adimi tamamlandi (ornegin okuma testi bitti, disk ici test atlandi).
        Dogrulandi         = Derin testin iki adimi da tamamlandi (1. okuma testi + 2. disk ici test).
     Kesin karar icin diski secip "Derin test" dugmesine basin (yaklasik 2-5 dakika, veri silinmez).
     Derin test icin once Tara ile diskleri listeleyip bir disk secin; baska diskler ayni anda test edilebilir.
     Ekranda ve raporda her disk icin "Hizli tarama" ve "Derin test" sonuclari ayri bloklarda gosterilir.
     Derin test diskin basindan/sonundan ve rastgele bolgelerden okur (varsayilan ayarlarla ~3 GB), okuma hatasi, zaman asimi,
     takilma ve bolgesel hiz cokusunu olcer; test oncesi/sonrasi SMART sayaclarini karsilastirir.
  5. Bir diske tiklayinca sagda "Kolay ozet" sekmesinde hizli tarama ve derin test bulgulari, her biri icin
     "Ne yapmali" aciklamasi gorunur. Diger sekmeler: Ozet, S.M.A.R.T. (Turkce aciklamali), Derin test ayrinti,
     Notlar, Ham veri.
  6. Rapor "Reports" klasorune otomatik kaydedilir (HTML + JSON). "Raporu Ac" ile tarayicida acilir.

KOMUT SATIRI
  DiskHealth.exe /auto          Pencere acmadan tarar, raporu kaydeder, cikis kodu verir
                                (0 kullanilabilir, 1 kosullu, 2 kullanilamaz, 3 kablo/sogutma, 4 karar verilemedi, 10 hata)
  DiskHealth.exe /auto /deep    Ayni, ancak once her diske derin test uygular

GEREKSINIMLER
  - Windows 7 SP1, 8, 8.1, 10, 11 (32 veya 64 bit). Kurulum gerekmez.
  - Yonetici yetkisi (UAC).

DOSYALAR
  DiskHealth.exe        Baslatici: dogru arayuzu secip acar (her Windows'ta calisir)
  DiskHealth.Wpf.exe    Ana program (WPF, .NET 4.5+)
  win7\                 Windows 7 icin .NET 3.5 surumu (DiskHealth.exe gerekirse otomatik secer)
  settings.json         Ayarlar (programdaki "Ayarlar" penceresinden duzenlenir)
  rules.json            Karar kurallari ve esik degerleri (Ayarlar > Karar esikleri sekmesinden duzenlenir)
  tools\x64, tools\x86  smartctl.exe (smartmontools 7.5, GPL v2 - bkz. tools\COPYING.txt)
  Reports\              Kaydedilen raporlar

NOTLAR
  - Hicbir test %100 garanti vermez; onemli veriler icin yedek duzeni sarttir.
  - SAS/SCSI diskler ve RAID denetleyici arkasindaki diskler (oznitelik tablosu yok) KARAR VERILEMEDI verir;
    arac istemci bilgisayarlar icindir, sunucular icin degil.
  - Okuma testi ornekleme yapar (varsayilan ~3 GB); tam yuzey taramasi degildir.
  - Antivirus smartctl.exe'yi engellerse beyaz listeye ekleyin.
  - USB salt okunursa raporlar Ortak Belgeler\DiskHealth\Reports klasorune yazilir.
  - rules.json degistirilirse ekranda ve raporda "ozel kural" uyarisi cikar; dosya bozuksa gomulu varsayilanlar kullanilir.
