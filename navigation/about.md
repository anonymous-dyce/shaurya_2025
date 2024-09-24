---
layout: page
title: About
permalink: /about/
---

Hi, my name is Shaurya Singh!
- Student at Del Norte High School, San Diego CA
- Class of 2024-25, 11th Grade (Junior Year)
- Classes I'm taking:
    - AP Calculus AB
    - AP English Language and Composition
    - AP Computer Science Principles (THE Best Class!)
    - AP Physics C: Mechanics
    - Honors Principles of Engineering (Trimester 2&3)
    - Spanish 4 (Trimester 1)
    - Online US History (Trimester 2&3)
- Aspiring to major in Electrical Engineering (and potentially Computer Science, so EE / EECS)



<style>
    /* Style looks pretty compact, 
       - grid-container and grid-item are referenced the code 
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://unsplash.com/s/photos/technology";
    var living_in_the_world = [
        
    ];

    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>
