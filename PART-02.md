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

This tutorial is Part 02 of the series. It focuses on the design of the Nuxt storefront.

## Prerequisites

To follow along with the tutorial you need to have some knowledge of the following:
- Basic understanding of HTML, CSS, and JavaScript
- Basic understanding of Node.js and npm
- Basic understanding of the command line
- Knowledge of Vue and Nuxt is a bonus but not a requirement.
- Knowledge of Medusa is a bonus but not a requirement.

In addition to knowing these tools, your computer system should have the following packages installed:
- [Node.js](https://nodejs.org/en/download/) (v16 and above) 
- [PostgreSQL](https://www.postgresql.org/download/). Alternatively, you can create a free PostgreSQL database with a [Neon](https://console.neon.tech/signup) account. This tutorial will use a database created using Neon.
- yarn (optional)
- git (optional)

## Make the storefront layout

Before connecting the Medusa server with the storefront, you need to add some components and pages to the storefront. Open the storefront’s project `my-nuxt-storefront` in your preferred code editor.

You should see the following directories:

```bash
my-nuxt-storefront
├── components
├── .editorconfig
├── .eslintrc.js
├── .git
├── .gitignore
├── node_modules
├── .nuxt
├── nuxt.config.js
├── package.json
├── pages
├── README.md
├── static
├── store
├── windi.config.ts
└── yarn.lock
```

You will be focusing mainly on the `components` and `pages` directories to design the layout for the storefront.

## Components

Components are what make up the different parts of your page. They can be reused and imported into your pages, layouts, and even other components.

The storefront you are creating will have the following components:

- Logo
- Navbar
- Footer
- Product card

Go to the `components` directory and delete the default components that come with the Nuxt.js installation. Then add the following files.

### Logo 

Add `components/App/Logo.vue`.

```html
<template>
  <div class="h-16 flex items-center">
    <div class="ml-4 flex lg:ml-0 lg:mr-8">
      <nuxt-link to="/">
        <img class="h-8 w-auto" src="https://i.imgur.com/y3yU55v.png" alt=""/>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppLogo'
}
</script>
```

### Navbar

Add `components/App/Navbar.vue`.

```html
<template>
  <div class="sticky top-0 z-20">
    <header class="relative bg-white">
      <nav class="px-4 sm:px-6 lg:px-8 border-b border-ui-medium flex items-center justify-between">
        <div class="flex items-center">
          <app-logo />
          <div class="hidden lg:flex lg:items-center">
            <div class="hidden flex-grow items-center justify-center lg:flex text-sm font-medium">
              <nuxt-link
                to="/"
                class="block mt-4 mr-4 lg:inline-block lg:mt-0 text-gray-700 hover:text-gray-600 last:mr-0"
              >
                Home
              </nuxt-link>
              <nuxt-link
                to="/products"
                class="block mt-4 mr-4 lg:inline-block lg:mt-0 text-gray-700 hover:text-gray-600 last:mr-0"
              >
                Products
              </nuxt-link>
            </div>
          </div>
        </div>

        <div class="flex items-center justify-end">
          <div class="hidden lg:flex">
            <div class="inline-block relative text-left">
              <div>
                <button
                  class="inline-flex justify-center w-full px-4 py-2 bg-white text-sm font-medium text-gray-700 hover:text-gray-600"
                  type="button"
                >
                  USA / USD
                </button>
              </div>
            </div><div class="relative inline-block text-left">
              <div>
                <button
                  class="inline-flex justify-center w-full px-4 py-2 text-sm font-medium text-gray-700 hover:text-gray-600"
                  type="button"
                >
                  Account
                </button>
              </div>
            </div>
          </div><div class="relative inline-block text-left">
            <div>
              <button
                class="inline-flex items-center justify-center w-full py-2 bg-white text-sm font-medium hover:opacity-1/2"
                type="button"
              >
                <svg width="40" height="41" viewBox="0 0 40 41" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M14.9968 16.2273C14.9921 16.1189 14.9888 16.0004 14.9877 15.8734C14.9826 15.2497 15.0333 14.4053 15.2648 13.551C15.4962 12.6975 15.9164 11.8043 16.6719 11.123C17.4366 10.4333 18.5016 10 19.9419 10C21.3822 10 22.4472 10.4333 23.212 11.123C23.9674 11.8043 24.3877 12.6975 24.619 13.551C24.8506 14.4053 24.9012 15.2497 24.8961 15.8734C24.8951 16.0004 24.8917 16.1189 24.887 16.2273H27.8836C29.0776 16.2273 30.0056 17.2667 29.8708 18.4531L28.7344 28.4531C28.6196 29.4638 27.7644 30.2273 26.7472 30.2273H13.1366C12.1194 30.2273 11.2643 29.4638 11.1494 28.4531L10.013 18.4531C9.87822 17.2667 10.8062 16.2273 12.0002 16.2273H14.9968ZM23.8859 16.2273C23.8912 16.1186 23.8951 15.9971 23.8962 15.8652C23.9008 15.2957 23.8535 14.5493 23.6538 13.8126C23.454 13.0752 23.1098 12.3775 22.5422 11.8656C21.984 11.3622 21.1673 11 19.9419 11C18.7165 11 17.8999 11.3622 17.3416 11.8656C16.774 12.3775 16.4299 13.0752 16.23 13.8126C16.0303 14.5493 15.983 15.2957 15.9877 15.8652C15.9888 15.9971 15.9926 16.1186 15.9979 16.2273H23.8859ZM12.0002 17.2273H27.8836C28.4806 17.2273 28.9446 17.747 28.8772 18.3402L27.7408 28.3402C27.6834 28.8455 27.2558 29.2273 26.7472 29.2273H13.1366C12.628 29.2273 12.2004 28.8455 12.143 28.3402L11.0066 18.3402C10.9392 17.747 11.4032 17.2273 12.0002 17.2273ZM15.4874 20.0455C15.8388 20.0455 16.1237 19.7605 16.1237 19.4091C16.1237 19.0576 15.8388 18.7727 15.4874 18.7727C15.1359 18.7727 14.851 19.0576 14.851 19.4091C14.851 19.7605 15.1359 20.0455 15.4874 20.0455ZM25.0328 19.4091C25.0328 19.7605 24.7479 20.0455 24.3965 20.0455C24.045 20.0455 23.7601 19.7605 23.7601 19.4091C23.7601 19.0576 24.045 18.7727 24.3965 18.7727C24.7479 18.7727 25.0328 19.0576 25.0328 19.4091Z"
                    fill="black"
                  /></svg>
                <span>0</span>
              </button>
            </div>
          </div>
        </div>
      </nav>
    </header>
  </div>
</template>

<script>
export default {
  name: 'NavBar'
}
</script>
```

### Footer

Add `components/App/Footer.vue`.

```html
<template>
  <footer>
    <div class="bg-white px-4 pt-24 pb-4 sm:px-6 lg:px-8 border-t border-ui-medium flex items-center justify-between text-sm">
      <div class="flex items-center">
        <a class="mr-3 last:mr-0 text-ui-dark hover:text-gray-700" href="/">Create return</a>
        <a class="mr-3 last:mr-0 text-ui-dark hover:text-gray-700" href="/">FAQ</a>
        <a class="mr-3 last:mr-0 text-ui-dark hover:text-gray-700" href="/">Terms &amp; Conditions</a>
      </div>
      <div class="flex items-center">
        <a href="https://www.github.com/medusajs" class="mr-3 last:mr-0 text-ui-dark hover:text-gray-700">GitHub</a>
        <a href="https://www.twitter.com/medusajs" class="mr-3 last:mr-0 text-ui-dark hover:text-gray-700">Twitter</a>
        <a href="https://discord.gg/ruGn9fmv9q" class="mr-3 last:mr-0 text-ui-dark hover:text-gray-700">Discord</a>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter'
}
</script>
```

### ProductCard 

Add `components/ProductCard.vue`.

```html
<template>
  <div>
    <nuxt-link :to="`/products/${item.id}`">
      <div
        class="group relative"
      >
        <div class="w-full min-h-auto bg-gray-200 aspect-w-1 aspect-h-1 rounded-md overflow-hidden group-hover:opacity-75 lg:h-80 lg:aspect-none">
          <div class="w-auto h-full object-center object-cover bg-gray-100">
            <img
              alt=""
              :src="item.thumbnail"
            >
          </div>
        </div>
        <div class="mt-4 flex justify-between">
          <h3 class="text-sm text-gray-700 font-normal">
            {{ item.title }}
          </h3>
          <p class="text-sm font-semibold text-gray-900">
            from {{ lowestPrice.amount/100 }} {{ lowestPrice.currency_code.toUpperCase() }}
          </p>
        </div>
      </div>
    </nuxt-link>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    item: {
      type: Object,
      default () {
        return {
          id: 1,
          title: 'Kitchen Table',
          thumbnail: 'https://picsum.photos/600/600',
          variants: [{ prices: [{ amount: 0 }] }]
        }
      }
    }
  },
  computed: {
    lowestPrice () {
      const lowestPrice = this.item.variants.reduce((acc, curr) => {
        return curr.prices.reduce((lowest, current) => {
          if (lowest.amount > current.amount) {
            return current
          }
          return lowest
        })
      }, { amount: 0 })

      return lowestPrice || { amount: 10, currency_code: 'usd' }
    }
  }
}
</script>
```

## Pages

The `pages` directory contains your storefront views and routes. For this tutorial you will need only 3 pages:

- Home page
- Products page
- Product detail page

In the `pages` directory, open the `index.vue` file and replace the code as follows:

```html
<template>
      <div>
        <div class="bg-ui-light pb-12 lg:pb-0 w-full px-4 sm:px-6 lg:px-12">
          <div class="flex flex-col lg:flex-row items-center max-w-screen-2xl mx-auto">
            <div class="w-auto h-full object-center object-cover p-12">
              <img
                width="600"
                alt=""
                src="https://start.medusajs.com/static/9803c162c71fd1960d9d11253859c701/246b5/hero-merch.webp"
              >
            </div>
            <div>
              <h1 class="text-4xl">
                CLAIM YOUR MERCH
              </h1>
              <p class="mt-2 text-lg font-normal">
                Contribute to Medusa and receive free merch<br>as a token of our appreciation
              </p>
              <button class="btn-ui mt-4 min-w-full lg:min-w-0">
                Learn more
              </button>
            </div>
          </div>
        </div>

        <div
          v-if="products.length"
          class="container mx-auto px-8 py-16"
        >
          <div class="flex items-center justify-between mb-6">
            <p class="text-2xl font-semibold text-gray-700">
              Featured
            </p>
            <nuxt-link
              class="text-ui-dark flex items-center"
              to="/products"
            >
              <span class="mr-2 text-ui-dark">Browse all products</span>
              <svg
                width="16"
                height="8"
                viewBox="0 0 16 8"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path d="M15.3536 4.35355C15.5488 4.15829 15.5488 3.84171 15.3536 3.64645L12.1716 0.464466C11.9763 0.269204 11.6597 0.269204 11.4645 0.464466C11.2692 0.659728 11.2692 0.976311 11.4645 1.17157L14.2929 4L11.4645 6.82843C11.2692 7.02369 11.2692 7.34027 11.4645 7.53553C11.6597 7.7308 11.9763 7.7308 12.1716 7.53553L15.3536 4.35355ZM0 4.5H15V3.5H0V4.5Z" fill="#89959C" />
              </svg>
            </nuxt-link>
          </div>
          <div class="grid grid-cols-4 gap-8">
            <ProductCard
              v-for="product in products"
              :key="product.id"
              :item="product"
            />
          </div>
        </div>
      </div>
    </template>

    <script>
    export default {
      name: 'IndexPage',
        data () {
        return {
          products: [{
            id: 1,
            title: 'Kitchen Table',
            thumbnail: 'https://picsum.photos/600/600',
            variants: [{ prices: [{ amount: 0, currency_code: 'usd' }] }]
          }]
        }
      },
    }
    </script>

    <style>
      .btn-ui {
        @apply py-2 px-4 bg-ui-dark text-white text-sm font-medium rounded-md shadow;
        @apply focus:outline-none focus:ring-2 focus:ring-ui-dark focus:ring-opacity-75 disabled:bg-ui-medium;
      }
    </style>
```

This page will be the home for your storefront. It is composed of a hero, header, and a grid configured to show only four products. The only thing to do here once you connect the storefront to the Medusa server will be to put the `ProductCard` component in a `v-for` loop to display the products.

Now, you need to create a new directory called `products` which will hold the products page, `/pages/products/index.vue` and the product detail page `/pages/products/_id.vue`. Add the following code to these pages.

### Products page 

Add /pages/products/index.vue

```html
<template>
  <div class="container mx-auto p-8">
    <div class="w-full border-b border-ui-medium pb-6 mb-2 lg:mb-6 flex items-center justify-between">
      <h1 class="font-semibold text-3xl">
        All Products
      </h1>
    </div>

    <div
      v-if="products.length"
      class="grid grid-cols-4 gap-8 "
    >
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :item="product"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductsIndex',
    data () {
    return {
      products: [{
        id: 1,
        title: 'Kitchen Table',
        thumbnail: 'https://picsum.photos/600/600',
        variants: [{ prices: [{ amount: 0, currency_code: 'usd' }] }]
      }]
    }
  },
}
</script>
```

This page is similar to the home page but without the hero header. Here you will show a grid with all the products sent by the Medusa server.

### Product Detail page

Add `/pages/products/_id.vue`.

```html
<template>
  <div class="container mx-auto p-8">
    <div class="flex flex-col lg:flex-row">
      <div class="lg:w-3/5 lg:pr-14">
        <div class="flex">
          <div class="hidden lg:flex flex-col items-center mr-4">
            <div class="w-auto h-full object-center object-cover px-4 space-y-4">
              <img
                v-for="image in product.images"
                :key="image.id"
                width="150"
                alt=""
                :src="image.url"
                class="cursor-pointer"
                @click="imageToShow = image.id"
              >
            </div>
          </div>

          <div class="h-auto w-full flex-1 flex flex-col rounded-lg overflow-hidden">
            <div class="w-auto h-full">
              <div
                v-for="image in product.images"
                :key="image.id"
              >
                <div v-if="image.id === imageToShow">
                  <img
                    alt=""
                    :src="image.url"
                    class=" w-full"
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="mt-8 lg:mt-0 lg:w-2/5 lg:max-w-xl">
        <h1 class="font-semibold text-3xl">
          {{ product.title }}
        </h1>
        <p v-if="product.variants" class="text-lg mt-2 mb-4">
          {{ product.variants[0].prices[0].amount/100 }} {{ product.variants[0].prices[0].currency_code }}
        </p>
        <p v-else>
          10 USD
        </p>
        <p class="font-light">
          {{ product.description }}
        </p>
        <div v-for="option in options" :key="option.id" class="mt-6">
          <div class="text-sm">
            <p class="font-medium mb-2">
              {{ option.title }}
            </p>
            <div>
              <button
                v-for="value in option.values"
                :key="value.id"
                class="bg-ui-dark text-white inline-flex items-center justify-center rounded-sm text-xs h-12 w-12 mr-2 last:mr-0 hover:bg-ui-dark hover:text-white"
              >
                {{ value.value }}
              </button>
            </div>
          </div>
        </div>
        <div class="inline-flex mt-12">
          <button class="btn-ui mr-2 px-12">
            Add to bag
          </button>
          <div class="flex items-center rounded-md px-4 py-2 shadow">
            <button>–</button>
            <span class="w-8 text-center">1</span>
            <button>+</button>
          </div>
        </div>
        <div class="mt-12">
          <div class="border-t last:border-b border-ui-medium py-6">
            <h3 class="-my-3 flow-root">
              <button
                class="py-3 bg-white w-full flex items-center justify-between text-sm text-gray-400 hover:text-gray-500"
                type="button"
                @click="showDetails = !showDetails"
              >
                <span class="font-medium text-gray-900">Details</span>
                <span class="ml-6 flex items-center">
                  <span>—</span>
                </span>
              </button>
            </h3>
            <div v-if="showDetails" class="pt-6">
              <div class="space-y-4 text-ui-dark text-sm">
                <ul class="list-inside list-disc space-y-2">
                  <li>Weight: {{ product.weight ? `${product.weight} g` : 'Unknown' }}</li>
                  <li>Width: {{ product.width ? `${product.width} cm` : 'Unknown' }}</li>
                  <li>Height: {{ product.height ? `${product.height} cm` : 'Unknown' }}</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  data () {
    return {
      showDetails: false,
      imageToShow: 'default_image',
      product: {
        id: 1,
        title: 'Medusa Coffee Mug',
        description: 'Every programmer\'s best friend.',
        thumbnail: '',
        variants: [{ prices: [{ amount: 0, currency_code: 'usd' }] }],
        images: [
          { id: 'default_image', url: 'https://picsum.photos/600/400' },
          { id: 'another_image', url: 'https://picsum.photos/600/400?id=100' }
        ]
      }
    }
  },
  computed: {
    lowestPrice () {
      const lowestPrice = this.product.variants.reduce((acc, curr) => {
        return curr.prices.reduce((lowest, current) => {
          if (lowest.amount > current.amount) {
            return current
          }
          return lowest
        })
      }, { amount: 0 })

      return lowestPrice || { amount: 10, currency_code: 'usd' }
    },
    options () {
      if (this.product.options) {
        return this.product.options.map((option) => {
          option.values = option.values.reduce((acc, curr) => {
            if (!acc.find(val => val.value === curr.value)) {
              return [...acc, { ...curr }]
            }
            return acc
          }, [])

          return option
        })
      }
    }
  }
}
</script>
```

On this page, you will display all the information related to a specific product. For example, sizes, images, price, description, variants, etc...

> *NOTE:*
>
> *The three pages include a `product` object on the `data` function to showcase the design while there isn’t a server to send requests. Once you connect the storefront with the Medusa server, the data coming from the server will replace the data in the `product` object.*

## Layouts

Layouts are a great help when you want to have a basic structure for your Nuxt app. For example, a navbar and footer that will be shown on all the pages of the app. By default, a Nuxt project doesn't come with layouts, but it is easy to add them to your project.

To have a default layout on your storefront, create a `layouts` directory in the root of the project, and inside it, add a new file called `default.vue` with the following code:

```html
<template>
  <div class="min-h-screen flex flex-col">
    <app-navbar />

    <main class="flex-1">
      <Nuxt />
    </main>

    <app-footer />
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout'
}
</script>
```

Since the layout file was named `default.vue`, the layout will automatically be applied to all the pages on the storefront.

## Styling

Replace the content of `windi.config.ts` in the root of your Nuxt.js project with the following:

```ts
import { defineConfig } from '@windicss/plugin-utils'

export default defineConfig({
  /**
   * Write windi classes in html attributes.
   * @see https://windicss.org/features/attributify.html
   */
  attributify: true,
  theme: {
    extend: {
      fontSize: {
        '2xs': '0.5rem'
      },
      maxWidth: {
        '1/4': '25%',
        '1/2': '50%',
        '3/4': '75%'
      },
      maxHeight: {
        review: 'calc(100vh - 10rem)'
      },
      boxShadow: {
        DEFAULT:
          '0 2px 5px 0 rgba(60, 66, 87, 0.08), 0 0 0 1px rgba(60, 66, 87, 0.16), 0 1px 1px rgba(0, 0, 0, 0.12)',
        error:
          '0 2px 5px 0 rgba(255, 155, 155, 0.08), 0 0 0 1px rgba(255, 155, 155, 0.70), 0 1px 1px rgba(0, 0, 0, 0.12)'
      },
      colors: {
        green: {
          DEFAULT: '#56FBB1'
        },
        blue: {
          DEFAULT: '#0A3149'
        },
        ui: {
          light: '#F7F7FA',
          DEFAULT: '#EEF0F5',
          medium: '#D9DFE8',
          dark: '#89959C'
        }
      }
    }
  }
})
```

## Change the Default Port

Change the port where the storefront app runs by default from `3000` to `3333`. To do that, open the `nuxt.config.js` file and add the following right after the `ssr` property.

```js
server: {
  port: 3333
},
```

Test your Nuxt storefront.

```bash
yarn dev
```

Visit localhost:3333 in your browser.

![Nuxt Storefront with static data](https://res.cloudinary.com/craigsims808/image/upload/v1708771042/articles/medusa-nuxt/nuxt-storefront-static_rt6gou.png)

The storefront just shows static data for now. You will link the storefront with the Medusa server in the next part of the tutorial series.

## Conclusion

In this part of the tutorial, we designed the layout and components for the Nuxt storefront. We created components like the navbar, footer, product card, and pages for the home, products listing, and product details. We also configured layouts to provide a consistent structure across pages. We styled the components using the Windi CSS utility library and updated some configuration settings like changing the default port. 

By the end, we had a basic storefront design in place with static product data. In the next part, we will connect this Nuxt frontend to the Medusa backend to fetch and display real product information, transforming it into a fully functional ecommerce site.

## Resources
- [GitHub Repo](https://github.com/Marktawa/medusa-nuxt)
- [Source Code](https://github.com/Marktawa/medusa-nuxt/releases/tag/v2.0.0)

## Author

[Mark Munyaka](https://markmunyaka.com)

GitHub: [@Marktawa](https://github.com/Marktawa)
Twitter: [@McMunyaka](https://twitter.com/McMunyaka)

## Sponsor

Support my passion for sharing development knowledge by making a donation to my [**Buy Me a Coffee**](https://www.buymeacoffee.com/markmunyaka) account. Your contribution helps me create valuable content and resources. Thank you for your support!

[![Buy Me A Coffee Banner](https://res.cloudinary.com/craigsims808/image/upload/v1708089939/articles/test/buymeacoffee_lqmwjn.png)](https://www.buymeacoffee.com/markmunyaka)

[Buy Me A Coffee](https://www.buymeacoffee.com/markmunyaka)








