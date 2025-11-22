# Spotify Analytics 
Dataset: [Kaggle](https://www.kaggle.com/equinxx/spotify-top-50-songs-in-2021?select=spotify_top50_2021.csv)

<br>

## Analytics
Analyzes data from a Spotify dataset, focusing on artist popularity, song duration, energy levels, and emotional valence.

<br>

### Who are the top 10 artists based on popularity?
```sql
SELECT
    artist_name,
    AVG(popularity) popularity
FROM BIT_DB.Spotifydata
GROUP BY artist_name
ORDER BY popularity DESC
LIMIT 10;
```

<details><summary><i>Show result</i></summary>

| artist_name        | popularity |
|--------------------|-----------:|
| Ed Sheeran         | 95         |
| Glass Animals      | 94         |
| Olivia Rodrigo     | 92.25      |
| The Neighbourhood  | 92         |
| The Weeknd         | 91.5       |
| Doja Cat           | 90.75      |
| Måneskin           | 90.5       |
| Lil Nas X          | 90         |
| Justin Bieber      | 90         |
| Harry Styles       | 90         |
</details>

<br>

### What are the top 25 longest songs in the dataset? (calculate duration from ms to seconds)
```sql
SELECT
    artist_name,
    track_name,
    (duration_ms / 1000) duration_seconds
FROM BIT_DB.Spotifydata
ORDER BY duration_seconds DESC
LIMIT 25;
```
<details><summary><i>Show result</i></summary>

| artist_name        | track_name                                 | duration_seconds |
|--------------------|--------------------------------------------|-----------------:|
| Farruko            | Pepas                                      | 287              |
| SZA                | Good Days                                  | 279              |
| Los Legendarios    | Fiel                                       | 261              |
| Olivia Rodrigo     | drivers license                            | 242              |
| Bruno Mars         | Leave The Door Open                        | 242              |
| The Neighbourhood  | Sweater Weather                            | 240              |
| Glass Animals      | Heat Waves                                 | 238              |
| Myke Towers        | Bandido                                    | 232              |
| Ed Sheeran         | Bad Habits                                 | 230              |
| Olivia Rodrigo     | traitor                                    | 229              |
| Doja Cat           | Streets                                    | 226              |
| J Balvin           | Qué Más Pues?                              | 217              |
| The Weeknd         | Save Your Tears                            | 215              |
| Olivia Rodrigo     | deja vu                                    | 215              |
| Lil Nas X          | INDUSTRY BABY (feat. Jack Harlow)          | 212              |
| Måneskin           | Beggin'                                    | 211              |
| Doja Cat           | Need to Know                               | 210              |
| Doja Cat           | Kiss Me More (feat. SZA)                   | 208              |
| Bad Bunny          | Yonaguni                                   | 206              |
| Bad Bunny          | DÁKITI                                     | 205              |
| Dua Lipa           | Levitating (feat. DaBaby)                  | 203              |
| Bad Bunny          | LA NOCHE DE ANOCHE                         | 203              |
| The Weeknd         | Blinding Lights                            | 200              |
| Rauw Alejandro     | Todo De Ti                                 | 199              |
| BTS                | Dynamite                                   | 199              |
</details>

<br>

### What songs have the most calming energy?
```sql
SELECT
    artist_name,
    track_name
FROM BIT_DB.Spotifydata
WHERE energy < 0.5
ORDER BY energy ASC;
```
<details><summary><i>Show result</i></summary>

| artist_name      | track_name             |
|------------------|------------------------|
| Olivia Rodrigo   | traitor                |
| Duncan Laurence  | Arcade                 |
| Tate McRae       | you broke me first     |
| Lewis Capaldi    | Someone You Loved      |
| The Kid LAROI    | WITHOUT YOU            |
| Olivia Rodrigo   | drivers license        |
| BTS              | Butter                 |
| Doja Cat         | Streets                |
| Giveon           | Heartbreak Anniversary |
</details>

<br>

### What are the max and minimum valence?
(scored between 0-10, valence measures whether a song will make a person feel happy (high) or sad (low))
```sql
SELECT
    artist_name,
    track_name,
    ROUND((valence * 10), 2) valence
FROM BIT_DB.Spotifydata
WHERE valence = (SELECT MAX(valence) FROM BIT_DB.Spotifydata)
OR valence = (SELECT MIN(valence) FROM BIT_DB.Spotifydata);
```
<details><summary><i>Show result</i></summary>

| artist_name   | track_name            | valence |
|---------------|-----------------------|---------|
| Måneskin      | I WANNA BE YOUR SLAVE | 9.58    |
| Tate McRae    | you broke me first    | 0.82    |
</details>

<br>
