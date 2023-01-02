# UFOs
JavaScript
## Background
Dana’s webpage and dynamic table are working as intended, but she’d like to provide a more in-depth analysis of UFO sightings by allowing users to filter for multiple criteria at the same time. In addition to the date, you’ll add table filters for the city, state, country, and shape.
## Deliverable 1: Filter UFO sightings on multiple criteria
Using JavaScript and HTML, you’ll modify the code in your index.html file to create more table filters. In addition to the date filter you created in this module, you’ll add filters for the city, state, country, and shape, as shown in the following image:

![image](https://user-images.githubusercontent.com/112348240/208986075-ca34daab-0009-430d-b455-e9d3835e05a5.png)

Using JavaScript, you’ll replace the `handleClick()` function in your `app.js` file with a new function that saves the element, value, and id of the filter that was changed. Then, you’ll create a new function to loop through the dataset and keep only the results that match the search criteria. The webpage will be updated with the search criteria after pressing "Enter".

Follow the instructions below and the numbered comments in the starter code to complete Deliverable 1.

1. Download the `ufo_starterCode.js`, rename it `app.js`, and place it in the js folder of your UFOs GitHub repository. The starter code includes the code used to populate the table from this module.
2. In the `index.html` file, remove the list `(<li></li>)` element that creates the button.
![image](https://user-images.githubusercontent.com/112348240/208989148-a0a21427-0e37-4d98-baf6-f1f0bbe87761.png)


3.Create four more list elements: city, state, country, and shape. These will be similar to the "Enter Date" list element. Each element should have the same "id" as the object properties in the `data.js` file.

4. In Step 1 of the `app.js` file, create an empty `filters` variable to keep track of all the elements that change when a search is entered. This variable will be used in Step 5 to store the property “id” and the value that was entered from user input.

5. Next, you will need to write code for two functions whose names we’ve provided in the starter code, `updateFilters()` and `filterTable()`.
    - The `updateFilters()` function will replace your `handleClick()` function and update the filters variable you created in Step 1.
    - The `filterTable()` function will filter the table data by the value that is entered for the "id" that has changed.
6. For Step 2, located before the `buildTable(tableData)` function at the end of the starter code, modify the event listener from this module so that it detects a "change" on each input element and calls the `updateFilters()` function.

7. In Step 3, we’ve provided the function, `updateFilters()`. Inside this function, you’ll write code in Steps 4-5 to update the filters based on user input.

8. In Step 4a, create a variable that saves the element that was changed using `d3.select(this)`.

9. In Step 4b, create a variable that saves the value of the changed element’s property.

10.In Step 4c, create a variable that saves the attribute of the changed element’s id.

11. In Step 5, write an `if-else` statement that checks if a value was changed by the user (variable from Step 4b). If a value was changed, add the element’s id (variable from Step 4c) as the property and the value that was changed to the `filters` variable you created in Step 1. If a value was not entered, then clear the element id from the `filters` variable.

    If you’d like a hint on how to update the filters based on user input, that’s totally okay. If not, that’s great too. You can always revisit this later if you change your mind.

12. In Step 6, inside the `updateFilters()` function, call the `filterTable()` function that will be used in Step 7.

13. In the `filterTable()` function in Step 7, write code to filter the table based on the user input that is stored in the `filters` variable.

14. In Step 8, create a variable for the filtered data that is equal to the data that builds the table. This variable will hold the updated table data based on the user input.

15. In Step 9, loop through the filters object and store the data that matches the filter values in the variable created in Step 8.

## **Below is the code that filter and make the changes using Javascript**

// from data.js
const tableData = data;

// get table references
var tbody = d3.select("tbody");

function buildTable(data) {
  // First, clear out any existing data
  tbody.html("");

  // Next, loop through each object in the data
  // and append a row and cells for each value in the row
  data.forEach((dataRow) => {
    // Append a row to the table body
    let row = tbody.append("tr");

    // Loop through each field in the dataRow and add
    // each value as a table cell (td)
    Object.values(dataRow).forEach((val) => {
      let cell = row.append("td");
      cell.text(val);
    });
  });
}

// 1. Create a variable to keep track of all the filters as an object.
var filters = {};

// 3. Use this function to update the filters. 
function updateFilters() {

    // 4a. Save the element that was changed as a variable.
    let changedElement = d3.select(this);

    // 4b. Save the value that was changed as a variable.
    let elementValue = changedElement.property("value");
    // 4c. Save the id of the filter that was changed as a variable.
    let filterId = changedElement.attr("id");
  
    // 5. If a filter value was entered then add that filterId and value
    // to the filters list. Otherwise, clear that filter from the filters object.
    if (elementValue) {
        filters[filterId]= elementValue;
    }
    else {
      delete filters[filterId];
    }
   
    // 6. Call function to apply all filters and rebuild the table
    filterTable();
  
  }
  
  // 7. Use this function to filter the table when data is entered.
  function filterTable() {
  
    // 8. Set the filtered data to the tableData.
  let filteredData =tableData;
      
    // 9. Loop through all of the filters and keep any data that
    // matches the filter values
  Object.entries(filters).forEach(([key,value])=> {
    filteredData = filteredData.filter(row => row[key]=== value);
  });
  
    // 10. Finally, rebuild the table using the filtered data
  buildTable(filteredData);
  }
  
  // 2. Attach an event to listen for changes to each filter
  d3.selectAll("input").on("change",updateFilters);
  
  
  // Build the table when the page loads
  buildTable(tableData);
  
## **END OF THE CODE**
 
16. In Step 10, rebuild the table with the filtered data by passing the variable created in Step 8.

17. Deploy the web app on your GitHub pages.

## Deliverable 2: A written report on the UFO analysis 
Initialize your repository with a README, and write your analysis of Deliverable 1. For your written analysis, be sure to use complete and coherent sentences. Your written analysis should contain three sections, which cover the following:

1. **Overview of Project**: Explain the purpose of this analysis.
    Dana is looking for UFO sightings by allowing users to filter for multiple criteria at the same time. In addition to the date, you’ll add table filters for the city, state, country, and shape.
2. **Results**: Describe to Dana how someone might use the new webpage by walking her through the process of using the search criteria. Use images of your webpage during the filtering process to support your explanation.
    First, If someone will like to use our HTML and filter the data by an specific, date, city, state, country or shape the just need to type on any of the blank space the information that needs to be search.
    The website will look like the screen shot below as well as the **Code**:
![image](https://user-images.githubusercontent.com/112348240/208985172-d0026e9e-9ab0-4910-9ee1-03f3d6196a00.png)

![image](https://user-images.githubusercontent.com/112348240/210194137-6737ac88-d875-4ff6-b5df-5c3f914e07c9.png)


3. **Summary**: In a summary statement, describe one drawback of this new design and two recommendations for further development.




![image](https://user-images.githubusercontent.com/112348240/208985301-4e256f79-fb2d-4af9-a616-2f8d5f942042.png)

![image](https://user-images.githubusercontent.com/112348240/208985422-1b70dabf-c8ed-4bbd-96dd-9346b4b77adb.png)

