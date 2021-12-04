# System-Network-Bootcamp-Final-Case

Trendyol System ve Network Bootcampinin bitirme projelerini ve çözümlerini içermektedir.

## Talimatlar

<details> <summary>Network Proje Talimatları </summary> 

# Network Proje Talimatları
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

<details> <summary>Sistem Proje Talimatları </summary> 
  
  # Sistem Proje Talimatları
  
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
  

## Çözümler

<details> <summary>Network Projesi Çözümüm </summary> 
  
  # Network Projesi Çözümüm
  
  ## Topoloji
	
   ![topology](https://user-images.githubusercontent.com/49712212/144723468-5b90c499-1aa0-40a2-b39c-ce220f462c2b.jpeg)

  
  [Network_topology.zip](https://github.com/Kubison/System-Network-Bootcamp-Final-Case/files/7654451/network.zip)

  
  
  ## Configler
  
  <details> <summary> Anaomurga Switch </summary>
      
      Building configuration...
      Current configuration : 2617 bytes
      !
      version 12.2(37)SE1
      no service timestamps log datetime msec
      no service timestamps debug datetime msec
      no service password-encryption
      !
      hostname Switch
      !
      !
      !
      !
      !
      !
      ip routing
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      spanning-tree mode pvst
      !
      !
      !
      !
      !
      !
      interface FastEthernet0/1
       switchport trunk allowed vlan 34,80
      !
      interface FastEthernet0/2
       switchport trunk allowed vlan 50,99
      !
      interface FastEthernet0/3
       no switchport
       ip address 172.34.100.1 255.255.255.252
       duplex auto
       speed auto
      !
      interface FastEthernet0/4
       no switchport
       ip address 172.34.101.1 255.255.255.252
       duplex auto
       speed auto
      !
      interface FastEthernet0/5
      !
      interface FastEthernet0/6
      !
      interface FastEthernet0/7
      !
      interface FastEthernet0/8
      !
      interface FastEthernet0/9
      !
      interface FastEthernet0/10
      !
      interface FastEthernet0/11
      !
      interface FastEthernet0/12
      !
      interface FastEthernet0/13
      !
      interface FastEthernet0/14
      !
      interface FastEthernet0/15
      !
      interface FastEthernet0/16
      !
      interface FastEthernet0/17
      !
      interface FastEthernet0/18
      !
      interface FastEthernet0/19
      !
      interface FastEthernet0/20
      !
      interface FastEthernet0/21
      !
      interface FastEthernet0/22
      !
      interface FastEthernet0/23
      !
      interface FastEthernet0/24
      !
      interface GigabitEthernet0/1
      !
      interface GigabitEthernet0/2
      !
      interface Vlan1
       no ip address
       shutdown
      !
      interface Vlan34
       mac-address 00e0.f7c8.dc01
       ip address 172.34.34.1 255.255.255.0
      !
      interface Vlan50
       mac-address 00e0.f7c8.dc02
       ip address 172.34.50.1 255.255.255.0
       ip access-group 102 in
      !
      interface Vlan80
       mac-address 00e0.f7c8.dc03
       ip address 172.34.80.1 255.255.255.0
      !
      interface Vlan99
       mac-address 00e0.f7c8.dc04
       ip address 172.34.99.1 255.255.255.0
       ip access-group 101 in
      !
      ip classless
      ip route 172.10.0.0 255.255.255.0 172.34.101.2 
      ip route 172.41.0.0 255.255.255.0 172.34.101.2 
      ip route 172.54.0.0 255.255.255.0 172.34.101.2 
      ip route 0.0.0.0 0.0.0.0 172.34.100.2 
      !
      ip flow-export version 9
      !
      !
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.34.34.0 0.0.0.255
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.34.80.0 0.0.0.255
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.34.50.0 0.0.0.255
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.34.101.0 0.0.0.3
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.41.0.0 0.0.0.255
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.54.0.0 0.0.0.255
      access-list 101 deny ip 172.34.99.0 0.0.0.255 172.10.0.0 0.0.0.255
      access-list 101 permit ip 172.34.99.0 0.0.0.255 any
      access-list 102 deny icmp 172.34.50.0 0.0.0.255 172.34.99.0 0.0.0.255
      access-list 102 permit icmp 172.34.50.0 0.0.0.255 any
      !
      no cdp run
      !
      !
      !
      !
      !
      !
      line con 0
      !
      line aux 0
      !
      line vty 0 4
       login
      !
      !
      !
      !
      end
    
  </details>
  
  <details> <summary> Merkez Router </summary>
      
      Building configuration...
      Current configuration : 1588 bytes
      !
      version 15.1
      no service timestamps log datetime msec
      no service timestamps debug datetime msec
      no service password-encryption
      !
      hostname Router
      !
      !
      !
      !
      !
      !
      !
      !
      no ip cef
      no ipv6 cef
      !
      !
      !
      !
      license udi pid CISCO2811/K9 sn FTX1017KH2G-
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      spanning-tree mode pvst
      !
      !
      !
      !
      !
      !
      interface FastEthernet0/0
       ip address 172.34.101.2 255.255.255.252
       duplex auto
       speed auto
      !
      interface FastEthernet0/1
       no ip address
       duplex auto
       speed auto
       shutdown
      !
      interface Serial0/0/0
       ip address 12.0.0.2 255.255.255.252
       clock rate 2000000
      !
      interface Serial0/0/1
       ip address 25.0.0.1 255.255.255.252
       clock rate 2000000
      !
      interface Vlan1
       no ip address
       shutdown
      !
      router bgp 100
       bgp log-neighbor-changes
       no synchronization
       neighbor 12.0.0.1 remote-as 200
       network 172.34.34.0 mask 255.255.255.0
       network 172.34.80.0 mask 255.255.255.0
       network 172.34.50.0 mask 255.255.255.0
       network 172.34.99.0 mask 255.255.255.0
       network 172.34.101.0 mask 255.255.255.252
       network 12.0.0.0 mask 255.255.255.252
       network 25.0.0.0 mask 255.255.255.252
       network 172.10.0.0 mask 255.255.255.0
       network 172.34.100.0 mask 255.255.255.252
      !
      ip classless
      ip route 172.10.0.0 255.255.255.0 25.0.0.2 
      ip route 172.34.34.0 255.255.255.0 172.34.101.1 
      ip route 172.34.80.0 255.255.255.0 172.34.101.1 
      ip route 172.34.50.0 255.255.255.0 172.34.101.1 
      ip route 172.34.99.0 255.255.255.0 172.34.101.1 
      ip route 172.34.100.0 255.255.255.252 172.34.101.1 
      ip route 0.0.0.0 0.0.0.0 172.34.101.1 
      !
      ip flow-export version 9
      !
      !
      !
      no cdp run
      !
      !
      !
      !
      !
      !
      line con 0
      !
      line aux 0
      !
      line vty 0 4
       login
      !
      !
      !
      end
  
  </details>
  
  <details> <summary> ISP Router </summary>
      
      Building configuration...
      Current configuration : 1358 bytes
      !
      version 15.1
      no service timestamps log datetime msec
      no service timestamps debug datetime msec
      no service password-encryption
      !
      hostname Router
      !
      !
      !
      !
      !
      !
      !
      !
      no ip cef
      no ipv6 cef
      !
      !
      !
      !
      license udi pid CISCO2811/K9 sn FTX1017ZGT4-
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      spanning-tree mode pvst
      !
      !
      !
      !
      !
      !
      interface FastEthernet0/0
       no ip address
       duplex auto
       speed auto
       shutdown
      !
      interface FastEthernet0/1
       no ip address
       duplex auto
       speed auto
       shutdown
      !
      interface Serial0/0/0
       ip address 12.0.0.1 255.255.255.252
      !
      interface Serial0/0/1
       ip address 13.0.0.1 255.255.255.252
       clock rate 2000000
      !
      interface Serial0/2/0
       ip address 14.0.0.1 255.255.255.252
      !
      interface Serial0/2/1
       no ip address
       clock rate 2000000
       shutdown
      !
      interface Vlan1
       no ip address
       shutdown
      !
      router ospf 1
       log-adjacency-changes
       network 13.0.0.0 0.0.0.3 area 0
       network 12.0.0.0 0.0.0.3 area 0
       network 14.0.0.0 0.0.0.255 area 0
      !
      router bgp 200
       bgp log-neighbor-changes
       no synchronization
       neighbor 12.0.0.2 remote-as 100
       network 12.0.0.0 mask 255.255.255.252
       network 13.0.0.0 mask 255.255.255.252
       network 14.0.0.0 mask 255.255.255.252
       network 172.41.0.0 mask 255.255.255.0
       network 172.54.0.0 mask 255.255.255.0
      !
      ip classless
      ip route 0.0.0.0 0.0.0.0 12.0.0.2 
      !
      ip flow-export version 9
      !
      !
      !
      no cdp run
      !
      !
      !
      !
      !
      !
      line con 0
      !
      line aux 0
      !
      line vty 0 4
       login
      !
      !
      !
      end
  
  </details>
  
  <details> <summary> Kocaeli Router </summary>
    
    Building configuration...
    Current configuration : 893 bytes
    !
    version 15.1
    no service timestamps log datetime msec
    no service timestamps debug datetime msec
    no service password-encryption
    !
    hostname Router
    !
    !
    !
    !
    !
    !
    !
    !
    no ip cef
    no ipv6 cef
    !
    !
    !
    !
    license udi pid CISCO2811/K9 sn FTX101797J4-
    !
    !
    !
    !
    !
    !
    !
    !
    !
    !
    !
    spanning-tree mode pvst
    !
    !
    !
    !
    !
    !
    interface FastEthernet0/0
     ip address 172.41.0.1 255.255.255.0
     duplex auto
     speed auto
    !
    interface FastEthernet0/1
     no ip address
     duplex auto
     speed auto
     shutdown
    !
    interface Serial0/0/0
     ip address 13.0.0.2 255.255.255.252
    !
    interface Serial0/0/1
     no ip address
     clock rate 2000000
     shutdown
    !
    interface Vlan1
     no ip address
     shutdown
    !
    router ospf 1
     log-adjacency-changes
     network 172.41.0.0 0.0.0.255 area 0
     network 13.0.0.0 0.0.0.3 area 0
    !
    ip classless
    ip route 0.0.0.0 0.0.0.0 13.0.0.1 
    !
    ip flow-export version 9
    !
    !
    !
    !
    !
    !
    !
    !
    line con 0
    !
    line aux 0
    !
    line vty 0 4
     login
    !
    !
    !
    end
  
  </details>
  
  <details> <summary> Sakarya Router </summary>
      
      Building configuration...
      Current configuration : 926 bytes
      !
      version 15.1
      no service timestamps log datetime msec
      no service timestamps debug datetime msec
      no service password-encryption
      !
      hostname Router
      !
      !
      !
      !
      !
      !
      !
      !
      no ip cef
      no ipv6 cef
      !
      !
      !
      !
      license udi pid CISCO2811/K9 sn FTX1017KDTA-
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      spanning-tree mode pvst
      !
      !
      !
      !
      !
      !
      interface FastEthernet0/0
       ip address 172.54.0.1 255.255.255.0
       duplex auto
       speed auto
      !
      interface FastEthernet0/1
       no ip address
       duplex auto
       speed auto
       shutdown
      !
      interface Serial0/0/0
       ip address 14.0.0.2 255.255.255.252
       clock rate 2000000
      !
      interface Serial0/0/1
       no ip address
       clock rate 2000000
       shutdown
      !
      interface Vlan1
       no ip address
       shutdown
      !
      router ospf 1
       log-adjacency-changes
       network 172.54.0.0 0.0.0.255 area 0
       network 14.0.0.0 0.0.0.3 area 0
      !
      ip classless
      ip route 0.0.0.0 0.0.0.0 14.0.0.1 
      !
      ip flow-export version 9
      !
      !
      !
      no cdp run
      !
      !
      !
      !
      !
      !
      line con 0
      !
      line aux 0
      !
      line vty 0 4
       login
      !
      !
      !
      end
    
  </details>
  
  <details> <summary> Bolu Atölye Router </summary>
      
      Building configuration...
      Current configuration : 797 bytes
      !
      version 15.1
      no service timestamps log datetime msec
      no service timestamps debug datetime msec
      no service password-encryption
      !
      hostname Router
      !
      !
      !
      !
      !
      !
      !
      !
      no ip cef
      no ipv6 cef
      !
      !
      !
      !
      license udi pid CISCO2811/K9 sn FTX10179Y35-
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      !
      spanning-tree mode pvst
      !
      !
      !
      !
      !
      !
      interface FastEthernet0/0
       ip address 172.10.0.2 255.255.255.0
       duplex auto
       speed auto
      !
      interface FastEthernet0/1
       no ip address
       duplex auto
       speed auto
       shutdown
      !
      interface Serial0/0/0
       ip address 25.0.0.2 255.255.255.252
      !
      interface Serial0/0/1
       no ip address
       clock rate 2000000
       shutdown
      !
      interface Vlan1
       no ip address
       shutdown
      !
      ip classless
      ip route 0.0.0.0 0.0.0.0 25.0.0.1 
      !
      ip flow-export version 9
      !
      !
      !
      no cdp run
      !
      !
      !
      !
      !
      !
      line con 0
      !
      line aux 0
      !
      line vty 0 4
       login
      !
      !
      !
      end
    
  </details>
  
  <details> <summary> Merkez Ofis Firewall </summary>
      
      ASA Version 8.4(2)
      !
      hostname ciscoasa
      names
      !
      interface Ethernet0/0
      !
      interface Ethernet0/1
       switchport access vlan 2
      !
      interface Ethernet0/2
      !
      interface Ethernet0/3
      !
      interface Ethernet0/4
      !
      interface Ethernet0/5
      !
      interface Ethernet0/6
      !
      interface Ethernet0/7
      !
      interface Vlan1
       nameif inside
       security-level 100
       ip address 172.34.100.2 255.0.0.0
      !
      interface Vlan2
       nameif outside
       security-level 0
       ip address 212.111.34.46 255.255.255.252
      !
      object network inside-network
       subnet 172.0.0.0 255.0.0.0
      !
      route outside 0.0.0.0 0.0.0.0 212.111.34.45 1
      route inside 172.34.34.0 255.255.255.0 172.34.100.1 1
      route inside 172.34.80.0 255.255.255.0 172.34.100.1 1
      route inside 172.34.50.0 255.255.255.0 172.34.100.1 1
      route inside 172.34.99.0 255.255.255.0 172.34.100.1 1
      route inside 172.41.0.0 255.255.255.0 172.34.100.1 1
      route inside 172.54.0.0 255.255.255.0 172.34.100.1 1
      route inside 172.10.0.0 255.255.255.0 172.34.100.1 1
      !
      !
      !
      object network inside-network
       nat (inside,outside) dynamic interface
      !
      !
      !
      class-map TUM-TRAFIK
       match default-inspection-traffic
      !
      policy-map 3X
       class TUM-TRAFIK
        inspect icmp 
      !
      service-policy 3X global
      !
      telnet timeout 5
      ssh timeout 5
      !
      dhcpd auto_config outside
      !
      !
      !
      !
      !
      !
    
  </details>
    
      

</details>

 <details> <summary>Sistem Projesi Çözümüm </summary>
  
  ## Sistem Projesi Çözümüm
  
  Önceki Sistem ödevleri için Vmware Tools kurup ardından sysprep yapıp hazırladığım Windows 2019 sanal makinesinden DC-1 klonumu oluşturmaya başlıyorum.
    
  ![Resim 1](https://user-images.githubusercontent.com/49712212/144721267-ea40a307-906e-4b08-9eeb-b772864069e8.png)
  
  Clone sihirbazı bana makinenin hangi durumunu klonlamak istediğimi soruyor. Makinem sysprep yapılıp kapandığı için o anki durumunu klonlamak istediğimi belirtiyorum.
  
  ![Resim 2](https://user-images.githubusercontent.com/49712212/144721349-e8a7d49a-6797-40d9-ba9a-744a09b4e077.png)
  
  Kişisel bilgisayarımdaki SSD üzerinde çok fazla alana sahip olmadığımdan Linked Clone seçiyorum. Böylece clone yapılan makinenin vm dosyaları kullanılıyor ve fazladan disk kaynağı kullanılmıyor (Eğer full clone seçilirse dosyalar birebir kopyalanır).
    
  ![Resim 3](https://user-images.githubusercontent.com/49712212/144721417-def56b1f-24ff-4c2e-8e91-a75f8b51e255.png)
  
  Sanal makinenin ismini belirleyip, klasörünü oluşturuyorum.  
  
  ![Resim 4](https://user-images.githubusercontent.com/49712212/144721433-14acf499-9781-47a5-ad35-2aaa391d4e72.png)
  
  Makineyi çalıştırmamın ardından kurulum ekranları karşıma geliyor. Klavye seçimi, uygulama dil ayarları, lisans sözleşmesinin kabul edilmesi, parolanın oluşturulmasının ardından DC-1 sanal makinem kullanılabilir hale geliyor.  

  ![Resim 5](https://user-images.githubusercontent.com/49712212/144721471-083204fb-164a-4780-a276-a51ebf8b5eb9.png)

  ![Resim 6](https://user-images.githubusercontent.com/49712212/144721475-0c165a44-14d3-401f-9cda-4b4a3cc39302.png)

  ![Resim 7](https://user-images.githubusercontent.com/49712212/144721481-8f7dbea2-b00f-4f0e-8ddb-fd2faa91749f.png)

  ![Resim 8](https://user-images.githubusercontent.com/49712212/144721483-1e8e08b1-5c77-46d3-83df-f6b2ced5478b.png)

  Server Manager panelinden DC-1 makinemin adını değiştiriyorum.
  
  ![Resim 9](https://user-images.githubusercontent.com/49712212/144721520-ee4eb664-6d48-454e-a70d-bbfacb60ae16.png)
  
  Remote Desktop servisini açıyorum. 
  
  ![Resim 10](https://user-images.githubusercontent.com/49712212/144721532-5468bf96-d728-4350-b5c2-01e1b0eed7dd.png)
  
  Statik bir ip veriyorum. Bu sunucu aynı zamanda dns görevi de göreceğinden dns sunucuya da kendi ipsini yazıyorum.
  
  ![Resim 11](https://user-images.githubusercontent.com/49712212/144721552-e2e70cdf-d01b-4973-90a9-c0fcc636031d.png)
  
  Ipv6'yı kapatıyorum.
  
  ![Resim 12](https://user-images.githubusercontent.com/49712212/144721566-6e5f85a3-913a-494d-b8dc-08d12bbb6d77.png)
  
  IE enchanced Security'i kapatıyorum.  
  
  ![Resim 13](https://user-images.githubusercontent.com/49712212/144721585-5be14e66-f119-45d7-b4a0-2e43aba8cf79.png)
  
  Eğitmenimizin aksine Firewall'ı kapatmıyorum. Gerek duyulduğunda GPO ile firewall üzerine istenilen kural yazılabilir. Ardından Sanal makinenin isminin değişmesi için sunucuyu restart ediyorum. Ayarların başarılı olduğunu görüyorum.
  
  ![Resim 14](https://user-images.githubusercontent.com/49712212/144721610-fc4a60d0-af27-4619-af7e-a5140c5d2c4e.png)
  
  Dashboard üzerinden Add roles and features seçeneğine tıklıyorum.
  
  ![Resim 15](https://user-images.githubusercontent.com/49712212/144721623-1ae21d24-debc-4dd3-8b57-10524285e356.png)
  
  Rol bazlı bir yükleme yapacağımdan onu seçiyorum.
  
  ![Resim 16](https://user-images.githubusercontent.com/49712212/144721646-2ff65112-61d1-439d-b916-7fbc49758d1e.png)
  
  Mevcut sunucumu seçiyorum.
  
  ![Resim 17](https://user-images.githubusercontent.com/49712212/144721696-b8c6d3f3-8c4b-4e5d-ac45-5f2dc9a46f1f.png)
  
  Ad Ds rolünü seçiyorum. Bana bu rol için gerekli featureları sıralıyor, yüklemesine izin verip ilerliyorum.  
  
  ![Resim 18](https://user-images.githubusercontent.com/49712212/144721727-c80e791f-6892-454c-9cf9-16ea8b0c75d8.png)
  
  Gerekli featurelar zaten seçildiğinden bir şey seçmeden ilerliyorum.  
  
  ![Resim 19](https://user-images.githubusercontent.com/49712212/144721761-d0b68cb5-b47c-42aa-9b78-7855f8788956.png)
  
  Ad Ds rolü hakkında bilgi veren bir ekranla karşılaşıyorum. Dns rolünün eğer networkte yoksa bu makineye kurulması gerektiğinden bahsediyor.
  
  ![Resim 20](https://user-images.githubusercontent.com/49712212/144721782-19f46860-549b-49cd-940f-fb0b3ced1051.png)
  
  Son bir onay istiyor, kurulumu onaylıyorum.  
  
  ![Resim 21](https://user-images.githubusercontent.com/49712212/144721793-05d50785-a722-4f35-b057-69a4af4ce47c.png)
  
  Kurulumun ardından konfigürasyona başlıyorum. Yeni bir domain oluşturacağımdan "Add a new forest" seçeneğini seçiyorum. Domain ismini belirtiyorum.
  
  ![Resim 22](https://user-images.githubusercontent.com/49712212/144721808-318fc670-782b-4deb-b4fe-e078af84b5eb.png)
  
  Domain yapımda 2016 dışında DC kullanmayacağımdan forest ve domain funtional seviyelerini 2016 seçiyorum. Dns Server rolunu eklemesine izin veriyorum. Olası bir kurtarma anında kullanılacak DSRM parolamı oluşturuyorum.
  
  ![Resim 23](https://user-images.githubusercontent.com/49712212/144721838-8cd2216d-0105-4985-b9dc-57f36c6c08b2.png)
  
  Kurulu bir Dns yapısı olmadığından -yeni kurduğumdan- Dns Delegation yapmamıza izin vermiyor. İlerliyorum.  
  
  ![Resim 24](https://user-images.githubusercontent.com/49712212/144721883-395aec2c-80fe-4e06-a99d-35cdd574538e.png)
  
  Netbios ismimizi Trendyol olarak oluşturuyor. Değiştirmiyorum.  
  
  ![Resim 25](https://user-images.githubusercontent.com/49712212/144721909-01277912-fb97-4dbe-b10b-20e04cf34ffa.png)
  
  Active Directory yapısının kullanacağı klasörlerin pathlerini belirtiyor. Değiştirmiyorum.
  
  ![Resim 26](https://user-images.githubusercontent.com/49712212/144721932-51055915-59e7-45a8-bc19-b271bb88aab4.png)
  
  Özet şeklinde kurulum ayarlarını bana sunuyor. İlerliyorum.  
  
  ![Resim 27](https://user-images.githubusercontent.com/49712212/144721963-a45d0f88-74ae-4024-9872-577caafcddf7.png)
  
  Tüm gereksinimleri sağladığını söyleyen bir uyarıyla karşılaşıyorum. Kurulumu başlatıyorum.  
  
  ![Resim 28](https://user-images.githubusercontent.com/49712212/144721984-b78167f4-90c3-47c3-8b14-747b0c57b40d.png)
  
  Restartın ardından domain yapısına dahil olmuş şekilde sunucu açılıyor.
  
  ![Resim 29](https://user-images.githubusercontent.com/49712212/144722001-eef95861-df98-4fd1-ae06-3031abb21f17.png)
  
  Domain rolu kurulduktan sonra File Server rolü kurulumuna geçtim. File Server rolu kurulu olduğundan Resource Manager featureını seçip yüklüyorum.
  
  ![Resim 30](https://user-images.githubusercontent.com/49712212/144722034-4e713926-6c31-470e-ac2e-c43beb54373f.png)
  
  Sonrasında domain yapısında oluşturulacak Ou sayıca az olduğundan Gui üzerinden oluşturuyorum.  
  
  ![Resim 31](https://user-images.githubusercontent.com/49712212/144722055-37a2b31f-c22f-4727-9cb5-634c4d8bcd2d.png)

  Kullanıcıların oluşturulması için kullanıcı özelliklerinin yazdığı csv'ye ve powershell scriptlerine ihtiyacım olduğunu farkettim. Python ile rastgele türkçe isimler, parola oluşturan bir script yazdım. Sonrasında da scriptle oluşturduğum csv’yi Powershell scripti ile okuyup kullanıcıları oluşturdum.

```python
import trnames
import random 
import string


def generate_random_password():
	letters = string.ascii_letters + string.digits
	result_str = ''.join(random.choice(letters) for i in range (12))
	return result_str+'!Qa1'


file = open("users.csv","w")
file.write("firstname,lastname,username,password,email,ou\n")

def create_user(ou,number_of_employee,file):

	for i in range(number_of_employee):
		first_name = trnames.get_first_name()
		last_name = trnames.get_last_name()
		file.write(first_name)
		file.write(",")
		file.write(last_name)
		file.write(",")
		file.write((first_name+"."+last_name).lower())
		file.write(",")
		file.write(generate_random_password())
		file.write(",")
		file.write((first_name+"."+last_name+"@trendyol.com.tr").lower())
		file.write(",")
		file.write("\""+ou+"\"")
		file.write("\n")
	

## Ankara
create_user("OU=IK,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Pazarlama,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Satis,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local",100,file)
## İzmir
create_user("OU=IK,OU=Izmir,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Pazarlama,OU=Izmir,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Satis,OU=Izmir,OU=Trendyol,DC=trendyol,DC=local",100,file)
## İstanbul
create_user("OU=IK,OU=Istanbul,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Pazarlama,OU=Istanbul,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Satis,OU=Istanbul,OU=Trendyol,DC=trendyol,DC=local",100,file)
create_user("OU=IT,OU=Istanbul,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Muhasebe,OU=Istanbul,OU=Trendyol,DC=trendyol,DC=local",5,file)
create_user("OU=Yonetim,OU=Istanbul,OU=Trendyol,DC=trendyol,DC=local",5,file)


file.close()
  
```
Örnek csv dosyası
  
      firstname,lastname,username,password,email,ou
      Pelin,Oren,pelin.oren,TagYMfJO7lBu!Qa1,pelin.oren@trendyol.com.tr,"OU=IK,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Fatma,Ceri,fatma.ceri,m2mUcTT9JsOP!Qa1,fatma.ceri@trendyol.com.tr,"OU=IK,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Emre,Kocaaslan,emre.kocaaslan,Kgxp8mwNTm7H!Qa1,emre.kocaaslan@trendyol.com.tr,"OU=IK,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Fatma,Kuzey,fatma.kuzey,cGn80c8q3nLN!Qa1,fatma.kuzey@trendyol.com.tr,"OU=IK,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Gulsen,Kurak,gulsen.kurak,6yKoexkF3bSw!Qa1,gulsen.kurak@trendyol.com.tr,"OU=IK,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Halil,Elik,halil.elik,Iuf7Ut0Ecdc9!Qa1,halil.elik@trendyol.com.tr,"OU=Pazarlama,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Zeynep,Yasar,zeynep.yasar,SvG3NLXxxTlR!Qa1,zeynep.yasar@trendyol.com.tr,"OU=Pazarlama,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Yasemin,Kirmizi,yasemin.kirmizi,qm9Y7UZ7Ouw3!Qa1,yasemin.kirmizi@trendyol.com.tr,"OU=Pazarlama,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Bekir,Guven,bekir.guven,LCWFNBYODeQs!Qa1,bekir.guven@trendyol.com.tr,"OU=Pazarlama,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Serife,Ezeroglu,serife.ezeroglu,5sFCMos2Kgfi!Qa1,serife.ezeroglu@trendyol.com.tr,"OU=Pazarlama,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Salih,Karadeniz,salih.karadeniz,tboXDJRLg2BU!Qa1,salih.karadeniz@trendyol.com.tr,"OU=Satis,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Nergiz,Gungor,nergiz.gungor,AUIPRSUqhp2q!Qa1,nergiz.gungor@trendyol.com.tr,"OU=Satis,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"
      Serap,Yel,serap.yel,O5IvT6z9Rbel!Qa1,serap.yel@trendyol.com.tr,"OU=Satis,OU=Ankara,OU=Trendyol,DC=trendyol,DC=local"

  
```powershell
  
  #Csv'den dosyayı al
$Users = Import-csv C:\users.csv

foreach ($User in $Users)
{
	#Her satırda kullanıcı bilgisini al
		
	$Username = $User.username
	$Password = $User.password
	$Firstname = $User.firstname
	$Lastname = $User.lastname
	$OU = $User.ou 
  $email=$User.email
	
	#kullanıcıyı oluştur
	New-ADUser `
	-SamAccountName $Username `
	-UserPrincipalName "$Username@trendyol.local" `
	-Name "$Firstname $Lastname" `
	-GivenName $Firstname `
	-Surname $Lastname `
	-Enabled $True `
	-DisplayName "$Lastname, $Firstname" `
	-Path $OU `
	-EmailAddress $email `
	-AccountPassword (convertto-securestring $Password -AsPlainText -Force) -ChangePasswordAtLogon $True
            
	
}

```

  ![Resim 35](https://user-images.githubusercontent.com/49712212/144722317-0e5eb183-ce9d-4e90-8186-ccb1c94e9461.png)

  Ardından 5gb-5gb olacak şekilde iki disk ekledim.
  
  ![Resim 36](https://user-images.githubusercontent.com/49712212/144722348-dab00e01-3dce-4128-a89f-2816e517f1df.png)
  
  Disk Management kısmına gittim, iki diski initalize ettim. Ardından Raid 0 için New Striped Volume seçeneğini seçtim.
  
  ![Resim 37](https://user-images.githubusercontent.com/49712212/144722363-c8169f6e-8d3b-4e5b-b1a2-0240452f2352.png)
  
  Eklediğim iki diski de seçtim.
  
  ![Resim 38](https://user-images.githubusercontent.com/49712212/144722370-74934bce-bd17-458c-a897-a1857780d3f2.png)
  
  Kontrolun ardından Raid 0 olarak diskin eklendiğini gördüm. 
  
  ![Resim 39](https://user-images.githubusercontent.com/49712212/144722380-495063b8-4f1b-4703-aea1-645f14a59bcb.png)
  
  Security Groupların oluşturulması ve ilgili OU'daki kullanıcıların eklenmesi için Powershell scriptleri kullandım.

```powershell

$group_il = 'Istanbul','Izmir','Ankara'
$group_departman = 'Satis','Pazarlama','IK'
$group_merkez = 'Yonetim','Muhasebe','IT','Satis','Pazarlama','Ik'

foreach($il in $group_il)
{
    
 if ($il -eq 'Istanbul') {
    foreach($departman in $group_merkez){
        New-ADGroup ` ${il}_$departman -Path "OU=$departman,OU=$il,OU=Trendyol,DC=trendyol,dc=local" -GroupCategory Security -GroupScope Global -PassThru –Verbose `
        
        Get-ADUser ` -SearchBase "OU=$departman,OU=$il,OU=Trendyol,DC=trendyol,DC=local" -Filter * | ForEach-Object {Add-ADGroupMember ` -Identity ${il}_$departman -Members $_ ` } `
    }
}
else{
    foreach($departman in $group_departman){
        New-ADGroup ` ${il}_$departman -Path "OU=$departman,OU=$il,OU=Trendyol,DC=trendyol,dc=local" -GroupCategory Security -GroupScope Global -PassThru –Verbose `
        
        Get-ADUser ` -SearchBase "OU=$departman,OU=$il,OU=Trendyol,DC=trendyol,DC=local" -Filter * | ForEach-Object {Add-ADGroupMember ` -Identity ${il}_$departman -Members $_ ` } `
    }
}

}
```
  
  Klasörlerin paylaştırılması ve doğru yetkilendirmenin yapılması için Powershell scriptleri kullandım.
  
  
```powershell
  
$folder_il = 'Istanbul','Izmir','Ankara'
$folder_departman = 'Satis','Pazarlama','IK'
$folder_merkez = 'Yonetim','Muhasebe','IT','Satis','Pazarlama','IK'

New-Item   ` "E:\Public" -itemtype directory `

New-SMBShare ` -Name "Public" –Path "E:\Public" –FullAccess "TRENDYOL\Domain Admins" -ChangeAccess "TRENDYOL\Domain Users"   `

foreach($il in $folder_il)
{
    New-Item   ` "E:\$il" -itemtype directory `  


if ($il -eq 'Istanbul') {
    foreach($departman in $folder_merkez){

        New-Item   ` "E:\$il\$departman" -itemtype directory `     
      
        New-SMBShare ` -Name "${il}_$departman" –Path "E:\$il\$departman" –FullAccess "TRENDYOL\Domain Admins", "Trendyol\Istanbul_IT" -ChangeAccess "TRENDYOL\${il}_$departman"  -verbose  `     

        
        
    }
}
else{
    foreach($departman in $folder_departman){

        New-Item   ` "E:\$il\$departman" -itemtype directory `

        New-SMBShare ` -Name ${il}_$departman –Path "E:\$il\$departman" –FullAccess "TRENDYOL\Domain Admins", "TRENDYOL\Istanbul_IT" -ChangeAccess "TRENDYOL\${il}_$departman"   `     
        
    }
}

}

```
  Kontrolümün ardından problemsiz şekilde klasörlerin oluşturulup atamaların yapıldığını gördüm.
  
  ![Resim 42](https://user-images.githubusercontent.com/49712212/144722483-1667e1dd-5337-40dc-ac87-cba05edc200e.png)
  
  ![Resim 43](https://user-images.githubusercontent.com/49712212/144722496-56a1e72d-09df-4f16-8671-a70cc55ee102.png)
  
  Yedekliliğin sağlanması için bir bat dosyası oluşturup günlük çalışacak şekilde Task Scheduler'a ekledim.
  
  ![Resim 44](https://user-images.githubusercontent.com/49712212/144722517-44565e33-fe20-4e61-96f7-cd0d8149a64f.png)
  
  ![Resim 45](https://user-images.githubusercontent.com/49712212/144722528-a3c4fa6f-0ce8-4106-acbe-6bbdfbac2ba9.png)
  
  ![Resim 46](https://user-images.githubusercontent.com/49712212/144722534-9dd3084c-f773-4dbb-b2fb-1147260c1dbc.png)  

  ![Resim 47](https://user-images.githubusercontent.com/49712212/144722554-75560c6a-54b2-44b3-9115-503b6b925e6b.png)
  
  ![Resim 48](https://user-images.githubusercontent.com/49712212/144722567-a8cfbb4e-da5e-4308-a0af-254c07ec4bc9.png)  
  
  ![Resim 49](https://user-images.githubusercontent.com/49712212/144722580-1e5bbb4c-ae1b-45c2-9787-83d2775c83ff.png)

  Ekledikten sonra bir kere çalıştırıp dosyaların kopyalandığını doğruladım.
  
  ![Resim 50](https://user-images.githubusercontent.com/49712212/144722629-35d42b9f-077b-4ddf-98b7-8eaf42b24aa8.png)
  
  Resource Manager kısmına geçip yetkilendirmeleri yapmaya başladım. Öncelikle tüm dosya türlerini blokladım. Ardından istenildiği şekilde exceptionlar yazdım. 
  
  ![Resim 51](https://user-images.githubusercontent.com/49712212/144722659-86160bb8-e3d5-476a-97d2-1b2bd2836225.png)
  
  ![Resim 52](https://user-images.githubusercontent.com/49712212/144722672-2e2d6029-7221-4512-8133-9506ca6a5f59.png)
  
  Telnet Client kurulumu için Add Roles And Features kısmından gerekli feature'ı ekledim.
  
  ![Resim 53](https://user-images.githubusercontent.com/49712212/144722689-7388bbea-55dd-4f7e-9e63-72429be2f704.png)
  
  Telnet kurulduktan sonra elimdeki temiz vmden bir klon daha oluşturdum. Aynı gateway ve ip bloğundan statik ip verdim. Sonrasında Firewall üzerinden Rdp'ye izin verip servislerden de Rdp'yi enable ettim.  
  
  ![Resim 54](https://user-images.githubusercontent.com/49712212/144722715-4bc065d4-09cc-4078-89a6-2c9519d30206.png)  

  ![Resim 55](https://user-images.githubusercontent.com/49712212/144722721-8c1f1705-6180-4077-82ec-358d5c556462.png)
  
  ![Resim 56](https://user-images.githubusercontent.com/49712212/144722728-e91a7596-0670-46f0-acc0-66707e745ce2.png)
  
  ![Resim 57](https://user-images.githubusercontent.com/49712212/144722741-91b6df2a-6878-44a8-9c95-2936c0f71d9f.png)
  
  Sunucuma geçip telnet komutunu parametreleri ile çalıştırdım ve başarılı olduğunu gördüm.
  
  ![Resim 58](https://user-images.githubusercontent.com/49712212/144722755-fdd32770-9a34-4ab8-af25-aac8d90c32a6.png)
  
  ![Resim 59](https://user-images.githubusercontent.com/49712212/144722766-68a3ba35-f236-4289-a89c-f33f3e265b9a.png)



  
  </details>
