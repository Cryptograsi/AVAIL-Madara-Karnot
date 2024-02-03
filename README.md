# AVAIL-Madara-Karnot

Celestia ve Dymension node ödüllerinden sonra bu alana hızlı bir ilgi artışı oldu. Avail, içeriği ile son dönemin en öne çıkan projesi. Validatörlük için başvuru aldılar ve 300 kişi seçildi. Seçilenler haricinde nod kurulamıyor. Fakat şu an yeni başlayan Madara&Karnot roller testine katılabilirsiniz. Ayrıca discordlarında Lightnode için de hala bir başvuru formu açık. Başvurup şimdiden nodunu kurabilirsiniz.


## Sistem Gereksinimleri
```
Ubuntu 22.04
4 CPU
8 GB RAM
160 GB SSD
```

## Gerekli Portları Açalım
```
sudo ufw enable
sudo ufw allow 22
sudo ufw allow 4000
sudo ufw allow 5353
sudo ufw allow 47250
sudo ufw allow 39276
sudo ufw allow 36347
sudo ufw allow 43759
sudo ufw allow 40815
sudo ufw allow 30333
sudo ufw allow 9944
sudo ufw allow 9615
```

## Sunucumuzu Güncelleyelim
```
sudo apt-get update -y && sudo apt-get upgrade -y
```

## Rust Kuralım
Bize ne yapmak istediğimizi soracak, bu kısım geldiğinde 1 seçip enter ile devam edelim!!!
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Bu kod Rust'ı sistem yolumuza PATH olarak ekler. Bu yüzden restart yapmadan Rust çalıştırmak için alttaki kodu girelim

```
source $HOME/.cargo/env
```

Versiyonumuzu kontrol edelim. Çıktımız "rustc 1.75.0 (82e1608df 2023-12-21)" olmalı
```
rustc --version
```

## Git Kuralım
Eğer daha önce sunucunuzda başka bir proje için alttaki kodu girmişseniz bunu atlayabilirsiniz!
```
sudo apt install git
```

