<script>
    import {count} from './stores.js';
</script>

<button on:click={count.increment}>+</button>
<button on:click={count.decrement}>-</button>
<button on:click={count.reset}>Reset</button>