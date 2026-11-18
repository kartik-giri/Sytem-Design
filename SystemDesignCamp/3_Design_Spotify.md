# Design Spotify.
![Spotify](../img/Spotify.png) 

1. CLARIFY:
- Spotify is the music streaming platform which allows the publisher to puclish the songs and listner to listen the song.
- App have 500k users and 30 million songs

- Func req:
1. Allows artists to publish tere songs.
2. Users can search and browser the song to listen it.
3. Users can maintain there playlist.
4. Users can maintain there own profiles.

- Non func req.
1. Will use AAC and OGG audio files format.
- AAC: When building a mobile app, audio streaming platform, or general-purpose audio player.
- OGG/Opus: When building web-based real-time voice communication, games, or applications where efficient audio transmission matters.
- One. song takes 3 mb of starage.

2. What should be the playback latency?
- 1 or 2 sec max

![Spotify Req](../img/SpotifyReq.png) 

2. ESTIMATION:
1. 500k users * 1 kb of users metadata = 500 MB for user metadata.
2. 30 million songs = 3 mb = 90 tb of stroage for songs.
3. 300 bytes per song meta data * 30 millon songs = 9 GB.

4. User listens 10 songs per day = 500k *10 = 5 million songs per day
- 5 million / 1 lakh = 50 songs per sec.

5. our app is read heavy.

![Spotify Estimation](../img/SPotifyEstimation.png) 
