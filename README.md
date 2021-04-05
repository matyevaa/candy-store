# Shopping cart application with Redux and Emotion

### Assignment 4 for Advanced Web Development class at OSU instructed by professor R. Hess (2020).

The goal of this assignment is to use Redux to maintain the global state of an application.  You will specifically implement a basic shopping cart application for the "Penny Candy Store", an online store that sells penny candy.

Please refer to the demo below:

![Screen capture of full app demo](src/images/candy-store.gif)

# Application features

In addition to the basic Create React App code, there is a product data file in [`src/data/products.json`](src/data/products.json) and a custom React hook in [`src/hooks/useProducts.js`](src/hooks/useProducts.js) that simulates "fetching" those products from an API.

## 1. Display a list of all available products

The application you'll write will allow users to add products into a shopping cart and then to "buy" the products in their cart.  This, in turn will result in a change to the store's inventory of each product that was purchased.

The first task in the assignment is to display a list of all of the available products.  I'd encourage you to try to use the [`useProducts()` hook](src/hooks/useProducts.js) to "fetch" the products, but it's fine if you want to just `import` the JSON file directly.

Each product is comprised of several pieces of data:
  * `id` - A unique product ID
  * `name` - The name of the product
  * `price` - The price-per-unit of the product
  * `inStock` - The number of units of the product the store has in stock
  * `photoUrl` - A URL for an image of the product

To display the list of products, you should first add them to a Redux store.  The store should initially begin with an empty inventory, and products should be added via an action (e.g. `RECEIVE_PRODUCTS`).

Once the products are added to the store, you should use the store to display the list of products.  Each product item displayed in the list should have the following visual elements:
  * The name of the product.
  * The product image.
  * The price of a unit of the product.
  * The number of units in stock.
  * A button that says "add to cart".

Implement a distinct component to display each individual product.  You should also add some CSS to make this list relatively visually appealing.  The styling doesn't need to be super polished, but you should make your application look roughly like a regular online store.  For example, all of the product images displayed in the product list should be the same size.  You may choose how to implement this CSS.  For example, writing a simple CSS file is fine, or you can use Emotion (or another CSS-in-JS library, if you want to explore).

## 2. Add a shopping cart widget

Once your app can successfully display the list of products, you should add a shopping cart widget to the app.  Specifically, you should modify the app so that when the user enters a positive number of units for a specific product and clicks the "add to cart" button for that product, the specified number of units of that product are added to the shopping cart.  The data for the shopping cart should also be kept in the Redux store.

The shopping cart itself should be implemented as a distinct component, and visually, the shopping cart should look like one you might expect in a typical online store.  Specifically, it should list the products the user has added to the cart along with the total cost of all products.  Each product should be listed with the following information:
  * The name of the product
  * The price-per-unit of the product
  * The total number of units of the product added to the cart
  * The total cost of the units of the product (e.g. if Swedish Fish cost $0.01 each and the user has added 5 of them to their cart, the total cost of Swedish Fish is $0.05)

Like the product list, you should write CSS to make the shopping cart relatively visually appealing, though, again, high polish is not necessary here.

The shopping cart and the product list should interact in the following ways:
  * When the user clicks the "add to cart" button for a product and units of that product are added to the shopping cart, the same number of units should be deducted from the in-stock inventory of the product.  For example if the user enters a quantity of 5 Swedish Fish and clicks the "add to cart" button, the number of Swedish Fish in the cart should increase by 5, and the number of Swedish Fish in stock in the product list should decrease by 5.
  * If the user enters a quantity greater than the number of units in stock for a product and tries to add that quantity to their cart, they should be prevented from doing so.  Try to display an appropriate error to the user when this happens.
  * If a user adds all of the units of a given product to their cart, the "add to cart" button for that product should become disabled (to do this, you should just be able to add the [`disabled` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled) to the `<button>` element), and its text should change to "out of stock".

The shopping cart should also have the following features:
  * The shopping cart should be implemented so that it is initially hidden and is only displayed when the user clicks a button or link.  The text of that button/link should contain the number of distinct products in the cart (not the total number of items of the products).  For example, if the user has 40 Swedish Fish, 2 Tootsie Pops, and 10 Jolly Ranchers in their cart, the button/link should say something like "Cart (3)".  This displayed count should be derived from data in the Redux store.
  * There should be some mechanism that allows the user to remove a product from their cart (e.g. a "remove" button or link for each product in the cart).  If a product is removed from the user's cart, the appropriate number of units of that product should be added back to the in-stock inventory in the product list.
  * The shopping cart should contain a "checkout" button.  For this app, the "checkout" button should simply empty out the shopping cart (i.e. remove all products from it) *without* adding those products back to the in-stock inventory.

## Application styling

To accomplish some of the layout required in the description above, Emotion style has been written for this application.

## Working with this code

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).
Before running this app for the first time, make sure to run `npm install` to install needed dependencies. Then, to run the app and see it in your browser, you can run
```
npm start
```
This will run the app in the development mode, and it should automatically open [http://localhost:3000](http://localhost:3000) to view the app in your browser (though you can manually open that URL in your browser, too).
