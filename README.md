# Hızlıca Facebook Etkinliğizi Silin

Bu programı, tüm hesabınızı silmeden Facebook hesabınızdaki datalarınızı temizlemek için kullanılabilirsiniz.

_Uyarı: Facebook, bu aracın sağladığı gibi yüksek hızda etkinlikleri önlemek için bazı önlemlere sahiptir. Mevcut hız sınır değeri, algılamayı önlemek için şu anda 100 ms'ye ayarlanmıştır, ancak gecikme yeterli olmayabilir. Bu etkinlik günlüğünüzün geçici olarak engellenmesine neden olabilir. Bu gecikmeyi artırmak/azaltmak istiyorsanız lütfen [Hız sınırlama](#hız-sınırlama) bölümüne bakın._

_Not: Facebook'un çok tuhaf bir giriş süreci var. Program giriş yapamıyorsa lütfen bir GitHub 'da bize bir issue açın. Eğer hesabınızda iki faktörlü kimlik doğrulama etkinse kullanabileceğiniz bir geçici çözüm: (https://github.com/marcelja/facebook-delete/wiki/Login-with-browser-cookie)._

![Demo](demo.gif)

## Program nasıl çalıştırılır?

Linux, macOS ve Windows için mevcut dosyalar release olarak eklenmiştir.

### Binary olarak indirin

Kullandığınız platform için "binary" dosyayı indirin [latest release](https://github.com/marcelja/facebook-delete/releases).

Linux/macOS: "Binary" dosyayı yürütülebilir yapın ve çalıştırın. Örnek:

```bash
chmod +x deleter-linux
./deleter-linux
```

Windows: Mevcut .exe dosyasını çalıştırın ve "Yine de çalıştır" 'a dokunun.

### Kaynaktan indirin

Son [Go](https://golang.org/) versiyonu yüklü olmadıdır. Paket yöneticisi veya golang web sitesi aracılığıyla indirebilirsiniz.

#### Kaynağı klonlayarak indirin

```bash
git clone https://github.com/marcelja/facebook-delete.git
cd facebook-delete
go install
go run deleter.go
```

## Çerezler (Cookies)

Eğer `$GOCOOKIES` değeri ayarlanmadıysa, mevcut çerezler `$HOME/.go-cookies` 'e kayıt olacaktır. (bknz: <https://github.com/juju/persistent-cookiejar>).

## Ayarlar

### Hız-sınırlama

Çok fazla istekte bulunursanız, Facebook aktivite günlüğünüzü geçici olarak engeller. Her istekten önce özel bir gecikme eklemek için konsola `-rateLimit <ms cinsinden sure>` kullanarak çalıştırın. Yalnızca arama veya silme işlemlerine takılıp kalıyorsanız, `-limitSearch=0` veya `-limitDelete=0` ile biri veya diğeri için hız sınırlamasını devre dışı bırakabilirsiniz.

Kullanım örnekleri:

```bash
./deleter-linux -rateLimit 500 # 500ms gecikme ekleyin
./deleter-linux -rateLimit 500 -limitSearch=0 # 500 ms'lik bir gecikme ekler. (arama eylemi için geçerli değil)
./deleter-linux -rateLimit 500 -limitDelete=0 # 500 ms'lik bir gecikme ekler. (silme eylemi için geçerli değil)
```

### "Flag" 'ler aracılığıyla seçim

Manuel seçimi atlamak istiyorsanız, mevcut "flag" 'leri kullanmakta özgürsünüz.

| Flag              | Tip      | Açıklama                                                                                       | Örnek Kullanım                                          |
|-------------------|----------|------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| -customYears      | `string` | Seçmek için (YYYY) kullanın, yıllar arasına virgül ekleyin. Tüm yılları seçmek için "select all" 'ı kullanın.                 | `-customYears="2006,2009,2020"` veya `-customYears="all"` |
| -customMonths     | `string` | Virgülle ayırarak ayları yazarak seçin. Tüm ayları seçmek için "select all" 'ı kullanın.    | `-customMonths="1,2,12` veya `-customMonths="01,02,12"`   |
| -selectAllContent | `bool`   | Değer "true" olarak ayarlanırsa, tüm içeriği soru sormadan seçer ve işler.                     | `-selectAllContent=true`                                |

_Note: Eğer "flag" 'leri kullanırken geçersiz argumanlar kullanırsanız, uyarı alacak ve manuel seçim yapmanız istenecektir._
