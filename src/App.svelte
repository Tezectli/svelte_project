<script>
  import svelteLogo from "./assets/svelte.svg";
  import Card from "./lib/textSqure.svelte";
  import Phone from "./lib/Phone.svelte";
  import { fade } from "svelte/transition";
  // 基础模板语法
  let name = "测试一下";

  function sayHi() {
    return `${name} 世界！`;
  }
  let a = 1;
  let b = 2;
  let state = false;
  let count = 0;
  $: doubled = count * 2;

  function handleClick() {
    count += 1;
  }

  // 样式绑定
  let color = "red";
  let text = true;
  let visible = true;
  function handleColorClick() {
    if (color == "red") {
      color = "blue";
    } else {
      color = "red";
    }
  }

  // 条件渲染
  let ifCount = 0;
  let list = ["a", "b", "c", "d", "e", "f"];
  function ifClick() {
    if (ifCount > 2) {
      ifCount = 1;
    } else {
      ifCount++;
    }
  }

  // 父子组件传值
  function print(data) {
    console.log(`手机号: ${data.detail}`);
  }
</script>

<main>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div>
    <p class="contain">基础模板语法</p>
    <!-- 基础语法 -->
    <Card>
      <div>1. 在 Svelte 中，使用大括号将 script 里的数据绑定到 HTML 中。</div>

      <div class="contain-show">name = {name}</div>

      <div class="contain-show">
        <div>{sayHi()}</div>
        <div>{a} + {b} = {a + b}</div>
        <div>{state ? "测试一下" : "成功哩！"}</div>
      </div>

      <div class="contain-show">
        <div title={name}>Hello</div>
      </div>

      <div class="contain-show">
        <button on:click={handleClick}>
          点了 {count} 次
        </button>
        <p>{count} 的两倍是 {doubled}</p>
      </div>
    </Card>

    <!-- 样式绑定 -->
    <p class="contain">样式绑定</p>
    <Card>
      <div class="contain-show" on:click={handleColorClick} style="color: {color}">测试一下llallalalallalalalalal</div>
      <div style="margin-top: 10px;">
        1. 在 HTML 里可以使用 class:xxx 动态设置要激活的类。这里的 xxx 是对应的类名。 语法是 class:xxx={state} ，当 state 为 true 时，这个样式就会被激活使用。 如果类的名称与它绑定的变量通常是相同的，也可以使用速记属性
      </div>
      <div class="contain-show" class:text>速记模式测试 class:text=text ==> class:text</div>
      <div style="margin-top: 10px;">2. svelte内置了动画和转场功能，不需要下载额外的包，直接transition引入想要的动画即可</div>
      <div class="contain-show" style="height: 80px;">
        <input type="checkbox" bind:checked={visible} />
        visible
        {#if visible}
          <p transition:fade>Fades in and out</p>
        {/if}
      </div>
    </Card>

    <!-- 条件渲染以及列表渲染 -->
    <p class="contain">条件渲染&列表渲染</p>
    <Card>
      <p>条件渲染使用 #if 开头，/if 结尾。</p>
      <div class="contain-show">
        <button type="input" on:click={ifClick}>点我点我</button>
        {#if ifCount === 1}
          <div>测试一下</div>
        {:else if ifCount === 2}
          <div>成功哩！</div>
        {:else}
          <div>失败哩！</div>
        {/if}
      </div>

      <p>如果你有一堆数据需要展示出来，可以使用 #each 方法。 使用 #each 开头，/each 结尾。</p>
      <div class="contain-show">
        <div>
          #each 源数据 as 元素
          <span>元素</span>
          /each
        </div>
        <ul>
          {#each list as item, index}
            <li>{index} -- {item}</li>
          {/each}
        </ul>
      </div>
    </Card>

    <!-- 父子组件传值 -->
    <p class="contain">父子组件传值</p>
    <Card>
      <div class="contain-show">
        <p>子组件 Phone 的内容：</p>
        <Phone number="88888888" />

        <div>子组件 Phone 的内容：</div>
        <Phone on:printPhone={print} />
      </div>
    </Card>
  </div>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .contain {
    font-size: 24px;
    font-weight: 700;
  }

  .contain-show {
    margin-top: 10px;
    padding: 10px 0 10px 20px;
    background: rgb(224, 224, 224);
    border-radius: 15px;
    color: rgb(0, 0, 0);
    text-align: left;
  }

  .text {
    font-size: 18px;
    font-weight: 700;
    color: rgb(0, 0, 0);
  }
</style>
