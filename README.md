# -CN-Wireshark-Traceroute-and-IPv4-Questions
 - 2017년 1학기 성균관대학교 최형기 교수님 컴퓨터네트웤개론 수업 1번째 과제
 - Wireshark, Traceroute 프로그램에 관한 문제와 IPv4 및 router에 관한 문제 풀이
 - 2017 1st semester Sungkyunkwan University Professor Hyoung-Kee Choi's Introduction to Computer Networking class, 1st assignment
 - Problems with Wireshark, Traceroute program and problems with IPv4 and router


## 1.	Wireshark
 **- Download an application Wireshark in your computer from https://www.wireshark.org/.**

### a)	What is this application for?
 - Wireshark는 유선과 무선 네트워크를 살펴볼 수 있는 Host에서 동작하는 프로그램으로, 네트워크 프레임을 수집 또는 캡처하고, 해석함으로써 네트워크 문제점 해결, 최적화, 보안, 애플리케이션 분석을 위한 도구이다.
 - Wireshark는 네트워크상에서 누가 최상위 대화자인지, 현재 어떤 애플리케이션이 사용되고 있는지, 네트워크상에서 어떤 프로토콜이 지원되는지, 요청이 오류 응답을 수신했는가 대한 여부, 패킷이 경로에서 폐기되거나 지연되고 있는가에 대한 여부를 쉽게 결정하는데 사용된다.

### b)	How is this application related to Tcpdump and Pcap library?
 - TCPdump는 일반적인 패킷 가로채기 소프트웨어로, 사용자가 TCP/IP뿐 아니라 컴퓨터에 부착된 네트워크를 통해 송수신되는 기타 패킷을 가로채고 표시할 수 있도록 한다.
 - Pcap library는 Portable Packet Capturing Library 이며, 간단하게 패킷을 캡처하기 위한 함수 모음 또는 라이브러리를 말한다. Pcap library는 운영체제에 상관 없이 범용적으로 사용가능한 API를 제공해줌으로써, 공용 프로그램 혹은 공용 라이브러리의 제작이 가능하도록 도와준다. libpcap을 이용한 가장 대표적인 프로그램이 Tcpdump이다.
 - 즉, 네트워크 패킷을 캡처하기 위해 필요한 함수 모음 또는 라이브러리를 pcap library이라 하고, 이를 기반으로 사용자가 쉽게 패킷을 가로채도록 하는 프로그램이 tcpdump이다. Wireshark는 네트워크 패킷 및 프레임을 수집 또는 캡처할 뿐만 아니라 분석, 해석하여 네트워크 상태 및 문제점을 파악하는 프로그램이다.


## 2.	Traceroute
 **- This explanation is based on the Linux version.**
 
### a)	What is this application for? When do you use this application?
 - Traceroute는 인터넷을 통해 거친 경로를 표시하고, 구간의 정보를 기록하고, 인터넷 프로토콜 네트워크를 통해 패킷 전송의 지연을 측정하기 위한 컴퓨터 네트워크 진단 유틸리티이다.

### b)	Run the application for a server of your choice and capture a screen of the ouput.  
  ![image](https://user-images.githubusercontent.com/26705935/40757011-52edc166-64c1-11e8-8952-1984dac90672.png)

### c)	Outputs of the command show the five columns. What are those columns??
 - 각 단계의 첫 번째는 순서 번호, 두 번째는 경로 상에 놓여진 라우터 이름 혹은 IP, 세 번째부터 다섯 번째 까지는 각 라우터의 응답 시간을 의미한다. 각각의 라우터마다 ping을 3번씩 전송하여 돌아오는 응답시간을 표시하기 때문에 결과에 나타나는 응답 시간은 3개씩이다.


## 3. Problems about IPv4
### (1) IPv4 and subnet mask
 **- My IP address is 203.255.252.170 and the subnet mask is 255.255.255.192.**
 
#### a)	What is the 32-bit binary representation of my IP address?
 - 11001011 . 11111111 . 11111100 . 10101010(2)
 
#### b)	How many IP addresses are assigned for this network? 
 - Subnet mask : 11111111 . 11111111 . 11111111 . 11000000(2)  
 즉, 이 subnetwork는 26 = 64개의 IP 주소가 할당되어 있다.
 
#### c)	Specify the starting IP address and the ending IP address for this network. 
 - IP 주소와 subnet mask와 AND연산을 한다.
 - starting IP address : 11001011 . 11111111 . 11111100 . 10000000(2)
 - ending IP address : 11001011 . 11111111 . 11111100 . 10111111(2)
-----------------------------------------------------------------------

### (2) Router and CIDR
 **- A router has the following (CIDR) entries in its routing table:**   
  ![image](https://user-images.githubusercontent.com/26705935/40757319-e055e230-64c2-11e8-8923-6ec8b9fc3aad.png)

#### For each of the following IP addresses, what does the router do if a packet with that address arrives?
 - 135.46.56.0/22 : 10000111 . 00101110 . 001110 | 00 . 00000000(2)  
   135.46.60.0/22 : 10000111 . 00101110 . 001111 | 00 . 00000000(2)  
   192.53.40.0/23 : 11000000 . 00110101 . 0010100 | 0 . 00000000(2)  
   
 - 네트워크 주소를 2진법으로 표현한 것이다. | 는 network와 host IP 주소의 경계를 나타낸다.
 
 **a) 135.46.63.10**
   - 위의 IP 주소의 135.46 까지 부분은 Ifc0, Ifc1과 똑같다. 따라서 둘 중 하나로 이동한다고 예상하고, subnet mask는 /22를 적용한다.  
   IP주소를 2진법으로 표현하면, 135.46.63.10 : 10000111 . 00101110 . 001111 | 11 . 00001010(2) 이다.  
   위의 주소에서 왼쪽부터 22번째 비트까지의 network address는 Ifc1의 network address와 같다.  
   따라서 Router는 Ifc1라는 interface로 보낸다.
   
 **b)	192.53.56.7**
   - 위의 IP 주소의 192.53 까지 부분은 Ifc2와 똑같다. 따라서 subnet mask는 /23를 임시로 적용한다.  
   IP주소를 2진법으로 표현하면, 192.53.56.7 : 11000000 . 00110101 . 0011100 | 0 . 00000111(2) 이다.  
   위의 주소에서 왼쪽부터 23번째 비트까지의 network address는 Ifc2의 network address와 다르다.  
   따라서 Router는 Ifc3이라는 interface로 보낸다.
