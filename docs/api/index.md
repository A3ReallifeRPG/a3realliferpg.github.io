# ReallifeRPG APIv1

### Notification

````html
GET /v1/notification

Reponse 200 (application/json)
	Object
      - Notification (String)
      - Active (Bool)
      - requested_at (Unix-Timestamp)
````

### Mods

```html
GET /v1/mods

Reponse 200 (application/json)
	Array (Mod)
      - Id (Int) 
      - Name (String)
      - appId (Int)
      - DownloadUrl (String)
      - Torrent (String)
      - IsActive (Int)
      - Description (String)
      - ImageUrl (String)
      - HasGameFiles (Int)
    - requested_at (Unix-Timestamp)
```

### Servers

```html
GET /v1/servers

Reponse 200 (application/json)
	Array (Server)
      - Id (Int) 
      - ModId (Int)
      - online (Int)
      - appId (Int)
      - Servername (String)
      - IpAdresss (String)
      - Port (Int)
      - ServerPassword (String)
      - Gamemode (Int)
      - StartParameters (String)
      - Slots (Int)
      - Playercount (Int)
      - Civilians (Int)
      - Medics (Int)
      - Cops (Int)
      - Adac (int)
      - Players 
		Array (Player)
      - Side
		Array (Side)
		 Array (Civ)
		 Array (Medic)
		 Array (Cop)
		 Array (RAC)
      - updated_at (Timestamp)
    - requested_at (Unix-Timestamp)
```

## More Methods

### Servers/Log

````
GET /v1/servers/log
````

### Server/Log

````
GET /v1/server/log/{id}
````

### Server/Fuelstation

`````
GET /v1/server/fuelstations/{id}
`````

### Changelog	

````
GET /v1/changelog
````

### Teamspeaks

````
GET /v1/teamspeaks
````

### Fuelstations

````
GET /v1/fuelstations
````

### Player

````
GET /v1/player/{secret}
````

### Player/Vehicles

````
GET /v1/player/{secret}/vehicles
````

### Player/Validate

````
GET /v1/player/validate/{secret}
````

### Twitch

````
GET /v1/twitch
````

### Market

````
GET /v1/market/{server_id}
````

### Market_logs

````
GET /v1/market_logs/{server_id}/{itemname}/{backlog}
````

### Info-Items

````
GET /v1/info/items
````

### Info-Items Shop

````
GET /v1/info/items/{shop}
````

### Info-Items Shoptypes

````
GET /v1/info/items_shoptypes
````

### Info-Vehicles

````
GET /v1/info/vehicles
````

### Info-Vehicles Shop

````
GET /v1/info/vehicles/{shop}
````

### Info-Vehicles Shoptypes

````
GET /v1/info/vehicles_shoptypes
````

### Info-Licenses Shoptypes

````
GET /v1/info/licenses
````

### Info-Houseshoptypes

````
GET /v1/info/houses
````

### Info-Buildings Shoptypes

````
GET /v1/info/buildings
````

### Map Markers

````
GET /v1/map_markers
````