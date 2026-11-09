# Self-Hosted Messenger (VoceChat)

Schlanker, selbst gehosteter Messenger auf Basis von **VoceChat** (in Rust geschrieben, typischerweise unter 25 MB RAM-Verbrauch) mit nativer App-Unterstützung für iOS & Android, integriertem Web-Client und einfacher In-App-Registrierung.

---

## Features

- **Einfache Registrierung:** Benutzer können sich direkt in der Smartphone-App registrieren (ohne kryptografische Schlüssel oder manuelle Freischaltungen).
- **Mobile Apps:** Offizielle Apps im [Apple App Store](https://apps.apple.com/app/vocechat/id1631779678) und [Google Play Store](https://play.google.com/store/apps/details?id=com.privoce.vocechat_flutter).
- **Eingebauter Web-Client:** Direkt im Browser unter `https://chat.bergerdd.de` nutzbar.
- **Ressourcenschonend:** Minimaler Speicher- und CPU-Bedarf (< 25 MB RAM).
- **Private Kanäle:** Trennung von Gruppen (z. B. Familie, Freunde, Projekte) über geschützte, private Kanäle.
- **Vollständige Datenkontrolle:** Alle Daten liegen lokal im Verzeichnis `./data`.

---

## Schnellstart

### 1. Docker-Netzwerk anlegen
Falls das externe Netzwerk `edge` noch nicht existiert:

```bash
docker network create edge
```

### 2. Server starten

```bash
docker compose up -d
```

---

## Reverse Proxy (Caddy)

Beispiel-Konfiguration für Caddy (`/etc/caddy/Caddyfile`):

```caddy
chat.bergerdd.de {
    reverse_proxy messenger_vocechat:3000 {
        header_up X-Forwarded-Proto https
    }
}
```

---

## Ersteinrichtung

1. Rufe **`https://chat.bergerdd.de`** im Browser auf.
2. Der Einrichtungs-Assistent führt dich durch die Erstellung des Administrator-Kontos (Name, E-Mail, Passwort).
3. In den Server-Einstellungen (Zahnrad-Icon) unter **Registration** festlegen, ob sich jeder frei registrieren darf oder Einladungen erforderlich sind.

### Smartphone-Verbindung
1. App **VoceChat** im App Store / Play Store installieren.
2. Server-Adresse eingeben: `chat.bergerdd.de`
3. Auf **„Sign Up“ (Registrieren)** oder **„Log In“** tippen.

---

## Lizenz

Dieses Deployment-Setup steht unter der [MIT License](LICENSE). VoceChat selbst unterliegt der jeweiligen Lizenz des [Privoce VoceChat Projekts](https://github.com/Privoce/vocechat-server).
