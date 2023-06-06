# Vue

## Week 6 Day 1 - Building out Initial <u>Server Side</u> Functionality

* Building your backend client
  + Run bcw i to install dependencies

  + Set up environment variables in .env backend

  + Start your server

  + Build out your first schema model

  + Build your time stamp

  + Build out your virtuals

  + Build out your first service layer

  + Make your first controller

  + Register it in DBContext within your DB folder

  + Run a sample test in postman (it will fail but you should see the route)

  + Find your bearer token in the network tab and your preview subtab

  + Copy and paste it into postman within the Variables tab

  + MAKE SURE you save right after this so it can store your token

  + Start with a post request to your first route so you can visualize something
  other than an empty array, as you would with a get request

  + You should come back with a 404, but it should pass an object as a test result response
  
  + Buiid your first post request within your controller {Example: .post('') this.create}
  
  + Also build out your first use case for your authorized user
  
  + Build your first async create function in your controller (BE SURE TO SET IT EQUAL TO THE CURRENT USER WITH CREATORID EQUAL TO THE USER ID)
  
  + Build out your first "create" async function in your service layer
  
  + Go into your controller. You can now write your first get requests
  
  + Be sure to add a colon in front of your first route parameter

  + Write an async function to go with it that will find the object by id in your controller
  
  + In the service layer, write an async function that will find the object by id as well. Use a find one method and pass in the id
  
  + Write your "get all" async function in your controller and service layer
  
  + If you're ever entrusted with an enum and forget to add it to your schema, you can add it now in your schema and it will update your database
  
  + MAKE SURE YOU ARE **POPULATING** YOUR CREATOR ID IN YOUR GET ALL ASYNC FUNCTION IN YOUR SERVICE LAYER
  
  + NOTE: "Archiving" is a common use case for a delete request. You can use a put request to change the status of an object to "archived" and then filter it out of your get all request
  
  + You can flip the bool in your schema by using the ! operator in your delete request

  + Which leads to the next step in your controller, which is to write your delete request like so: {Example: .delete('/:id') this.delete}

  + The async function within your controller should look like this:
  
  {Example: async delete(id) 
  {return await dbContext.YourSchema.findOneAndUpdate({ _id: id }, { isDeleted: true }, { new: true })}}
  
  + After that, go to your service layer and write your delete async function like so:
  
  + Example: 
  ```js
  async delete(id, userId) {
    return await dbContext.YourSchema.findOneAndUpdate({ _id: id, creatorId: userId }, { isDeleted: true }, { new: true })
    OR
    async delete(id, userId) {
      const banana = await this.findBananaById(albumId)
      if (!banana) {
        throw new Forbidden('Invalid Id')
      }
      album.archived = true
      await album.save()
      return album
    }
  }
  ```
  
  + Postman will probably make a get request to your delete request, but it should still pass the test
  
  + Although you could go in and add an edit request, you can technically now move on to the next step, which is to build out your first relationship! Woohoo!!!
  
  + MICK LEFT OUT 2 CHECKS THAT WE WILL NEED TO LOOK INTO FOR YOUR UPCOMING CHECKPOINT! 

  POSSIBLE LEFT OUT SCENARIOS? (1) CHECK FOR NULL AND (2) CHECK FOR EMPTY STRING
  
  + Build out the next schema. Remember to include the creatorId and the isDeleted bool along with timestamps and virtuals pertaining to the name of the reference
  
  + Add your schema object references to your DBContext

  + Continue by building out your next controller and service layer for your newly created schema
  
  + Your object will come back as undefined go back to your schema and build out your virtuals
  
  + The next step is to build out your first relationship. Go to your controller and build out your first post request. It will go in your controller like so and remember to return your res.send before your catch block like so: 
  ```js
  .post('')
  async create(req, res, next) {
    try {
      req.body.creatorId = req.userInfo.id
      const banana = await bananaService.create(req.body)
      res.send(banana)
    } catch (error) {
      next(error)
    }
  }
  ```
  
  + TEST YOUR POST REQUEST IN POSTMAN
  
  + Then run your first get request in your controller. It will look like this:
  ```js
  .get('/:id')
  async findAllBananasInObject(req, res, next) {
    try {
      const banana = await bananaService.getById(req.params.bananaId)
      res.send(banana)
    } catch (error) {
      next(error)
    }
  }
  ```
  
  + Then build it in your service layer like so:
  ```js
  async findAllBananasInObject(bananaId) {
    const banana = await dbContext.Banana.find({ bananaId: bananaId }).populate('creator', 'name picture')
    if (!banana) {
      throw new BadRequest('Invalid Id')
    }
    return banana
  }
  ``` 
  
  + After that, re-spin postman and test your get request

  + One you start your front-end, the first thing you should do ( when forking a project ), is to run npm i
  
  + Next, you should add the proper files into your env.js file
  
  + Start your client by spinning it up in your debug tab
  
  + Go into your server and grab your schema to build out your model

  ## Week 6 Day 2 - Building out Initial <u>Client Side</u> Functionality

  + <h2><u>**Day 2 - Building out the Client**</u></h2>
  
  + In your model, you will need to add the creator, creatorId and the id of the object you are referencing
  
  + **NOTE:** You can add a new profile in this layer by adding a new profile to your model
  
  + In your model under your initial constructor, build out the new profile like so:
  ```js
    export class Profile {
      constructor(data) {
        this.name = data.name
        this.picture = data.picture
        this.id = data.id
      }
    }
  ```
  + This allows you to have some privacy in your front-end by only showing the name and picture of the user, while keeping the id and other information private. Here is an example of what all of your code should look like:
  ```js
  export class Album {
    constructor(data) {
      this.title = data.title
      this.description = data.description
      this.creatorId = data.creatorId
      this.creator = data.creator
      this.id = data.id
    }

    export class Profile {
      constructor(data) {
        this.name = data.name
        this.picture = data.picture
        this.id = data.id
      }
    }
  }
  ```
  
  + Now you can create your next model. Here is an example using the word "picture"
  ```js
  export class Picture {
    constructor(data) {
      this.title = data.title
      this.description = data.description
      this.creatorId = data.creatorId
      this.creator = new Profile(data.creator)
      this.id = data.id
    }
  }
  ```
  
  + Build your service layer. Here is an example of what it should look like for "pictures":
  ```js
  import { AppState } from '../AppState'
  import { api } from './AxiosService'

  class PicturesService {
    async getAllPictures() {
      const res = await api.get('api/pictures')
      AppState.pictures = res.data.map(p => new Picture(p))
    }
  }

  export const picturesService = new PicturesService()
  ```
  
  + Next, build your controller. Here is an example of what it should look like for "albums" on your server side:
  ```js
  async getAlbums() {
    try {
      await albumService.getAlbums()
    } catch (error) {
      Pop.error(error.message)
      logger.error('Failed to get albums', error)
    }
  }
  ```
  + Go into your devtools and check your network tab to see if your get request is working
  
  + Build your service function for albums. Here is an example of what it should look like:
  ```js
  async getAlbums() {
    const res = await api.get('api/albums')
    logger.log('[SHOW ME THE ALBUM DATA]'res.data)
    AppState.albums = res.data.map(a => new Album(a))
    logger.log('[SHOW ME THE ALBUM OBJECT]'AppState.albums)
  }
  ```
  
  + Save your album object to your AppState and then go into your devtools and check your network tab to see if your get request is working in your console.

  + Next, go to your vue page for your album and write your computed function. Here is an example of what it should look like:
  ```js
  computed: {
    albums() {
      return 
      albums: computed(() => {AppState.albums})
    }
  }
  ```
  
  + Add raw data to the page with curly braces and wrapping your album within it inside of your first template.
  
  + Next, build a skeleton mock wrapped in a div that is "container-fluid". An example of what it should look like is below:
  ```html
  <template>

    <div class="container-fluid">

      <section class="row">
        <div class="col-md-3">
          <h1>Albums</h1>
          <div class="border-danger border-end elevation-5">
            <img class="img-fluid" src="example-img.com" alt="image">
            <div class="text-center">
              <p>Album Title</p>
              <p>Album Content</p>
            </div>
          </div>
        </div>
      </section>

      <section class="row">
        <div class="col-md-3">
          <h1>Albums</h1>
          <div class="border-danger border-end elevation-5">
            <img class="img-fluid" src="example-img.com" alt="image">
            <div class="text-center">
              <p>Album Title</p>
              <p>Album Content</p>
            </div>
          </div>
        </div>
      </section>

      <section class="row">
        <div class="col-md-3">
          <h1>Albums</h1>
          <div class="border-danger border-end elevation-5">
            <img class="img-fluid" src="example-img.com" alt="image">
            <div class="text-center">
              <p>Album Title</p>
              <p>Album Content</p>
            </div>
          </div>
        </div>
      </section>

    </div>
  ```

  + After you build out your visible skeleton mock, you can now build out your v-for loop. Here is an example of what it should look like:

  ```html
  <template>

    <div class="container-fluid">

      <section class="row">
        <div class="col-md-3" v-for="album in albums" :key="album.id">
          <h1>Albums</h1>
          <div class="border-danger border-end elevation-5">
            <img class="img-fluid rounded-top" src="example-img.com" alt="image">
            <div class="text-center">
              <p>Album Title</p>
              <p>Album Content</p>
            </div>
          </div>
        </div>
      </section>

    </div>
  ```
  
  + The v-for statement should look like this:
  ```html
  <div class="col-md-3" v-for="a in albums" :key="a.id">
    <AlbumCard :album="a" />
  ```
  + Set up your prop in your AlbumCard component. Here is an example of what it should look like:
  ```js
  props: {
    album: { type: Album, required: true }
  }
  ```
  
  + This directly references the album object in your vue page 

  + Go back to your AlbumCard.vue and build out your props. Here is an example of what it should look like:

  ```html
  <template>
    <div class="card shadow elevation-5">
      <img class="card-img-top" :src="album.coverImg" :alt="album.title" >
      <div class="card-body">
        <h5 class="card-title">{{ album.title }}</h5>
        <p class="card-text">{{ album.description }}</p>
        <p class="card-text">
          <small class="text-muted">Last updated 3 mins ago</small>
        </p>
      </div>
    </div>
  </template>
  ```
  
  + Add CSS to make your card a uniform size like so:
  ```css
  .card {
    width: 16rem;
    height: 10vh;
    
  }
  ```
  
  + To write your CSS, write it in your assets folder. Make sure you don't have any spaces in your CSS file. If you do, it will not work.
  
  + To set a background image, you can use the following code in html and css:
  ```html
  <div class="card bg-img">
  ```
  ```css
  .bg-img {
    width: 16rem;
    height: 10vh;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-image: url(examle-img.com);
  }
  ```
  + To add a keyframe in your background image in vue, you can do so using the following processes:
  ```css
  .bg-img {
    width: 16rem;
    height: 10vh;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-image: url(examle-img.com);
    animation: bg-img 10s infinite;
    object-fit: contain;
  }

  @keyframes bg-img {
    0% {
      background-image: url(example-img.com);
    }
    50% {
      background-image: url(example-img.com);
    }
    100% {
      background-image: url(example-img.com);
    }
  }
  ```
  
  + For your keyframe to work, you need to add the following files:

  ```css
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');
  ```
  
  + You can also add a robust hover effect to your card like so:

  ```css
  .card:hover {
    transform: scale(1.1);
    transition: 0.5s;
    opacity: 0.8;
  }
  ```

  + Create a new endpoint in your router.js by adding the following code:

  ```js
  {
    path: '/albums/:id',
    name: 'AlbumDetails',
    component: loadPage('AlbumDetails')
  }
  ```

  + Bring it into your template with example text between your template tags.
  
  + Wrap it with a router-link tag like so:

  ```html
  <router-link :to="{ name: 'AlbumDetails', params: { id: album.id } }">
    <div class="card shadow elevation-5">
      <img class="card-img-top" :src="album.coverImg" :alt="album.title" >
      <div class="card-body">
        <h5 class="card-title">{{ album.title }}</h5>
        <p class="card-text">{{ album.description }}</p>
        <p class="card-text">
          <small class="text-muted">Last updated 3 mins ago</small>
        </p>
      </div>
    </div>
  </router-link>
  ```
  + If you check your vueTools tab within your devTools, you should see your router-link tag.
  
  + Your route should now be linked to your album details page. You can now build out your album details page with a script like so:
    
    ```js
    <script>
    import { reactive } from 'vue'
    import { useRoute } from 'vue-router'
    import { albumsService } from '../services/AlbumsService'
    import { logger } from '../utils/Logger'

    export default {
      setup() {
        const route = useRoute()
        const state = reactive({
          album: {}
        })

        async function getAlbum() {
          try {
            const albumId = route.params.id
            AppState.album = await albumsService.getAlbumById(albumId)
          } catch (error) {
            logger.error('Failed to get album', error)
          }
        }

        async function getAlbumById() {
          try {
            logger.log('[GET ALBUM BY ID]', route.params.id]')
            await albumsService.getAlbumById(route.params.id)
          } catch (error) {
            logger.error('Failed to get album', error)
          }
        }

        async function getPictureByAlbumId() {
          try {
            const albumId = route.params.id
            logger.log('[GET PICTURE BY ALBUM ID]', albumId)
            await picturesService.getPictureByAlbumId(albumId)
          } catch (error) {
            logger.error('Failed to get picture', error)
          }
        }

      onMounted(() => {
        getAlbum()
        getAlbumById()
        getPictureByAlbumId()
      })

        return {
          
        }
      }
    }
    </script>
    ```
  
  + This grabs the album by its ID, it's pictures, and its creator.
  
  + Grab the ID from the URL to send off the request to the server.

  + Build your albumService layer out furthermore like so:

  ```js
  async getAlbumById(albumId) {
    const res = await api.get('api/albums/' + albumId)
    logger.log('[GET ALBUM BY ID]', res.data)
    AppState.activeAlbum = new Album(res.data)
    return AppState.activeAlbum
  }
  
  async getPicturesByAlbumId(albumId) {
    const res = await api.get('api/albums/' + albumId + '/pictures')
    logger.log('[GET PICTURES BY ALBUM ID]', res.data)
    AppState.pictures = res.data.map(p => new Picture(p))
  }
  ```
  
  + Add your activeAlbum and picture objects to your AppState like so:

  ```js
  export const AppState = reactive({
    account: {},
    profile: {},
    albums: [],
    activeAlbum: {},
    album: {},
    pictures: [],
    picture: {}
  })
  ```
  
  + Build your picturesService layer out furthermore like so:

  ```js
  async getPicturesByAlbumId(albumId) {
    AppState.pictures = []
    const res = await api.get('api/pictures/' + albumId)
    logger.log('[GET PICTURE BY ID]', res.data)
    AppState.pictures = new Picture(res.data)
    return AppState.pictures
  }
  ```

  + Be SURE that you are importing your necessary files into your AlbumDetails.vue page like so:

  ```js
  import { reactive, onMounted } from 'vue'
  import { useRoute } from 'vue-router'
  import { albumsService } from '../services/AlbumsService'
  import { picturesService } from '../services/PicturesService'
  import { logger } from '../utils/Logger'
  import { AppState } from '../AppState'
  import { Album } from '../models/Album'
  import { Picture } from '../models/Picture'
  ```
  
  + Start building out your next template in your AlbumDetails.vue page like so:

  ```html
  <template>

    <div class="container-fluid">

      <section class="row">
        <div class="col-md-3">
          <h1>Albums</h1>
          <div class="border-danger border-end elevation-5">
            <img class="img-fluid" :src="album.coverImg" :alt="album.name">
            <div class="text-center">
              <p>Album Title</p>
              <p>Album Content</p>
            </div>
          </div>
        </div>
      </section>

    </div>

  </template>
  
  + Next, place card image in your page vue page like so:

  ```html
  <template>

    <div class="container-fluid">

      <section class="row">
        <div class="col-md-3" v-for="a in albums" :key="a.id">
          <PictureCard :picture="picture" />
          </div>
        </div>
      </section>

    </div>
  
  + Bind your picture to your script layer of your page vue like so:
  
    ```js
    <script>
    import { reactive, onMounted } from 'vue'
    import { useRoute } from 'vue-router'
    import { albumsService } from '../services/AlbumsService'
    import { picturesService } from '../services/PicturesService'
    import { logger } from '../utils/Logger'
    import { AppState } from '../AppState'
    import { Album } from '../models/Album'
    import { Picture } from '../models/Picture'

    export default {
      setup() {
        const route = useRoute()

        async function getAlbum() {
          try {
            const albumId = route.params.id
            AppState.album = await albumsService.getAlbumById(albumId)
          } catch (error) {
            logger.error('Failed to get album', error)
          }
        }

        async function getAlbumById() {
          try {
            logger.log('[GET ALBUM BY ID]', route.params.id]')
            await albumsService.getAlbumById(route.params.id)
          } catch (error) {
            logger.error('Failed to get album', error)
          }
        }

        async function getPictureByAlbumId() {
          try {
            const albumId = route.params.id
            logger.log('[GET PICTURE BY ALBUM ID]', albumId)
            await picturesService.getPictureByAlbumId(albumId)
          } catch (error) {
            logger.error('Failed to get picture', error)
          }
        }

      onMounted(() => {
        getAlbum()
        getAlbumById()
        getPictureByAlbumId()
      })

        ****** return {
          album: computed(() => { AppState.album }),
          pictures: computed(() => { AppState.pictures }),
        } ******
      }
    }
    </script>
    ```

  + The computed function brings elements in from your AppState to your vue page and binds them to your script layer.
  
  + The next step here would be to crate an album
  
  + Next is building a form for your album with a modal. The step by step process to ensure your modal imports correctly are the following procedures:
  
  + 1) you need to import your modal into your AlbumDetails.vue page like so:
  
  ```js
  import { Modal } from 'bootstrap'
  ```

  + 2) Next, you need to add the following code to your AlbumDetails.vue page:
  
  ```js
  <script>
  import { Modal } from 'bootstrap'
  import { reactive, onMounted } from 'vue'

  export default {
    setup() {
      const modalElement = ref(null)
      const modal = ref(null)

      onMounted(() => {
        modal.value = new Modal(modalElement.value)
      })

      return {
        modalElement,
        modal
      }
    }
  }

  </script>
  ```
  
  + 3) Next, you need to add the following code to your AlbumDetails.vue page:
  
  ```html
  // This is the button that will open your modal
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
    Launch demo modal
  </button>
  ```
  
  + 4) Next, use a slot to place your modal in your AlbumDetails.vue page:
  
  ```html
  <slot>
    // This is your modal content
  </slot>

  + 5) add your <Modal /> and it's id like so:

  ```html
  <Modal id="targetModal">
    // This is your modal content
  ```
  + 5) Target your modal by changing the data-bs-target and the id to the same name like so:
  
  ```html
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#targetModal" id=targetModal>
  ```

  + 6) Inject your modal template you've created by doing the following:

  ```html
  <template>

    <Modal id="targetModal">
      <!-- Modal template content (from your modal slot within your Modal.vue component) -->
    </Modal>

  </template>
  ```

  + **NOTE: You can reuse a modal by the same ID name and data-bs-target name by using slots.**
  
  + 7) You can build out your robust and professionally developed form by using the following code:
  
  ```html
  <template>

    <Modal id="targetModal">

      <form class="form-group" @submit.prevent="createAlbum">
        <div class="form-group">
          <label for="title"> {{ editable.title }} </label>
          <input type="text" class="form-control" id="title" v-model="editable.title" placeholder="Enter title">
        </div>
        <div class="form-group">
          <label for="description"> {{ editable.description }} </label>
          <input type="text" class="form-control" id="description" v-model="editable.description" placeholder="Enter description">
        </div>
        <div class="form-group">
          <label for="coverImg"> {{ editable.coverImg }} </label>
          <input type="text" class="form-control" id="coverImg" v-model="editable.coverImg" placeholder="Enter cover image">
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>

    </Modal>
  ```

  + 8) Make your script layer to your form like so:

  ```js
  <script>

  export default {
    setup() {
      const editable = ref({})

      const modal = ref({})

      onMounted(() => {
        modal.value = new Modal(editable.value),
      })

      return {
        editable,
        modal
      }
    }
  }
  ```
  + 9) Your modal form should now be stored within your vueTools tab in your devTools.

  + 10) Write out your createAlbum function in your controller layer like so:

  ```js
  async createAlbum() {
    try {
      const formData = editable.value
      const album = await albumService.createAlbum(formData)
    } catch (error) {
      logger.error(error)
      Pop.toast(error.message, 'error')
    }
  }
  ```
  
  + 11) Now you need to go into your album service layer to create your album like so:

  ```js
  async createAlbum(formData) {
    const res = await api.post('api/albums', formData)
    logger.log('[CREATING THE ALBUM DATA]', res.data)
    return res.data
    logger.log('[CREATING THE ALBUM OBJECT]', AppState.albums)
  }
  ```

  + 12) To ensure the button can only open and show when the user is logged in, you can use the following code:

  ```html
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#targetModal" id=targetModal v-if="user.id">
  </button>
  ```
  
  + 13) Add a computed to your script for your user like so:

  ```js
  album: computed(() => { AppState.album})
  ```
  
  + 15) To add a option to select different editable values to your form, you can change your editable values within your script layer like so:

  ```js
  const editable = ref({
    
  })
  ```
  
  + 16) It is written into your form like so with select tags:
  
  ```html
  <select class="form-select" aria-label="Default select example" v-model= >
    <option selected>Open this select menu</option>
    <option value="cats">Cats</option>
    <option value="pugs">Pugs</option>
    <option value="technology">Technology</option>
  </select>
  ```
  ( Feel free to add more editable values to your form for however many fixed values you would like assigned to a selectable tag with options. )

  + 17) Now you must create the instance for your modal so that it won't be targeted for a "missing backdrop" error and allow it to be closable, you can do this by adding the following code to your AlbumDetails.vue page:

  ```js
  Modal.getOrCreateInstance(#targetModal).hide()
  ```
  
  + 18) Add a router const to your createAlbum function within your form.vue like so:

  ```js
  const router = useRouter()
  ```
  
  + 19) vAttach the router to your createAlbum function like so:

  ```js
  async createAlbum() {
    try {
      const formData = editable.value
      const newAlbum = await albumService.createAlbum(formData)
      router.push({ 
        name: 'AlbumDetails', 
          params: { id: newAlbum.id }
      })

    } catch (error) {
      logger.error(error)
      Pop.toast(error.message, 'error')
    }
  }
  ```
  
  + 20) If something did not import correctly, it is likely that we did not establish an Elvis Operator. To do this, you can add the following code to your form.vue page:

  ```html
  <div class="form-group">
    <label for="title"> {{ editable?.title }} </label>
    <input type="text" class="form-control" id="title" v-model="editable.title" placeholder="Enter title">
  </div>
  <div class="form-group">
    <label for="coverImg"> {{ editable?.coverImg }} </label>
    <input type="text" class="form-control" id="coverImg" v-model="editable.coverImg" placeholder="Enter cover image">
  </div>
  ```
  
  + **NOTE: An easier way to complete this without an Elvis Operator, replace it in the top of your template with a "v-if" call like so:**

  ```html
  <form v-if="editable">
  ```
  
  + 21) Add your album to your page.vue from your form.vue like so:

  ```html
  <AlbumForm v-if="editable" :editable="editable" @submit.prevent="createAlbum" />
  ```
  
  + **REMEMBER FOR YOUR MODAL ATTRIBUTE NAMING CONVENTIONS, YOU KEEP YOUR ID AS THE SAME NAME, BUT CHANGE THE NAME OF YOUR DATA-BS-TARGET LIKE SO:**

  ```html
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#targetModalForPictures" id=targetModalForAlbums v-if="user.id">
  ```

  + 22) If your form is not injecting into your modal, be sure your slot is in the right place. It should be placed in your AlbumDetails.vue page like so:

  ```html
  <template>

    <div class="container-fluid">

      <section class="row">
        <div class="col-md-3">
          <h1>Albums</h1>
          <div class="border-danger border-end elevation-5">
            <img class="img-fluid" :src="album.coverImg" :alt="album.name">
            <div class="text-center">
              <p>Album Title</p>
              <p>Album Content</p>
            </div>
          </div>
        </div>
      </section>

    </div>

    <Modal id="targetModal">
      <AlbumForm v-if="editable" :editable="editable" @submit.prevent="createAlbum" />
    </Modal>

  </template>
  ```
  
  + 23) If your backdrop is still not defined, import it into your ref like so:

  ```js
  const modal = ref({
    backdrop: true
  })
  ```
  
  + 24) If something in your form is broken, it will make your modal fail. Be sure to check all of your form naming conventions - as well as your form values - to ensure that they are all correct.
  
  + 25) <h5>***Now your modal should be working correctly!!! Woohoo!!! You can now add a picture to your album!!!***</h5
  
  + Write out your async function to create a picture within your album in your controller layer like so:

  ```js
  async function createPicture() {
    try {
      const formData = editable.value
      const newPicture = await pictureService.createPicture(formData)
    } catch (error) {
      logger.error(error)
      Pop.toast(error.message, 'error')
    }
  }
  ```
  + Now write out your function in your service layer like so:

  ```js
  async createPicture(formData) {
    const res = await api.post('api/pictures', formData)
    logger.log('[CREATING THE PICTURE DATA]', res.data)
    return res.data
    logger.log('[CREATING THE PICTURE OBJECT]', AppState.pictures)
  }
  ```

  + **BE SURE TO ASSIGN YOUR ALBUM ID.** You can achieve this by adding the following code in the top of your script tag:

  ```js
  const route = useRoute()
  ```
  
  + Now your function should look like this in your controller layer:

  ```js
  async function createPicture() {
    try {
      const formData = editable.value
      formData.albumId = route.params.id
      const newPicture = await pictureService.createPicture(formData.albumId)
      bootstrap.getOrCreateInstance('#targetModalForPictures').hide()
      editable.value = {}
    } catch (error) {
      logger.error(error)
      Pop.toast(error.message, 'error')
    }
  }
  ```
  
  + You should now be receiving your object data.
  
  + Save the information to your AppState like so:

  ```js
  async createPicture(formData) {
    const res = await api.post('api/pictures', formData)
    logger.log('[CREATING THE PICTURE DATA]', res.data)
    AppState.pictures = res.data.map(p => new Picture(p))
    logger.log('[CREATING THE PICTURE OBJECT]', AppState.pictures)
  }
  ```
  
  ## Week 6 Day 2 - Continuing to build out <u>Server Side</u> Functionality

  + Once you switch back to your server side, be sure to respin your server in your Debug tool tab in vsCode.
  
  + Create your next model for your picture like so:

  ```js
  export const collaboratorSchema = new Schema(

    const ObjectId = Schema.Types.ObjectId

    {
      albumId: { type: ObjectId, ref: 'Album', required: true },
      accountId: { type: ObjectId, ref: 'Profile', required: true }
    },
    { timestamps: true, toJSON: { virtuals: true } }

    CollaboratorSchema.virtual('album', ) {
      accountId: {
        localField: 'albumId',
        ref: 'Album',
        foreignField: '_id',
        justOne: true
      }
    }

    Collaborvirtuals.virtual('profile', ) {
      : {
        localField: 'accountId',
        ref: 'Account',
        foreignField: '_id',
        justOne: true
      }
    }
  )
  ```
  
  + Next, mold out your information into your dbContext file like so:

  ```js
  import mongoose from 'mongoose'
  import { AccountSchema } from '../models/Account'
  import { AlbumSchema } from '../models/Album'
  import { CollaboratorSchema } from '../models/Collaborator'
  import { PictureSchema } from '../models/Picture'
  import { ValueSchema } from '../models/Value'

  class DbContext {
    Values = mongoose.model('Value', ValueSchema);
    Account = mongoose.model('Profile', AccountSchema);
    Albums = mongoose.model('Album', AlbumSchema);
    Collaborators = mongoose.model('Collaborator', CollaboratorSchema);
    Pictures = mongoose.model('Picture', PictureSchema);
  }
  ```

  + Build out your constructor, super and methodology inside of your controller layer like so:

  ```js
  import { dbContext } from '../db/DbContext'
  import { BadRequest } from '../utils/Errors'


  export class CollaboratorsController extends BaseController {
    constructor() {
      super('api/collaborators')
      this.router
        .get('', this.getAll)
        .get('/:id', this.getById)
        .post('', this.create)
        .delete('/:id', this.delete)
    }
  }

  async createCollaborator(req, res, next) {
    try {
      req.body.accountId = req.userInfo.id
      const collabData = req.body
      const collaborator = await collaboratorsService.createCollaborator(collabData)
      res.send(collaborator)
    } catch (error) {
      next(error)
    }
  }
  ```

  + Build out your service function to your collaborators service layer like so:

  ```js
  import { dbContext } from '../db/DbContext'
  import { BadRequest } from '../utils/Errors'

  class CollaboratorsService {

    async createCollaborator(collabData) {
      const collab = await dbContext.Collaborators.create(collabData)
      await collab.populate('profile album')
      return collab
    }
  }

  export class collaboratorsService = new CollaboratorsService()
  ```
  ```
  
  + Go into postman and test your new endpoint with a getter to see if the necessary data draws from your database.
  
  + All your tests should pass at this point. If not check your spelling and naming conventions.
  
  + Build out the next async functions within your controller like so:

```js
async findAlbumCollaborators(req, res, next) {
  try {
    const collaborators = await collaboratorsService
    .findAlbumCollaborators(req.params.id)
    res.send(collaborators)
  } catch (error) {
    next(error)
  }
}
```

  + Write those functions to continue within your service layer like so:

  ```js
  async findAlbumCollaborators(albumId) {
    const collaborators = await dbContext.Collaborators
    .find({ albumId }).populate('profile')
    return collaborators
  }
  ```

  + Next, go into your account controller and add the collaborator endpoint in your constructor on the back-end like so:
  
  ```js
  this.router
    .get('/collaborators', this.getCollaboratorsByAccountId)
  ```
  
  + Write out a function in your account controller like so:
  
  ```js
  async getCollaboratorsByAccountId(req, res, next) {
    try {
      const accountId = req.userInfo.id
      const collaborators = await collaboratorsService
      .getCollaboratorsByAccountId(accountId)
      res.send(collaborators)
    } catch (error) {
      next(error)
    }
  }
  ```
  
  + Now build that function out as a continuance within your account service layer like so:
  
  ```js
  async getCollaboratorsByAccountId(accountId) {
    const collabs = await dbContext.Collaborators
    .find({ accountId }).populate('album')
    return collabs
  }
  ```
  
  + At this point in testing your endpoints in postman, you should be able to see your collaborators in your database.
  
  + Write your next function to get the collaborators ONLY that are collaborating in your controller layer with you like so:
  
  ```js
  async getCollabs(req, res, next) {
    try {
      const userId = req.userInfo.id
      const collaborators = await collaboratorsService
      .getCollabs(accountId: userId)
      res.send(collaborators)
    } catch (error) {
      next(error)
    }
  }
  ```

  + Next, add it into your service layer like so:

  ```js
  async getCollabs(userId) {
    const collabs = await dbContext.Collaborators.find
    (filter).populate('album profile')
    return collabs
  }
  ```
  
  + Add a delete function in your controller layer like so:
  
  ```js
  async deleteCollaborator(req, res, next) {
    try {
      const collabId = req.params.collabId
      const userId = req.userInfo.id
      const message = await collaboratorsService
      .deleteCollaborator( collabId, userId)
      res.send(collaborator)
    } catch (error) {
      next(error)
    }
  }
  ```

  + Next, build that function out completely in your service layer like so:

  ```js
  async deleteCollaborator(collabId, userId) {
    const collab = await dbContext.Collaborators
    .findById(collabId).populate('album profile')

    if (!collab) {
      throw new BadRequest('Invalid Id')
    }
    if (userId !== collab.accountId) {
      throw new BadRequest('You are not the owner')
      await collab.remove()
      return `collaboration between ${collab.profile.name} and ${collab.album.title} has been closed.`
    }
  }
  ```
  
  ## Week 6 Day 2 - <u>Server Side</u> **STRETCH GOALS**

  ###*<u>Get Albums with Collab Counts</u>*

  + **NOTE: Bird Brain is a good reference to dive deeper into this strech goal and what it requires**
  
  + Build out your schema virtual to support your collab count like so:

  ```js
  AlbumSchema.virtual('memberCount', {
    localField: '_id',
    ref: 'Collaborator',
    foreignField: 'albumId',
    count: true
  })
  ``` 
  
  + Next, build out your function in your controller layer like so:

  ```js
  async getAlbumsCollabCount(req, res, next) {
    try {
      const albums = await albumsService.getAlbumsCollabCount()
      res.send(albums)
    } catch (error) {
      next(error)
    }
  }
  ```
  
  + After that, complete your async function within your service layer like so:
  
  ```js
  async getAlbumsCollabCount() {
    const albums = await dbContext.Albums.find()
    .populate('profile').populate('memberCount')
    return albums
  }
  ```
  
  + Add the property of 'memberCount' to your async functions within your service layer that require a count like so:
  
  ```js
  async getAlbumById(albumId) {
    const album = await dbContext.Albums.findById(albumId)
    .populate('album').populate(path: 'memberCount', path: 'profile')
    return album
  }
  ```

  + OR
  
  ```js
  async getAlbumById(albumId) {
    const album = await dbContext.Albums.findById(albumId)
    .populate('album').populate( accountId: accountId )
    return album
  }
  ```

  + To add a collaborator for the project in postman, they can sign in and select a new bearer token. Then, they can add the albumId and accountId to the body of the request like so ( **THIS IS <u>*NOT*</u> RECOMMENDED!!!** ) :

  ```js
  {
    "albumId": "60b9b0b3b3b3b3b3b3b3b3b3",
    "accountId": "60b9b0b3b3b3b3b3b3b3b3b3"
  }
  ```
  
  + To properly validate your schema against these restrictions, we added the necessary code to our schema already to protect against these issues arising.
  
  ## Week 6 Day 2 - Back to the <u>Client Side</u>

  + **ADDING A BUTTON BY FILTERING OUT THE ARRAY**
  
  + Add a ref to your script layer like so:

  ```js
  const filter = ref('')
  ```
  
  + Add that to your ***return*** of your script layer like so:
  
  ```js
  return {
    filter
  }
  ```

  + To change the value of your filter, you can add the following code to your template layer like so:

  ```html
  <button type="button" class="btn btn-outline-light w-25 mx-2" @click="filterBy=''"></button>
  <button type="button" class="btn btn-outline-light w-25 mx-2" @click="filterBy='animals'">Animals</button>
  <button type="button" class="btn btn-outline-light w-25 mx-2" @click="filterBy='games'">Games</button>
  <button type="button" class="btn btn-outline-light w-25 mx-2" @click="filterBy='books'">Books</button>
  <button type="button" class="btn btn-outline-light w-25 mx-2" @click="filterBy='misc'">Misc</button>
  ```
  
  + Be sure to **import** your ref into your script layer like so:
  
  ```js
  import { ref } from 'vue'
  ```

  + After that, apply some logic to your computed in your *return* under *filterBy* like so:

  ```js
  computed(() => {
    filterBy
    if (filterBy.value == '' {
      return AppState.albums //if no filter...this returns ALL albums
    }
    return AppState.albums.filter(a => a.category === filterBy.value)
  })
  ```
  
  + **Playing with your server side many-to-many relationships**
  
  + To hit the endpoint of all of the albums that you are a collaborator on. go into your auth service to retrieve the account from your database or any other information that belongs to them like so:

  ```js
  async getCollabsByAccountId() {
    const res = await api.get('account')
    AppState.account = new Account(res.data)
  }
  ```

  + Making this request within your AuthService ensures that you do not have to make this request every time you need to access the account information.
  
  + Create your service for your collaborators like so:

  ```js
  async getCollabsByAccountId() {
    const res = await api.get('account/collaborators')
    logger.log('[GETTING COLLABORATORS BY THEIR ACCOUNT ID]', res.data)
    AppState.myCollabs = res.data.map(c => new Collaborator(c))
  }
  ```
  
  + If you get a 404 error, it is likely that you did not add the endpoint to your account controller like so:
  
  ```js
  this.router
    .get('/collaborators', this.getCollabsByAccountId)
  ```
  
  + Add the collaborators you are collaborating with to your AppState:

  ```js
  collaborators: [],
  ``` 

  + Add the information into your details page.
  
  + Create your model for your collaborators:
    
    ```js
    export class Collaborator {
      constructor(data) {
        this.id = data.id
        this.albumId = data.albumId
        this.accountId = data.accountId
        this.album = new Album(data.album)
        this.account = data.account
        this.profile = new Profile(data.profile)
      }
    }
    ```
  
  + Write out the next function for your collab model in your service layer like so:

  ```js
  async getCollabsByAccountId() {
    const res = await api.get('account/collaborators')
    logger.log('[GETTING COLLABORATORS BY THEIR ACCOUNT ID]', res.data)
    AppState.myCollabs = res.data.map(c => new Collaborator(c))
  }
  ```

  + For the time being, this will stay as an empty array until you add the collaborators to your AppState.
  
  + Next, get your *memberCount* drawn by adding them to your controller layer like so ( **NOTE: ADD THE ROUTER INTO YOUR SCRIPT TAG SO YOU CAN ENACT ROUTE.PARAMS.ID** ):

  ```js
  async getAlbumsCollabCount() {
    try {
      const albumId = route.params.id
      const albums = await albumsService.getAlbumsCollabCount(albumId)
      res.send(albums)
    } catch (error) {
      next(error)
    }
  }
  ```
  
  + Add this to your service layer like so:

  ```js
  async getAlbumsCollabCount(albumId) {
    const res = await api.get(`api/albums/${albumId}/collaborators`)
    logger.log('[GETTING COLLABORATORS BY THEIR ALBUM ID]', res.data)
    AppState.albums = res.data.map(a => new Album(a))
  }
  ```
  
  + Add your "collabs" to your AppState like so:

  ```js
  myCollabs: [],
  ```
  
  + You should be reading an error in devTools that "id is not defined". To fix this, you can add the following code to your collaborator model like so:

  ```js
  export class Collaborator {
    constructor(data) {
      this.id = data.id
      this.albumId = data.albumId
      this.accountId = data.accountId
      this.album = new Album(data.album) || null
      this.account = data.account
      this.profile = new Profile(data.profile) || null
    }
  }
  ```
  
  + If you're still getting ID reading as undefined, go back into your ***SERVER-SIDE SERVICE LAYER*** and add the following code to your service layer like so as a **DOUBLE POPULATION**
    
    ```js
    async getAlbumsCollabCount(albumId) {
      const albums = await dbContext.Albums.findById(albumId)
      .populate('profile').populate('memberCount')
      return albums
    }
    ```
  
  + If that doesn't fix the issue, you need to add secondary models ***under your Collab model*** like so:
  
  ```js
  export class Collab {
    constructor(data) {
      this.id = data.id
      this.albumId = data.albumId
      this.accountId = data.accountId
      this.album = new Album(data.album) || null
      this.account = data.account
      this.profile = new Profile(data.profile) || null
    }
  }

  export class AlbumMember extends Collab {
    constructor(data) {
      super(data)
      this.profileId = data.profile.id
      this.name = data.data.profile.name
      this.picture = data.profile.picture
    }
  }

  export class CollabingAlbum extends Collab {
    constructor(data) {
      super(data)
      this.title = data.album.title
      this.coverImg = data.album.coverImg
    }
  }
  ```

  + **NOTE: THIS IS FOR A FUTURE SUBJECT. YOU <u>DO NOT</u> NEED TO DO THIS FOR YOUR CHECKPOINT. IT IS BEST TO WAIT UNTIL WE START GOING OVER THIS MATERIAL IN THE NEXT 1-2 WEEKS**
  
  + Draw an image for each of the member of your profiles within your neccessary details page like so:

  ```html
  <div class="col-md-3">
    <div class="card">
      <img v-for="c in collabs" :key="id" class="card-img-top" :src="collab.profile.picture" alt="Card image cap">
      <div class="card-body">
        <h5 class="card-title">{{ collab.profile.name }}</h5>
        <p class="card-text">{{ collab.profile.email }}</p>
        <p class="card-text">{{ collab.profile.picture }}</p>
      </div>
    </div>
  </div>
  ```
  
  + In order to be able to add functionality to a button that allows you to become a collaborator of an album, write an @click function on your button like so:

  ```html
  <button type="button" class="btn btn-outline-light w-25 mx-2" @click="addCollab(album.id)">Add Collaborator</button>
  ```
  
  + Build out the function within your controller layer like so:

  ```js
  async addCollab(albumId) {
    try {
      const albumId = route.params.id
      const collab = await collaboratorsService.addCollab(albumId)
      logger.log('[ADDING COLLABORATOR]', collab)
      }
    } catch (error) {
      logger.error(error)
    }
  }
  ```
  
  + Add the functionality of your async to your service layer like so:

  ```js
  async addCollab(albumId) {
    const res = await api.post(`api/collabotors/, ${albumId}`)
    logger.log('[ADDING COLLABORATOR]', res.data)
    AppState.collaborators.push(new Collaborator(res.data))
  }
  ```
  
  + To add a button that toggles if you aren't a collaborator, you can add the following code to your template layer like so:

  ```html
  <button v-if="isCollaborator" type="button" class="btn btn-dark w-25 mx-2" @click="removeCollab(albumId)">Add Collaborator
  </button>
  <button v-else> type="button" class="btn btn-outline-light w-25 mx-2" @click="removeCollab(albumId)">Remove Collaborator</button>
  ```

  + Create your own computed that will read as true or false for whether or not the collaborator is in the collaborator's array like so:

  ```js
  return {
    isCollaborator: computed(() => AppState.collabs.find(c => c.accountId == AppState.user.id)),
  }
  ```
  
  + Write the function to remove the collaborator that is attached as an @click to your button by doing the following in your controller layer:
  
  ```js
  async removeCollab(albumId) {
    try {
      if (await Pop.confirm) {
      const collab = AppState.collaborators.find(c => c.account.id == AppState.account.id)
      }
      const collabId = collab.id
      await collaboratorsService.removeCollab(collabId)
      logger.log('[REMOVING COLLABORATOR]', collab)
      }
    } catch (error) {
      logger.error(error)
    }
  }
  ```
  
  + **BE SURE** that you added and imported your *route* into your script section of your code like so:

  ```js
  import { computed, ref, useRoute } from 'vue'

  const route = useRoute()
  ```

  + Add the functionality of your previous async function into your service layer like so:

  ```js
  async removeCollab(collabId) {
    const res = await api.delete(`api/collaborators/${collabId}`)
    logger.log('[REMOVING COLLABORATOR]', res.data)
    AppState.collabs = AppState.collabs.filter(c => c.id !== collabId)
  }
  ```

  + To add a button with the functionality to *archive* an entire album, you can add the following code to your template layer like so:

  ```html
  <button v-if="album.creatorId" type="button" class="btn btn-outline-light w-25 mx-2" @click="archiveAlbum(albumId)">Archive Album</button>
  ```
  
  + Add the functionality into your computed with the value of "user" like so:

  ```js
  return {
    user: computed(() => AppState.user),
  }
  ```
  
  + To write the async for this function, here is an example of what you could do to make this happen:

  ```js
  async archiveAlbum(albumId) {
    try {
      if (await Pop.confirm) {
      await albumsService.find(a => a.id == albumId)
      }
      const albumId = album.id
      await albumsService.archiveAlbum(albumId)
      logger.log('[ARCHIVING ALBUM]', album)
      }
    } catch (error) {
      logger.error(error)
    }
  }
  ```

  + Write the previous controller async function to your service layer like so:

  ```js
  async archiveAlbum(albumId) {
    const res = await api.delete(`api/albums/${albumId}`)
    logger.log('[ARCHIVING ALBUM]', res.data)
    AppState.albums = AppState.albums.filter(a => a.id !== albumId)
  }
  ```
  
  + Add myCollabs to the computed array of your script tag like so:

  ```js
  myCollabs: computed(() => AppState.myCollabs),
  ```

  + You can add the the activation to your album card like so:

  ```html
  <div v-for="c in myCollabs" :key="c.id"
  <AlbumCard :album="c.album" 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 

  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 
  
  + 