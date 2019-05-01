<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <form name="test">
            <float-input v-model=v1 v-on:change=onChange></float-input>
            +
            <float-input v-model=v2 v-on:change=onChange></float-input>
            = {{res}}
        </form>
    </div>
</template>

<script>
  import FloatInput from './FloatInput';

  export default {
    name: 'Sum',
    components: {FloatInput},
    data: function(){
      /**
       * Функция для вычисления суммы 2 чисел, пример использования - sum(1)(2)
       * Для корректной обработки дробей переводит в целые числа умножая на 10 в степени.
       * Нет проверки на слишком большую велечину числа
       * @param v1
       * @returns {function(*=): *}
       */
      this.sum = function (v1) {
        /**
         * Возвращает количество занков после точки
         * @param number
         * @returns {number}
         */
        var numAfterPoint = function(number){
          var str = number.toString();
          if(str.indexOf(".")==-1)
            return 0;
          return str.split('.')[1].length;
        }
        return function (v2) {
          var k = 1;
          var maxAfterPoint = Math.max(numAfterPoint(v1), numAfterPoint(v2));
          if(maxAfterPoint>0){
            k = Math.pow(10,maxAfterPoint);
            v1 *= k;
            v2 *= k;
          }
          var sum = v1 + v2;
          if(maxAfterPoint>0){
            sum /= k;
          }
          return sum;
        }
      }
      this.calculate = function () {
        this.res = this.sum(this.v1)(this.v2);
        return this.res;
      }
      this.v1 = 0.1;
      this.v2 = 0.2;
      var r = this.calculate();
      this.res = this.sum(this.v1)(this.v2);
      return {res:r};
    },
    props: {
      msg: String
    }, methods: {
      onChange: function () {
        this.calculate();
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
