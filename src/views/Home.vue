<template>
  <div class="">
    <input v-model="name" placeholder="Escriba el nombre a buscar" />
    <br />
    <input
      v-model="description"
      placeholder="Escriba la descripcion a buscar"
    />
    <br />
    <div>
      <select v-model="category">
        <option value="Books">Books</option>
        <option value="Magazines">Magazines</option>
        <option value="Newspapers">Newspapers</option>
        <option value="Others">Others</option>
        <option value="All">All</option>
      </select>
    </div>
    <body>
      <table>
        <thead>
          <tr>
            <th :key="column" v-for="column in columns">
              <a
                href="#"
                v-on:click="sortBy(column)"
                v-bind:class="{ active: sortKey == column }"
              >
                {{ column }}
              </a>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr :key="item.name" v-for="item in searchbyName">
            <td>{{ item.code }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.category }}</td>
          </tr>
          <tr :key="item.name" v-for="item in searchbyDescription">
            <td>{{ item.code }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.category }}</td>
          </tr>
          <tr :key="item.name" v-for="item in filterbycategory">
            <td>{{ item.code }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.category }}</td>
          </tr>
        </tbody>
      </table>
    </body>
  </div>
</template>

<script>
export default {
  // Single component
  name: "Home",

  components: {
    // HelloWorld
  },

  // Init when component is been created
  data() {
    // like "private" properties
    return {
      searchName: "",
      searchDescription: "",
      columns: ["Code", "Name", "Description", "Category"],
      name: "",
      description: "",
      code: "",
      category: "",
      list: [
        {
          name: "item1",
          description: "desc1",
          code: "001",
          category: "Books"
        },
        {
          name: "item2",
          description: "desc2",
          code: "002",
          category: "Magazines"
        },
        {
          name: "item3",
          description: "desc3",
          code: "003",
          category: "Newspapers"
        },
        {
          name: "item4",
          description: "desc4",
          code: "004",
          category: "Others"
        },
        {
          name: "item5",
          description: "desc5",
          code: "005",
          category: "Books"
        }
      ]
    };
  },

  // LIKE LIKE "" data ""
  // like "public" properties
  props: {
    // props here => see at HelloWorld.vue
  },

  // auto calculated variables
  // It is not necessary to assign due these are auto calculated based on:
  // the reactive data/properties
  computed: {
    searchbyName: function() {
      return this.list.filter(item => item.name === this.name);
    },
    searchbyDescription: function() {
      return this.list.filter(item => item.description === this.description);
    },
    filterbycategory: function() {
      if (this.category == "All") {
        return this.list;
      }
      return this.list.filter(item => item.category === this.category);
    }
  },
  // START LIFECYCLE HOOKS (OPTIONAL)
  created() {
    // this.name = "mauricio t r";
    // this.className = "certi!"; // it is allowed but is not recommendable
    // http://api.com/products/{id}
  },
  mounted() {
    // this.name = "m t r";
    // subscription a socket
  },
  updated() {
    // this.name = "udpated";
  },
  destroyed() {
    // unsubscribe a socket
  },
  // END LIFECYCLE HOOKS

  methods: {}
};
</script>

<style src="./home.css" scoped></style>
