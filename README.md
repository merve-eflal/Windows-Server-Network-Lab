# Windows Server Kurulumu ve Ağ Servisleri Yönetimi (Laboratuvar Çalışması)

Bu depo; sanal ortamda Windows Server ve Windows istemciler üzerinde Active Directory, DNS, NAT, Group Policy, DHCP, FTP, Web (IIS) ve E-Posta servislerinin sıfırdan kurulum, konfigürasyon ve doğrulama süreçlerini içermektedir.

---

## 🏗️ Ağ Altyapısı ve IP Mimarisi

Sistem üzerinde 3 adet sanal Ethernet kartı yapılandırılmış, CIDR `/22` alt ağları üzerinden iç ve dış ağ yönlendirmeleri sağlanmıştır:

| Arayüz / Kart | IP Bloğu | Alt Ağ Maskesi | Açıklama |
| :--- | :--- | :--- | :--- |
| **Ethernet 1 (WAN / Dış Hat)** | `172.16.10.1` | `255.255.252.0` (/22) | Doğrudan internete bağlı bacak; NAT çıkışını yönetir. |
| **Ethernet 2 (LAN 1 / İç Ağ)** | `172.16.20.1` | `255.255.252.0` (/22) | NAT üzerinden dışarıya çıkan istemci yerel ağı. |
| **Ethernet 3 (LAN 2 / İç Ağ)** | `172.16.30.1` | `255.255.252.0` (/22) | NAT üzerinden dışarıya çıkan istemci yerel ağı. |

---

## 📂 Yapılandırma Adımları ve Ekran Görüntüleri

### A. Sanallaştırma ve Windows Server Kurulumu
1. Sanallaştırma yazılımının kurulum ortamı (`1.png`).
2. Windows Server işletim sistemi kurulum başlangıç anı (`2.png`).
3. Kurulum tamamlandıktan sonra yönetici (Administrator) parolası belirleme ekranı (`3.png`).

<p align="center">
  <img src="screenshots/A/1.png" width="30%" alt="Sanallastirma Ortami" />
  <img src="screenshots/A/2.png" width="30%" alt="Kurulum Baslangici" />
  <img src="screenshots/A/3.png" width="30%" alt="Yonetici Sifresi" />
</p>

---

### B. Active Directory Domain Services (AD DS)
1. Active Directory rol ve özellik ekleme başlangıcı (`1.png`).
2. Domain adı yapılandırma aşaması (`2.png`).
3. Active Directory kurulumunun başarıyla tamamlanmış hali (`3.png`).

<p align="center">
  <img src="screenshots/B/1.png" width="30%" alt="AD Kurulum Baslangici" />
  <img src="screenshots/B/2.png" width="30%" alt="Domain Adi Girisi" />
  <img src="screenshots/B/3.png" width="30%" alt="AD Kurulumu Tamamlandi" />
</p>

---

### C. DNS Sunucu ve Bölge Kayıtları (Zone Transfer)
1. DNS Sunucu yönetim ve yapılandırma arayüzü (`1.png`).
2. Forward Lookup Zone alan adlarının oluşturulması (`2.png`).
3. Alan adları içerisinde `A`, `MX`, `NS`, `CNAME`, `SRV` ve `PTR` kayıtlarının tanımı (`3.png`).

<p align="center">
  <img src="screenshots/C/1.png" width="30%" alt="DNS Yapilandirma" />
  <img src="screenshots/C/2.png" width="30%" alt="Alan Adlari" />
  <img src="screenshots/C/3.png" width="30%" alt="DNS Kayitlari" />
</p>

---

### D. Çoklu Ethernet Yapılandırması, NAT ve Güvenlik Duvarı
1. Birinci Ethernet kartı IP yapılandırması (`172.16.10.1/22`) (`1.png`).
2. İkinci Ethernet kartı IP yapılandırması (`172.16.20.1/22`) (`2.png`).
3. Routing and Remote Access üzerinden NAT kurulum başlangıcı (`3.png`).
4. NAT iç (Private) ve dış (Public) ağ kartı seçimleri (`4.png`).
5. NAT yönlendirmesinin tamamlanmış arayüz görüntüsü (`5.png`).

<p align="center">
  <img src="screenshots/D/1.png" width="18%" alt="Ethernet 1" />
  <img src="screenshots/D/2.png" width="18%" alt="Ethernet 2" />
  <img src="screenshots/D/3.png" width="18%" alt="NAT Baslangic" />
  <img src="screenshots/D/4.png" width="18%" alt="NAT Ag Secimi" />
  <img src="screenshots/D/5.png" width="18%" alt="NAT Tamamlandi" />
</p>

---

