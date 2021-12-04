# System-Network-Bootcamp-Final-Case

## Talimatlar

<details> <summary> Network Talimatları </summary> 

# Network Talimatları
3X Tekstil firması kuruluyor! 3X Firmasının Merkezi İstanbul’da, Kocaeli ve Sakarya’da Satış ofisleri, Bolu’da
üretim atölyesi bulunuyor.

Ofislerdeki kullanılacak network cihazlarının envanteri aşağıdaki gibidir;

## Topoloji Oluşturulması

### Merkez Ofis
-----------

3X Firmasının Merkez Ofisinde 1 Adet omurga switch kullanılacak.
Bu omurga switchte;

● Internet erişimi için Vlan100, 172.34.100.0/30 subneti kullanılacak.\
● Intranet erişimi için Vlan101, 172.34.101.0/30 subneti kullanılacak.\
● Misafir erişimi için Vlan99, 172.34.99.0/24 subneti kullanılacak.\
● Sunucu erişimi için Vlan80, 172.34.80.0/24 subneti kullanılacak.\
● Kullanıcı erişimi için Vlan50, 172.34.50.0/24 subneti kullanılacak.\
● Yönetici erişimi için Vlan34, 172.34.34.0/24 subneti kullanılacak.

Bu omurga switch’e bağlı 2 adet kenar switch kullanılacak.\
Kenar switch’lerden bir tanesinde 1 Server 1 Yönetici Bilgisayarı kullanılacak\
Diğer kenar switch’te bir Misafir Bilgisayarı ve bir adet Kullanıcı Bilgisayarı kullanılacak.


Omurga switch aynı zamanda intranet erişimi için aynı lokasyondaki Merkez Ofis Router’a bağlı. \
Bağlı olduğu arayüz ip’si **172.34.101.2/30** olmalı.

Omurga switch internet erişimi için aynı lokasyondaki Merkez Ofis Firewall’a bağlı.\
Bağlı olduğu arayüz ip’si **172.34.100.2/30** olmalı.

Merkez Ofis Router’a\
1 Adet ISP Router bağlı.\
Bağlı olduğu arayüz ip’si **12.0.0.2/30** olmalı.\
Bolu Atölye Router bağlı.\
Bağlı olduğu arayüz ip’si **25.0.0.1/30** olmalı.

Merkez Ofis Firewall’a\
1 Adet Internet Router bağlı.\
Bağlı olduğu arayüz ip’si **212.111.34.46/30** olmalı.

Internet erişimi için firewall’a bağlı olan Internet Router’a bir adet sunucu bağlı.\
Bağlı olduğu arayüz ip’si **8.8.8.1/24** olmalı.\
Bu router’a bir adet sunucu bağlı.\
Bağlı olduğu arayüz ip’si **8.8.8.8/24** olmalı.


### Bolu Atölye
-----------

Bolu atölyede Router’da kullanıcı erişimi için **172.10.0.0/24** subneti kullanılacak.\
Bolu Router’a bağlı bir adet kullanıcı bilgisayarı kullanılacak.\
Bağlı olduğu arayüz ip’si **172.10.0.2/24** olmalı.

Bolu Router Intranet ve Internet erişimi için Merkez Ofis Router’a bağlı\
Bağlı olduğu arayüz ip’si **25.0.0.2/30** olmalı.

### Kocaeli Ofis
-----------

Kocaeli Ofiste 1 adet router, 1 adet switch ve 1 Adet Kullanıcı bilgisayarı kullanılacak.\
Kocaeli Ofiste kullanıcı erişimi için Vlan50 **172.41.0.0/24** subneti kullanılacak.

Kocaeli Router Intranet ve Internet erişimi için ISP Router bağlı.\
Bağlı olduğu arayüz ip’si **13.0.0.2/30** olmalı.\
Kocaeli Router Kocaeli Switch’e bağlı\
Kocaeli Switch’e bir adet kullanıcı bilgisayarı bağlı.\
Kullanıcı bilgisayarının ip’si **172.41.0.2/24** olmalı.

### Sakarya Ofis
--------------------

Sakarya Ofiste 1 adet router, 1 adet switch ve 1 adet kullanıcı bilgisayarı kullanılacak.\
Sakarya Ofiste kullanıcı erişimi için Vlan50 **172.54.0.0/24** subneti kullanılacak.

Sakarya Router Intranet ve Internet erişimi için ISP Router’a bağlı\
Bağlı olduğu arayüz ip’si **14.0.0.2/30** olmalı.\
Sakarya Switch’e bir adet kullanıcı bilgisayarı bağlı.\
Kullanıcı bilgisayarının ip’si **172.54.0.2/24** olmalı

