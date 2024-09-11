# VUE.js crash 2024:

Some VUE.js practice, from [Vue.js Crash Course 2024](https://www.youtube.com/watch?v=VeNfHj6MhgA) by TraversyMedia.

- See the basic of Vue API preference options:

![image](https://github.com/user-attachments/assets/41dfa1d6-e99a-4def-b3f5-ac9ee9c87242)

-> You can take a look at `App2.vue` file.

- See the basic of Vue API preference composiiton and lifecycle methods:

![image](https://github.com/user-attachments/assets/ae4125d4-cde5-41d4-8b38-048715b6aa8d)


-> You can take a look at `App3.vue` and  `App4.vue` file.

![image](https://github.com/user-attachments/assets/a5dd81d7-8924-4a4e-9072-1aacf066826d)

-View all jobs:

![image](https://github.com/user-attachments/assets/1f07d2ff-d625-45a3-9914-947bd49e1755)

-View one job:

![image](https://github.com/user-attachments/assets/bcd16e53-5045-40ee-bb1a-296c5d697bbc)

-Edit or Delete the job:

![image](https://github.com/user-attachments/assets/cec5eef9-5e59-4185-af1a-051c0ad5cd0f)

-Add a new job:

![image](https://github.com/user-attachments/assets/f5733517-bd79-4111-98a3-98329270fb70)

- Create an app of jobs, where I see these concepts:

```
- defineProps (to pass props to a component)
- slot (similar to children of React)
- bind
- ref, reactive
- computed (similar to dependency array of useEffect hook).
- lifeCycled methods: 
onMounted (similar to useEffect with [] as dependency array, call when the component it's mounted).
- vue-router: 
RouterView
createRouter
createWebHistory
RouterLink
useRoute
not-found route (with path: "/:catchAll(.*)")
dynamic routes with :id
useRoute with .params (to get the params from the URL)
useRouter
push()
- @submit, .prevent, v-model (for forms)
```

---

## TECHNOLOGIES:


- <img width="28" height="28" src="https://img.icons8.com/fluency/38/html-5.png" alt="html-5"/> HTML5

- <img width="28" height="28" src="https://img.icons8.com/fluency/38/css3.png" alt="css3"/> CSS3

- <img width="28" height="28" src="https://img.icons8.com/color/28/javascript--v1.png" alt="javascript--v1"/> JavaScript

- <img width="28" height="28" src="https://img.icons8.com/fluency/38/tailwind_css.png" alt="tailwind_css"/> TailwindCSS (for the styles)

- <img width="28" height="28" src="https://img.icons8.com/fluency/38/vuejs.png" alt="vuejs"/> VUE.js (Framework)

- vue-spinner

- vue-toastification (toast to show messages)

- PrimeIcons

- JSON Server

- Axios

- <img width="28" height="28" src="https://img.icons8.com/color/28/vite.png" alt="vite"/> Vite


---

## COMMANDS

1. Project Setup

```sh
npm install
```

2. Compile and Hot-Reload for Development

```sh
npm run dev
```

And see it running at: [http://localhost:3000/](http://localhost:3000/)


```sh
npm run server
```

To run the JSON-Server at port 8000, and use the endpoints:

GET JOBS LIST: [http://localhost:8000/jobs](http://localhost:8000/jobs)

3. Compile and Minify for Production

```sh
npm run build
```

---

## NOTES

At file [`notas.md`](https://github.com/eugenia1984/vue-crash-2024/blob/main/notas.md) you can take a look of some annotations I did with the basic of VUE.js

---

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

---
