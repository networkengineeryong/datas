# Network Basic Concept
* 네트워크란 두개 이상의 기기를 연결해 서로 통신 가능 할 때 형성된다
* 네트워크의 분류
    * PAN ( Personal Area Network ) : 가장 작은 규모의 네트워크
    * LAN ( Local Area Network ) : 근거리 영역 네트워크
    * MAN (Metropolitan Area Network) : 대도시 영역 네트워크
    * WAN (Wide Ares Network) : 광대역 네트워크
    * VAN (Value Added Network) : 여러 종류의 정보서비스가 부가된 통신망
    * ISDN (Integrated Services Digital Network) : 종합정보 통신망
* 네트워크의 연결 구조
    * Point to Point: 기기와 기기간의 일대일 연결
    * Point to Multicast: 한 기기에 여러 기기가 연결된 구조
        * 서버, 클라이언트의 구조에서 쉽게 찾아볼 수 있다
* Subnet Mask
    * 인구의 증가, IP소비율의 증가로 인해 고안된 방법
    * 네트워크를 세부적으로 나눠 더 많은 기기가 IP를 효과적으로 사용할 수 있다
    * 2진수 32개로 나타낸다
    * 쉽게 찾아볼 수 있는 192.168.0.1/24로 예를 들어본다
    * /24 는 Prefix라 하여 서브넷 마스크를 쉽게 읽을 수 있게하는 문법이다
    * /24 는 24번째까지가 네트워크, 255.255.255.0 으로 표현된다
        * 2진수 표현: 1111 1111, 1111 1111, 1111 1111, 0000 0000
    * 192.168.0.1 부터 192.168.0.254의 IP를 사용할 수 있다
        * 192.168.0.0은 네트워크 대표주소, 192.168.0.255는 브로드캐스트 주소로 사용
        * 브로드 캐스트 주소는 ARP등 한 네트워크의 모든 기기들에게 데이터를 보낼 때 사용 

# SSH (Secure Shell)
* 네트워크 보안 도구
* 원격접속을 안전하게 할 수 있게 해주는 프로토콜
* Putty, Secure CRT 등 많은 SSH 도구들이 있다

# Packet
* 네트워크를 통해 데이터를 전송하기 쉽도록 나눈 데이터의 전송단위
* 패키지 + 버킷의 합성어
* 데이터를 보내기 전에 Source IP, Destination IP 등을 기입해서 보낸다

# Unicast, Broadcast
* Unicast
    * 1:1 통신에 사용되어 Source IP, Destination IP가 필요하다
    * PC A에서 PC B에게 패킷을 전달할 때 사용된다 
* Broadcast
    * 1:多 통신에 사용된다 Source IP가 필요하다
    * PC A가 PC B에게 패킷을 전달하는데 서로의 맥주소를 모를 때 ARP가 발생한다
* ARP (Address Resolution Protocol)
    * Broadcast 통신 방식을 사용한다
    * 네트워크에 연결된 모든 기기에 패킷을 보내 IP, 맥주소를 얻어온다
    * A가 요청한 IP를 가진 기기의 맥주소를 얻으면 포워딩 해준다

# What is PING
* Paket Internet Groper
* 사용 프로토콜: ICMP (Internet Control Message Protocol)

* 네트워크의 연결성을 확인하기 위해 사용하는 프로토콜이다

&nbsp;

<pre><code>[root@localhost ~]# ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=42.7 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=38.4 ms
</code></pre>

* icmp_seq: 핑 전송 순서
* ttl: 통신시 거쳐간 기기의 갯수 (Time To Live, OS마다 초기값이 다르다)
    * 기기를 하나 거칠 때 마다 1씩 감소한다 0이 되면 패킷을 폐기한다
* time: 통신에 소모된 시간

&nbsp;

* 에러 코드
<pre><code>H, !N or !P – host, network or protocol unreachable
S – source route failed
F – fragmentation needed
U or !W – destination network/host unknown
I – source host is isolated
A – communication with destination network administratively prohibited
Z – communication with destination host administratively prohibited
Q – for this ToS the destination network is unreachable
T – for this ToS the destination host is unreachable
X – communication administratively prohibited
V – host precedence violation
C – precedence cutoff in effect</code></pre>

* 라우터에서 PING 입력 시 ARP 테이블에 목적지 정보가 없으면 패킷이 하나 드랍된다 (ARP)

# DNS (Domain Name System)
* 외우기 힘든 IP주소 대신에 문자열을 사용해 통신하기 위해 사용
* 예시: naver.com, google.com
* 거의 모든 사이트에 사용되고 있다

