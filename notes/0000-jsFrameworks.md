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