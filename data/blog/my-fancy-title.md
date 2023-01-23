---
title: Generating a Chrome Extension with ChatGPT
date: '2021-12-01'
tags: ['chrome extension', 'javascript', 'code generation']
draft: false
summary: Learn how to generate a chrome extension using OpenAI's ChatGPT model, and see the code that it produces.
---

## Introduction
Chrome extensions are small programs that can modify and enhance the functionality of the Google Chrome browser. They are written in JavaScript and can be easily created by anyone with some basic web development knowledge. However, for those who are not familiar with web development, the process of creating a chrome extension can be overwhelming. This is where ChatGPT comes in.

ChatGPT is a large language model trained by OpenAI that can generate code based on a given prompt. By using ChatGPT, anyone can generate a chrome extension without needing to have extensive knowledge of web development. In this blog post, we will go over how to generate a chrome extension using ChatGPT, and see the code that it produces.

Generating a Chrome Extension with ChatGPT
To generate a chrome extension using ChatGPT, we can provide it with a series of prompts that describe the functionality that we want the extension to have. In this example, we will generate a simple to-do extension.

The first prompt we will use is to generate a basic project structure for a chrome extension written in JavaScript:

```javascript
I want you to generate a simple project structure for a chrome extension written in javascript.
```

ChatGPT will respond with the following code:

```javascript
MyExtension/
    |- manifest.json
    |- icon.png
    |- popup/
        |- index.html
        |- script.js
        |- style.css
```
This is the basic project structure for a chrome extension. The manifest.json file contains the configuration for the extension, such as the extension's name and permissions. The icon.png file is the icon that will be displayed in the chrome browser when the extension is installed. The popup directory contains the HTML, JavaScript, and CSS files that make up the extension's user interface.

We can then continue to add functionality to the extension by providing ChatGPT with more prompts. For example, we can ask ChatGPT to add code that extracts emails from the current page and displays them to the user:

```javascript
Now help me fill those in with code for a simple to do extension.
```
```javascript
// manifest.json
{
    "manifest_version": 2,
    "name": "Email Extractor",
    "description": "Extracts emails from the current page and displays them to the user",
    "version": "1.0",
    "permissions": ["activeTab"],
    "browser_action": {
        "default_popup": "popup/index.html",
        "default_icon": "icon.png"
    }
}
```
ChatGPT will respond with the following code:
```javascript
<!-- popup/index.html -->
<!DOCTYPE html>
<html>
    <head>
        <title>Email Extractor</title>
        <link rel="stylesheet" type="text/css" href="style.css">
    </head>
    <body>
        <h1>Extracted Emails</h1>
        <ul id="email-list"></ul>
        <button id="download-csv">Download as CSV</button>
        <script src="script.js"></script>
    </body>
</html>
```
```javascript
/* popup/style.css */
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

h1 {
    text-align: center;
    padding: 20px;
}

ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

li {
    display: flex;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

li img {
    margin-right: 10px;
    cursor: pointer;
}
```

```javascript
// popup/script.js
var emailList = document.getElementById('email-list');
var emails = [];

chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
    var tab = tabs[0];
    var tabUrl = tab.url;

    // Fetch the page's HTML
    fetch(tabUrl)
        .then(response => response.text())
        .then(html => {
            // Extract all email addresses from the HTML
            emails = extractEmails(html);

            // Display the emails in the popup
            for (var i = 0; i < emails.length; i++) {
                var email = emails[i];
                var emailListItem = document.createElement('li');
```
This code uses the chrome.tabs.query method to fetch the current tab's URL, and then uses the fetch method to retrieve the page's HTML. It then uses a extractEmails function to extract all email addresses from the HTML, and displays them in the popup by creating a new li element for each email and adding it to the email-list ul.

We can then further modify the extension by providing ChatGPT with more prompts. For example, we can ask ChatGPT to add a download button that allows the user to download the extracted emails as a CSV file:

```javascript
now modify that code so that the user has an option to download the extracted emails as a csv.
```
ChatGPT will respond with the following code:

```javascript
// popup/script.js
var downloadCsvBtn = document.getElementById('download-csv');

downloadCsvBtn.addEventListener('click', function() {
    // Convert emails array to CSV string
    var csv = emails.join(',');

    // Create a hidden link and click it to trigger the download
    var link = document.createElement('a');
    link.href = 'data:text/csv;charset=utf-8,' + encodeURIComponent(csv);
    link.download = 'emails.csv';
    link.style.display = 'none';
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
});
```
This code adds a new button with the id 'download-csv' to the HTML. It then creates an event listener for this button that converts the emails array to a CSV string using the join method and creates a hidden link, with the href set to the CSV string and the download attribute set to "emails.csv". The script then appends this link to the body and simulates a click on it, triggering the download.

In this way, we can continue to add functionality to the extension by providing ChatGPT with more prompts. However, please keep in mind that, even though the ChatGPT model can generate code, it is not without its limitations, and may not cover all the edge cases or provide the optimal solution to a problem.

## Conclusion
In this blog post, we have seen how to generate a chrome extension using ChatGPT, and the code that it produces. By providing ChatGPT with a series of prompts, we can quickly generate a basic project structure for a chrome extension and add functionality to it. However, it's important to note that the code generated by ChatGPT may not always be the best solution and it's important to manually review the code and test it before deploying it. Nevertheless, ChatGPT can be a great tool to quickly generate code and get started on a project.