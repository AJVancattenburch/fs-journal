# **JS Frameworks**

# *Day 1*
* Gregslist
  + In using Vue, there are no controllers, they are instead called "pages"
  + You will write your "controller functions" within the script tag of your HomePage.vue
  + Style ( CSS ) is also writtin within HomePage.vue
  + "Components folder" serve as blocks or chunks of reusable code
  + In your router.js, instad of mounting views and controllers there, we mount page components.
  + App.Vue is seen as the "top level hierarchy." You could not access any other pages or components without this file. Your ```<router-view />``` is where you your pages draw everything from "router.js".
  + Anything you want hard coded to the DOM regardless of what page you are on, do that in the App.Vue file.
  + <b>Veet</b> compiles all of your front-end js code.
  + In Vue, <b>reactives</b> are a way for setting up an "appState.on" and "appState.emit" by working inherently with the observer pattern. We no longer have to worry about writing out listeners/emitters as Vue handles that intelligence for you.
  + To communicate with the appState we use <b>computed</b>'s which is the equivalent to "appState.on."  It is our way of pulling in and listening to our active data.

  ## <u>Example of button functionality using "v-" tag attributes and ":disabled"</u> ##
  ```html
  <!-- NOTE Example 1: Increasing increment -->
  <!-- NOTE Example 2:  -->
  <!-- NOTE Example 3:  -->
  <!-- NOTE "number" is a banana word here -->
  <div>
    <h1>
      {{number}}
    </h1>
    <!-- NOTE "@" is the new replacement for "on" in Vue
    For example, "@click" is the new "onclick" -->
    <!-- NOTE you can invoke or not invoke your "@click" here -->
    <button class="btn btn-warning" @click="incrementNumber()">
      Increment
    </button>
  </div>

  <!-- NOTE only render the 'logged in' button if there is an account -->
  <!-- <button class="btn btn-success" v-if="account.id">Logged In</button> -->
  <!-- NOTE this is v-bind (shorthand is the '.') says add the disabled attribute if there is no account logged in -->
  <button class="btn btn-danger" :disabled="!account.id">Not Logged In</button>
  <button class="btn btn-success">Logged In</button>

  <!-- NOTE user example below (account example above) -->
  <button class="btn btn-danger" :disabled="!account.id">Not Logged In</button>
  <button class="btn btn-success" v-if="user.id">Logged In</button>
  ```

  ```js
  import { computed } from 'vue';
  import { AppState } from'../AppState.js';
  export default (await import('vue')).defineComponent({
    setup() {
      //NOTE this is where private functions go
      //NOTE you can this if this as similar to when we write functions outside of the controller class
      return {

          incrementNumber() {
            logger.log('increasing the number!')
            //NOTE when manipulating the AppState, good practice with MVC would be to move this to the service layer
            AppState.number++
          }
        //NOTE if you want to access a method or a variable from your template, those will be declared here
        account: computed(() => AppState.account),
        user: computed(() => AppState.user),
        number: computed(() => AppState.number)
      }
    }
  })
  ```
  + An empty object will always read as "true" in a true false statement.
  + The vue tab in your devTools allows you to click and highlight your view components to be able to debug and centralize issues as an itemized view.
  + There is a multitude of sub-tabs with details on each property.
  + If you need account or user details: from your network tab, see there is missing information, then go back into your vue tab in devTools and look in your appState.
  + <b>Difference between account and profile:</b> There will only ever be ONE account (you), while profiles are everybody else (not you).
  + STRETCH GOAL EXAMPLE:
  ```js
  //NOTE this is called inheritance. Essentially saying that Account will have everything that profile does - and then some

  //STUB PROFILE DATA
  export class Account extends Profile {
    constructor(data) {
      super(data)
      this.email = data.email
    }
  }

  //STUB MODEL DATA
  //NOTE This is unnecessary, but provides more intellisense when accessing properties on the 'creator' because it is mapped
  this.creator = new Profile(data.creator)
  ```
  + 
  + 
  + 

  <br><br>

