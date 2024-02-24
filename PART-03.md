# Building an ecommerce store using Nuxt and Medusa

![Article Cover](https://res.cloudinary.com/craigsims808/image/upload/v1708526494/articles/medusa-nuxt/medusa-nuxt-cover-2_gvincb.png)

## Introduction

[Nuxt](https://nuxt.com/) is a meta-framework built on top of [Vue.js](), a JavaScript library. It features SSR, SSG, SEO, File-System routing, Caching etc. It can be used to build ecommerce storefronts.

[Medusa](docs.medusajs.com) is a toolkit for developers to create digital commerce applications. It uses a Node.js backend with the core API, plugins, and modules installed through npm.

In this project, you will learn how an ecommerce store can be built using Nuxt for the frontend and Medusa for the backend. To do that, first, you will create a Nuxt project and set a few components, pages and layouts. Then, you will link the Nuxt project with a Medusa server to get the store products and display them on the home page including a product's page, and a product detail page.

- [Part 01: Setup and Installation](https://github.com/Marktawa/medusa-nuxt-article)
- [Part 02: Storefront Design](https://github.com/Marktawa/medusa-nuxt-article/PART-02.md) 
- [Part 03: Link Server to Storefront](https://github.com/Marktawa/medusa-nuxt-article/PART-03.md):
- Part 04:

This tutorial is Part 03 of the series. It focuses on the initial configuration to link the Nuxt storefront with the Medusa server.

## Configure Nuxt Storefront URL

To link the Medusa server with the Nuxt storefront, first, open up your Medusa project, `my-medusa-store` in your IDE, then open the `.env` file where all your environment variables are set up.

Add the variable `STORE_CORS` with the value of the URL where your storefront will be running. Remember that you changed the default port on the storefront, therefore the URL is `http://localhost:3333`.

```
STORE_CORS=http://localhost:3333
```

After this, your Medusa server will be ready to receive a request from your storefront and send back responses if everything works as expected.

### Testing connection with Medusa server

To list the products on the home page, you need to test whether you can send requests from your storefront to the Medusa server and receive data to display on the frontend.

Change the base URL for the `axios` module that you’ll use to make the requests to the server.

Open the `nuxt.config.js` file in `my-nuxt-storefront` and look for the `axios` property. Change the `baseURL` property to match the URL of the medusa server.

```js
axios: {
  baseURL: 'http://localhost:9000/'
},
```

To fetch data from the API, this tutorial uses the `fetch` function that Nuxt.js offers as part of the core.

Open the file `/pages/index.vue` and add the `fetch` function in the script section:

```js
async fetch () {
    try {
      const { products } = await this.$axios.$get('/store/products')
            console.log(products)
      this.products = products
    } catch (e) {
      // eslint-disable-next-line no-console
      console.log('The server is not responding')
    }
  }
```

This function receives just one parameter `$axios` which is a service that allows making an HTTP request to the Medusa server. So, inside the function, a request is sent to the endpoint `/store/products` to obtain the list of products from the Medusa server. Then, the list of products is returned.

To test this out, start your Medusa server and Nuxt.js dev server.

Visit localhost:3333 in your browser and open the Developer Tools. You must see a list of products in the console.

### Display Products on the Home Page

Next, let's render the products from the Medusa server on the storefront **Home** page. 

Update the `fetch` function in `/pages/index.vue`:

```js
async fetch () {
    try {
        const { products } = await this.$axios.$get('/store/products')
        this.products = products.splice(0, 4)
    } catch(e) {
        // eslint-disable-next-line no-console
        console.log('The server is not responding')
  }
}
```

With this update, product data from the server replaces the hardcoded `products` array on the **Home** page.

The `v-for` applied on the `ProductCard` iterates the `products` array and passes to the component, as a `prop`, a product with all the [properties specified on the Medusa API](https://docs.medusajs.com/api/store/product) for that endpoint.

Refresh the storefront **Home** page.

![Storefront Home page with list of products](storefront-home.png)

### Display Products on the Products Page

In the navigation bar, there is a "Products" link. Clicking on it redirects you to the **Products** page, where currently only one static product is displayed. Let's rectify this so that all the products from your Medusa server are shown on the page.

Open the `/pages/products/index.vue` file, go to the `script` section and add the following `fetch` function:

```js
async fetch () {
  try {
    const { products } = await this.$axios.$get('/store/products')
    this.products = products
  } catch (e) {
    // eslint-disable-next-line no-console
    console.log('The server is not responding')
  }
}
```

Visit localhost:3333/products in your browser.

![Storefront Products page with list of products](storefront-products.png)

### Display Product Details

The final page to update is the **Product Detail** page. Clicking on any product on either the **Home** page or the **Products** page redirects you to the product's detail page, where currently no details are displayed. To fix this, you need to request specific product information from the Medusa server to display all relevant details.

Open the file `/pages/products/_id.vue` and add the following `fetch` function:

```js
async fetch () {
  try {
    const { product } = await this.$axios.$get(`/store/products/${this.$route.params.id}`)
    this.product = product
    this.imageToShow = this.product.images[0].id
  } catch (e) {
    // eslint-disable-next-line no-console
    console.log('The server is not responding')
  }
},
```

Click on any product now, and you’ll see all details rendered on the page.

![Storefront Product Details page](storefront-product-details.png)

That's it for now!

## Conclusion

In this tutorial, we learned how to link a Nuxt storefront with a Medusa ecommerce backend. We configured the Medusa server to accept requests from the Nuxt app's URL, tested the connection, and fetched product data from the Medusa API. We then displayed the products on the home page, products page, and product details page of the Nuxt storefront. 

By following this approach, we can build a fully functional ecommerce site using the powerful capabilities of Nuxt for the frontend and the flexibility and scalability of Medusa for the backend. This integration allows developers to create customized ecommerce experiences while leveraging existing tools and libraries.

## Resources
- [GitHub Repo](https://github.com/Marktawa/medusa-nuxt)
- [Source Code](https://github.com/Marktawa/medusa-nuxt/releases/tag/v3.0.0)

## Author

[Mark Munyaka](https://markmunyaka.com)

GitHub: [@Marktawa](https://github.com/Marktawa)
Twitter: [@McMunyaka](https://twitter.com/McMunyaka)

## Sponsor

Support my passion for sharing development knowledge by making a donation to my [**Buy Me a Coffee**](https://www.buymeacoffee.com/markmunyaka) account. Your contribution helps me create valuable content and resources. Thank you for your support!

[![Buy Me A Coffee Banner](https://res.cloudinary.com/craigsims808/image/upload/v1708089939/articles/test/buymeacoffee_lqmwjn.png)](https://www.buymeacoffee.com/markmunyaka)

[Buy Me A Coffee](https://www.buymeacoffee.com/markmunyaka)
