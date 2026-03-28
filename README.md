# Wigell Dashboard

Wigell Dashboard är en centraliserad övervakningspanel baserad på **Spring Boot Admin**. Den ger en visuell översikt över status, hälsa och mätvärden för samtliga mikrotjänster i Wigell-ekosystemet.

## 🛠 Teknisk Stack
* **Java:** 24
* **Ramverk:** Spring Boot 3.5.4
* **Övervakning:** Spring Boot Admin Server 3.2.3

## 🚀 Kom igång
Dashboarden körs som standard på port **8081**.

1.  Kör applikationen:
    ```bash
    mvn spring-boot:run
    ```
2.  Öppna gränssnittet i din webbläsare:
    `http://localhost:8081`

---

## 📘 Integrationsguide

För att en mikrotjänst ska synas i denna dashboard krävs att den konfigureras som en klient.

### 1. Lägg till beroende
I klienttjänstens `pom.xml`, lägg till följande beroende:
```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>3.2.3</version>
</dependency>
```

### 2. Konfigurera klienten
I klienttjänstens `application.yml`, ange adressen till dashboarden och exponera nödvändiga endpoints via Actuator:
```yaml
spring:
  boot:
    admin:
      client:
        url: http://localhost:8081 # Adressen till denna dashboard

management:
  endpoints:
    web:
      exposure:
        include: "*" # Exponerar all data för övervakning (hälsa, loggar, metrics)
  endpoint:
    health:
      show-details: always
```

### 3. Verifiering
När klienttjänsten startar kommer den automatiskt att registrera sig. Statusen ändras till **UP** i dashboard-gränssnittet så snart anslutningen är etablerad.

---
*Utvecklad av Grupp C*