* ## <u>Steps</u> ##
  + Go into env.js and change route to what it is supposed to be
  + Re-login to your account.
  + Go to router.js and build new endpoint for project (e.g. path: '/cars' name: 'Cars' component: loadPage('CarsPage'))
  + Make a new CarsPage.vue
  + Use the snippet provided by instructor to build out page component quickly.
  + Type out a test example of text in your "```<template> tag```".
  + Go to Navbar Component. Use ```<router-link>``` as reference.
  + We talk to the router when we want to be sent somewhere else within the view page of the Vue application.
  + In your router link, write where you want to go (e.g. ```<router-link>Cars</router-link>```)
  + To not break the page with a router link, previously establish where the ":to=" route is (e.g. ```:to="{name:'Cars'}"```).
  + Go back to your CarsPage.vue and establish your next step or private function in your script tag.
  + This is written as a async "try-catch" function.

  ## <u>Example:</u> ##
  ```js
  export default (await import ('vue')).defineComponent({

  setup() {
    async getCars() {
    try {
      logger.log('getting cars')
      await carsService
    } catch (error) {
      Pop.error(error.message)
      logger.log(error)
    }
  }

  //NOTE this onMounted says run whatever block of code is inside it as soon as the page/components 'mounts' or renders
  //NOTE this is similar to calling a function/method in the constructor of a controller
  onMounted(() => {
    getCars()
  })

  return {
    cars: computed(() => AppState.cars)
  };
  }
  })
  ```
  + NOTE: Service layer is still written the same as we wrote service layers in the MVC pattern.
  + You may have to get used to writing your own imports in the CarsPage.vue layers.
  + Build your service layer async function response, then send it back into the AppState.
  + Create your model.
  + Copy your object path in devTools and use it as a template reference in your model layer.
  + Make sure to reference and notate your creator information in your model
  + If something is coming in as an ISOstring, if you map it within your model with a date constructor, you can use all the Date methods to change the value.
  + Define your @type parameter and object of  in your AppState
  + Create the new instance by mapping it in your service layer async function.
  + Make your 'car' template inside of a ```<template>'[YOUR TEMPLATE GOES HERE]'</template>``` tag within your "App.vue" file.
  + To grab a URL to paste in as your image source, you can go into your devTools, right click, and select the option "Copy String Content".
  + You can further edit your CSS in your templates in your "style tag" within the same file.
  + You need to throw in an elvis operator in your template so it doesn't read your template without reading what you have defined in your "script tag".

  ## <u>Example:</u> ##
  ```html
  <h1>{{c?.model}}</h1>
  ```

  + If you want to reuse a template, use a "v-for" like in the example below.

  ## <u>Example:</u> ##
  ```html
  <section class="row" v-
  for="c in cars" :key="c.id">
  ```

  + Vue will always require a ```:key``` to define your ```v-for``` for loop attribute function.
  + You can also <b>bind your image source by adding a colon at the beginning of src="" like this -- :src=""</b>
  + To activate your "CarCard" template, write the tag ```<CarCard :carProp="car" />``` in your App.vue file
  + When you want to pass data from a "parent component" to the "child", we use<b>"Props".</b>
  + <b>"Computed"</b> will almost always be done in the "Page.vue" file.
  ## <u>Example:</u> ##
  ```js
  export default (await import ('vue')).defineComponent({

  props: {
    car: { type: Car, required: true }
  }
  setup() {
      return {};
    }
  })
  
  ```
  + Declare props on the child components to be ready to take in data.
  + To create a new Page View when clicking on a reactive object is when you will make your new Page.vue (e.g. CarDetailsPage.vue as a new "Page Name") and (e.g. CarDetailsPage in your "router.js" for when you click on a CarCard)
  + Bring your new template into a new router-link tag in your new template tag within your CarDetailsPage.vue

  + Give your router-link the attribute of:
  ```html
  <router-link :to="{ name: 'CarDetails' }, { params: { carId:carProp.id } }">
  ```

  + The parameter car id comes from and refers to the param in your router.js file. In the CarCard.vue, we are setting the route parameter (carId) to be equal to the unique id of the car we clicked on.
  + This will give each car its own details page.

  ```js
  export default (await import ('vue')).defineComponent({
  }
  setup() {
      const route = useRoute() //NOTE gives me access to the current route or URL i am on
      const router = useRouter() //NOTE gives me access to the entire VUE router (this router.js)
      return {};
    }
  })
  ```
  
  + Remember to set your "activeCar" as equal to null in your AppState.
  + Bring in your activeCar in your CarDetailsPage.vue
  + **Modals** get their own file in the Components folder (file name e.g. Modal.vue)
  + Put your "modal-guts" inside of your template tag in your App.vue and *BE SURE TO IMPORT IN YOUR SCRIPT TAG*
  + Your modal get its own tag of ```<Modal>``` for your form.

  ## <u>Example HTML for Form with Object Name of "Car":</u> ##
  ```html
  <Modal id="create-car" class="fw-5">
    <template>
      <form @submit.prevent="submitCarForm()">
        <div class="mb-3">
          <label 
            for="make" 
            class="form-label">make</label>
          <input 
            required type="text" 
            v-model="editable.make" 
            class="form-control" 
            id="make" 
            placeholder="make..."
            name="make">
        </div>
        <div class="mb-3">
          <label 
            for="model" 
            class="form-label">model</label>
          <input 
            required type="text" 
            v-model="editable.model" 
            class="form-control" 
            id="model" 
            placeholder="model..."
            name="model">
        </div>
        <div class="mb-3">
          <label 
            for="year" 
            class="form-label">year</label>
          <input 
            required type="number" 
            v-model="editable.year" 
            class="form-control" 
            id="year" 
            placeholder="year..."
            name="year">
        </div>
        <div class="mb-3">
          <label 
            for="img" 
            class="form-label">img</label>
          <input 
            required type="text" 
            v-model="editable.imgUrl" 
            class="form-control" 
            id="img" 
            placeholder="img..."
            name="imgUrl">
        </div>
        <div class="mb-3">
          <label 
            for="price" 
            class="form-label">price</label>
          <input 
            required type="number"
            v-model="editable.price" 
            class="form-control" 
            id="price" 
            placeholder="price..."
            name="price">
        </div>
        <div class="mb-3">
          <label 
          for="description" 
          class="form-label">description</label>
          <textarea 
            name="description"
            v-model="editable.description" 
            class="form-control"
            id="description"
            rows="3">
          </textarea>
        </div>
        <div class="mb-3">
          <label 
            for="engineType" 
            class="form-label">Engine Type picker</label>
          <select
            name="engineType"
            id="engineType" 
            v-model="editable.engineType">
            <option 
              v-for="e in engineTypes" 
              :value="e" 
              class="text-capitalize">
                {{ e }}
            </option>
          </select>
        </div>

        <div>
          <button 
            type="submit" 
            class="btn btn-primary" 
            data-bs-dismiss="modal">
            {{ editable.id ? 'Save Changes' : 'Create Car' }}
          </button>
        </div>
      </form>
    </template>
  </Modal>
  ```
  + Be sure to add your *data-bs-target* equal to your target ID beginning with a *hash tag* (e.g. data-bs-target="#id-name")
  + A ```<slot>``` tag is a placeholder on a component that injects something into it later
  + Your form also gets its own file in the components folder (file name e.g. CarForm.vue)

  ## <u>Example of JS script syntax for Form with Object Name of "Car":</u> ##

  ```js
  <script>
    import { ref } from 'vue';
    import { router } from '../router.js';
    import { carsService } from '../services/CarsService.js';
    import Pop from '../utils/Pop.js';

    export default {
      setup() {

        const editable = ref({})

        // TODO make form work with edits

        return {
          editable,
          engineTypes: ['unknown', '2 stroke', '4 cylinder', 'v6', 'v8', 'v10', 'v12', 'small', 'medium', 'large', 'chuncko'],
          async submitCarForm() {
            try {
              const car = editable.value.id
                ? await carsService.editCar(editable.value)
                : await carsService.createCar(editable.value)

              // clears the form
              editable.value = {}
              if (car?.id) {
                router.push({ name: 'Car', params: { carId: car.id } })
              }
              // if (editable.value.id) {
              //   await carsService.editCar(editable.value)
              // }else{
              //   await carsService.createCar(editable.value)
              // }
            } catch (error) {
              Pop.error(error, '[Submitting Car]')
            }
          }

        }
      }
    }
  </script>
  ```
  
  + If you're going to use a icon as some sort of item, you have to have a **TITLE TAG** {e.g. ```<title id="btn-id" name="btn-name"```} for it to function.
  + If you want to delete the example of "Car" object, you would use the following syntax example in a new file named CarPage.vue with the following information:

    ```js
    <template>
      <div class="CarPage" v-if="car">
        <div class="container">
          <div class="row my-3">
            <div class="col-md-8 m-auto">
              <CarCard :car="car" :showSeller="false" />
              <div class="card my-2">
                <div class="card-body">
                  <p>
                    {{ car.description }}
                  </p>

                  <div>
                    <ul>
                      <li>Year: {{ car.year }}</li>
                      <li>Engine Type: {{ car.engineType }}</li>
                    </ul>
                  </div>

                </div>

                <div class="card-footer d-flex align-items-center justify-content-between">
                  <div>
                    <button @click="removeListing" v-if="account.id == car.creatorId" class="btn btn-danger">remove
                      listing</button>
                  </div>
                  <div>
                    <span class="me-2">{{ car.seller.name }}</span>
                    <img height="64" width="64" :src="car.seller.picture" :alt="car.seller.name">
                  </div>
                </div>

              </div>
            </div>
          </div>
        </div>

      </div>
      <div v-else>
        <h1>loading.... <i class="mdi mdi-pinwheel mdi-spin"></i></h1>
      </div>
    </template>


    <script>
      import { computed, onMounted } from 'vue';
      import { useRoute } from 'vue-router';
      import { AppState } from '../AppState.js';
      import { router } from '../router.js';
      import { carsService } from '../services/CarsService.js';
      import Pop from '../utils/Pop.js';

      export default {
        setup() {
          const route = useRoute()
          const carId = route.params.carId

          async function getCarById() {
            try {
              await carsService.getCarById(carId)
            } catch (error) {
              Pop.error(error, '[Getting Car By Id]')
            }
          }

          onMounted(() => {
            getCarById()
          })



          return {
            carId,
            account: computed(() => AppState.account),
            car: computed(() => AppState.car),
            async removeListing() {
              try {
                await carsService.removeCar(carId)
                router.push({ name: 'Cars' })
              } catch (error) {
                Pop.error(error, '[Removing Car]')
              }
            }
          }
        }
      }
    </script>
    ```
  + 
  + 
  + 
  + 
  + 
  + 
  + 


