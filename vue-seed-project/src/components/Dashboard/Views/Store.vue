<template>
<div>
 <div>

        <table style="width:100%">
        <div>
          <input type="text" v-model= "name"> Name <br>
          <input type="text" v-model= "price"> price <br>
          <input type="text" v-model= "deletion"> deleteProduct <br>
          <input type="text" v-model= "updatename"> updata name <br>
          <input type="text" v-model= "updateprice"> update Price <br>
          <input type="text" v-model= "updateId"> update Id <br>
            <button v-on:click="AddToApi"> add product</button>
            <button v-on:click="Deletion"> delete product</button>
            <button v-on:click="Update"> update product</button>
  </div>

<tr>
 <th>id</th>
 <th>name</th>
 <th>price</th>
 <th>created at</th>
 <th>updated at</th>
 <th>Seller Name</th>
 <th>actions</th>
</tr>
<tr v-for = "item in items.data">
 <td>{{item._id}}</td>
 <td>{{item.name}}</td>
 <td>{{item.price}}</td>
 <td>{{item.createdAt}}</td>
 <td>{{item.updatedAt}}</td>
 <td>Menna Wael</td>
 <td button type="editbutton" class="btn btn-primary">Edit</button>{{item.action}}</td>
 <td button type="deletebutton" class="btn btn-primary">Delete</button>{{item.action}}</td>
  </tr>
</table>
  </div>
  </div>
  </div>
  </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      items: [],
      deletion: '',
      updatename: '',
      updateprice: '',
      updateId: ''
    }
  },
  created () {
    this.fetchItems()
  },
  methods: {
    AddToApi () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.name,
        price: this.price,
        sellername: this.sellername
      }).then((response) => {
        console.log(response)
      })
    .catch(e => {
      this.errors.push(e)
    })
    },
    fetchItems () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.items = response.data
        console.log(response)
      })
  .catch(e => {
    this.errors.push(e)
  })
    },
    Deletion () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.deletion)
    .then((response) => {
      console.log(response)
    })
  .catch(e => {
    this.errors.push(e)
  })
    },
    Update () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.updateId, {
        name: this.updatename,
        price: this.updateprice})
    .then((response) => {
      console.log(response)
    })
  .catch(e => {
    this.errors.push(e)
  })
    }
  }
}
</script>
<style>

</style>
