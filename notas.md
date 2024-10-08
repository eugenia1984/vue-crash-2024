## NOTAS

Algunas anotaciones de cosas básicas de VUE.js.

---

---

## VUE API PREFERENCE: OPTIONS

## v-if y v-else

Para renderizar condicionalmente, es como el ternario de React, si cumple el `if`, sino en el `else`.

```vue
<script>
export default {
  data() {
    return {
      name: "John Doe",
      status: true,
    };
  },
};
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
  </div>
  <div>
    <p v-if="status">User is active.</p>
    <p v-else="status">User is inactive.</p>
  </div>
</template>
```

---

## v-if , v-else-if y v-else

Para renderizar condicionalmente. Observar que tanto en el `if`como en el `else-if` tengo una condición, que no la tengo en el `else`

```vue
<script>
export default {
  data() {
    return {
      status: "pending",
    };
  },
};
</script>

<template>
  <div>
    <p v-if="status === 'active'">User is active.</p>
    <p v-else-if="status === 'pending'">User is pending.</p>
    <p v-else>User is inactive.</p>
  </div>
</template>
```

---

## v-for

Como el `.map`para recorrer los elementos:

```vue
<script>
export default {
  data() {
    return {
      tasks: ["Task 1", "Task 2", "Task 3"],
    };
  },
};
</script>

<template>
  <div>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
  </div>
</template>
```

---

## v-bind

Para bindear cualquier data, por ejemplo en un `<a>` con el `href`:

```vue
<script>
export default {
  data() {
    return {
      link: "https://google.com",
    };
  },
};
</script>

<template>
  <div>
    <a v-bind:href="link">Look at Google</a>
  </div>
</template>
```

Otro modo de hacerlo, sin `v-bind`, directamente con `:href`:

```vue
<a :href="link">Click for Google</a>
```

---

## v-on:click / @click

Para el evento `onClick`del `<button>`. Otro modo es con `@click`. Ejemplo:

```vue
<script>
export default {
  data() {
    return {
      status: "pending",
    };
  },
  methods: {
    toggleStatus() {
      console.log("toggleStatus");
      if (this.status === "active") {
        this.status === "pending";
      } else if (this.status === "pending") {
        this.status === "inactive";
      } else {
        this.status === "active";
      }
    },
  },
};
</script>

<template>
  <div>
    <!--<button v-on:click="toggleStatus" >Change status</button>-->
    <button @click="toggleStatus">Change status</button>
  </div>
</template>
```

---

---

## VUE API PREFERENCE: COMPOSITION (the hard way)

- Tengo que envolver todo en `setup()`.

- Para que las props sean reactive deben estar con su valor pasado como parametro en `ref()`.

- Y en el metodo, en vez de usar: `this.status`, es: `status.value`-

```vue
<script>
import { ref } from "vue";

export default {
  setup() {
    const name = ref("John Doe");
    const status = ref("active");
    const tasks = ref(["Task 1", "Task 2", "Task 3"]);

    const toggleStatus = () => {
      console.log("toggleStatus");
      if (status.value === "active") {
        status.value === "pending";
      } else if (status.value === "pending") {
        status.value === "inactive";
      } else {
        status.value === "active";
      }
    };

    return {
      name,
      status,
      tasks,
      toggleStatus,
    };
  },
};
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
  </div>
  <div>
    <p v-if="status === 'active'">User is active.</p>
    <p v-else-if="status === 'pending'">User is pending.</p>
    <p v-else>User is inactive.</p>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
    <button @click="toggleStatus">Change status</button>
  </div>
</template>
```

Y está el modo más corto con composition, donde **setup** va dentro del **Script**: `<script setup>`, no se necesita el `export default` ni el `return`:

```vue
<script setup>
import { ref } from "vue";

// COMPOSITION de la forma mas corta
const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);

const toggleStatus = () => {
  console.log("toggleStatus");
  if (status.value === "active") {
    status.value === "pending";
  } else if (status.value === "pending") {
    status.value === "inactive";
  } else {
    status.value === "active";
  }
};
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
  </div>
  <div>
    <p v-if="status === 'active'">User is active.</p>
    <p v-else-if="status === 'pending'">User is pending.</p>
    <p v-else>User is inactive.</p>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>
    <button @click="toggleStatus">Change status</button>
  </div>
</template>
```

---

## FORMULARIOS

Similar a React donde guardamos en un estado los datos del formulario, en vue se crea una constante (prop) y con `ref()`se le puede dar un valor inciial, ejemplo: `const newTask = ref('Task 4'); `o bien `const newTask = ref(''); `.

Y en el **formulario** con el `@submit`es como el `onSubmit`de React y para hacer el `preventDefault` ya tiene el metodo `.prevent`: `@submit.prevent`.

Luego como siempre relaciono el `label`con el atributo `for`, con el `input`con el atributo `id`y tambien nombro al `name`igual.

