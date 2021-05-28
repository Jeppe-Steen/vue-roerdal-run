<template>
  <footer class="pageFooter">
    <ul>
      <li>Om rørdal run</li>
      <li>Ruter</li>
      <li>Tilmelding</li>
      <li>Distancer</li>
    </ul>
    <ul>
      <li>+45 35 67 90 87</li>
      <li>Rørdalrun@mail.com</li>
    </ul>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  data() {
    return {}
  },
}
</script>

<style scoped>
.pageFooter {
  width: 100%;
  height: 25vh;
  border-top: 1px solid #673399;
  padding: 50px;
  display: grid;
  grid-template: auto / 1fr 1fr 1fr;
}

ul {
  list-style: none;
  color: #673399;
  text-transform: uppercase;
}
</style>
