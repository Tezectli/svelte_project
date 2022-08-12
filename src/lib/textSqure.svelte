<script>
  let count = 0
  const increment = () => {
    count += 1
  }
</script>

<div class="card" on:click={increment}>
  <slot></slot>
</div>

<style>
  .card {
    width: 700px;
    padding: 20px;
    margin-bottom: 20px;
    background: rgb(111, 111, 111);
    border-radius: 25px;
    color: aliceblue;
    text-align: left;
  }
</style>
