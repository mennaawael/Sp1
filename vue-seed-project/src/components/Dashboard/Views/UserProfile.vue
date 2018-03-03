<script>
export default {
  data () {
    return {
      items: []
    }
  },

  created: function () {
    this.fetchItems()
  },

  methods: {
    fetchItems () {
      let uri = 'http://localhost:3000/api/product/getProducts'
      this.axios.get(uri).then((response) => {
        this.items = response.data
      })
    }
  }
}

</script>
<style>

</style>
