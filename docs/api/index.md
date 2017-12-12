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

(Not completed)