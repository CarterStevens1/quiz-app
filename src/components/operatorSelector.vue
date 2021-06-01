<template>
  <!-- creates the buttons for each operator -->
  <div>
    <button @click="$emit('selectOperator', '+')">Addition <br />+</button>

    <button @click="$emit('selectOperator', '-')">Subtract <br />-</button>

    <button @click="$emit('selectOperator', '/')">Division <br />/</button>

    <button @click="$emit('selectOperator', '*')">
      Multiplication <br />*
    </button>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
