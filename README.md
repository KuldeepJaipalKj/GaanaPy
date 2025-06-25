# 🎶 GaanaPy

GaanaPy is an unofficial JSON API for [`Gaana`](https://gaana.com), an Indian music streaming service.

## 📖 Table Of Contents

* [`🎧 Features`](#-features)
* [`👨‍🔧 Usage`](#-usage)
* [`💻 Local Development`](#-local-development)
* [`🏥 Contributing`](#-contributing)
* [`🐳 Docker Deployment`](#-docker-deployment)

## 🎧 **Features**

The API provides structured JSON responses for:

- **Tracks** – Search and retrieve details for specific tracks.
- **Albums** – Search and fetch album information.
- **Artists** – Search, view artist details, and find similar artists.
- **Playlists** – Retrieve playlist details (search not supported).
- **Top Charts** – Curated playlists across all languages.
- **Trending Tracks** – Per-language trends.
- **New Releases** – Latest music by language.

### Example Track Response
```json
[
  {
    "seokey": "tyler-herro",
    "album_seokey": "tyler-herro",
    "track_id": "32408795",
    "title": "Tyler Herro",
    "artists": "Jack Harlow",
    "artist_seokeys": "jack-harlow",
    "artist_ids": "817522",
    "artist_image": "https://a10.gaanacdn.com/gn_img/artists/XYybzrb2gz/Yybzn4Bgb2/size_m_1607927137.webp",
    "album": "Tyler Herro",
    "album_id": "3487503",
    "duration": "156",
    "popularity": "18444~18444",
    "genres": "Hip Hop",
    "is_explicit": true,
    "language": "English",
    "label": "Generation Now/Atlantic",
    "release_date": "2020-10-22",
    "play_count": "<100K",
    "favorite_count": 231,
    "song_url": "https://gaana.com/song/tyler-herro",
    "album_url": "https://gaana.com/album/tyler-herro",
    "images": {
      "urls": {
        "large_artwork": "https://a10.gaanacdn.com/gn_img/albums/4Z9bqo3yQn/Z9bq2AG1Ky/size_l.jpg",
        "medium_artwork": "https://a10.gaanacdn.com/gn_img/albums/4Z9bqo3yQn/Z9bq2AG1Ky/size_m.jpg",
        "small_artwork": "https://a10.gaanacdn.com/gn_img/albums/4Z9bqo3yQn/Z9bq2AG1Ky/size_s.jpg"
      }
    },
    "stream_urls": {
      "urls": {
        "very_high_quality": "https://vodhlsgaana.akamaized.net/hls/3/3487503/32408795/320.mp4.master.m3u8?hdnts=st=1750835850~exp=1750850250~acl=/*~hmac=ebd312837a89763eb967627048071b22ee619be14219ff402143d023c50cf7bb",
        "high_quality": "https://vodhlsgaana.akamaized.net/hls/3/3487503/32408795/128.mp4.master.m3u8?hdnts=st=1750835850~exp=1750850250~acl=/*~hmac=ebd312837a89763eb967627048071b22ee619be14219ff402143d023c50cf7bb",
        "medium_quality": "https://vodhlsgaana.akamaized.net/hls/3/3487503/32408795/64.mp4.master.m3u8?hdnts=st=1750835850~exp=1750850250~acl=/*~hmac=ebd312837a89763eb967627048071b22ee619be14219ff402143d023c50cf7bb",
        "low_quality": "https://vodhlsgaana.akamaized.net/hls/3/3487503/32408795/16.mp4.master.m3u8?hdnts=st=1750835850~exp=1750850250~acl=/*~hmac=ebd312837a89763eb967627048071b22ee619be14219ff402143d023c50cf7bb"
      }
    }
  }
]
```

## 👨‍🔧 **Usage**

API documentation (when running locally):
http://127.0.0.1:8000/docs

#### **Search For Songs**: (Requires a search query, limit is optional)
```sh
http://127.0.0.1:8000/songs/search?query=<insert-query-here>&limit=<insert-limit-here, eg. 5>
```
**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/songs/search?query=tyler herro` to get a JSON response of song results in return.

---
#### **Search For Albums**: (Requires a search query, limit is optional)
```sh
http://127.0.0.1:8000/albums/search?query=<insert-query-here>&limit=<insert-limit-here, eg. 5>
```
**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/albums/search?query=all over the place` to get a JSON response of album results in return.

----
#### **Search For Artists**: (Requires a search query, limit is optional)
```sh
http://127.0.0.1:8000/artists/search?query=<insert-query-here>&limit=<insert-limit-here, eg. 5>
```
**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/artists/search?query=KSI` to get a JSON response of artist results in return.

----
#### **Get Similar Artists**: (Requires an Artist ID)
```sh
http://127.0.0.1:8000/artists/similar?artist_id=ARTIST_ID
```
**How do I find an artist's ID?:**

* Using [`Search For Songs`](#search-for-songs-requires-a-search-query-limit-is-optional) or [`Search For Albums`](#search-for-albums-requires-a-search-query-limit-is-optional), locate:
```json
[
  {
    "artist_ids": "817522", (There may be more than 1 artist ID depending on the number of artists in the song/album.) 
  }
]
 ```

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/artists/similar?artist_id=817522` to get a JSON response of similar artists in return.

----
#### **Get Song Info**: (Requires a SEOKEY)
```sh
http://127.0.0.1:8000/songs/info?seokey=SEOKEY
```
**How do I find a song's seokey?:**

* In a URL, for example, `https://gaana.com/song/tyler-herro`, `tyler-herro` is the song's seokey.  
* Using [`Search For Songs`](#search-for-songs-requires-a-search-query-limit-is-optional), locate:
```json 
[
  {
    "seokey": "tyler-herro", 
  }
]
 ```

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/songs/info?seokey=tyler-herro` to get a JSON response of the song's info in return.

----
#### **Get Album Info**: (Requires a SEOKEY)
```sh
http://127.0.0.1:8000/albums/info?seokey=ALBUM_SEOKEY
```
**How do I find an albums's seokey?:**

* In a URL, for example, `https://gaana.com/album/tyler-herro`, `tyler-herro` is the albums's seokey.  
* Using [`Search For Albums`](#search-for-albums-requires-a-search-query-limit-is-optional), locate:
```json 
[
  {
    "seokey": "tyler-herro", 
  }
]
 ```
* Using [`Search For Songs`](#search-for-songs-requires-a-search-query-limit-is-optional), locate:
```json 
[
  {
    "album_seokey": "tyler-herro", 
  }
]
```

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/albums/info?seokey=tyler-herro` to get a JSON response of the album's info in return.

----
#### **Get Artist Info**: (Requires a SEOKEY)
```sh
http://127.0.0.1:8000/artists/info?seokey=SEOKEY
```
**How do I find an artist's seokey?:**

* In a URL, for example, `https://gaana.com/artist/jack-harlow`, `jack-harlow` is the song's seokey.  
* Using [`Search For Songs`](#search-for-songs-requires-a-search-query-limit-is-optional) or [`Search For Albums`](#search-for-albums-requires-a-search-query-limit-is-optional), locate:
```json 
[
  {
    "artist_seokeys": "jack-harlow", (There may be more than 1 seokey depending on the number of artists in the song/album.) 
  }
]
 ```

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/artists/info?seokey=jack-harlow` to get a JSON response of the artist's info in return.

----
#### **Get Playlist Info**: (Requires a SEOKEY)

```sh
http://127.0.0.1:8000/playlists/info?seokey=SEOKEY
```
**How do I find a playlists's seokey?:**

* In a URL, for example, `https://gaana.com/playlist/gaana-dj-gaana-international-top-50`, `gaana-dj-gaana-international-top-50` is the playlist's seokey. 


**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/playlists/info?seokey=gaana-dj-gaana-international-top-50` to get a JSON response of the playlist's info in return.

----
#### **Get Trending Tracks**: (Requires a LANGUAGE)
```sh
http://127.0.0.1:8000/trending?lang=LANGUAGE
```
**Language Options:** English, Hindi, Punjabi, Telugu, Tamil etc. (Warning: Case sensitive!). Defaults to Hindi if no language is provided or if an invalid language is entered.

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/trending?lang=English` to get a JSON response of the trending English songs in return.

----
#### **Get New Releases**: (Requires a language)
```sh
http://127.0.0.1:8000/newreleases?lang=LANGUAGE
```
**Language Options:** English, Hindi, Punjabi, Telugu, Tamil etc. (Warning: Case sensitive!). Defaults to Hindi if no language is provided or if an invalid language is entered.

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/newreleases?lang=English` to get a JSON response of both new English songs and English albums in return.

----
#### **Get Charts** (Returns a list of popular playlists):
```sh
http://127.0.0.1:8000/charts
```

**Example:** Create a GET request or navigate to `http://127.0.0.1:8000/charts` to get a JSON response of the top charts.

## 💻 **Local Development**

Clone the Repository
```sh
$ git clone https://github.com/ZingyTomato/GaanaPy
```
Enter `/GaanaPy` and install all the requirements using
```sh
$ pip3 install -r requirements.txt
```
Run the app using
```sh
$ python3 -m uvicorn app:app --reload
```

Navigate to: `http://127.0.0.1:8000` to get started.

## **🐳 Docker Deployment**

Deploy the API locally using the following Docker-Compose stack: 

```
---
services:
  gaanapy:
    image: zingytomato/gaanapy:main
    container_name: gaanapy
    ports:
      - 8000:8000 # External port can be changed
    restart: unless-stopped
```

Navigate to: `http://SERVER_IP:8000` to get started.

## 🏥 Contributing

Feel free to create an issue if you encounter any bugs or would like to suggest something!