## Erişim Kuralları

### Merkez Ofis
------------------------

Merkez Ofis Omurgada;\
● Misafir Vlan’dan yalnızca Internet erişimi olmalı. Omurgada ACL yazılarak bu erişim sınırlandırılmalı.\
● Kullanıcı Vlan’dan her yere erişim olmalı.\
● Sunucu Vlan’dan her yere erişim olmalı.\
● Yönetici Vlan’dan her yere erişim olmalı.\
● Merkez Ofis Omurgada Internete doğru default route olmalı.\
● Merkez Ofis Omurgadan Intranet bölgesindeki Subnetlere default route olmalı.

Merkez Ofis Router - Bolu Router Arasında statik route olmalı.\
Merkez Ofis Router - ISP Router Arasında BGP yapılandırılmalı. Merkez Ofis Router’da statik routelar BGP içerisine redistribute edilmeli.

Merkez Ofis Firewall’da\
Default route Internet Router’a doğru yazılacak.\
3X Firmasının Local networklerin routeları Merkez Ofis Omurgaya doğru yazılacak\
Internet erişim trafiği Internet Router’a doğru NAT’lanacak.\
Internet Router\
3X Firmasının Local networklerin routeları Merkez Ofis Firewall’a doğru yazılacak

### Bolu Ofis
---------------
Bolu Ofis Router’da Merkez Ofis Router’a doğru default route olmalı.

### Kocaeli Ofis
--------------------
Kocaeli Ofis Router - ISP Router arasında OSPF yapılandırılmalı.\
Local networkler anons edilmeli.\
ISP Router’a doğru default route yazılmalı.

### Sakarya Ofis
-------------------
Kocaeli Ofis Router - ISP Router arasında single area OSPF yapılandırılmalı.\
Local networkler anons edilmeli.\
ISP Router’a doğru default route yazılmalı.

## Erişim Testleri

Merkez Ofis Kullanıcı Bilgisayarının Misafir Kullanıcı Bilgisayarı hariç tüm ip’lere ping erişimi olmalı\
Merkez Ofis Misafir Bilgisayarının Yalnızca 8.8.8 ip’sine ping erişimi olmalı diğer Bilgisayar ve Sunuculara
erişimi olmamalı

</details>

<details> <summary>Sistem Talimatları </summary> 
  
  # Sistem Talimatları
  
  1. Bir domain yapısı kurulmalı. (Domain Controller kurulacak)
  
  2. Domain Controller üzerinde Active Directory, File Server rolleri kurulmalı (tüm roller Domain Controller üzerinde kurulabilir, kaynağı olanlar Additional Domain Controller kurarak dağıtabilir rolleri)
  
  3. Active Directory üzerinde;\
     İstanbul, Ankara, İzmir olmak üzere üç farklı ilde konumlanacak şekilde; her bölgede satış, pazarlama ve IK departmanları olmalı.\
     İstanbul lokasyonunda bunlara ek IT, yönetim ve muhasebe olmalı.    
  
  4. Her ilde satış departmanında 100’er user olmalı.
  
  5. Her ilde diğer tüm departmanlarda 5’er kişi olmalı.
  
  6. Kullanıcı isimleri rastgele oluşturulmalı.
  
  7. File Server’da kullanılacak olan ek disk alanı toplamda 10 GB olacak şekilde RAID0 yapısında olmalı.Share edilecek ilgili klasörler RAID0 disk alanında bulunmalı.
  
  8. File Server’da her departmanın ortak klasörü ve ayrıca herkesin erişebildiği public bir klasör olmalı.\
    Her departman userları kendi klasöründe read & write yetkisi olmalı.\
    IT departmanındaki userlar tüm klasörlerde yetkili olmalı.
  
  9. File Server için oluşturulan disk Operating System katmanında yedekliliği sağlanmalı, tüm lokasyonlar ve departmanlar için yetkilendirmeleri yapılmalı.\
    Sadece IT departmanı “.exe” ve “.rar” dosyaları kopyalayabilmeli,\
    IK sadece ofis dosyaları kopyalayabilir,\
    Muhasebe departmanı müzik, video gibi dosyaları ekleyebilir,\
    Hiçbir departman “.exe” dosyalarını çalıştıramamalı.
  
  10. Active Directory’de “telnet client” kurulumu yapılarak , client pc’lerden birine 3389 (RDP) portuna telnet bağlantısı kurulmalı.
  
  </details>
  

