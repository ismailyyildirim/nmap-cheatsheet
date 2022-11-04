 # NMAP -01-
 Bir ana bilgisayardan gelen herhangi bir yanıt, çevrimiçi olduğunun bir göstergesidir. Aşağıda, ele aldığımız Nmap için komut satırı seçeneklerinin hızlı bir özeti bulunmaktadır.
| Tarama tipi    | Örnek Komut       |
| ------------------------- | ----------- |
| ARP Taraması      | `sudo nmap -PR -sn MACHINE_IP/24` |
| ICMP Yankı Taraması    | `sudo nmap -PE -sn MACHINE_IP/24` |
| ICMP Zaman Damgası Taraması    |  `sudo nmap -PP -sn MACHINE_IP/24`  |
| ICMP Adres Maskesi Taraması  |`sudo nmap -PM -sn MACHINE_IP/24`     |
| TCP SYN Ping Taraması       | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30`     |
|TCP ACK Ping Taraması      | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30`     |
| UDP Ping Taraması      | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30`|


`-sn`Bağlantı noktası taraması olmadan yalnızca ana bilgisayar keşfiyle ilgileniyorsanız eklemeyi unutmayın . Atlamak, Nmap'in `-sn`varsayılan olarak canlı ana bilgisayarları bağlantı noktası taramasına izin verecektir.

| seçenek    | Amaç       |
| ------------------------- | ----------- |
| -n     | DNS araması yok|
| -R   | tüm ana bilgisayarlar için ters DNS araması |
|-sn    |  yalnızca ana bilgisayar keşfi   |


# NMAP -02-
Bu bölümde üç tür taramayı kapsıyor.
| Bağlantı Noktası Tarama Türü    | Örnek Komut       |
| ------------------------- | ----------- |
|TCP Bağlantı Taraması     | `nmap -sT MACHINE_IP`|
| TCP SYN Taraması   | `sudo nmap -sS MACHINE_IP` |
|UDP Taraması    |  `sudo nmap -sU MACHINE_IP`   |

Bu tarama türleri, hedef ana bilgisayarda çalışan TCP ve UDP hizmetlerini keşfetmeye başlamanızı sağlamalıdır .

| seçenek    | Amaç       |
| ------------------------- | ----------- |
| `-p-`     | tüm bağlantı noktaları|
| `-p1-1023`   | 1'den 1023'e kadar olan portları tara |
|`-F`    |  En yaygın 100 bağlantı noktası   |
|`-r`    |  portları ardışık sırayla tarayın   |
|`-T<0-5>`    |  -T0 en yavaş ve T5 en hızlısı   |
|`--max-rate 50`    |  hız <= 50 paket/sn|
|`--min-rate 15`   |  oran >= 15 paket/sn  |
|`--min-parallelism 100`    |  paralel olarak en az 100 prob |


# NMAP -03-
Gelişmiş tarama türleri.

| Bağlantı Noktası Tarama Türü    | Örnek Komut       |
| ------------------------- | ----------- |
|TCP Null Scan| `sudo nmap -sN MACHINE_IP`|
| TCP FIN Scan  | `sudo nmap -sF MACHINE_IP` |
|TCP Xmas Scan   |  `sudo nmap -sX MACHINE_IP`   |
|TCP Maimon Scan  |  `sudo nmap -sM MACHINE_IP`  |
|TCP ACK Scan    |  `sudo nmap -sA MACHINE_IP`   |
|TCP Window Scan  | `sudo nmap -sW MACHINE_IP`|
|Custom TCP Scan  |  `sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP`|
|Spoofed Source IP   |  `sudo nmap -S SPOOFED_IP MACHINE_IP`|
|Spoofed MAC Address  |  `--spoof-mac SPOOFED_MAC` |
|Decoy Scan   |  `nmap -D DECOY_IP,ME MACHINE_IP` |
|Idle (Zombie) Scan |`sudo nmap -sI ZOMBIE_IP MACHINE_IP`|
|Fragment IP data into 8 bytes  |`-f` |
|Fragment IP data into 16 bytes  |  `-ff` |

| Seçenek    |Amaç      |
| ------------------------- | ----------- |
|`--source-port PORT_NUM`     | kaynak bağlantı noktası numarasını belirtin|
|`--data-length NUM`   | verilen uzunluğa ulaşmak için rastgele veri ekle |

Bu tarama türleri, yanıt için bağlantı noktalarından beklenmeyen şekillerde TCP bayrakları ayarlamaya dayanır. Null, FIN ve Xmas taraması kapalı bağlantı noktalarından bir yanıta neden olurken, Maimon, ACK ve Window taramaları açık ve kapalı bağlantı noktalarından bir yanıt oluşturur.

| seçenek    | Amaç       |
| ------------------------- | ----------- |
| `--reason`     | Nmap'in sonuca nasıl ulaştığını açıklıyor|
| `-v`   | ayrıntılı |
|`-vv`    |  çok ayrıntılı  |
|`-d`   |  hata ayıklama |
|`-dd`    |  hata ayıklama için daha fazla ayrıntı   |

# NMAP -04-
 Son olarak, tarama sonuçlarını ileride incelemek üzere kaydetmek için farklı biçimleri ele aldık. Aşağıdaki tablo, bu odada ele aldığımız en önemli seçenekleri özetlemektedir.

| seçenek    | Amaç       |
| ------------------------- | ----------- |
| `-sV`     | açık bağlantı noktalarında hizmet/sürüm bilgilerini belirleyin|
| `-sV --version-light`   | en olası probları deneyin (2) |
|`-sV --version-all`   |  mevcut tüm probları deneyin (9)   |
|`-O`   |  işletim sistemini algıla  |
|`--traceroute` |  hedef için traceroute'u çalıştırın |
|`--script=SCRIPTS`   |  Çalıştırılacak Nmap betikleri |
|`-sC` or `--script=default`   |  varsayılan komut dosyalarını çalıştır|
|`-A`  |  eşittir`-sV -O -sC --traceroute`   |
|`-oN`  | çıktıyı normal biçimde kaydet  |
|`-oG`  |  çıktıyı grepable biçimde kaydet  |
|`-oX`   |  çıktıyı XML biçiminde kaydet |
|`-oA`  |  çıktıyı normal, XML ve Grepable formatlarında kaydedin   |


