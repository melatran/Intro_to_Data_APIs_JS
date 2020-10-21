# Learning Objectives

1. Learn `fetch` for GET requests with Promises and async/await
    * See locading data from local image/JSON/CSV

2. Learn to "render" data with native JS DOM manipulation

3. Discover missing pieces: no persistance, API keys not hidden

# Fetch

<img width="645" alt="Screen Shot 2020-10-21 at 7 26 26 AM" src="https://user-images.githubusercontent.com/59414750/96726622-61eaaf80-136f-11eb-8e7d-ed2ffcf8d671.png">

- fetch function returns a promise

- convert response to an image blob which trigges another promise that you chain using `.then`

- first fetch the rainbow, then look at the resolved promise and then complete reading the stream of data to convert to a blob

- `document.getElementById('rainbow').src = blob;` takes the image source element and place it in the dom

- image doesn't show up because blob isn't in the format dom image element expects so `src = URL.createObjectURL(blob)`

<img width="744" alt="Screen Shot 2020-10-21 at 11 04 09 AM" src="https://user-images.githubusercontent.com/59414750/96753501-2fe84600-138d-11eb-8d3b-f84eb95392b8.png">

```
<body>
  <img src="" id="rainbow" width= 75% height= 75%/>
  <script>
    console.log('about to fetch a rainbow');
    fetch('rainbow.jpg')
      .then(response => {
        console.log(response);
        return response.blob();
    })
      .then(blob => {
        console.log(blob);
        document.getElementById('rainbow').src = URL.createObjectURL(blob);
      });
  </script>
</body>
```

- with the original code above, problems: no promises that deal with errors and include async/await into JS code

- use `await` with async functions

- await the result of fetch and store in this variable called response

- removed console.log for clean code but `console.log("yay!)` lets us inspect in the console and if it as a success, it will print out yay to notify us (good check purposes)
