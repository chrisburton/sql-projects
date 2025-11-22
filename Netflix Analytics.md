# Netflix Analytics 
Dataset: [db-fiddle](https://www.db-fiddle.com/f/5XjDEBzg6DR1XzKVwNapdD/0)

<br>

## Analysis    
Extracts various insights from a Netflix titles database using PostgreSQL, focusing on content counts, recent additions, sorting, directorship, and historical records.

<br>

### How many movie titles are there in the database? (movies only, not tv shows)
```sql
SELECT 
  COUNT(titles.type)
FROM "netflix_titles_info" titles
WHERE titles.type = 'Movie';
```
<details>
  <summary><i>Show result</i></summary>

| count |
|:-----:|
| 8     |
</details>

<br>

### When was the most recent batch of tv shows and/or movies added to the database?
```sql
SELECT 
  MAX(DATE(date_added))
FROM "netflix_titles_info";
```
<details>
  <summary><i>Show result</i></summary>
    
| max                  |
|---------------------|
| 2021-09-25T00:00:00Z |
</details>

<br>

### List all the movies and tv shows in alphabetical order. 
```sql
SELECT 
  title
FROM "netflix_titles_info"
ORDER BY title ASC;
```
<details>
  <summary><i>Show result</i></summary>

| title                                               |
|-----------------------------------------------------|
| Bangkok Breaking                                    |
| Blood & Water                                       |
| Confessions of an Invisible Girl                    |
| Crime Stories: India Detectives                     |
| Dear White People                                   |
| Dick Johnson Is Dead                                |
| Europe's Most Dangerous Man: Otto Skorzeny in Spain |
| Falsa identidad                                     |
| Ganglands                                           |
| Intrusion                                           |
| Jaguar                                              |
| Jailbirds New Orleans                               |
| Je Suis Karl                                        |
| Kota Factory                                        |
| Midnight Mass                                       |
| My Little Pony: A New Generation                    |
| Sankofa                                             |
| The Great British Baking Show                       |
| The Starling                                        |
| Vendetta: Truth Lies and The Mafia                  |
</details>

<br>

### Who was the Director for the movie The Starling? 
```sql
SELECT 
  director
FROM "netflix_titles_info" titles
LEFT JOIN "netflix_people" people
ON titles.show_id = people.show_id
WHERE titles.title = 'The Starling';
```
<details>
  <summary><i>Show result</i></summary>

| director       |
|----------------|
| Theodore Melfi |
</details>

<br>

### What is the oldest movie in the database and what year was it made? 
```sql
SELECT 
  title, 
  release_year
FROM "netflix_titles_info"
WHERE type = 'Movie'
ORDER BY release_year ASC
LIMIT 1;
```
<details>
  <summary><i>Show result</i></summary>

| title   | release_year |
|---------|:------------:|
| Sankofa | 1993         |
</details>

<br>
