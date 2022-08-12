<script>
  export let number = "13266668888";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  function printPhone() {
    dispatch("printPhone", "13288888888");
  }
</script>

<div style="color: green;">电话：{number}</div>
<button on:click={printPhone}>输出手机号</button>
