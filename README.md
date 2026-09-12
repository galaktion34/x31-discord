# x31 — Discord Access Tool for Türkiye

**x31**, Türkiye’de Discord’a uygulanan DPI/SNI tabanlı erişim engelini VPN kullanmadan aşmak için geliştirilmiş küçük ve bağımsız bir Windows aracıdır.

x31'in temel amacı, sisteme mümkün olduğunca az müdahale ederek **yalnızca Discord trafiğini** ele almaktır.

Sistem genelindeki DNS ayarlarını, internet bağlantısını, ağ yapılandırmasını veya diğer uygulamaların trafiğini değiştirmez.

> Bu araç özellikle Türkiye’deki Discord erişim engeli için geliştirilmiştir. Arayüz dili Türkçedir.

## x31'i farklı yapan nedir?

Benzer amaçla geliştirilen birçok Windows aracı, erişim engelini aşabilmek için sistem genelinde değişiklikler yapabilir veya ek bileşenlere ihtiyaç duyabilir.

Örneğin bazı çözümler:

- Sistem DNS ayarlarını değiştirebilir.
- Tüm ağ trafiğini farklı bir katmandan geçirebilir.
- GoodbyeDPI benzeri harici araçlara ihtiyaç duyabilir.
- WinDivert gibi ağ sürücüleri kurabilir veya kullanabilir.
- Windows ağ yapılandırmasına kalıcı ya da sistem genelinde müdahale edebilir.
- Discord dışındaki uygulamaların bağlantılarını da etkileyebilir.

**x31 bu yöntemleri kullanmaz.**

x31:

- GoodbyeDPI, WinDivert veya benzeri üçüncü parti ağ araçlarına ihtiyaç duymaz.
- Ek bir ağ sürücüsü kurmaz.
- VPN veya sanal ağ adaptörü oluşturmaz.
- Sistem DNS ayarlarını değiştirmez.
- Windows yönlendirme tablosunu değiştirmez.
- Proxy ayarlarını sistem genelinde değiştirmez.
- Diğer uygulamaların internet trafiğine müdahale etmez.
- Yalnızca gerekli Discord alan adlarını yerel olarak ele alır.
- İşlem tamamlandıktan sonra bağlantıyı doğrudan Discord sunucularına devam ettirir.

Başka bir deyişle x31, bilgisayarınızdaki internet bağlantısını genel olarak yeniden yapılandırmak yerine müdahaleyi mümkün olduğunca **Discord ile sınırlı** tutar.

## Kullanım

1. `x31.exe` dosyasını indirin.
2. Dosyaya sağ tıklayıp **Yönetici olarak çalıştır** seçeneğini kullanın.

   Yönetici izni, Windows `hosts` dosyasına gerekli kayıtların eklenebilmesi için gereklidir.

3. Açılan pencereden çalışma şeklini seçin:

   - **RunOnce:** Programı yalnızca mevcut oturum için çalıştırır. Kapatıldığında eklediği kayıtları temizler.
   - **Startup:** Windows açıldığında x31'in otomatik olarak başlamasını sağlar.

Program başlatıldıktan sonra ana pencere kapanır ve x31 sistem tepsisinde çalışmaya devam eder.

Saatin yanındaki x31 simgesine sağ tıklayarak:

- **Göster** seçeneğiyle çalışma durumunu görüntüleyebilir,
- **Çıkış** seçeneğiyle programı kapatabilirsiniz.

Program çalışırken Discord'u normal şekilde açabilirsiniz.

## Sistem gereksinimleri

- Windows 10 veya Windows 11
- 64-bit işletim sistemi
- Microsoft Edge WebView2 Runtime

WebView2 Runtime güncel Windows kurulumlarının çoğunda hazır olarak bulunur. Sisteminizde yüklü değilse x31 sizi Microsoft'un indirme sayfasına yönlendirir.

