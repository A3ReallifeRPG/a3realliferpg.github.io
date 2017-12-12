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

(Not completed)