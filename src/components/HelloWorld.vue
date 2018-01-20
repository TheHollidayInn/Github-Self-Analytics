<template lang="pug">
  div(class="hello")
    div(v-for='(group, key) in prsGroupedByRepo')
      h2 {{key}}
      .card
        h3 {{group.length}}
</template>

<script>
import axios from 'axios'
import moment from 'moment'
import groupBy from 'lodash/groupBy'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      prsGroupedByRepo: []
    }
  },
  async mounted () {
    const response = await axios.get('https://api.github.com/search/issues?q=state:open+author:thehollidayinn+type:pr')
    const items = response.data.items

    const startOfThisWeek = moment().startOf('week')
    const prsThisWeek = items.filter(item => {
      return moment(item.updated_at) >= startOfThisWeek
    })

    const prsGroupedByRepo = groupBy(prsThisWeek, 'repository_url')
    this.prsGroupedByRepo = prsGroupedByRepo
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1 {
    font-size: 3em;
  }

  h2 {
    font-size: 1.5em;
  }

  h1, h2 {
    font-family: Nunito,sans-serif;
    font-weight: 900;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }

  .card {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    transition: box-shadow 250ms;
    will-change: box-shadow;
    color: #33334f;
    font-family: Nunito,sans-serif;
    font-weight: 400;
    font-size: 1.25rem;
    text-overflow: ellipsis;
    line-height: 1.625;
    padding: .375rem 1.25rem;
    background: #fff;
    box-shadow: 0 5px 15px rgba(51,51,79,.15);
    border: 1px solid #f2f5ff;
    border-radius: 1.625rem;
    outline: 0;
    width: 100px;
    margin: 0 auto;
  }

  /* Spin Numbers: https://stackoverflow.com/questions/27956723/css-animation-number-increment-effect */
  /* div {
    width: 1em;
    height: 1em;
    overflow: hidden;
    line-height: 1em;
    display: inline-block;
  } */
  span {
    position: relative;
  }
  .animate {
    -webkit-animation: spinit 0.2s 5;
    -moz-animation: spinit 0.2s 5;
    animation: spinit 0.2s 5;
  }
  @-webkit-keyframes spinit {
    0% {
      top: 0em;
    }
    50% {
      top: -5em;
    }
    100% {
      top: -9em;
    }
  }
  @-moz-keyframes spinit {
    0% {
      top: 0em;
    }
    50% {
      top: -5em;
    }
    100% {
      top: -9em;
    }
  }
  @keyframes spinit {
    0% {
      top: 0em;
    }
    50% {
      top: -5em;
    }
    100% {
      top: -9em;
    }
  }

  /* Setting the required value to top will make the spinner end at that number */
  .digit1 {
    top: 0em;
    /* -4em means 5 will be the number */
  }

  .digit2 {
    top: 0em;
  }

  .digit3 {
    top: 0em;
  }
</style>
