<template>
  <div>
    <table>
      <th>
        <td>
          categories
          <input placeholder="search..." v-model="filterTxt" />
        </td>
      </th>
      <template v-if="categoriesDisplay.length > 0">
        <tr v-for="item in categoriesDisplay" :key="item">
          <td>
          {{ item }}
          </td>
        </tr>
      </template>
      <template v-else>
        <tr>
          <td>
          result not found.
          </td>
        </tr>
      </template>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      categories: [],
      filterTxt: "",
    };
  },
  computed: {
    categoriesDisplay() {
      if (!this.filterTxt) return this.categories;
      return this.categories.filter(
        (item) => item.toLowerCase().search(this.filterTxt.toLowerCase()) > -1
      );
    },
  },
  mounted() {
    fetch("https://api.publicapis.org/categories")
      .then((response) => response.json())
      .then((data) => {
        this.categories = data.categories;
      });
  },
};
</script>

<style>
table,
td {
  border: 1px solid;
}
th td {
  border: 0px;
}
</style>
