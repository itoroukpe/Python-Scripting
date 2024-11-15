Here’s how to convert the Python script into a web application using HTML, CSS, and JavaScript. This application will allow users to add, retrieve, display, and delete contacts in a browser-based interface.

### **HTML and JavaScript Code**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Address Book</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
        }
        h1 {
            color: #4CAF50;
        }
        .form-group {
            margin-bottom: 15px;
        }
        input, button {
            padding: 10px;
            margin: 5px 0;
            width: 100%;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .output {
            margin-top: 20px;
            border: 1px solid #ccc;
            padding: 10px;
            background: #f9f9f9;
        }
    </style>
</head>
<body>
    <h1>Address Book</h1>
    <div>
        <div class="form-group">
            <label for="contactName">Contact Name:</label>
            <input type="text" id="contactName" placeholder="Enter contact name">
        </div>
        <div class="form-group">
            <label for="contactPhone">Phone Number:</label>
            <input type="text" id="contactPhone" placeholder="Enter phone number">
        </div>
        <button onclick="addContact()">Add Contact</button>
        <button onclick="retrieveContact()">Retrieve Contact</button>
        <button onclick="displayAllContacts()">Display All Contacts</button>
    </div>
    <div class="output" id="output"></div>

    <script>
        const addressBook = {};

        // Function to add a contact
        function addContact() {
            const name = document.getElementById("contactName").value.trim();
            const phone = document.getElementById("contactPhone").value.trim();
            
            if (name && phone) {
                addressBook[name] = phone;
                document.getElementById("output").innerHTML = `Contact <b>${name}</b> added successfully.`;
                document.getElementById("contactName").value = '';
                document.getElementById("contactPhone").value = '';
            } else {
                document.getElementById("output").innerHTML = "Please enter both name and phone number.";
            }
        }

        // Function to retrieve a contact
        function retrieveContact() {
            const name = document.getElementById("contactName").value.trim();
            
            if (name) {
                if (addressBook[name]) {
                    document.getElementById("output").innerHTML = `<b>${name}</b>'s phone number is <b>${addressBook[name]}</b>.`;
                } else {
                    document.getElementById("output").innerHTML = `No contact found for <b>${name}</b>.`;
                }
            } else {
                document.getElementById("output").innerHTML = "Please enter a name to retrieve the contact.";
            }
        }

        // Function to display all contacts
        function displayAllContacts() {
            if (Object.keys(addressBook).length === 0) {
                document.getElementById("output").innerHTML = "No contacts available.";
            } else {
                let contacts = "<h3>All Contacts:</h3><ul>";
                for (const [name, phone] of Object.entries(addressBook)) {
                    contacts += `<li><b>${name}</b>: ${phone}</li>`;
                }
                contacts += "</ul>";
                document.getElementById("output").innerHTML = contacts;
            }
        }
    </script>
</body>
</html>
```

---

### **How It Works**
1. **Input Fields**: Users can enter a contact name and phone number.
2. **Add Contact**: When the "Add Contact" button is clicked:
   - The name and phone are stored in the `addressBook` object.
   - A success message is displayed.
3. **Retrieve Contact**: When the "Retrieve Contact" button is clicked:
   - The entered name is used to search the `addressBook`.
   - If found, the phone number is displayed; otherwise, a "not found" message is shown.
4. **Display All Contacts**: Clicking this button lists all stored contacts in a user-friendly format.
5. **Output Section**: Displays feedback and results for the user.

---

### **Key Features**
- Fully interactive web-based application.
- Dynamic updates without requiring page reloads.
- Simple, user-friendly design and navigation.

This implementation brings the functionality of the original Python script to a modern web interface, making it accessible and convenient for users.
