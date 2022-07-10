<template>
  <div class="comp">
    <nav class="navbar">
      <!-- <h1 class="h-header-4">VA Quiz</h1> -->
      <ul class="navbar__list">
        <li class="navbar__item">
          <router-link class="router-link" to="/">Home</router-link>
        </li>
        <li class="navbar__item">
          <router-link class="router-link" to="/qna">Add Questions</router-link>
        </li>
        <li class="navbar__item">
          <router-link class="router-link" to="/about">Highscore</router-link>
        </li>
      </ul>
    </nav>
  </div>
</template>
<style lang="scss" scoped>
.navbar {
  width: 100%;
  height: 4rem;
  box-sizing: border-box;
  padding: 5px 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--color-brand-5);

  &__list {
    width: 20%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    list-style: none;
    padding: 0;

    &__item {
      font-weight: bold;
      color: var(--color-white-1);
    }
    &__item:visited,
    &__item:link,
    &__item:active {
      color: var(--color-white-2);
    }
  }
}
.router-link:visited,
.router-link:link,
.router-link:active,
.router-link {
  font-weight: bold;
  color: var(--color-white-1);
  text-decoration: none;
  font-size: var(text-size-4);
  text-decoration: underline 0.1em rgba(0, 0, 0, 0);
  text-underline-offset: 0.1em;
  transition: text-decoration-color 300ms;
}
.router-link:hover {
  text-decoration-color: var(--color-white-2);
}
.h-header-4 {
  color: var(--color-white-2);
}
</style>