Nuevo: tengo `v-model` para relacionar con la constante reactiva del estado (prop).

```vue
<template>
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task: </label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
</template>
```

Se tiene también el boton de `type="submit"`.

Y en el `script` agrego el método para agregar al task nueva:

```vue
<script>
const addTask = () => {
  // If there is a value for newTask, then add new task
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    // Reset the newTaskValue to be able to add a new one
    newTask.value = "";
  }
};
</script>
```


Como agrego una nueva Task tambien puedo eliminarla, ais me queda todo el codigo:

```vue
<script setup>
import { ref } from 'vue';

// COMPOSITION de la forma mas corta
  const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
  const newTask = ref(''); 

  const addTask = () => {
    // If there is a value for newTask, then add new task
    if(newTask.value.trim() !== '') {
      tasks.value.push(newTask.value);
      // Reset the newTaskValue to be able to add a new one
      newTask.value = '';
    } 
  }

  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  }

</script>

<template>
  <div>
    <form @submit.prevent="addTask">
      <label for="newTask">Add Task: </label>
      <input type="text" id="newTask" name="newTask" v-model="newTask"/>
      <button type="submit">Submit</button>
    </form>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span class="task-item-name">
          {{ task }}
        </span> 
        <button @click="deleteTask(index)">X</button> 
      </li>
    </ul>
  </div>
</template>
```

---

## LIFECYCLE METHODS - onMounted

Se puede usar por ejemplo cuando se hace un fetch y se quiere atualizar un state, es similar al useEffect.

Ejemplo:

```vue
<script setup>
import { ref, onMounted } from 'vue';

// COMPOSITION de la forma mas corta
  const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
  // Similar to useState in order to save form data
  const newTask = ref(''); 

  // To add a new Task
  const addTask = () => {
    // If there is a value for newTask, then add new task
    if(newTask.value.trim() !== '') {
      tasks.value.push(newTask.value);
      // Reset the newTaskValue to be able to add a new one
      newTask.value = '';
    } 
  }

  // To delete a task
  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  }

// LifeCycle Methods
onMounted(async() => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map( (task) => task.title)
  } catch(error) {
    console.log('Error fetching tasks')
  }
})
</script>

<template>
  <div>
    <form @submit.prevent="addTask">
      <label for="newTask">Add Task: </label>
      <input type="text" id="newTask" name="newTask" v-model="newTask"/>
      <button type="submit">Submit</button>
    </form>
    <br />
    <h3>Tasks:</h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span class="task-item-name">
          {{ task }}
        </span> 
        <button @click="deleteTask(index)">X</button> 
      </li>
    </ul>
    <br />
     <button @click="toggleStatus" type="button" >Change status</button>
  </div>
</template>
```

---

## ESTILOS CON TAILWIND 

Me fijo en la [documentación de Tailwind](https://v2.tailwindcss.com/docs/guides/vue-3-vite).

1. Instalar Tailwind: `npm install -D tailwindcss@latest postcss@latest autoprefixer@latest`

2. Generar los archvos `tailwind.config.js` y `post.config.js`con: `npx tailwindcss init -p`.

En el archivo de configuracion en **content** detallo todos los archivos en los que quiero aplicar Tailwind, y en el **theme** solo voy a setear la font-family y agregar una clase para el grid:

```JavaScript
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./index.html', './src/**/*.{vue, js, ts, jsx, tsx}'],
  theme: {
    extend: {
      fontFamily: {
        sans: ['Poppins', 'sans-serif']
      },
      gridTemplateColumns: {
        '70/30': '70% 28%'
      }
    },
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```

Y en `src/assets/main.css`tengo que agregar los import de Tailwind:

```CSS
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## computed

Es similar al dependency array de useEffect hook. Se usa con `ref`para tener data reactiva y como tenemos `ref`se usa el `.value` para obtener el valor (similar al state de React).

Ejemplo:

```vue
<script setup>
import { defineProps, ref, computed } from 'vue';

const props = defineProps({
  job: Object
})

const showFulDescription = ref(false);

const toggleFullDescription = () => {
  showFulDescription.value = !showFulDescription.value;
}

const truncatedDescription = computed(() => {
  let description = props.job.description;

  if(!showFulDescription.value) {
    description = description.substring(0, 90) + '...';
  }

  return description;
});
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="p-4">
      <div class="mb-5 px-2">
        <div>
          {{ truncatedDescription }}
          <button
            @click="toggleFullDescription" 
            class="text-green-500 hover:text-green-600 mb-5 border-solid border-2 border-green-500 px-2 rounded-md ml-2"
          >
            {{ showFulDescription ? 'Less': 'More' }}
          </button>
        </div>
      </div>
      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <div class="text-orange-700 mb-3">
          <i class="pi pi-map-marker text-orange-700"></i>
          {{ job.location }}
        </div>
        <a
          :href="`/job/${job.id}`"
          class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm"
        >
          Read More
        </a>
      </div>
    </div>
  </div>
</template>
```

---
---

## VUE-ROUTER

Para hacer el ruteo de la aplicación.

1. Creo: `/src/router/index.js` donde voy a tener mi `router`con las rutas. 

2. Usamos **history** con  `createWebHistory` para contar con el historial de navegacion y asi poder ir a la pagina previa visitada.

3. Usamos **routes** que va a ser el array de las rutas, va a tener el `path`, el `name` de la ruta y el `componente`(la view que va a mostrar).

```JavaScript
import { createRouter, createWebHistory } from 'vue-router';
import HomeView from '@/views/HomeView.vue';

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    }
  ]
});

