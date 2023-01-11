```C
/* Writing responses in C so it is easier to read/understand to developers on types and lengths */
struct uniqueViewMapping {
  /* Primary IDs */
  uint32_t serverId;
  uint32_t userId;
  
  /* Date */
  uint32_t unixTS;                                // UNIX Timestamp
};

struct userCountStatsMapping {
  /* Primary IDs */
  uint32_t serverId;
  uint32_t unixTs;                                // UNIX Timestamp
  
  /* Stats */
  uint32_t users;
  uint32_t usersMax;
  uint32_t bots;
};
  
struct usersResponse = {
  char name[64];
  char auth[256];
  uint32_t score;
};

struct tagsResponse = {
  char name[64];
};

struct serverResponse = {
  /* Primary & Unique IDs */
  uint64_t id;
  char url[256];
  
  /* User Counts & List */
  uint32_t users;
  uint32_t usersMax;
  struct userResponse users[];
  
  /* General Info */
  char banner[256];                               // e.g. /images/servers/banners/{id}.png
  char name[256];
  char mapName[64];
  char shortDescription[512];
  struct tagsResponse tags[32];
  
  /* One To Many Relations */
  uint32_t platformId;                            // Platform or Game ID (e.g. Discord or Minecraft)
  uint32_t communityId;                           // Community ID from Gamecom
  
  /* Mappings */
  struct uniqueViewMapping uniqueViews[];
  struct userCountStatsMapping userCountStats[];
  
  /* Statistics */
  uint32_t rating;                                // Default 1
  uint32_t views;                                 // Default 0
  uint32_t uniqueViews;                           // Default 0
 
  /* Location */
  float lat;
  float lon;
  char city[64];
  char state[64];
  char country[32];
  char countryCode[2];
  
  /* HTML5/Web Support */
  bool hasHTML5File;                            // loader file => /servers/{id}/loader.js
  char HTML5Url[256];                           // For IFrame (e.g. example.com/gametest/index.html?ip={ip}&port={port})
};
```

# API Info
## `api/servers`
### GET
#### Query
* **id** - The ID of the server.
* **url** - The URL of the server (e.g. `bestservers.io/view/{url}`).
* **name** - Match (partial) server name.
* **map** - Match (partial) server map.
* **tags** - Match (partial) server tags.
* **limit** - Total amount of entries to retrieve.
#### Response
```C
return struct serverResponse{...};
```

## `api/servers/stats`
### GET
#### Query
* **id** - The ID of the server.
* **url** - The URL of the server (e.g. `bestservers.io/view/{url}`).
* **startdate** - UNIX timestamp of start date.
* **enddate** - UNIX timestamp of end date.
* **limit** - Total amount of entries to retrieve.
#### Response
```C
return struct userCountStatsMapping[]{...};
```
