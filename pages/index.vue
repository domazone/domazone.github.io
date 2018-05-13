<template>
  <div class="domains">
    <div class="container">
      <div class="domain-list">
        <div class="columns">
          <div class="column col-xs-6 col-md-12">
            <div class="popover popover-bottom">
              <button class="btn">Filters</button>
              <div class="popover-container">
                <div class="card">
                  <div class="card-header">
                    Length
                    <div class="form-group">
                      <label class="form-checkbox" v-for="length in [2, 3, 4, 5, 6]" :key="length">
                        <input type="checkbox" :value = "length" v-model = "filters.length" >
                        <i class="form-icon" ></i> {{ length }} letters
                      </label>
                    </div>
                  </div>
                  <hr>

                  <div class="card-body">
                    Starts with
                    <div class="form-group">
                      <label class="form-checkbox" v-for = "letter in 'abcdefghijklmnopqrstuvwxyz'.split('')" :key="letter">
                        <input type="checkbox" :value = "letter" v-model = "filters.starts">
                        <i class="form-icon"></i> {{ letter.toUpperCase() }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <span class="chip" v-for="(letter, index) in filters.starts" :key="letter">
              Starts with {{letter.toUpperCase()}}
              <a @click ="removeLetter(index)" class="btn btn-clear" aria-label="Close" role="button"></a>
            </span>

            <span class="chip" v-for="(l, index) in filters.length" :key="l">
              {{l}} letters
              <a @click="removeLength(index)" class="btn btn-clear" aria-label="Close" role="button"></a>
            </span>
          </div>
        </div>
        <br>

        <div class="columns">
          <div class="column col-4 col-md-6 col-xs-12" v-for="(app, index) in domains" :key="index">
            <div class="card">
              <div class="card-header">
                <button class="btn float-right btn-sm">Buy Now</button>
                <div class="card-title h5">{{ app.domain }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import http from 'axios'
const querystring = require('querystring')

export default {
  data: function() {
    return {
      filters: {
        length: [],
        starts: [],
        last_evel_key: null
      },
      domains: Object,
    }
  },
  created() {
    http.get('http://localhost:3000/domains?' + querystring.stringify(this.filters))
        .then(function (response) {
          this.last_evel_key = response.data.last_eval_key
          console.log(this.last_evel_key)
          this.domains = response.data.domains
        }.bind(this))
        .catch(function (error) {
          console.log(error);
        });
  },

  methods: {
    removeLength(index) {
      this.filters.length.splice(index, 1)
    },

    removeLetter(index) {
      debugger
      this.filters.starts.splice(index, 1)
    }
  },

  components: {
  }
}
</script>

<style lang="sass">
  .domains
    margin: 3% 0

  .column
    margin-bottom: 20px

  .domain-list
    margin: 5% 0
</style>
