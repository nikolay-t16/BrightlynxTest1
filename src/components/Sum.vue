<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <form name="test" v-on:submit="calculate">
            <float-input v-model=v1 value=v1 @change=onChangev1></float-input>
            <float-input v-model=v2  value=v2 @change=onChangev2></float-input>
            <input type="submit" value="Вычислить"/>
        </form>
    </div>
</template>

<script>
  import FloatInput from './FloatInput';

  export default {
    name: 'Sum',
    components: {FloatInput},
    data: function(){
      this.sum = function (v1) {
        return function (v2) {
          return v1 + v2
        }
      }
      return {v1:0.1, v2:0.2};
    },
    props: {
      msg: String
    }, methods: {
      calculate: function (e) {
        e.preventDefault();
        console.log(this.sum(this.v1)(this.v2));
      },
      onChangev1: function (data) {
        this.v1 = +data.val;
      },
      onChangev2: function (data) {
        this.v2 = +data.val;
      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
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
</style>
