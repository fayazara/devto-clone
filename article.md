Let's clone dev.to with the actual dev.to api to get the articles.

I will be using Nuxt.js as the web framework and Tailwindcss for making the UI.

I am taking a different approach to write this post, I will keep writing as I code, so you might feel the article a little different. PS, I will be making only the Desktop version for now as the article might become very long, I will write about making this responsive, in a part 2 maybe, if people ask for it.

### 1. Setup a the project

Create a new nuxt project with the command `npx create-nuxt-app devto-clone` and make sure you select tailwindcss. Once done let's upgrade to tailwindcss v2 as most frameworks dont support PostCSS 8 yet so you need to install the Tailwind CSS v2.0 PostCSS 7 compatibility build for now as shown below.

Uninstall the @nuxtjs/tailwindcss modules with `npm uninstall @nuxtjs/tailwindcss tailwindcss` and then re install the dependencies along with **postcss7-compat** modules

```
npm install -D @nuxtjs/tailwindcss tailwindcss@npm:@tailwindcss/postcss7-compat @tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

This will install all the right dependencies for us to work with Tailwindcss v2.

More information on how to use Tailwind with Nuxt.js [can be found here](https://tailwindcss.com/docs/guides/nuxtjs).

Once your project is bootstrapped, make sure you delete all the boilerplate from the `pages/index.vue` and `layouts/default.vue`. Something like the below screenshot.

![Nuxt.js project](https://dev-to-uploads.s3.amazonaws.com/i/r8xd9ioj263wweqkoqnd.jpg)

### 2. Breaking down the layout of Dev.to

Well, one the top level dev.to has a layout what's popularly known as "The Holygrail Layout" - A three column layout with fixed content sidebars on either sides and a scrollable lazyloaded list of content in the middle.

![Site Breakdown](https://dev-to-uploads.s3.amazonaws.com/i/6d94pgw54tgggud2fbhi.jpg)

**Navbar**

The navbar has `position: fixed` and `display: flex` with the right content having `margin-left: auto`

We can also just do `justify-content: space-between`, but let's just do it the dev-to way.

**The Content Area**
This section is using `display: grid` with the middle section having a little more area than the others, can be done via tailwind grid utilities.

### Coding the Navbar

Make a component called `navbar.vue` and let's add a fixed header and put it in a container. I have also made 3 components to add the navbar elements.

{% gist https://gist.github.com/fayazara/da8377cd4fb953323dee38e1f87c765f %}

This will make the navbar look exactly like the dev to, here's the code for the individual components.

**Search.vue**

I have used a fixed width, which is not really a good practice, elements like these need to have a relative width to screen sizes, but just for the sake of this article, let's have a `w-96` class.

I have also used the `@apply` directive to extract tailwind's classed and made a custom class out of it, to all who say my html class keeps getting longer when using tailwindcss, this is what you do to keep your code clean.

{% gist https://gist.github.com/fayazara/90176b7db1e3977d7c3fb85d4f54ba53 %}

**Navbar Actions Component**

So, I have used the `ml-auto` class to keep the content pushed to the left and flex with the `space-x-4` class to add a little space between each of these elements inside.

I have also made use of svgbox api to get the icons.

{% gist https://gist.github.com/fayazara/236c389cec1ddac9173ea2de4492231c %}

The **logo.vue** is just svg inside a vue component.

This is how it looks like when rendered.
![Navbar](https://dev-to-uploads.s3.amazonaws.com/i/pbnfbatxicwc11jvz70y.jpg)

Now, let's do the dropdown on image hover, which shows the account options.

I have made use of the same concept of the dropdown from my previous article, which you can read [here](https://dev.to/fayaz/vue-tailwindcss-a-match-made-in-heaven-animated-dropdown-1nm).

Here's the code for the dropdown.

{% gist https://gist.github.com/fayazara/c417a1d61cf3cbd159ab27c8b8b52324 %}

Now that we have the navbar ready, let's go to the actual home page.

### Making the home page layout

So, I have decided to use css grid for this with a 4 columns layout and giving the center child a span of 2. Here's the blueprint of the layout. (I will be making a component for each column, the below code snippet is for your reference).

{% gist https://gist.github.com/fayazara/236c389cec1ddac9173ea2de4492231c %}

This code is all we need to have the layout like dev.to, it will generate the UI like below, note that I have added a `margin-top: 65px` as the height of the navbar is 65px exactly.

![The layout blueprint](https://dev-to-uploads.s3.amazonaws.com/i/fm4grrz0vzqkorkhcqri.jpg)

Okay, let's start coding the actual content into these placeholders.

### Making the left column

The left column has three sections, a menu, tags list, and a ad banner for the dev.to shop.

1. The First section in this column is a static list with some icons.
2. The second part is a list of tags, which I will pull from the dev.to api's tags endpoint, which you can find here [https://dev.to/api/tags](https://dev.to/api/tags)
3. The third one just a banner image for the shop.dev.to.

Here is the code for the left column, I have hardcoded the first section and I am pulling the tags from the above api and using the nuxt fetch method to load the data, thanks to this module, I can also show the loading states with `$fetchState.pending` and `$fetchState.error`

{% gist https://gist.github.com/fayazara/5e4167b2ec9a9093d83f2030905335fb %}

This is how it ended up looking.

![Layout with left Column](https://dev-to-uploads.s3.amazonaws.com/i/vp0j9yyls476vw4oazok.jpg)

Looks great actually.

### Making the right column

I won't be making the Hackathon listing, as when the time you're reading this, it might have been over. So, I will just code the Listing page, again we have a api for this [https://dev.to/api/listings](https://dev.to/api/listings), it returns more data than we need, which we won't be needing.

> PS the right column also shows some other things like news, help and discuss, for which I believe there's no api, so I will be skipping it for now, the code for this will be open source, if anyone wants to contribute to this example, please go ahead and submit a PR, will be happy to involve you.

Again, I used the nuxt's fetch and showting the listing data.

{% gist https://gist.github.com/fayazara/9d2783c5b320f39754c8dce7e3720abf %}

This is how it looks as of now
![Right Column](https://dev-to-uploads.s3.amazonaws.com/i/5p8anhmytzwyz3sfyx55.jpg)

### The posts section

To get the latest 3 posts, you can use this endpoint [https://dev.to/api/articles/](https://dev.to/api/articles/) and this is how the UI has turned out at the end.

![Final UI](https://dev-to-uploads.s3.amazonaws.com/i/eei16vv41mnx0cl6inrs.jpg)

Embedding code for all this might make it too hard to read right here in this post, so you can find the code for this on the github repo.

Here's the live demo -
Here's the github repo -

I am planning to write more content on Web, Javascript, CSS, Nuxt, Vue and many other things on how to build for the internet. If you like my content, please consider supporting by buying me coffee by clicking [here](https://fayazz.co/coffee).