* ## <u>STEPS (Day 2)</u> ## 
  + FOR TODAY - THE EXAMPLE THAT WILL BE REFERENCED FOR YOUR API 'NAME' WILL BE THE BANANA WORD 'OBJECT'
  + Run bcw create
  + No auth today
  + Build out AxiosService.js with your "export const objectAPI" attributes. Include your baseURL, timeout of 8000, and Params for your api_key: '' and and its api request params

    ## <u>Example of JS script syntax for AxiosService params:</u> ##
    ```js
    params:
    {
    api_key: 'e098eyrwg098ewfy098yn0ser98y',
    includes_adult: false,
    }
    ```

  + In your HomePage.vue, set up a function request your API with the "onMounted" function like so:
  ## <u>Example of JS script syntax for your onMounted function:</u> ##
    ```js
    import { computed, onMounted } from 'vue';
    import { logger } from '../utils/Logger.js';
    import { objectsService } from '../services/ObjectsService.js'
    import Pop from '../utils/Pop.js';
    import { AppState } from '../AppState.js';
    import ObjectCard from '../components/ObjectCard.vue';

    export default (await import('vue')).defineComponent({
      setup() {
        async function getObjects() {
          try {
            await objectsServices.getObjects()
            logger.log ('[GETTING OBJECTS]')
          } catch (error) {
            logger.error (error)
            Pop.toast ('[COULD NOT GET OBJECTS...]', error.message)
          }
        }
        //NOTE - OnMounted says "run this code as soon as this component mounts"
        onMounted(() => {
            getObjects()
        })

        return {
            placeholderImg: 'http://thiscatdoesnotexist.com',
            // NOTE computed's almost always go on pages and 'parent components'.
            // NOTE computed's are also how we talk to the AppState to bring in data from the AppState.
            objectsInAppState: computed(() => AppState.objects)
        };
      }
    })
    ```

  + Build out your **objectsService** so your **getObjects()** function has some data to log and render that you just built in your **ObjectPage.vue**
  
  ## <u>Example of JS syntax for building your initial 'getter' within Service Layer:</u> ##
  ```js
  import { AppState } from "../AppState.js"
  import { Object } from "../models/Object.js"
  import { logger } from "../utils/Logger.js"
  import { api } from "./AxiosService.js"

  class ObjectsService {

      async getObjects() {
          const res = await api.get('api/objects')
          logger.log('[GETTING OBJECTS]', res.data)
          //NOTE - IMPORTANT!!! >>>PAY ATTENTION to where you get the response back from the API. Ocassionally, you'll have to go deeper than 'res.data' (e.g. res.data.map) in order to breach past the 'res.data is not a function' error. It can typically be solved by reaching one layer deeper in the URL path like; for example, '.results'
          AppState.objects = res.data.results.map(o => new Object(o))
          // NOTE the bottom reference is for switching the 'currentPage'
          AppState.currentPage = res.data.page
          logger.log(AppState.objects)
      }
  }

  export const objectsService = new ObjectsService()

  ```
  + **In the Model Layer,** the adapter pattern allows you to 'massage' your query into looking like something else like so:

  ## <u>Example of JS syntax for building a Model Layer for banana object named "Object.js":</u> ##
  ```js
  import { Profile } from "./Account.js"

  export class House {
      constructor(data) {
        this. = data.
        this. = data.
        this. = data.
        this. = data.
        this. = data.
        this. = data.
      }
  }
  ```

  + After building out your model, **save an instance of it to your AppState**
  + 
  + Build out your template in your HomePage.vue

  ## <u>Example of HTML syntax for building a template with a Modal:</u> ##
  ```html
  <template>
    <div class="container-fluid">

      <section class="row p-3 justify-content-end">
          <button class="col-3 btn btn-primary" data-bs-toggle="modal" data-bs-target="#create-object">
            Create Object 📦
          </button>
      </section>
      <!-- ANCHOR instead of  -->
      <!-- NOTE v-for is iterating over the objects computed in the return...we aliased out each one as 'o' -->
      <!-- NOTE for the v-for...vue requires a 'key' so have a unique identifier (typically the id of the object or 'objectId'). Operates in the SAME WAY AS A '.forEach()' -->
      <section class="row">
          <!-- NOTE when I want to pass data from a parent component to the child... we do that using props -->
          <div class="col-md-3 my-3" v-for="o in objects" :key="object.id">
              <!-- NOTE the below 'ObjectCard' essentially says "for all my objects, draw my ObjectCard Template" -->
              <ObjectCard :objectProp="o" />
          </div>
          <button 
          @click="deleteObject(objectProp?.id)" v-if="objectProp?.creator.id == account?.id" class="btn btn-danger" 
          title="Delete Object"><i class="mdi mdi-delete"></i> </button>
      </section>

    </div>
    <Modal id="create-object">
      <ObjectForm/>
    </Modal>
  </template>
  ```

  + Build the **script tag** that pertains to the template you just created in your ObjectCard.vue

  ## <u>Example of JS syntax for ObjectCard.vue script:</u> ##
  ```js
  <script>

    import { computed } from 'vue';
    import { Object } from '../models/Object.js';
    import { AppState } from '../AppState.js';
    import { logger } from '../utils/Logger.js';
    import { objectsService } from '../services/ObjectsService.js';

    export default {
      props: {
          objectProp: { type: Object, required: true }
      },
      setup() {

          return {

              async deleteJob(objectId) {
                  try {
                      await objectsService.deleteJob(objectId)
                  } catch (error) {
                      logger.error(error)
                      Pop.toast(error.message, 'error')
                  }
              },

              account: computed(() => AppState.account)
          };
      },
    };

  </script>
  ```

  + Build out your ObjectDetailsPage.vue **AFTER** adding the necessary path in your **router.js** file.

  ## <u>Example of build setup for ObjectDetailsPage.vue (HTML Template tag + JS Script tag):</u> ##
  ```html
  <template>
    <div class="container-fluid">
        <section class="row justify-content-center">

            <div class="col-8">
                <ObjectCard :objectProp="activeObject" />
                <h1>{{ activeObject?.price }}</h1>
                <h2>{{ activeObject?.description }}</h2>
                <h3 class="text-center mt-2">Image URL: <u style="color: darkblue;" role="button">{{ activeObject?.imgUrl }}</u></h3>
            </div>

        </section>
    </div>
  </template>
  ```

  ```js
  <script>
    import { computed, onMounted } from 'vue';
    import { useRoute, useRouter } from 'vue-router';
    import Pop from '../utils/Pop.js';
    import { logger } from '../utils/Logger.js';
    import { objectsService } from '../services/ObjectsService.js';
    import { AppState } from '../AppState.js';
    import ObjectCard from '../components/ObjectCard.vue';
    export default {
      setup() {
          const route = useRoute(); // NOTE: gives me access to the current route or URL I am on
          const router = useRouter(); // NOTE gives me access to the entire VUE router (this router.js here)
          async function getObjectById() {
              try {
                  // NOTE grab the objectId from the route parameters
                  const objectId = route.params.objectId;
                  await objectsService.getObjectById(objectId);
              }
              catch (error) {
                  Pop.error(error.message);
                  logger.log(error);
              }
          }
          onMounted(() => {
              getObjectById();
          });
          return {
              activeObject: computed(() => AppState.activeObject)
          };
      },
      components: { ObjectCard }
    };
  </script>
  ```
  + Build out your **Service Layer** for your **ObjectDetailsPage.vue** function **getObjectById()**
  + If you get a **404 error here,** it is likely you **aren't 'getting'** or **'hitting'** the **correct endpoint** in your **URL path.** Check your **.get(`objects/${objectId}`)** syntax in your **getObjectById(objectId)** within your *ObjectsService Layer.*
  + You can bind a style for a background image with the following syntax if done with an inline-styling technique.

  ## <u>Example using ***inline-styling:***</u> ##
  ```html
  <div class="container-fluid" :style="{ backgroundImage: `url(${object?.backdropImg})`}" >
  ```

  ## Example (Adding a Search Bar): ##

  ```html
  <template>
    <div class="container-fluid">
      <div class="row justify-content-center pt-5">
      </div>
    </div>
    <form @submit-"searchObject()">
      <input class="w-100" type="text" placeholder="Search..." />
      <button type="submit" class="btn btn-success">
        Search
      </button>
    </form>
  </template>
  ```

  ```js
  <script>
    import {  } from ''
    import {  } from ''
    import Pop from ''
    export default (await import('vue')).defineComponent({
      setup() {
        const search = ref('')
        return{
          search,

          async searchObject() {
            try {
              const searchTerm = search.value
              logger.log ('[SEARCHING FOR OBJECT]')
              await objectsServices.searchObject()
            } CATCH (error) {
              logger.error (error)
              Pop.toast (error.message, '[COULD NOT PERFORM OBJECT SEARCH...]')
            }
          }
        };
      }
    })
  </script>
  ```

  ## <u>Example using **queries** *in the AppState* for your searchbar:</u> ##
  ```js
  async searchObjects(query) {
    // NOTE In axios we format queries as objects so they read as key:value pairs
    const res = await objectApi.get('search/object', { 
      params: {
        // NOTE for searching an API, use keyword 'query' and assign the value of whatever the 'search' is
        query: searchTerm,
        api_key: '3498ry345908y3rf0938yef345',
        includes_adult: false,
      } 
    })
    AppState.query = searchTerm
    logger.log('[SEARCHING FOR OBJECTS]')
    AppState.objects = res.data.results.map(o=> new Object(o))
  }
  ```

  + To create multiple pages in order to break down page space, you can adust your getObjects() async function within your service layer with the bottom line of code: ```AppState.currentPage = res.data.results``` and then set a **currentPage** and **totalPage** value in your AppState with appropriate parameters of 'null'.
  + You then add the async function to **change the page in your HomePage.vue file.** ***BE SURE TO ADD AN @CLICK TO YOUR TEMPLATE IN THE APPROPRIATE BUTTON*** like in the **example provided below**:
  ```js
  async changePage(pageChangeSwitch) {
    try {
      if ( pageChangeSwitch == 'next' ) {
        AppState.currentPage++
      } else if ( pageChangeSwitch == 'previous' )
        AppState.currentPage--
        logger.log ('[CHANGING PAGE]', AppState.currentPage)
    } catch (error) {
      logger.error (error)
      Pop.toast (error.message, '[COULD NOT CHANGE PAGE...]')
    }
  }
  ```

  ## <u>Example of adding 'previous' and 'next' page buttons in your template:</u> ##
  ```html
  <button :disabled="currentPage == 1" @click="changePage('previous')">
    Previous
  </button>
  <button :disabled="currentPage == 1" @click="changePage('next')">
    Next
  </button>
  ```

   ## <u>Example for changePage() async function in Service Layer:</u> ##
  ```js
  async changePage() {
    const savedQuery = AppState.savedQuery

    if (!savedQuery) {

    const res = await objectApi.get('discover/object?page=${AppState.currentPage}')

    } else {

      const res = await objectApi.get('search/object') { 

        params: {
          // NOTE for searching an API, use keyword 'query' and assign the value of whatever the 'search' is
          query: savedQuery,
          page: AppState.currentPage,
          api_key: '3498ry345908y3rf0938yef345',
          includes_adult: false,
        } 
      }
    }

    logger.log ('[CHANGING PAGE]', res.data)
    AppState.objects = res.data.results.map(o => new Object(o))
  }
  ```

