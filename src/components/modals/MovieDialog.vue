<template>
  <modal name="MovieDialog" @before-open="beforeOpen">
      <h3>{{ movie.movieName }}</h3>
      <tabs :options="{ useUrlFragment: false }">
        <tab name="Data">

        </tab>
        <tab name="Files">
          <ul>
            <li v-for="(file, index) in movie.Files"
                        v-bind:key="file.id">
              <span>{{ file.path }}</span>
            </li>
          </ul>
        </tab>
      </tabs>
  </modal>
</template>

<script>
  export default {
    name: 'MovieDialog',
    data () {
      return {
        movie: {}
      }
    },
    methods: {
      async beforeOpen (event) {
        this.movie = {}
        this.movie = (await this.axios.get('/movie/' + event.params.movie.id + `/info`)).data
        console.log(this.movie)
      }
    }
  }
</script>

<style scoped lang="sass">
  .container
    padding: 10px

  h3
    width: 100%
    color: white
    margin: 0
    margin-bottom: 10px
    padding: 20px

    background-color: rgba(0,0,0,0.3)

    box-shadow: 0px 0px 5px 2px rgba(darken(darken(#696060,17) + #000000,6), 0.75)

  ul
    list-style: none
    padding: 0
    margin: 0
    li
      span
        display: inline-block
        width: 100%
        padding: 10px 20px
        color: white
        text-decoration: none

        -webkit-transition: background-color 0.1s
        -moz-transition: background-color 0.1s
        -ms-transition: background-color 0.1s
        -o-transition: background-color 0.1s
        transition: background-color 0.1s
      span:hover
        background-color: rgba(0,0,0,0.1)
        box-shadow: 0px 0px 2px 2px rgba(darken(darken(#696060,17) + #000000,6), 0.2)

</style>
