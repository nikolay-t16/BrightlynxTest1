<template>
    <input v-model=val type="text" placeholder="введите число (1.5)" v-on:keydown="onKeydown" v-on:keyup="onKeyup" />
</template>

<script>
  /**
   * Компонент для ввода числа
   */
  export default {
    name: 'FloatInput',
    props: {
      value: Number
    },
    data: function () {
      //Доступные действия
      this.validKey = ['Delete', 'Backspace', 'ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight'];
      return {
        val: this.value
      }
    },
    methods: {
      //Ограничения ввода, для того что бы можн было вводить только число
      onKeydown: function (e) {
        if(this.validKey.indexOf(e.key) != -1 ||
         isNumeric(e.key) ||
          e.key == "." && this.val.indexOf(".") == -1
        )
          return;
        e.preventDefault();
      },
      onKeyup: function () {
        // Запуск действия для смены значения
        this.$emit('change', { val: this.val })
      }
    }
  }

  function isNumeric(n) {
    return !isNaN(parseFloat(n)) && isFinite(n);
  }
</script>

<style scoped>

</style>