export default router;
```

4. En `src/views` voy a ir creando todas mis vistas (similar al folder `pages` de Next.js) que van a ser las que nombre en **component** dentro del objeto de `createRouter`.*:

5. En `main.js` tenemos que importar y usar **router** que creamos en `/src/router/index.js`:

```JavaScript
import "./assets/main.css";
import "primeicons/primeicons.css";
import router from './router';

import { createApp } from "vue";
import App from "./App.vue";

const app = createApp(App);

app.use(router);
app.mount("#app");
```

6. Para que se puedan ver las views en `App.vue` se usa el `RouterView` que es similar al `outlet` de React, y se pone en la parte de la aplicación donde voy a tener las view, o sea justo abajo del NavBar:

```vue
<script setup>
  import Navbar from '@/components/Navbar.vue';
  import { RouterView } from 'vue-router';
</script>

<template>
  <Navbar />
  <RouterView />
</template>
```

7. Y asi vamos creando `views`, las agregamos en el  `router`y las podemos ir viendo.

8. Tal como tenemos el Link de React-Router o de Next-Router, tenemos `RouterLink` en Vue para las `<a>`. Y en vez de `href`es: `to`.

9. Para tener una ruta de **not found**, el **path** debe ser:  `path: '/:catchAll(.*)',`.

10. Cuando las rutas son dínámica, se contruyen pasando por ejemplo un id, el **path** debe indicar con **:**, por ejemplo: `path: '/jobs/:id',`.

---
---

## LIFECYCLED METHOD - onMounted

Es similar al hook **useEffect** cuando el dependency array está vacío, ya que se llama al montar el componente.

Dentro uso el fecth de axios para traer la lista de trabajo, se usa junto al `ref`, por lo que luego se hace el setter del estado ocn el `.value`.

Ejemplo:

```vue
<script setup>
  import { RouterLink } from 'vue-router';
  import { ref, defineProps, onMounted } from 'vue';
  import  JobListing  from '@/components/JobListing.vue';
  import axios from 'axios';

  defineProps({
    limit: Number
  })

  const jobs = ref([]);

  onMounted(async() => {
    try {
      const response = await axios.get('http://localhost:5000/jobs');
      jobs.value = response.data;
    } catch(error) {
      console.error('Error fetching jobs');
    }
  })
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse jobs
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job"/>
      </div>
    </div>
  </section>
</template>
```

-> En vez de **ref** se puede usar **reactive** pero hay diferencia entre ellas:

| ref | reactive |
| --- | -------- |
| toma **objects** y **primitives** (String, Number, Boolean) | solo toma **objects** |
| tiene la propiedad **.value** para reasignar valor | no tiene .value, ni puede reasignar |

Forma facil de decidirse que usar, como por ejemplo en un form cuando se tiene cda valor del input en un estado, ahi se usari `ref`, pero si en cambio se tiene todo en un objeto se podria usar `reactive`.

-> Ejemplo usando **Reactive**:

```vue
<script setup>
  import { RouterLink } from 'vue-router';
  import { reactive, defineProps, onMounted } from 'vue';
  import  JobListing  from '@/components/JobListing.vue';
  import axios from 'axios';

  defineProps({
    limit: Number
  })

  const state = reactive({
    jobs: [],
    isLoading: true
  });

  onMounted(async() => {
    try {
      const response = await axios.get('http://localhost:5000/jobs');
      state.jobs = response.data;
    } catch(error) {
      console.error('Error fetching jobs');
    } finally {
      state.isLoading = false;
    }
  });
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse jobs
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job"/>
      </div>
    </div>
  </section>
</template>
```
---
---

## vue-router

Para obtener los parametros de la URL:

En este caso como al parametro lo nombre `id`es `.id`, si el parametro fuera `slug`, x ej, deberia ser: `. slug`-

```vue
<script setup>
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
  import { reactive, onMounted } from 'vue';
  import { useRoute, RouterLink } from 'vue-router';
  import axios from 'axios';
  
  // In order to get the id from the params
  const route = useRoute();
  const jobId = route.params.id;

  const state = reactive({
    job: {},
    isLoading: true
  })
</script>
```