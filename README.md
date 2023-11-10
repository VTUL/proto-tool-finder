This app allows for makerspaces to create a visual map of their tool cabinets using an SVG file in order to help users find tools and employees know where to restock tools that have been left out. It was created by the University Libraries at Virginia Tech.

To run this app, you will need to first clone the repo, and then open a bash window within the cloned folder.

*Note that you will need to have [Node.js](https://nodejs.org) installed.*

## Get started

Install the dependencies...

```bash
npm install
```

Once you have installed the dependencies, there are some changes you will need to make to the code.

1. First you'll want to add the url to your own inventory spreadsheet into the App.svelte file. We use a Google Sheet that has been published as a csv file.
2. You'll need to create an SVG map of your space. We've provided a sample in the folder called example.svg for you to use in creation of your own. Keep in mind that you'll need to set the ids and classes of the baskets or other areas you want to be shown on the map. If you change the name of the file, you'll also need to update that in the Map.svelte file.
3. In Footer.svelte, you'll need to update the text name of your space. You'll also need to add an svg file of your group's logo to the "common" folder in the app, or remove the img tag that displays the logo from Footer.svelte.
4. You can also make any other aesthetic changes to the app that you'd like. You can change the text that displays in the various areas, and most of the css can be found in global.css under the public folder, but some of the css is component specific and can be found in the appopriate .svelte file for the component.
5. In index.html in the public folder, you'll want to update the html title attribute for the page to reflect your space/service.


If you want to run the program locally for testing purposes, you can use:

```bash
npm run dev
```

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

## Deploying to the web

After running the build command, you can upload the "public" folder to any static hosting server and the app should operate.

## License

This project is offered under the MIT license.
