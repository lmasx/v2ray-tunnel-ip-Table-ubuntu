# v2ray-tunnel-ip-Table-ubuntu
در این ریپو با آی پی تیبل یک تونل آی پی آی پی ورژن چهار درست میکنیم و به سرور خارجی از طریق تونل سرور داخلی وصل میشیم




## Deployment

To deploy this solution run this in order

1-اوله به سرور خودتون با هر کلاینت که میتونید اس اس اچ بزنید بعدش به ترتیب دستور ها رو ااجرا کنید
```bash
  sudo apt-get update -y && sudo apt-get upgrade -y
```

2-بعدی با این دستور آی پی تیبل رو نصب میکنیم.

```bash
sudo apt-get install iptables
```
3-بررسی صحت نصب آی پی تیبل.


```bash
sudo iptables -L -v
```
4-بعدش یک فایل با این مسیر و با نام cr.local بسازید.برای ساخت این فایل من از ادیتور نانو استفاده کردم.


```bash
sudo nano /etc/rc.local
```


5 این متن رو کپی کنید و در یک ادیتور داخل لوکال خودتون بازش کنید و به این صورت ادیتش کنید.به جای "local-server-ip" آی پی سرور داخلی تون رو قرار بدین و به جای "forign-server-ip" آی پی سرور خارجی رو قرار بدید.بدون کوتیشن بزارید آی پی خالی.


```bash
#! /bin/bash
sysctl net.ipv4.ip_forward=1
iptables -t nat -A PREROUTING -p tcp --dport 22 -j DNAT --to-destination "local-server-ip"
iptables -t nat -A PREROUTING -j DNAT --to-destination "forign-server-ip"
iptables -t nat -A POSTROUTING -j MASQUERADE
exit 0
```
