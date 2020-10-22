# Learning Objectives

1. Learn `fetch` for GET requests with Promises and async/await
    * See locading data from local image/JSON/CSV

2. Learn to "render" data with native JS DOM manipulation

3. Discover missing pieces: no persistance, API keys not hidden

# Fetch Images and Text

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

### Summary
1. Written async function that makes the fetch request

2. Turns the body of what comes in the HTTP response into a blob

3. Convert blob into a function that the dom element can work with

# Fetch CSV
- fetch the CSV file and build a graph from the data

- using the Zonal annual means, 1880-present, collected through [NASA](https://data.giss.nasa.gov/gistemp/)

- create a `test.csv` file to start parsing through first to get the data on the page before parsing through the entire csv file

- parse CSV file using `split()` (split up the rows and split up the columns)

- `/\n/` splits based on the breakpoint 

- slice will just chop off the first row

- for this data, I need the year and the mean

- for each row, 

<img width="823" alt="Screen Shot 2020-10-21 at 5 07 58 PM" src="https://user-images.githubusercontent.com/59414750/96799282-04328380-13c0-11eb-9f1b-720abba3c242.png">

```
const rows = data.split(/\n/).slice(1);
      rows.forEach(element => {
        const row = element.split(',');
        // const year = row[0];
        // const temp = row[1];
        console.log(row);
      });
```

<img width="823" alt="Screen Shot 2020-10-21 at 5 17 52 PM" src="https://user-images.githubusercontent.com/59414750/96799916-5d4ee700-13c1-11eb-8654-00d977dd766c.png">

When there aren't rows or years, it ended up parsing the CSV individually into separate data for each row.

With the addition of defining the year and temp, it only took the information relevant for us and displayed it as such where it's parsing through the CSV file to retrive the year and the temp

<img width="823" alt="Screen Shot 2020-10-21 at 5 18 58 PM" src="https://user-images.githubusercontent.com/59414750/96799979-82dbf080-13c1-11eb-9679-24ff9e21cabf.png">

### Summary

1. Taking the raw data as text

2. Split the data into rows from the table and put it into a varaible called table

3. Going through each row and split each row into its corresponding column

## Creating a Graph

<img width="1213" alt="Screen Shot 2020-10-22 at 7 42 14 AM" src="https://user-images.githubusercontent.com/59414750/96880405-5e702a80-143a-11eb-9ce0-298c47e7799d.png">

- `<script src="https://cdn.jsdelivr.net/npm/chart.js@2.9.4/dist/Chart.min.js"></script>` this is a JS library from the internet that can be imported

- you need a canvas for the graph to be worked on

- order matters

# Fetch JSON
