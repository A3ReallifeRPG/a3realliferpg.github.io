# ReallifeRPG APIv1

## Categories

1. [Mod](#mod)
2. [Server](#server)
3. [Player](#player)
4. [Licenses](#licenses)
5. [Companies](#companies)
6. [Market](#market)
7. [Items & itemshops](#items-itemshops)
8. [Vehicles & vehicleshops](#vehicles-vehicleshops)
9. [Community Building System](#community-building-system)
10. [Houses & buildings](#houses-buildings)
11. [Fuelstations](#fuelstations)
12. [Twitch](#twitch)
13. [Other](#other)

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
GET /v1/market_logs/{server_id}/{itemname}/{backlog_count}
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
