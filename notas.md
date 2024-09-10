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