* ## <u>STEPS (Day 3)</u> ## 

  + ***HINT:*** In your router.js - if you type the following as an argument for your 'beforeEnter' path component, it will redirect the user to '/examplepage' beforeEnter(to, from, next) then on the next line write if(AppState.account?.id) and then invoke return next('/examplepage') on the following line
  + To have a user's cover image appear on their profile, add the following computed in your AccountPage.vue:
  ```js
    coverImg: computed() => `url(${AppState.account?.coverImg})`
  ```
  + After that, **rebind your cover image with CSS** with background-image: v-bind(coverImg)
  + ***HINT:*** 
  + Example of someone's account page and it's form to change account settings:
  ```html

  ```
  + Build account card in AccountPage.vue
  + Build out your form in your created .vue of AccountForm.vue
  + **Test form by adding {{ editable }} in your form template view**
  + Now you can go back in your ExampleForm.vue and use a watchEffect to change the value of your editable is and let vue Magic 🪄 handle the rest...

    ```js
    watchEffect(() => {
      editable.value = { ...AppState.account }
    })
    ```

  + The **spread operator** pushes things into a new object (syntax is ...)
  + When routing to another page, wrap your **desired tags to be placed in your other page** with a **router-link tag.**
  + After you establish your wrapped **router-link,** create your new .vue page for it to be directed to(HINT: PROFILE PAGE)
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