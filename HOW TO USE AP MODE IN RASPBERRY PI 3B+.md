* HOW TO USE AP MODE IN RASPBERRY PI 3B+
* SUBNET : 172.24.1.0/24
* SSID : YongTest
* PWD : testpass1234
* NETWORK INTERFACE = eth0
* AP INTERFACE = wlan0
* USE MASQUERADE, FORWARD ROUTING
* ALL THE COMMANDS TYPED ON ROOT PRIVILEGE
<pre><code># apt install hostapd</code></pre>

<pre><code># systemctl unmask hostapd
# systemctl enable hostapd</code></pre>

<pre><code># apt install dnsmasq</code></pre>

<pre><code># DEBIAN_FRONTEND=noninteractive apt install -y netfilter-persistent iptables-persistent</code></pre>

<pre><code># nano /etc/dhcpcd.conf</code></pre>

<pre><code>interface wlan0
    static ip_address=172.24.1.1/24
    nohook wpa_supplicant</code></pre>

<pre><code># nano /etc/sysctl.d/routed-ap.conf</code></pre>

<pre><code># sysctl -w net.ipv4.ip_forward=1</code></pre>

<pre><code># iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE</code></pre>

<pre><code># netfilter-persistent save</code></pre>

<pre><code># mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
# nano /etc/dnsmasq.conf</code></pre>

<pre><code>interface=wlan0
dhcp-range=172.24.1.2,172.24.1.254,255.255.255.0,24h
domain=wlan
address=/gw.wlan/172.24.1.1</code></pre>

<pre><code># rfkill unblock wlan</code></pre>

<pre><code># nano /etc/hostapd/hostapd.conf</code></pre>

<pre><code>interface=wlan0
driver=nl80211
ssid=YongTest
hw_mode=g
channel=6
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=testpass1234
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP</code></pre>

<pre><code># systemctl reboot</code></pre>