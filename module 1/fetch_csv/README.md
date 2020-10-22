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