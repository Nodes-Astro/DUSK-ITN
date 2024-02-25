# DUSK-ITN

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/177b330f-e6a0-48f2-846f-691ebbdfa344)


### Dusk teşvikli testnet için Ubuntu 22.04 rehberidir.

## Sistem Gereksinimleri

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/3430556d-a617-4036-ad27-b569eeaae0cf)

#### ℹ️ Teşvikli testnet için gereken node'umuz Prover node ve sistem gereksinimleri bu şekilde.

## Gereken Yüklemeler

```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install curl build-essential pkg-config libssl-dev git wget jq make gcc chrony clang screen -y
```
```
apt-get install protobuf-compiler
```

## ITN Installer Yükleyelim

```
curl --proto '=https' --tlsv1.2 -sSfL https://raw.githubusercontent.com/dusk-network/itn-installer/main/itn-installer.sh | sudo sh
```

#### ⚠️Bu aşamada kernel ile ilgili hata alırsanız terminalden çıkıp tekrar login olun ve kodu tekrar çalıştırın düzelecektir.

## Rusk Konfigürasyonu

Öncelikle buradaki linkten bir Dusk cüzdanı oluşturalım:
https://wallet.dusk.network/setup/


Ardından fauceti kullanalım, fauceti kullanmak için discord'a giriyoruz:
https://discord.gg/dusknetwork

Verify ettikten sonra Dusk Testnet Faucet'e dm atıyoruz

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/c8bfb70e-dc82-480f-9abe-7391567964c2)

!dusk yazıyoruz ve bot bizden cüzdan adresimizi istedikten sonra oluşturduğumuz cüzdanın adresini buraya kopyalıyoruz.

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/194c820c-b340-4dcf-9356-c7e22cde396b)

Bunu gördükten sonra işlem tamam, tokenleri gelmesi yarım saat kadar sürebiliyor

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/4cf335b7-6d74-4793-b564-ba535a74ea2e)

Şimdi cüzdanımızı import edip devam edebiliriz.

```
rusk-wallet restore
```
#### ⚠️Kelimeleri tek tek "küçük harfle yazalım".

ℹ️ Şifremizi oluşturalım ve devam edelim.

#### ⚠️"Some operations won't be available" diye bir error görürseniz aldırış etmeden devam edin henüz çalışan bir node olmadığı için bu hatayı veriyor.

```
rusk-wallet export -d /opt/dusk/conf -n consensus.keys
```
#### ⚠️ Sizden kriptolanmış bir konsensüs key isteyecek bunu unutmayın. Şifreyi yazın ve devam edin.

```
sh /opt/dusk/bin/setup_consensus_pwd.sh
```
#### ℹ️ Eğer doğru konfigürasyonu yaptıysanız node'umuzu başlatabiliriz

## Node'umuzu Başlatıyoruz
```
service rusk start
```
#### ℹ️ Çalışıyor mu kontrol ediyoruz
```
service rusk status
```
#### ℹ️ Logları bu komut ile kontrol edebilirsiniz.
```
grep "block accepted" /var/log/rusk.log
```
#### Loglar bu şekilde gözükmeli (1 dakika bekleyin sonrasında loglar görünecektir.)

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/a1a954d6-74ef-48e9-88ff-7255df8fa76b)

#### ℹ️ Buradan sonra sync olmayı bekliyoruz explorerdan block height'a bakın ve node'unuz ile karşılaştırın. Güncel blok height'a ulaştığınızda bir sonraki aşamaya geçebilirsiniz. (Yeşil işaretlediğim yer kendi block height'ınız)

https://explorer.dusk.network/

## Stake tDUSK

Artık son aşamadayız, nodeumuza 1000 tDUSK üzerinde stake yaptığımız taktirde block producer olabiliyoruz, eğer node'umuz sync olduysa bu aşamaya geçebiliriz.

```
rusk-wallet stake --amt 1000
```
1000 veya daha yüksek miktar yazabilirsiniz, şifremizi girip devam edelim.

#### ℹ️ Tx onaylanana kadar bekleyelim, bittiğinde kontrol edelim

```
rusk-wallet stake-info
```

![image](https://github.com/Alping0/DUSK-ITN/assets/105454859/02c8a8de-31c5-41db-adba-6b71d5b5d205)

#### ℹ️ Stake received diyorsa ve aşağıda stake ettiğiniz miktar gözüküyorsa tamamdır.

Node başarılı bir şekilde konsensüse katılıp blok üretiyor mu kontrol etmek için

```
grep "execute_state_transition" /var/log/rusk.log | tail -n 5
```
#### ℹ️ Bunu görüntülemek için en az 2 epoch geçmesi lazım yani uzun sürebilir, loglarınız sağlıklı ise kurulum tamamlandı, hayırlı olsun.



