# How To Interpret The Routing Table
<pre><code>Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         router.asus.com 0.0.0.0         UG    100    0        0 ens33
192.168.0.0     0.0.0.0         255.255.255.0   U     100    0        0 ens33</code></pre>

* Destination
    * 목적지 IP주소
    * default는 발생한 패킷의 목적지 IP주소를 라우팅 테이블에서 찾지 못했을 때 사용됨
* Gateway
    * 패킷을 forwarding할 interface의 IP주소
* Genmask
    * Subnetmask와 동일한 개념, 네트워크의 분리에 사용되는 개념
* Flags
    * 경로의 상태를 나타낸다
    * U : 유효한 경로
    * G : 경로가 라우터를 향한다
    * H : 경로가 호스트를 향한다
* Metric
    * 최적 경로를 정하기 위해 사용하는 값
* Ref
    * 해당 경로가 없으면 통신이 불가능한 경로의 수
* Use
    * 전송한 패킷 수
* Iface
    * 사용할 인터페이스 명

# Default Gateway
* Default G/W 동작방식
    * 패킷 발생 -> 라우팅 테이블과 목적지 SUBNET 비교
    * 라우팅 테이블에 목적지 SUBNET이 없으면 Default G/W로 Forwarding

# DHCP (Dynamic Host Configuration Protocol)
* 서버에서 클라이언트에게 IP를 자동으로 제공하는 프로토콜
* 한 네트워크에 많은 호스트가 생기고, 그 호스트들이 인터넷을 이용해야 한다면

    모든 호스트는 IP를 할당 받아야 한다
* 많은 호스트에게 일일히 IP를 할당 해줘야 한다면 너무 번거롭기 떄문에 사용한다


# NAT (Network Address Translation)
* NAT의 종류
    * NAT (사설IP를 공인IP로 변환)
    * Reverse NAT (공인IP를 사설IP로 변환)
    * Redirect NAT (특정 서비스 FORWARDING에 사용)
    * Exclude NAT (NAT를 적용하지 않는 객체 지정에 사용)
    * Dynamic NAT (사설IP 다수 : 공인IP 다수)
    * Static NAT (사설IP : 공인IP)
    * SNAT (Source IP주소 변경)
    * DNAT (Destination IP주소 변경)

# MASQUERADE
* 리눅스의 SNAT

* 다른 기기에서 보낸 트래픽을 다른 네트워크에 Forward하는데에 사용한다

* 사용 예시
    * 리눅스 컴퓨터를 A, 이어 붙인 컴퓨터를 B라고 가정하고 설명한다
    * A와 B는 eth1 인터페이스로 연결되어 있다 가정한다
    * A는 라우터와 eth0 인터페이스로 연결되어 있다 가정한다

    &nbsp;

    * 리눅스 컴퓨터에 다른 컴퓨터를 연결해 인터넷을 공유하여 사용하는 상황
    * 이어 붙인 컴퓨터는 무조건 리눅스 컴퓨터로 빠져나갈 수 밖에 없다
    
    &nbsp;

    * B에서 8.8.8.8 (구글)로 핑을 보낸다고 가정한다
    * B는 default g/w인 A에게로 트래픽을 전송한다
    * A는 패킷과 자신의 라우팅 테이블을 분석해 8.0.0.0/8 대역의 경로가 없다면 
    * default g/w로 트래픽을 forwarding 하게 되는데 여기에 Masquerade 설정이 필요하다
    * B의 트래픽을 라우터로 forwarding 하는 과정에서 source ip를 자신의 ip로 변환한다
    * 고로 라우팅 테이블에 eth1 subnet이 등록되어 있지 않아도 보내고, 받을수 있게 되는 것이다

    &nbsp;

    <pre><code># iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE</code></pre>

# VPN
* 가상 사설망
* 주로 트래픽을 외부에 노출시키지 않고 통신하기 위해 사용한다
* 재택근무 등 다양한 환경에 사용할수 있다 (비용 절감)
    * 전용선을 재택근무를 하는 모든 사원들의 집에 설치해주는게 비현실적이기 때문이다
* 사용 이유는 크게 터널링, 데이터 암호화로 나눌수 있다

# DMZ (Demilitarized Zone)
* 내, 외부 네트워크 구간 사이에 위치한 중간 지점
* 침입차단 시스템 등 접근 제한을 수행
* 외부 네트워크에서 직접 접근이 가능한 영역
* 메일 서버, 웹 서버, DNS 서버, DB를 주로 위치시킨다