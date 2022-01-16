# My Chinook JSON Server

## Story

Your company, Chinook Ltd., decided the build a RESTful HTTP interface in front of its music store database.

Your task is to build a mock version of this interface using [`json-server`](https://github.com/typicode/json-server).

## What are you going to learn?

- Understand the building blocks of JSON: objects, arrays, scalars (strings, numbers, booleans and `null`)
- What REST is, what REST APIs are
- Learn about HTTP, status codes, etc.
- Using `curl` to make requests and how to inspect status codes

## Tasks

1. You'll be using [`json-server`](https://github.com/typicode/json-server#getting-started) to create a fake REST API on your local machine. For this you'll need to install [`node`](https://nodejs.org) on your OS and install the `json-server` package after that, then finally start your server.
    - `node` is installed ([from here](https://nodejs.org/) or by any other means) on the student's OS, executing `node --version` in a terminal `v14.x.x` or something similar or more recent is displayed
    - `json-server` is installed by executing `npm install -g json-serverv0.16.3`, executing `json-server --version` outputs `0.16.3`
    - Executed `json-server --watch db.json` from the project's root Git directory
    - The server is kept in a running state while doing this exercise (e.g. while modifying `db.json`)

2. Create an `artists` resource/collection in `db.json` containing at least 3 separate artists from the Chinook database sample.
    - `db.json` contains an `artists` array/collection
    - `artists` contains 3 artist objects (e.g. `AC/DC`, `Accept`, `Aerosmith`)
    - Individual `artist` objects have the following keys:
- `id` (the artist's ID)
- `name` (the artist's name)

3. Create an `albums` resource/collection in `db.json` containing albums for the 3 artists created earlier. Each artist should have 1 to 3 albums listed in this array.
    - `db.json` contains an `albums` array/collection
    - `albums` contains 3 to 9 album objects (e.g. `For Those About To Rock We Salute You` by `AC/DC`)
    - Individual `album` objects have the following keys:
- `id` (the album's ID)
- `title` (the album's name)
- `artistId` (the artist's ID)
    - `curl -v http://localhost:3000/albums` returns a 200 status code and the array of albums defined in `db.json`
    - `curl -v http://localhost:3000/albums/<id>` returns
- a single album and a 200 status code if `<id>` is an existing album ID
- nothing and a 404 status code if `<id>` is a non-existent album ID
    - `curl -v http://localhost:3000/albums/<id>/tracks` returns an array of tracks for the album defined by `<id>`

4. Create a `tracks` resource/collection in `db.json` containing tracks for the albums created earlier. Each albums should have 1 to 3 tracks listed in this array.
    - `db.json` contains a `tracks` array/collection
    - `tracks` contains 3 to 9 track objects (e.g. `Rag Doll` by `Aerosmith`)
    - Individual `track` objects have the following keys:
- `id` (the track's ID)
- `name` (the track's name)
- `albumId` (the album's ID)
- `isFavorite` (whether the track is your favorite or not)
    - `curl -v http://localhost:3000/tracks` returns a 200 status code and the array of tracks defined in `db.json`
    - `curl -v http://localhost:3000/tracks/<id>` returns
- a single track and a 200 status code if `<id>` is an existing track ID
- nothing and a 404 status code if `<id>` is a non-existent track ID

5. Use `curl` to make `GET` requests against the fake API you're creating.
    - `curl -v http://localhost:3000/artists` returns a 200 status code and the array of artists defined in `db.json`
    - `curl -v http://localhost:3000/artists/<id>` returns
- an artist and a 200 status code if `<id>` is an existing artist ID
- nothing and a 404 status code if `<id>` is a non-existent artist ID
    - `curl -v http://localhost:3000/artists/<id>/albums` returns an array of albums for the artist defined by `<id>`

6. Create a new artist resource via `POST`ing a data into the `artists` resource/collection.
    - `curl` is used to `POST` a new artist, e.g. create a new artist object with the `name` _Scooter_ (omitting the `id` which is generated when _creating_ a new resource)

7. Update an existing album resource via `PUT`ing a data into an existing `album` resource.
    - `curl` is used to `PUT` new data for an existing album, e.g. change the album object's `title` to something else (the `id` is optional since the resource's URL contains it)

8. Delete an existing track resource via sending a `DELETE` request to an existing resource's URL.
    - `curl` is used to `DELETE` an existing track (by using a URL containing an track's ID)

## General requirements

- `db.json` is saved and committed in Git _before_ destructive operations (`POST`, `PUT`, `DELETE`) are taken on it :)

## Hints

- Here's how you can install `node` and `json-server` in one go in Ubuntu 18.04 LTS
  ```sh
  curl -sL https://deb.nodesource.com/setup_15.x | sudo -E bash -
  sudo apt-get install -y nodejs
  sudo npm install --global json-server
  ```
- When issuing `POST`, `PUT` or `DELETE` requests with `curl` to a `json-server` watch out: _these operations are destructive!_ Commit your `db.json` ASAP after you think you're done :)
- Watch out for case-sensitivity, `artistId` should be as is, not `ArtistId`, `artistid` or similar
- `curl` by default issues `GET` requests, but when you use certain flags (like `--data`) it'll use a different HTTP verb instead
- Watch out when `POST`ing or `PUT`ing data with `curl`, the content type usually must be specified in these cases (to be JSON or something else dependending on the circumstances)
- When reading [`json-server`'s reference](https://github.com/typicode/json-server#getting-started) you don't need to deal with `npm` or `node` or install anything since we provide an executable version of `json-server` for you inside the project's repository
- In [the `json-server` video tutorial](https://egghead.io/lessons/javascript-creating-demo-apis-with-json-server) skip the part about JavaScript, focus only when `db.json` is being dealt with, and also, you should use `curl` instead of something like _Rest Client_ as shown in the video (they serve the same purpose)
- When dealing with JSON focus on understanding the difference between objects, arrays and scalars (simple values like a string, number or a boolean)
- When reading about [REST status codes](https://www.restapitutorial.com/httpstatuscodes.html) you don't need to memorize everypossible code, just focus on the meaning of the followings:
  - 200, 201, 204
  - 301, 302
  - 400, 401, 403, 404,
  - 500

## Background materials

- [`json-server` reference](https://github.com/typicode/json-server#routes)
- [`json-server` video tutorial](https://egghead.io/lessons/javascript-creating-demo-apis-with-json-server)
- [JSONLint - online JSON validation](https://jsonlint.com/)
- [JSON syntax with images](https://www.json.org/json-en.html)
- [`POST`ing JSON with `curl`](https://stackoverflow.com/a/7173011)
- [REST HTTP methods and their meaning](https://www.restapitutorial.com/lessons/httpmethods.html)
- [REST quick tips](https://www.restapitutorial.com/lessons/restquicktips.html)
- [REST (resource) naming](https://www.restapitutorial.com/lessons/restfulresourcenaming.html)
- [REST status codes](https://www.restapitutorial.com/httpstatuscodes.html)
