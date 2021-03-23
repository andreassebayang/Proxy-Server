# Proxy-Server
Squid adalah proxy caching untuk Web yang mendukung HTTP, HTTPS, FTP, dan banyak lagi. Ini mengurangi bandwidth dan memperbaiki waktu respon dengan cara menyimpan dan menggunakan ulang halaman web yang sering diminta. Squid memiliki kontrol akses yang luas dan membuat akselerator server yang baik. Ini berjalan pada sebagian besar sistem operasi yang ada, termasuk Windows dan dilisensikan di bawah GNU GPL.

Squid digunakan oleh ratusan Penyedia Internet di seluruh dunia untuk memberi pengguna akses web terbaik kepada penggunanya. Squid mengoptimalkan aliran data antara client dan server untuk meningkatkan kinerja dan cache konten yang sering digunakan untuk menghemat bandwidth. Squid juga dapat mengarahkan permintaan konten ke server dengan berbagai cara untuk membangun hierarki server cache yang mengoptimalkan throughput jaringan.

Berikut Langkah - langkah mengkonfigurasi Squid

Instalasi Squid

apt -y install squid

Edit konfigurasi squid agar komputer di LAN kita dapat menggunakan Squid tersebut

vi /etc/squid/squid.conf

Beberapa contoh setting yang penting


#visible_hostname xxx.xxx.xx.xx #IP address server Squid
  "Namun bisa menghiraukan bagian visible_hostname karena sudah diatur secara otomatis mencari hostname"

find acl localnet lalu hilangkan tanda #

#Example rule allowing access from your local networks.
#Adapt to list your (internal) IP networks from where browsing
#should be allowed
acl localnet src 10.0.0.0/8     # RFC1918 possible internal network
acl localnet src 172.16.0.0/12  # RFC1918 possible internal network
acl localnet src 192.168.0.0/16 # RFC1918 possible internal network

find http_access allow lalu tambahkan baris dibawah ini
http_access allow localnet
Restart Squid

service squid restart
systemctl restart squid.service


Setup Client
Tidak banyak yang perlu di set di sisi Client. Arahkan proxy di sisi Client ke

IP address Server Squid
Port       3128
