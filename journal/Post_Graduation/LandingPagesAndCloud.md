[]: # FILEPATH: LandingPagesAndCloud.md

# Landing Page Best Practices

## **Launching into Development via Github Pages**

* Name a repo ending in 'github.io', which automatically enables you to use github pages
* Clone the repo to your local machine
* Create an index.html file in the root of the repo
* Add the following code to the index.html file:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Landing Page</title>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```
  + Source code is *NOT* browser compatible! Index.html is a file that is automatically loaded by the browser when a user visits a website. It is the main file that contains the structure of the website. The `<!DOCTYPE html>` declaration defines the document to be HTML5. The `<html>` element is the root element of an HTML page. The `<head>` element contains meta information about the document. The `<title>` element specifies a title for the document. The `<body>` element contains the visible page content. The `<h1>` element defines a large heading. The `<h1>` element is the largest heading, and the `<h6>` element is the smallest heading. JUST LIKE when we first started the cohort.

* Commit the changes to the repo
* Push the changes to the main branch
* Go to the repo settings and scroll down to the GitHub Pages section
* Select the main branch and click save
* The site will be published at the following URL: https://your-username.github.io/your-repo-name/
* You can now add more files to the repo and link to them from the index.html file by using relative paths. For example, if you add a vue app to the repo, you can link to it from the index.html file like this:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Landing Page</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <div id="app"></div>
    <script src="vue-app.js"></script>
  </body>
</html>
```
* To make `.vue` files work, you need to use a bundler like Webpack to compile them into `.js` files. You can do this by having your `main.js` file and `registerGlobalComponents.js` file in the root of your repo like so:
<br>
main.js:
```js
import '@mdi/font/css/materialdesignicons.css'
import 'bootstrap'
import { createApp } from 'vue'
// @ts-ignore
import App from './App.vue'
import { registerGlobalComponents } from './registerGlobalComponents'
import { router } from './router'
import './utils/SocketProvider.js'

const root = createApp(App)
async function init() {
  await registerGlobalComponents(root)
  root
    .use(router)
    .mount('#app')
}
init()
```
registerGlobalComponents.js:
```js
export async function registerGlobalComponents(root) {
  const components = import.meta.glob('./components/**/*.vue', { eager: true })
  for (const fileName in components) {
    const component = components[fileName]
    const componentName = fileName
      .substring(fileName.lastIndexOf('/') + 1)
      .replace(/\.\w+$/, '')
    root.component(componentName, component.default)
  }
}
```
* You can then add a `.gitignore` file to the root of your repo to ignore the `node_modules` folder and other files that you don't want to be tracked by git. For example:
```
node_modules
.DS_Store
dist
```
* This will make your repo cleaner and faster to load. Add them to the `.gitignore` file and commit the changes to the repo.

## **Using Secret Keys in a GitHub Repo**
* In your github repo, go to the settings tab
* Click on the secrets tab
* Click on the new repository secret button
* Add a secret key and value
* You can then use the secret key in your code by using the following syntax in your .yml file:
```yml
jobs:
  build:
    runs-on: ubuntu-latest # The type of machine to run the job on
    steps: # The sequence of steps to run in the job
      - name: Checkout code # The name of the step. This is displayed in the GitHub Actions UI
        uses: xxxxxxxxxxxxxxxx@xx # The action to use or the name of the action in the repo. The action is the code that will be executed
      - name: Use Node.js # This example will use the Node.js version specified in the package.json file. If the version is not specified, it will use the latest version of Node.js
        uses: xxxxxxxxxxxxxxxxxx@xx # The action to use or the name of the action in the repo. The action is the code that will be executed
        with:
          node-version: '14'
      - name: Install dependencies # The name of the step. This is for clarity and is displayed in the GitHub Actions UI
        run: npm install # The command to run in the step. This is what will deploy the code.
      - name: Run tests # Again, for clarity
        run: npm test # The command to run in the step. This is what will deploy the code.
      - name: Deploy to GitHub Pages # The name of the action
        uses: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx@x.x.x # The action to use or the name of the action in the repo. The action is the code that will be executed
        with: # The input parameters for the action
          ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
          BRANCH: gh-pages # The branch to deploy to
          FOLDER: dist # The folder to deploy
```
To change a target branch, you can change the `BRANCH` value to the desired branch. To change the folder, you can change the `FOLDER` value to the desired folder:

