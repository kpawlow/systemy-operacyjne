# Konfiguracja Samby na Ubuntu — dostęp użytkownika `stefan` do `/home/stefan`

## 🔧 1. Instalacja Samby

```bash
sudo apt update
sudo apt install samba -y
```

---

## 👤 2. Utworzenie użytkownika (jeśli jeszcze nie istnieje)

```bash
sudo adduser stefan
```

---

## 🔐 3. Ustawienie hasła do Samby

> UWAGA: To jest osobne hasło niż systemowe.

```bash
sudo smbpasswd -a stefan
```

### Aktywacja konta

```bash
sudo smbpasswd -e stefan
```

---

## 📁 4. Ustawienie uprawnień do katalogu domowego

```bash
sudo chown stefan:stefan /home/stefan
sudo chmod 700 /home/stefan
```

---

## ⚙️ 5. Edycja konfiguracji Samby

### Otwórz plik konfiguracyjny

```bash
sudo nano /etc/samba/smb.conf
```

### Na końcu pliku dodaj:

```ini
[stefan]
   comment = Folder domowy Stefana
   path = /home/stefan
   valid users = stefan
   browseable = yes
   read only = no
   writable = yes
   create mask = 0700
   directory mask = 0700
```

---

## 🔄 6. Restart usługi Samby

```bash
sudo systemctl restart smbd
```

---

## 🌐 7. Sprawdzenie działania

### Sprawdzenie adresu IP serwera

```bash
ip a
```

### Połączenie z Windows

W eksploratorze plików wpisz:

```text
\\IP_SERWERA\stefan
```

### Przykład

```text
\\192.168.1.10\stefan
```
