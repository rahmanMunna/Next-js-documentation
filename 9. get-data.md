# Documentation: Fetch API Integration in React/Next.js

## 📌 Overview
This documentation explains how to make a **GET request** using the `fetch()` API in a React/Next.js project.  
We will create a reusable function inside a **private `_lib` folder** to fetch product data from an API and then use it inside a component to display the results.

---

---

## ⚙️ Step 1: Create a Fetch Function
Inside the `_lib` folder, create a file named **`getAllProducts.tsx`**.

```tsx
// _lib/getAllProducts.tsx
export default async function getAllProducts() {
    const url = "http://localhost:2000/products";
    const result = await fetch(url);
    return result.json(); // returns a Promise resolved as JSON
}
```
🔑 Key Points
- fetch(url) makes a GET request to the given endpoint.
- result.json() parses the response into JSON format.
- Since this function is async, it returns a Promise.
👉 You must use await when calling it.

## ⚙️ Step 2: Use the Function in a Component : 
```
// components/Products.tsx
import getAllProducts from "../_lib/getAllProducts";

export default async function Products() {
    const products = await getAllProducts(); 
    // console.log(products) // Debugging: check fetched data

    return (
        <>
          {/* Design your UI here to display all product data */}
        </>
    );
}
```
🔑 Key Points
- Import the function from _lib.
- Use await getAllProducts() to resolve the Promise and get actual product data.
- The products variable will contain the JSON response from the API.
- You can now map over products to render UI elements.

- Here api is calling and resaolved in server side. No client side rendering.
- As it is server side rendering, we dont need to use `useEffect()` hooks as like react to call the api.
- In next js we can make any component async, as it is server side rendering.