### E. Grup İlkeleri (Group Policy - GPO) ve İstemci Kısıtlamaları
1. Group Policy Management konsolu kurulumu (`1.png`).
2. GPO ilke ayarlarının düzenlenmesi (`2.png`).
3. Organizasyonel Birimlere (StajyerOU / YoneticiOU) ilkelerin bağlanması (`3.png`).
4. Kullanıcı hesabı oluşturma ekranı (`4.png`).
5. Kullanıcının ilgili gruba atanması (`5.png`).
6. Etki alanındaki tüm kullanıcıların genel görünümü (`6.png`).
7. İstemci işletim sisteminde Domain hesabı ile oturum açılması (`7.png`).
8. `StajUser1` kullanıcısında Görev Yöneticisi ve Regedit erişim kısıtlamalarının doğrulanması (`8.png`).

<p align="center">
  <img src="screenshots/E/1.png" width="23%" alt="GPO Kurulum" />
  <img src="screenshots/E/2.png" width="23%" alt="GPO Ayari" />
  <img src="screenshots/E/3.png" width="23%" alt="Grup Ilke Baglantisi" />
  <img src="screenshots/E/4.png" width="23%" alt="Kullanici Olusturma" />
</p>
<p align="center">
  <img src="screenshots/E/5.png" width="23%" alt="Gruba Ekleme" />
  <img src="screenshots/E/6.png" width="23%" alt="Kullanici Listesi" />
  <img src="screenshots/E/7.png" width="23%" alt="Domain Oturumu" />
  <img src="screenshots/E/8.png" width="23%" alt="Kisitlama Testi" />
</p>

---

### F. Kullanıcı ve Güvenlik Grubu Yönetimi
1. Kullanıcı tanımlama sihirbazı (`1.png`).
2. 4 adet kullanıcının oluşturulduğunu gösteren liste (`2.png`).
3. İlgili güvenlik gruplarının listesi (`3.png`).
4. Gruplara ait üyelik detayları (`4.png`).

<p align="center">
  <img src="screenshots/F/1.png" width="23%" alt="Kullanici Ekleme" />
  <img src="screenshots/F/2.png" width="23%" alt="Kullanicilar" />
  <img src="screenshots/F/3.png" width="23%" alt="Gruplar" />
  <img src="screenshots/F/4.png" width="23%" alt="Grup Uyeleri" />
</p>

---

### G. DHCP Sunucu Yapılandırması ve IP Kiralama
1. DHCP Rolünün yetkilendirilmiş (authorized) genel görünümü (`1.png`).
2. Tanımlanan 1. IP Havuzu (Pool) yapılandırması (`2.png`).
3. Tanımlanan 2. IP Havuzu (Pool) yapılandırması (`3.png`).
4. İstemci makineye 3. havuz üzerinden başarıyla IP adresi atanması ve kira kaydı (`4 (3. pooldan ip adresi kiraladım).png`).

<p align="center">
  <img src="screenshots/G/1.png" width="23%" alt="DHCP Kurulum" />
  <img src="screenshots/G/2.png" width="23%" alt="Pool 1" />
  <img src="screenshots/G/3.png" width="23%" alt="Pool 2" />
  <img src="screenshots/G/4%20(3.%20pooldan%20ip%20adresi%20kiralad%C4%B1m).png" width="23%" alt="IP Kiralama" />
</p>

---

### H. FTP Sunucu ve Yetkilendirme Seviyeleri
1. IIS üzerinden FTP sitesi kurulum ve bağlama ekranı (`1.png`).
2. Farklı kullanıcı seviyelerine göre (Okuma, Okuma-Yazma, Tam Yönetim) yetkilendirme doğrulaması (`2.png`).

<p align="center">
  <img src="screenshots/H/1.png" width="45%" alt="FTP Kurulum" />
  <img src="screenshots/H/2.png" width="45%" alt="FTP Haklari" />
</p>

---

### J. Web Sunucu (IIS) ve Çoklu Site Yayını
1. IIS Web Sunucu rolünün aktif durumu (`1.png`).
2. Her iki alan adı için oluşturulan web sitelerinin listesi (`2.png`).
3. Birinci alan adının istemci tarayıcısında yayını (`3.png`).
4. İkinci alan adının istemci tarayıcısında yayını (`4.png`).

<p align="center">
  <img src="screenshots/J/1.png" width="23%" alt="IIS Kurulum" />
  <img src="screenshots/J/2.png" width="23%" alt="Web Siteleri" />
  <img src="screenshots/J/3.png" width="23%" alt="Site 1 Browser" />
  <img src="screenshots/J/4.png" width="23%" alt="Site 2 Browser" />
</p>

---

### K. E-Posta Sunucusu (Mail Server)
1. Mail sunucu servisinin yapılandırılmış arayüzü (`1.png`).
2. Kullanıcılar için mail hesabı açılış ekranı (`2.png`).
3. İstemci üzerinde gelen kutusuna başarılı e-posta iletiminin doğrulanması (`3.png`).

<p align="center">
  <img src="screenshots/K/1.png" width="30%" alt="Mail Sunucu" />
  <img src="screenshots/K/2.png" width="30%" alt="Hesap Olusturma" />
  <img src="screenshots/K/3.png" width="30%" alt="Gelen Kutusu Dogrulama" />
</p>