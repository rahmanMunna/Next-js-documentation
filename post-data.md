# Making a POST Request from Client Side (React / Next.js Client Component)

This document explains **how to send data from the client side to a backend API using a POST request**, following best practices.  
All examples are based on the **Fetch API** and **form submission handling**.

---

## Key Guidelines

When making a POST request from the client side, always ensure the following:

- ✅ Create a **reusable function** for the POST request and export it
- ✅ Explicitly mention the HTTP method as **POST**
- ✅ Add proper **request headers**
- ✅ Convert data into a **JSON string** and attach it to the request body
- ✅ Handle form submission using an **event handler**
- ✅ Use a **client component** (event handlers are not allowed in server components)

---

## 1. Reusable POST Request Function

Create a reusable function to send data to the backend API.

```js
export default async function addProduct(data) {
    const url = "http://localhost:2000/products/add";

    const result = await fetch(url, {
        method: "POST", // HTTP method
        headers: {
            "content-type": "application/json", // Request header
        },
        body: JSON.stringify(data), // Convert JS object to JSON string
    });

    return await result.json(); // Parse response
}
```
## 2. Creating a Form to Collect User Input
```
return (
    <div>
        <form method="post" onSubmit={addProductHandler}>
            <div>
                <input name="name" />
            </div>

            <div>
                <input name="qty" />
            </div>

            <div>
                <input name="price" />
            </div>

            <button type="submit">Add Product</button>
        </form>
    </div>
);
```
### Important Notes
- method="post" must be mentioned in the <form> tag
- onSubmit event handler captures form submission
- Each input must have a name attribute (used to retrieve values)
- Button type should be submit
## 3. Client Component Requirement
- Since we are using an event handler (onSubmit), this component must be a client component.
- Add this at the top of the file (for Next.js App Router):
```
"use client";
```
### Why?
- Server components cannot handle browser events
- Form submission and event handling require client-side execution

## 4. Handling Form Submission and Sending Data
### Use an event handler to:
- Prevent page reload
- Extract form data
- Create a product object
- Send data using the reusable POST function

```
async function addProductHandler(e) {
    e.preventDefault(); // Prevent page refresh

    const formData = new FormData(e.target);

    const product = {
        name: formData.get("name"),
        qty: formData.get("qty"),
        price: formData.get("price"),
    };

    const result = await addProduct(product);
    console.log(result);
}
```