## **Production Pull Requests**
* When you are ready to deploy your code to production, you can create a pull request from the main branch to the production branch by using the following steps:
  + Go to the main branch
  + Click on the pull request tab
  + Click on the new pull request button
  + Select the production branch as the base branch
  + Click on the create pull request button
  + Add a title and description to the pull request
  + Click on the create pull request button
  + You can then merge the pull request to deploy the code to production


## **Using a blob to upload images to a GitHub Repo**
* A good option (but not free) is using `Microsoft Azure Blob Storage`. This is a `cloud storage service` that is designed for:
  + Storing large amounts of unstructured data, such as text or binary data.
  + It is `highly scalable` and can be accessed from anywhere in the world.
  + It is also `highly available and durable`, with multiple copies of your data stored in different data centers.
  + Can be used for `storing large amounts of data, such as images, videos, and audio files`.
* Download the `Azure Tools` Extension for Visual Studio Code
* There are many ways you can `trigger these serverless functions`, such as:
  + Using an `HTTP trigger`, which is a function that is `triggered by an HTTP request`.
  + Using a `timer trigger`, which is a function that is `triggered on a schedule`.
  + Using a `blob trigger`, which is a function that is `triggered when a new blob is uploaded to a storage account`.
* You can use a function to call back to Auth0 to get the user's information and then use that information to `authorize the user` to access the blob storage by using the `Azure Blob Storage SDK`:
```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "AZURE_STORAGE_CONNECTION_STRING": "DefaultEndpointsProtocol=https;AccountName=youraccountname;AccountKey=youraccountkey;EndpointSuffix=core.windows.net",
    "AUTH0_DOMAIN": "yourauth0domain",
    "AUTH0_CLIENT_ID": "yourauth0clientid",
    "AUTH0_CLIENT_SECRET": "yourauth0clientsecret"
  }
}
```
* You can `process an http request` by using the following syntax:
<h3><b>Original Example</b></h3>

```js
const { app } = require('@azure/functions');

app.http('ImageSandwich', {
  methods: ['GET', 'POST'],
  authLevel: 'anonymous',
  handler: async (request, context) => {
    context.log(`http function processed a request for url: ${request.url}`);

    const name = (request.query.get('name') || await request.text() || 'World';

    return { body: `Hello, ${name}!` };
    )
  }
})
```


* Here is a more detailed example of how to process an `http request` by using the `Azure Blob Storage SDK` to upload an image to the blob storage:

<h3><b>Mick's Walkthrough Example</b></h3>