-----------------------------------------------------------------------

### (3) IPv4 allocation
 **- Consider a router that interconnects three subnets: Subnet 1, Subnet 2, and Subnet 3. Suppose all of the interfaces in each of these three subnets are required to have the prefix 223.1.17/24. Also suppose that Subnet 1 is required to support at least 60 interfaces, Subnet 2 is to support at least 90 interfaces, and Subnet 3 is to support at least 12 interfaces. Provide three network addresses (of the form a.b.c.d/x) that satisfy these constraints.**
 
   - 한 interface 당 하나의 IP가 필요하다. 또한 IP 주소는 2n 개의 형태로 할당할 수 있다.
   
   - Subnet 1은 60개 이상의 IP 주소가 필요하다. 따라서 Subnet 1에게는 26 = 64(>60)개의 IP 주소를 할당해준다.  
   Subnet 2는 90개 이상의 IP 주소가 필요하다. 따라서 Subnet 2에게는 27 = 128(>90)개의 IP 주소를 할당해준다.  
   Subnet 3은 12개 이상의 IP 주소가 필요하다. 따라서 Subnet 3에게는 24 = 16(>12)개의 IP 주소를 할당해준다.
   
   - 할당되는 IP 주소가 많은 subnet 순서대로 할당한다. 즉, 2 -> 1 -> 3 순서로 할당한다.
   
     Subnet 2 는 00000000(2) ~ 01111111(2) 까지 할당해줘야 하므로, Subnet 2의 subnet mask 는  
     11111111 . 11111111 . 11111111 . 1 | 0000000(2) 이다. 따라서 Subnet 2 의 network address : 223.1.17.0/25 이다.
     
     Subnet 1 은 10000000(2) ~ 10111111(2) 까지 할당해줘야 하므로, Subnet 1의 subnet mask 는  
     11111111 . 11111111 . 11111111 . 11 | 000000(2) 이다. 따라서 Subnet 1 의 network address : 223.1.17.128/26 이다.
     
     Subnet 3 은 11000000(2) ~ 11001111(2) 까지 할당해줘야 하므로, Subnet 3의 subnet mask 는  
     11111111 . 11111111 . 11111111 . 1111 | 0000(2) 이다. 따라서 Subnet 3 의 network address : 223.1.17.192/28 이다.
-----------------------------------------------------------------------

### (4) Router using longest prefix matching
 **- Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the following forwarding table:**
 
 ![image](https://user-images.githubusercontent.com/26705935/40758095-9f20cec0-64c6-11e8-9115-4868b22244fb.png)
 
 **- For each of the five interfaces, give the associated range of destination host addresses and the number of addresses in the range.**  
   - Interface 0 : 00000000(2) ~ 00111111(2) : 64개  
   - Interface 1 : 01000000(2) ~ 01011111(2) : 32개  
   - Interface 2 : 01100000(2) ~ 01111111(2) : 32개  
   - Interface 3 : 10000000(2) ~ 10111111(2) : 64개  
   - Interface 4 : 11000000(2) ~ 11111111(2) : 64개  