## Docker Kuralım
Dikkat: Kodları tek tek girelim. Hepsini tek seferde girmeyin!!!
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo systemctl start docker
sudo systemctl enable docker
```

## Gerekli Güncellemeleri ve Dosya Derleme Araçlarını Yükleme İşlemlerini Yapalım
Dikkat: Kodları tek tek girelim. Hepsini tek seferde kopyalayıp yapıştırmayın!!!
```
sudo apt-get update -y && sudo apt-get upgrade -y
sudo apt install build-essential
sudo apt install pkg-config
sudo apt install libssl-dev
sudo apt install clang
sudo apt install protobuf-compiler
```

##  Nihayet Madara Kurulumuna Geçebiliriz, Madara dosyalarını sunucumuza indirelim
Dikkat: Kodları yine sırayla girelim. İkinci koddan sonra compiling yapar. Bu işlem uzun sürüyor. Sabredip bekleyeceksiniz mecburen:)
```
git clone https://github.com/karnotxyz/madara-cli
cd madara-cli
cargo build --release
```

#### Dikkat: Bu komuttan sonra bize bazı sorular soracak, yanlış yapmamaya özen gösterelim
1) Sizden bir chain adı belirlemenizi isteyecek. Burada ağınıza istediğiniz ismi verebilirsiniz. Mesela ben gonluzengin seçtim, sonra enter ile devam edelim.


2) İkinci adımda spesifik bir şey yok, enter ile devam edelim.


3) Burada Avail seçip enter ile ilerleyelim.
   ```
   ./target/release/madara init
   ```
   Size en sonunda bir Avail cüzdanı verecek, eğer ilk kez avail cüzdan oluşturuyorsanız mnemonic keylerinizi mutlaka kaydedin. Daha önce faucette kullandığınız bir üzdan varsa ve bunu kullanmak istiyorsanız app-chains dosyası içindeki mnemonic keyleri ve bir önceki kodun bize verdiği cüzdan adresini değiştirmemiz gerekecek. Bunun için alttaki kodu giriyoruz. < ve > işaretlerini silip kendinize göre düzenleyin.


   Dikkat: Bu kodu sadece eski cüzdanını Madara&Karnot testinde kullanmak isteyenler kullansın. Eğer ilk kez Avail adresi oluşturduysanız bu adımı atlayın!!!
   ```
   nano /root/.madara/app-chains/<Ağınıza-versiğiniz-isim>/da-config.json
   ```
   Bu kodu girip dosya içindeki Seed yazan yerdeki keyi ve cüzdan adresini eski mnemonicler ve cüzdan adresinizle değiştirin. CTRL X+Y+Enter ile dosyadan çıkalım.

   ## Ağı Çalıştıralım
   Bunu screen açıp yapacağız. Bazı sunucular önce screen yüklememizi ister, bazıları ise direkt screen açılarak ilerlenebilir. Örneğin Contabo kullanıyorsanız ve daha önce yüklemediyseniz apt install screen kodunu sizden ister fakat Hetnzer kullanıcılarının bu kodu girmesine gerek yok.
   ```
   apt install screen
   ```
   ```
   screen -S roll
   ```
   Bu kodu girmeden önce Avail Discord Goldberg faucetten token almanız gerekiyor. /deposit cüzdan adresiniz şeklinde token alın. Token gelince alttaki komutu çalıştırın
   ```
   ./target/release/madara run
   ```
   CTRL A aynı anda basıp çok kısa aralıkla D'ye basıp screenden çıkalım. Yeni arkadaşlar burada biraz zorlanacaktır ama el zamanla buna da alışıyor:))

   ## Explorer Sayfasını Çalıştıralım
   Kodları tek tek girin bence, hata riski sıfırlansın:) Son kodun sonuna kendi sunucunuzun ip'sini yazın!
   ```
   cd
   cd madara-cli
   ./target/release/madara explorer --host=Sunucunun-IPadresi
   ```
   Explorer çalıştıktan sonra http://sunucunuzunipadresi:4000/ ip adresini değiştirip explorer sayfasınızı görebilirsiniz. Bundan sonra sunucuyu kapatabilirsiniz. Artık burada yapacak bir şeyimiz kalmadı.

   ![Ekran görüntüsü 2024-02-03 162004](https://github.com/Cryptograsi/AVAIL-Madara-Karnot/assets/101165594/b7ce8f49-d2b1-4f65-ae14-42d4c371eb6a)

   ##### Eveeeet asıl işin basit ama insanı gıcık eden kısmına geldik:) App'imizi yayınlayacağız. Bunun için ID ve bir profil fotoğrafı ayarlamalıyız. ID için https://www.uuidgenerator.net/#google_vignette sitesine gidiyoruz. Eğer uid görünmezse sayfayı yenileyelim ve verdiği id'yi kopyalayıp bir yere kaydedelim.
   

![Ekran görüntüsü 2024-02-03 162731](https://github.com/Cryptograsi/AVAIL-Madara-Karnot/assets/101165594/dbd12b28-3fa0-4579-9089-a9de35e0375d)


   Profil fotoğrafı için https://resimlink.com/ ya da https://www.resizepixel.com/ sitelerini kullanabilirsiniz. Burada uzantının png ve boyutun da 400x400 olmasına dikkat edin.

![Ekran görüntüsü 2024-02-03 162947](https://github.com/Cryptograsi/AVAIL-Madara-Karnot/assets/101165594/c76781de-a694-40ae-8e8b-040b43e4469b)

  #### Aşağıdaki kodu kendimize göre düzenleyelim
  ```
{
    "name": "Ağ-Adınız-Buraya",
    "logo": "Logonuzun-Linki-Buraya", 
    "rpc_url": "http://sunucu-ipni-yaz:9944",
    "explorer_url": "http://sunucu-ipni-yaz:4000",
    "metrics_endpoint": "http://sunucu-ipni-yaz:9615/metrics",
    "id": "Siteden-Aldığın-UID-Buraya"
  }
```
Not: Burada satır sonlarında boşluk kalmamasına özen gösterin. Çünkü pull requist oluştururken birçok insan bu basit nedenden ötürü hata aldı.



https://github.com/karnotxyz/avail-campaign-listing   Bu repoya gidelim ve forklayalım. Yeni öğrenenler için, forklamak bir nevi Twitter'daki RT olayına benziyor...


![Ekran görüntüsü 2024-02-03 164428](https://github.com/Cryptograsi/AVAIL-Madara-Karnot/assets/101165594/53399124-df40-4afe-a02a-fdf1f88353e1)

Forkladıktan sonra Add File tıklayıp Create new file tıklıyoruz.

![Ekran görüntüsü 2024-02-03 164736](https://github.com/Cryptograsi/AVAIL-Madara-Karnot/assets/101165594/f993a766-f3db-4cb0-bb92-d1648bf821b9)

1 ile işaretlediğim yere siteden aldığınız UID yazıp sonuna .json ekleyin. Mesela 20eda53b-843f-415d-8600-9c4aa4191ee6.json gibi. 2 ile işaretlediğim yere daha önce kendinize göre düzenlediğiniz kodu yapıştırıp sağ üstteki yeşil renkli Commit Changes butonuna tıklayıp kaydediyoruz.

Bundan sonra pull requist açacağız. Sol tarafta Pull Requist sekmesi var, ona tıklayalım ve New Pull Requist tıklayıp Create diyoruz. Bizden bir isim ister ✨️Adding yazıp yanına ağınıza verdiğiniz ismi ekleyin ve Commit yapın. 


Bundan sonra onay bekleyeceksiniz.


Takıldığınız yer olursa Twitter adresim: https://twitter.com/cryptograsi
TG kullanıcı adım: @de_fabula_narratur

Yıldızlamayı ve Forklamayı unutmayın lütfen:))





  
