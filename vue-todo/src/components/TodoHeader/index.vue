<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <header>
    <nav class="container">
      <div class="branding">
        <img src="@/assets/vue-logo.png" alt="Vue logo." />
        <h3>Vue Todo</h3>
      </div>
      <ul class="nav-items">
        <li>
          <RouterLink to="/">Home</RouterLink>
        </li>
        <li>
          <RouterLink to="/about">About</RouterLink>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
header {
  background-color: #f1f1f1;
  box-shadow: 0 0 10px 1px rgba($color: #000000, $alpha: 0.1);
}
.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.5rem 0;
  margin: 0 2rem;

  .branding {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    img {
      max-width: 50px;
    }
  }

  .nav-items {
    list-style: none;
    display: flex;
    align-items: center;
    gap: 1.5rem;

    li {
      a {
        text-decoration: none;
        color: #3b3b3b;
        padding: 0.5rem;
        border-radius: 0.2rem;

        &:hover {
          color: #2b8b61;
          background-color: #b9ffdf83;
        }
      }
      .active {
        color: #41b080;
        background-color: #b9ffdf83;
      }
    }
  }
}
</style>
