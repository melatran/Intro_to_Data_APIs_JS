# Data Selfie App

## Tech Requirements

- Install Node.JS for server side programming (data persistance)

- Terminal to run Node commands

- run `npm init` to create package.json

- Use Express package ontop of Node `npm install express`

- ES6 syntax (=>)

## What I Want Server(index.js) To Do

- JS is the server file sent as raw text and executed on the browser

- serve web pages
    - host static files

       - index.html (sent to the client and renders on the browser)

    - save to database

    - authentication

- client

    - geolocate and send data back to the server

- take server and deploy to cloud

## Geolocation

The **Navigator** interface represents the state and the identity of the user agent. It allows scripts to query it and to register themselves to carry on some activities.

A Navigator object can be retrieved using the read-only window.navigator property.

- geolocation can be accessed via the navigator object

- only works in secure contexts(HTTPS)

    - developing locally, is a lot easier with only us as a user

    - need permission to grant access to webcams

```
    if ('geolocation' in navigator) {
      console.log('geolocation available');
      navigator.geolocation.getCurrentPosition(function(position) {
        console.log(position.coords.latitude);
        console.log(position.coords.longitude);
      });
    } else {
      console.log('geolocation not available');
    }
```

- when it's ready to get the lat and lon, call on this function and then console log it

- after refreshing the page, a popup about localhost wants to use your position and user has to give permission in order for geolocation to work; cannot secretly bypass this step

- go through a `POST` request to save the geolocation in the db

## HTTP POST with fetch()

- routes live in index.js (server)

- client to fetch my POST in the index.html file

- take the JS object data and make it into a JSON string

- header is something that gets packaged with the server

```
// index.js (server)

app.post('/api', (request, response) => {
  console.log(request.body);
  const data = request.body;
  response.json({
    status: 'success',
    latitude: data.lat,
    longitude: data.lon
  });
});
```

- express.json for server to understand incoming data as json

- fetch returns a promise

```
//index.html (client)

const data = { lat, lon };
        const options = {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(data)
        };

        const response = await fetch('/api', options);
        const json = await response.json();
      });
```

- server recieves the data (handshake complete)

- Node File system package to save array

## Saving to Database

- Firebase saves data for you

- MongoDB stores data as documents

- this app uses NeDB (not for giant applications just for learnin

- when user clicks submit, it adds the new lat and lon to the array in our db (db starts of empty)

- `database.insert({name: "MoMo", status: '🧑🏻‍🎤'});`

- result save in db `{"name":"MoMo","status":"🧑🏻‍🎤","_id":"D8JO3fY4tJN1EMqj"}`

- this will save to database.db file from the client side