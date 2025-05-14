# Plattform Docker Setup
Dieses Repository dient dem starten der [Plattform](https://github.com/aschallenberg-platform/platform).

Die Plattform verwendet Docker und Docker Compose, um die Plattform in Form einer Spring Boot Anwendung zusammen mit einer MySQL-Datenbank in Containern zu starten. In dieser Anleitung wird beschrieben, wie das Projekt lokal auf einem eigenen Computer zum Laufen gebracht wird.

## 1) Repository herunterladen
Das Repository kann als zip auf der [GitHub-Seite des Projekts](https://github.com/aschallenberg-platform/platform-docker-setup) heruntergeladen werden. Dann muss die zip in einem gewünschten Verzeichnis entpackt werden.

Alternativ kann man das Projekt von GitHub klonen:
```bash
git clone https://github.com/aschallenberg-platform/platform-docker-setup.git
cd platform
```

## 2) Konfigurieren
Zur Konfiguration der Plattform steht die .env Datei bereit.

### Datenbank konfigurieren
Im ersten Abschnitt der Datei sind Konfigurationsmöglichkeiten der Datenbank mit Standardwerten.

| Variablenname                       | Standardwert                                                 | Beschreibung                                                                               |
|-------------------------------------|--------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| `MYSQL_USER`                        | `platform_user`                                              | Benutzername des MySQL-Benutzers, über den die Plattform auf die Datenbank zugreift.       |
| `MYSQL_PASSWORD`                    | `password`                                                   | Passwort des MySQL-Benutzers, über den die Plattform auf die Datenbank zugreift.           |
| `MYSQL_DATABASE`                    | `platform_db`                                                | Name der MySQL-Datenbank, in der die Plattform ihre Daten ablegt                           |
| `MYSQL_PORT`                        | `3307`                                                       | Port, über den MySQL angesprochen wird                                                     |
| `MYSQL_CONTAINER_NAME`              | `platform-db`                                                | Name des MySQL-Containers (in Docker)                                                      |
| `MYSQL_ROOT_PASSWORD`               | `rootpass`                                                   | Passwort für den MySQL-Root-Benutzer (relevant für manuelle Eingriffe in die Datenbank)    |


### E-Mail konfigurieren.
Es muss eine E-Mail-Adresse konfiguriert werden, über die die Plattform Confirmation-E-Mails wie Verfikationslinks und Links zum Ändern des Passwords für die Nutzer versendet wird.
Hierbei ist zu beachten, dass manche E-Mail-Dienste (z.B. Gmail) statt des Passworts einen speziellen API-Token braucht, der über Gmail erstellt wird.

| Variablenname                      | Standardwert                                                 | Beschreibung                                                                              |
|------------------------------------|--------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| `SPRING_MAIL_SENDING_HOST`         | *(leer)*                                                     | Hostname des SMTP-Servers                                                                 |
| `SPRING_MAIL_SENDING_PORT`         | *(leer)*                                                     | Port des SMTP-Servers                                                                     |
| `SPRING_MAIL_USERNAME`             | *(leer)*                                                     | Benutzername für SMTP-Authentifizierung (idR. Postfach-Benutzername oder E-Mail-Adresse)  |
| `SPRING_MAIL_PASSWORD`             | *(leer)*                                                     | Passwort für SMTP-Authentifizierung (idR. Postfach-Passwort oder API-Token)               |
| `SPRING_MAIL_SENDING_PROTOCOL`     | `smtps`                                                      | Verwendetes Protokoll zum Senden von E-Mails (z. B. `smtp`, `smtps`)                      |
| `SPRING_MAIL_SMTP_AUTH`            | `true`                                                       | SMTP-Authentifizierung erforderlich (`true` oder `false`)                                 |
| `SPRING_MAIL_SMTP_STARTTLS`        | `true`                                                       | TLS-Verschlüsselung via STARTTLS aktivieren (`true` oder `false`)                         |
| `SPRING_MAIL_SMTP_SSL`             | `true`                                                       | SSL-Verschlüsselung aktivieren (`true` oder `false`)                                      |

### Plattform-Einstellungen treffen
Des Weiteren müssen Plattform-spezifische Einstellungen getroffen werden.

| Variablenname                      | Standardwert                                                       | Beschreibung                                                                                           |
|------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| `PLATFORM_PORT`                    | `8080`                                                             | Port, auf dem die Plattform erreichbar ist                                                             |
| `PLATFORM_SSL`                     | `true`                                                             | Ob SSL (HTTPS) für die Plattform verwendet werden soll                                                 |
| `PLATFORM_USERLOCK`                | `false`                                                            | Ob Nutzer standardmäßig gesperrt sein sollen und erst von Administratoren freigeschaltet werden sollen |
| `PLATFORM_SUPERUSER_USERNAME`      | *(leer)*                                                           | Benutzername des Superusers                                                                            |
| `PLATFORM_SUPERUSER_EMAIL`         | *(leer)*                                                           | E-Mail-Adresse des Superusers                                                                          |
| `PLATFORM_SUPERUSER_PASSWORD`      | *(leer)*                                                           | Passwort für den Superuser                                                                             |
| `PLATFORM_LINK_GAME_LIBRARY`       | `https://github.com/aschallenberg-platform/platform-game-library`  | Git-Link zur Spielebibliothek                                                                          |
| `PLATFORM_LINK_GAME_TEMPLATE`      | `https://github.com/aschallenberg-platform/platform-game-template` | Git-Link zur Spielvorlage                                                                              |
| `PLATFORM_LINK_BOT_LIBRARY`        | `https://github.com/aschallenberg-platform/platform-bot-library`   | Git-Link zur Bot-Bibliothek                                                                            |
| `PLATFORM_LINK_BOT_TEMPLATE`       | `https://github.com/aschallenberg-platform/platform-bot-template`  | Git-Link zur Bot-Vorlage                                                                               |


## Voraussetzungen für Docker

Bevor du das Projekt mit Docker-Compose startest, stelle sicher, dass du die folgende Software installiert hast:

1. **Docker**: [Download und Installation von Docker](https://www.docker.com/get-started)
2. **Docker Compose**: Docker Compose ist in Docker Desktop bereits integriert. Falls du Docker Compose separat installieren musst, findest du die Anleitung [hier](https://docs.docker.com/compose/install/).

Stelle sicher, dass Docker und Docker Compose ordnungsgemäß installiert und betriebsbereit sind. Du kannst dies überprüfen, indem du die folgenden Befehle in deiner Kommandozeile ausführst:

```bash
docker --version
docker-compose --version
```

## Docker starten

### Repository herunterladen



### Docker-Compose Setup

#### 1. Docker-Container starten

Das Projekt verwendet **Docker Compose**, um sowohl den MySQL-Container als auch den Spring Boot-Container zu starten und zu verbinden. Docker Compose wird alle erforderlichen Dienste basierend auf der `compose.yaml`-Datei konfigurieren und starten.

Navigiere im Terminal in das Verzeichnis des Projekts (falls du es noch nicht getan hast) und führe folgenden Befehl aus:

```bash
docker-compose up -d
```

##### Erklärung der Optionen:

- `up`: Startet die Container.
- `-d`: Führt die Container im Hintergrund (detached mode) aus.

Docker Compose wird nun die folgenden Schritte ausführen:
1. Das MySQL-Image wird heruntergeladen und ein Container wird gestartet.
2. Der Spring Boot-Container wird heruntergeladen und ein Container wird gestartet.
3. Die beiden Container werden miteinander verbunden, sodass die Spring Boot-Anwendung auf die MySQL-Datenbank zugreifen kann.

#### 2. Container prüfen

Um zu überprüfen, ob die Container erfolgreich gestartet wurden, kannst du den folgenden Befehl verwenden:

```bash
docker ps
```

Dieser Befehl zeigt dir alle laufenden Docker-Container. Du solltest die beiden Container sehen: `platform-db` und `platform-app`.

#### 3. Logs anzeigen

Um die Logs eines Containers zu prüfen und etwaige Fehler zu debuggen, verwende den folgenden Befehl:

```bash
docker logs platform-app
```

Dies gibt dir eine Ausgabe der Spring Boot-Anwendung, einschließlich aller Fehler oder Startinformationen.

## Docker stoppen

Wenn du die Container stoppen möchtest, kannst du den folgenden Befehl ausführen:

```bash
docker-compose down
```

Dieser Befehl stoppt und entfernt alle Container, Netzwerke und Volumes, die durch Docker Compose erstellt wurden.
