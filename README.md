# AutoXRay & AWG 2.0
 
Автоматическая установка и настройка VPN-сервера на Debian с использованием:
- **Xray** (VLESS + REALITY, Shadowsocks)
- **AmneziaWG 2.0** (userspace, с обфускацией)
- **UFW** (firewall)
## Требования
 
- Debian 10+
- root доступ (sudo)
- Минимум 512 MB RAM
- Открытые порты: 22 (SSH), 443, 8443, 2040, 51820
## Установка
 
```bash
sudo bash setup_vpn.sh
```
 
Скрипт автоматически:
1. Обновит систему и установит необходимые пакеты
2. Установит и настроит Xray с VLESS+REALITY на портах 443/8443
3. Установит Shadowsocks на порту 2040 (резервной протокол)
4. Собери и настроит AmneziaWG 2.0 на порту 51820
5. Настроит UFW firewall
6. Выведет готовые конфиги для клиентов
## Конфиги клиентов
 
После установки скрипт выведет:
- **VLESS+REALITY (443)** — основной протокол, маскируется под обычный HTTPS
- **VLESS+REALITY (8443)** — резервной (второй SNI)
- **Shadowsocks** — запасной вариант
- **AmneziaWG** — конфиг сохранён в `/etc/amnezia/amneziawg/client_awg.conf`
### Копирование конфигов
 
```bash
# VLESS ссылки копируй в приложение (Happ, v2rayNG, Nekoray и т.д.)
# AmneziaWG конфиг:
cat /etc/amnezia/amneziawg/client_awg.conf
```
 
## Приложения клиентов
 
- **iOS**: Happ, v2rayTun, FoXray
- **Android**: Happ, v2rayTun, v2rayNG
- **Windows**: Happ, Nekoray, Hiddify, winLoadXRAY
- **macOS**: Happ, Nekoray
## Файлы конфигов
 
```
/usr/local/etc/xray/config.json        # Xray конфиг
/etc/amnezia/amneziawg/awg0.conf       # AmneziaWG server
/etc/amnezia/amneziawg/client_awg.conf # AmneziaWG client
```
 
## Управление сервисами
 
```bash
# Xray
systemctl status xray
systemctl restart xray
 
# AmneziaWG
systemctl status awg-quick@awg0
systemctl restart awg-quick@awg0
 
# Firewall
ufw status
```
 
## Примечания
 
- Каждый запуск скрипта генерирует новые ключи и параметры обфускации
- AmneziaWG требует клиент версии ≥ 4.8.12.7 (поддержка AWG 2.0)
- Для добавления новых клиентов в AmneziaWG отредактируй `/etc/amnezia/amneziawg/awg0.conf` и добавь новые `[Peer]` секции
- SSH открыт на порту 22 (не закрывается firewall'ом)
## Лицензия
 
MIT
 
