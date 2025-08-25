# 01 — Wireshark: ICMP, DNS, HTTP (Wi-Fi)

**Tarih:** 2025-08-25  
**Amaç:** Temel trafiği yakalayıp üç protokolün paketlerini gözle görmek ve ölçülebilir not çıkarmak.

## Ortam
- Windows + Wireshark 4.x, Wi-Fi adaptörü
- Trafik üretimi: `ping 1.1.1.1`, `nslookup example.com`, HTTP GET/HEAD
- Yakalama dosyası: `sample.pcapng`
- Ekran görüntüleri: `screenshots/icmp.png`, `dns.png`, `http.png`

## Ben nasıl yaptım?
Wireshark’ta Wi-Fi’yi seçip kaydı başlattım. CMD’de önce 1.1.1.1’e ping attım,
sonra `example.com` için nslookup yaptım, en sonda da HTTP başlıklarını görmek için
`curl -I` kullandım. Wireshark’ta sırayla `icmp`, `dns`, `http` filtrelerini uygulayıp
ekran görüntülerini aldım ve kaydı `sample.pcapng` olarak kaydettim.

## Gördüklerim (kısa, sayılı)
- **ICMP:** Echo request/reply çiftleri net. Request’lerde başlangıç TTL **128**; yanıtta TTL **47** civarı → yaklaşık atlama sayısını gösteriyor.  
- **DNS:** `1.1.1.1`’e `example.com` için **A/AAAA** sorguları görünüyor; yanıtlar Cloudflare’dan.  
- **HTTP:** `HTTP/1.1 200 OK` ve `GET` satırları açıkça seçiliyor.  
- Ek: Yakalamada **“Time-to-live exceeded” (ICMP Type 11)** paketleri de var; bu testin parçası değil, muhtemelen başka uygulamadan kalan trafik.

## Dosyalar
