# ReallifeRPG APIv1

## Categories

- [Mod](#mod)
- [Server](#server)
- [Player](#player)
- [Online Banking](#online-banking)
- [Licenses](#licenses)
- [Companies](#companies)
- [Market](#market)
- [Items & itemshops](#items-itemshops)
- [Vehicles & vehicleshops](#vehicles-vehicleshops)
- [Community Building System](#community-building-system)
- [Houses & buildings](#houses-buildings)
- [Fuelstations](#fuelstations)
- [Twitch](#twitch)
- [Other](#other)

---

## Mod

#### Notification

```
GET /v1/notification
Reponse 200 (application/json)
```

#### Changelogs

```
GET /v1/changelog
Response 200 (application/json)
```

#### Mods

```
GET /v1/mods
Reponse 200 (application/json)
```

---

## Server

#### Teamspeak

```
GET /v1/teamspeaks
Response 200 (application/json)
```

#### Servers

```
GET /v1/servers
Reponse 200 (application/json)
```

#### Server logs

```
GET /v1/servers/log
Response 200 (application/json)
```

#### Specific servers log

```
GET /v1/server/log/{server_id}
Response 200 (application/json)
```

---

## Player

#### Player

```
GET /v1/player/{secret}
Response 200 (application/json)
```

#### Player vehicles

```
GET /v1/player/{secret}/vehicles
Response 200 (application/json)
```

#### Player validate

```
GET /v1/player/validate/{secret}
Response 200 (application/json)
```

---

## Online Banking

### Transactions

**Header**

| Header       | Value                                   |
| ------------ | --------------------------------------- |
| `set-cookie` | `XSRF-TOKEN={XSRF-TOKEN}`               |
| `set-cookie` | `laravel_session={LARAVEL_SESSION_KEY}` |

```
POST info.realliferpg.de/banking/{IBAN}/data
Response 200 (application/json)
```

### Transfer money

**Header**

| Header       | Value                                   |
| ------------ | --------------------------------------- |
| `set-cookie` | `XSRF-TOKEN={XSRF-TOKEN}`               |
| `set-cookie` | `laravel_session={LARAVEL_SESSION_KEY}` |

**Body**

| Key      | Value              |
| -------- | ------------------ |
| `_token` | `{TRANSFER_TOKEN}` |
| `type`   | `init_transaction` |
| `amount` | `balance`          |
| `iban`   | `{RECEIVER_IBAN}`  |
| `info`   | `{INFO}`           |

```
POST info.realliferpg.de/banking/{IBAN}
Response 200 (application/html)
```

---

## Licenses

#### Licenses

```
GET /v1/info/licenses
Response 200 (application/json)
```

---

## Companies

#### Company shops

```
GET /v1/company_shops
Response 200 (application/json)
```

---

## Market

#### Serverwide market

```
GET /v1/market_all
Response 200 (application/json)
```

#### Market

```
GET /v1/market/{server_id}
Response 200 (application/json)
```

#### Market logs

```
GET /v1/market_logs/{server_id}/{itemname}/{backlog}
Response 200 (application/json)
```

---

## Items & itemshops

#### Items

```
GET /v1/info/items
Response 200 (application/json)
```

#### Item shoptypes

```
GET /v1/info/items_shoptypes
Response 200 (application/json)
```

#### Item shops

```
GET /v1/info/items/{shoptype}
Response 200 (application/json)
```

---

## Vehicles & vehicleshops

#### Vehicles

```
GET /v1/info/vehicles
Response 200 (application/json)
```

#### Vehicle shoptypes

```
GET /v1/info/vehicles_shoptypes
Response 200 (application/json)
```

#### Vehicle shop

```
GET /v1/info/vehicles/{shoptype}
Response 200 (application/json)
```

---

## Community Building System

#### CBS

```
GET /v1/cbs
Response 200 (application/json)
```

---

## Houses & buildings

#### Housetypes

```
GET /v1/info/houses
Response 200 (application/json)
```

#### Buildingtypes

```
GET /v1/info/buildings
Response 200 (application/json)
```

---

## Fuelstations

#### Fuelstations

```
GET /v1/fuelstations
Response 200 (application/json)
```

#### Specific fuelstation

```
GET /v1/server/fuelstations/{id}
Response 200 (application/json)
```

---

## Twitch

#### Twitch

```
GET /v1/twitch
Response 200 (application/json)
```

#### Twitch with limit

```
GET /v1/twitch/{limit}
Response 200 (application/json)
```

---

## Other

#### Map markers

```
GET /v1/map_markers
Response 200 (application/json)
```
