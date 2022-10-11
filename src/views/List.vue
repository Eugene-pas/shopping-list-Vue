<template>
  <v-list subheader flat>
    <v-col>
      <v-text-field v-model="newItemTitle" @click:append="addNewItem" append-icon="mdi-cart-plus" label="Add item"
        outlined clearable>mdi-add</v-text-field>
      <div v-for="item in shoppingList" :key="item.id">
        <v-list-item :class="{ 'blue lighten-5' : item.bought }" @click="(doneBought(item.id))">
          <template>
            <v-list-item-action>
              <v-checkbox :input-value="item.bought" color="primary">
              </v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title stop :class="{ 'text-decoration-line-through' : item.bought }">
                {{item.title}}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn @click="deleteItem(item.id)" icon>
                <v-icon color="grey lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-col>
  </v-list>
</template>

<script>

export default {
  name: 'ListView',
  data: () => {
    return {
      shoppingList: [
        { id: 1, title: 'Abibas shoes', bought: false },
        { id: 2, title: 'Intel i-5 8300H', bought: false },
        { id: 3, title: 'Nvidia RTX 4090 Super', bought: false }
      ],
      newItemTitle: ''
    }
  },
  methods: {
    doneBought: function (id) {
      const item = this.shoppingList.filter(value => value.id === id)[0]
      item.bought = !item.bought
    },
    deleteItem: function (id) {
      const item = this.shoppingList.filter(value => value.id === id)[0]
      const index = this.shoppingList.indexOf(item)
      if (index > -1) {
        this.shoppingList.splice(index, 1)
      }
    },
    addNewItem: function () {
      if (this.newItemTitle !== '') {
        this.shoppingList.push(
          {
            id: this.shoppingList.at(-1).id + 1,
            title: this.newItemTitle,
            bought: false
          })
      }
    }
  }
}
</script>