Bunun dışında herhangi bir **üçüncü parti ağ uygulaması, sürücü, VPN, DNS yazılımı veya ek servis kurulumu gerekmez.**

## Nasıl çalışır?

x31, Discord'a ait belirli alan adlarını Windows `hosts` dosyası üzerinden bilgisayarınızdaki yerel proxy'ye yönlendirir.

Bu yönlendirme yalnızca x31'in ihtiyaç duyduğu Discord alan adları için uygulanır. Sistem genelindeki DNS yapılandırması değiştirilmez.

Yerel proxy, TLS bağlantısını sonlandırmadan el sıkışma paketlerini parçalayarak SNI bilgisini inceleyen engelleme sistemlerinin bağlantıyı tespit etmesini zorlaştırır.

Bağlantı daha sonra doğrudan Discord sunucularına devam eder.

Bu işlem sırasında:

- TLS şifrelemesi açılmaz.
- Discord trafiğinin içeriği okunamaz.
- MITM uygulanmaz.
- Sisteme herhangi bir sertifika yüklenmez.
- Sistem DNS ayarları değiştirilmez.
- Windows yönlendirme tablosu değiştirilmez.
- Sistem genelinde proxy ayarı yapılmaz.
- Ağ sürücüsü kurulmaz.
- Discord dışındaki internet trafiğine müdahale edilmez.
- Kullanıcı verisi toplanmaz veya başka bir sunucuya gönderilmez.
- VPN kullanımı engellenmez; x31 VPN ile birlikte çalışabilir.

Program kapatıldığında `hosts` dosyasına eklediği kayıtları kaldırır.

x31 yalnızca açılış sırasında kullanılan sürümün geçerli olup olmadığını kontrol etmek için tek seferlik bir bağlantı kurar. Program çalışırken sürekli olarak bağlı kaldığı ayrı bir servis bulunmaz.

## `hosts` dosyasında kayıt kalırsa

Bilgisayarın aniden kapanması, elektrik kesintisi veya programın normal şekilde sonlandırılamaması durumunda x31 tarafından eklenen kayıtlar `hosts` dosyasında kalabilir.

Böyle bir durumda Discord'a erişilemiyorsa:

1. x31'i yeniden açın.
2. Ardından programı normal şekilde kapatın.

x31 açılış sırasında önceki kayıtları kontrol eder ve gerektiğinde temizler.

İlk değişiklik yapılmadan önce mevcut `hosts` dosyasının yedeği şu konuma kaydedilir:

```text
C:\Windows\System32\drivers\etc\hosts.x31.bak
```

## Dosya bütünlüğü

İndirdiğiniz `x31.exe` dosyasının değiştirilmediğini doğrulamak için SHA-256 değerini kontrol edebilirsiniz.

```text
c4e1e927dcdc3db78d9d0fb599fc291b77a60165496d71a8ef86322eee54349d
```

PowerShell üzerinden kontrol etmek için:

```powershell
Get-FileHash .\x31.exe -Algorithm SHA256
```

Komutun ürettiği değer yukarıdaki SHA-256 değeriyle birebir aynı olmalıdır.

## Güvenlik

x31 kaynak kodu kapalı olarak dağıtılmaktadır.

Bu nedenle uygulamayı yalnızca bu GitHub deposundaki resmi sürüm bağlantısından indirmeniz önerilir. Farklı sitelerde, forumlarda veya dosya paylaşım servislerinde bulunan kopyaların güvenli olduğu doğrulanamaz.

## Sorumluluk reddi

x31 kişisel kullanım amacıyla geliştirilmiş ve olduğu gibi paylaşılmıştır.

Aracın kesintisiz çalışacağı, her internet servis sağlayıcısında sonuç vereceği veya gelecekte uygulanabilecek farklı engelleme yöntemleriyle uyumlu kalacağı garanti edilmez. Kullanımdan doğabilecek sonuçların sorumluluğu kullanıcıya aittir.
