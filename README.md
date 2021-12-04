# System-Network-Bootcamp-Final-Case

## Talimatlar

<details> <summary>Network Talimatları </summary> 

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
  

## Çözümler

<details> <summary>Network Projesi Çözümüm </summary> 
  
  # Network Çözümü
  
  ## Topoloji
  
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

 <details> <summary> Sistem Projesi Çözümüm </summary>
    
  </details>
