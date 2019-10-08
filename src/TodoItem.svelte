<script>
  import { createEventDispatcher } from 'svelte';
  export let id;
  export let title;
  export let description;
  export let completed;

  const dispatch = createEventDispatcher();
</script>

<style>

</style>

<div class="todo-item">
    <div class="todo-item-left">
        <input type="checkbox">
        <div class="todo-item-label">{title}</div>
    </div>
    <div class="remove-item">
        x
    </div>
</div>