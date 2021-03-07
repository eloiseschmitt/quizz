<template>
  <header class="container">
    <nav class="navbar">
      <a class="logo" href="#"
        ><img
          alt="logo"
          :src="require(`@/assets/${logoLink}`)"
          :width="logoWidth"
          class="logo--app"
      /></a>
      <ul class="nav-links">
        <li><a href="#">Home</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: "HeaderApp",
  props: {
    logoLink: String,
    logoWidth: Number,
  },
  setup() {},
};
</script>

<style scoped lang="scss">
header {
  position: relative;
  .container {
    max-width: 1368px;
    margin: 0 auto;
    padding: 1rem 2rem;
  }
  .navbar {
    min-height: 10vh;
    display: flex;
    align-items: center;
    justify-content: space-between;
    .logo {
      font-size: 2.25rem;
      text-decoration: none;
      text-transform: uppercase;
      color: #fff;
      font-weight: 700;
    }
    .nav-links {
      display: flex;
      align-items: center;
      li {
        list-style-type: none;
        a {
          text-decoration: none;
          margin: 0 1.25rem;
          font-weight: 500;
          font-size: 1.05rem;
          position: relative;
          &::after {
            position: absolute;
            content: "";
            background-color: #fff;
            bottom: -5px;
            left: 0;
            width: 0%;
            height: 3px;
            transition: 0.3s ease all;
          }
          &:hover::after {
            width: 100%;
          }
        }
      }
      button {
        border: none;
        outline: none;
        cursor: pointer;
        padding: 0.75rem 1rem;
        margin: 0 1rem;
        border-radius: 6px;
        background: transparent;
        border: 2px solid #fff;
        color: #fff;
        font-weight: 500;
      }
    }
  }
}
</style>