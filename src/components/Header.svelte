<script lang="ts">
  import type { Snippet } from "svelte";

  let { username, name, children } = $props<{ 
    username: string, 
    name: string,
    children: Snippet
  }>();
  // let { name, age = undefined }: { name: string, age?: number } = $props();
</script>

<div class="header">
  <h2>Logo</h2>
  {@render children()}
  <div class="profile">Profile User: {name} ({username})</div>
</div>

<style>
  .header {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    background: aquamarine;
    border-bottom: 1px solid black;
    padding: 3px 20px;
    display: flex;
    align-items: center;
  }

  h2 { flex: 1;}

  .profile { 
    flex: 5; 
    text-align: right;
    margin: 0 10px;
  }
</style>