```js
import { app } from '@azure/functions';
import { Auth0Provider } from '@bcwdev/auth0provider';
import { multipart } from 'parse-multipart';
import { BlobServiceClient } from '@azure/storage-blob';

const { app } = require('@azure/functions');

app.http('ImageSandwich', {
  methods: ['POST'],
  authLevel: 'anonymous',
  handler: async (request, context) => {
  try {
    const audience = process.env.AUTH0_AUDIENCE;
    const domain = process.env.AUTH0_DOMAIN;
    const clientId = process.env.AUTH0_CLIENT_ID;
    Auth0Provider.configure({ audience, domain, clientId }); // Allows us to use the Auth0Provider to get the user's information

    const token = request.headers.get('Authorization'); // This is the token that is typically stored in the headers of our request

    const userInfo = await Auth0Provider.getUserInfo(token); // This will post the user's information to the console

    context.log(userInfo);

    const body = await request.arrayBuffer(); // This will get the body of the request and convert it to an array buffer or binary data. Which is what we need to upload the image to the blob storage to take out the base64 encoding
    const bodyBuffer = Buffer.from(body); // This will convert the array buffer to a buffer
    const boundary = request.headers.get('Content-Type'); // This will parse the boundary from the content type of the request
      context.log('boundary', boundary);

    const files = multipart.Parse(bodyBuffer, boundary); // This will parse the body of the request and get the files from it

    if (files.length >= 0) throw new Error('No files found in request'); // This will throw an error if there are no files in the request

    const file = files[0]; // This will get the first file from the files array
    const fileName = file.filename; // This will get the filename of the file
    const fileType = file.type; // This will get the content type of the file

    const KBSize = file.data.length / 1024; // This will get the size of the file in kilobytes

    // NOTE - You can now use the `Azure Blob Storage SDK` to upload the image to the blob storage:
    const blobStorage = BlobServiceClient.fromConnectionString(process.env.AzureWebJobsStorage); // This will create a new instance of the BlobServiceClient using the connection string from the environment variables
    const container = blobStorage.getContainerClient('images'); // This will get the container client for the images container

    const folder = userInfo.id; // This will create a folder with the user's id to store the images in
    const blockBlob = container.getBlockBlobClient(`${folder}/${fileName}`); // This will create a new block blob client for the file
    const blobOptions = { blobHTTPHeaders: { blobContentType: fileType, blobCacheControl: 'max' } }; // This will set the content type and cache control for the blob
    await blockBlob.upload(file.data, file.data.length, blobOptions); // This will upload the file to the blob storage. The options are important because they set the content type and cache control for the file, along with showing the user that the file has been uploaded and what the content type is.

    const jpgOptions = { blobHTTPHeaders: { blobContentType: 'image/jpg', blobCacheControl: 'max' } }; // This will set the content type and cache control for the jpeg image
    const webPOptions = { blobHTTPHeaders: { blobContentType: 'image/webp', blobCacheControl: 'max' } }; // This will set the content type and cache control for the webp image

    const jpgBlob = container.getBlockBlobClient(`${folder}/thumbnail/${fileName}`);
    await jpgBlob.upload(jpegImage, jpegImage.length, jpgOptions); // This will upload a jpeg image to the blob storage
    const webpBlob = container.getBlockBlobClient(`${folder}/webp/${fileName}`);
    await webpBlob.upload(webpImage, webpImage.length, webPOptions); // This will upload a webp image to the blob storage

    //If you want to establish a progress bar for how long it is taking to upload the image, you can use the following code:
    const onProgress = (progress) => {
      context.log(`Progress: ${progress.loadedBytes}/${progress.totalBytes}`); 
    };  // This will log the progress of the upload to the console. You can access it in your code by using the onProgress function like this: onProgress(progress)

    //To create a payload to send back to the client, you can use the following code:
    const payload = { fileName, fileType, url: blockBlob.url, fileSizeKB: KBSize, imageWidth, imageHeight }; // This will create a payload with the filename, content type, size, and url of the file

    return {
      body: JSON.stringify(payload), // This will send the payload back to the client as a JSON string
      headers: { 'Content-Type': 'application/json' } // This will set the content type of the response to application/json
    };

    } catch (error) {
      context.error(error);
      return {
        status: error.status || 400,
        body: '{ Bad Sandwich }: Not logged in'
      }
    }
  }
})

```


* Then under 'main' in your `package.json` file, you can add the following code so that Azure knows where to find your functions:
```json
"main": "src/functions/*.mjs",
```

* To configure your deployment source and upload local settings, you can right click on the `functions` folder and select `Deploy to Function App...` from the context menu. This will open the `Deploy to Function App` view, where you can select the function app you want to deploy to and configure the deployment source and local settings. You can also use the `Azure Functions` extension to deploy your functions to Azure. To do this, you can right click on the `functions` folder and select `Deploy to Function App...` from the context menu. This will open the `Deploy to Function App` view, where you can select the function app you want to deploy to and configure the deployment source and local settings.

* Before clicking the `Deploy` button, you can click the `View Output` button to see the output of the deployment process. This will show you the progress of the deployment and any errors that occur during the deployment process. Once the deployment is complete, you can click the `View Output` button. This will show you the output of the deployment process.

* Install `sharp` by running `npm i sharp` in the terminal. This will allow you to resize the image before uploading it to the blob storage. You can then use the following code to resize the image and much more before uploading it to the blob storage extremely easily:

```js
//Image Processing Example:
import sharp from 'sharp';

const imageBuffer = Buffer.from(file.data); // This will convert the file data to a buffer
const jpegImage = await sharp(imageBuffer) // This will create a new sharp image from the buffer
  .metadata()
  .then(({ width, height }) => {
    .jpeg({ quality: 80, chromaSubsampling: '4:4:4' }) // This will set the quality and chroma subsampling for the jpeg image
      return sharp(imageBuffer)
        .resize(Math.round(width * .25)) // This will resize the image to half its original size
        .toBuffer(); // This will convert the image to a buffer
    }
  );
```

* You can then use the `resizedImage` to upload the resized image to the blob storage. This will allow you to upload the image to the blob storage and then use the `resizedImage` to display the resized image on the client side.

* IMPORTANT! MICK HAS A STEP-BY-STEP README ON HOW TO PROPERLY EXECUTE