<template>
  <div>
    <div class="container">
      <header class="navbar">
        <section class="navbar-center">
          <h3 class="logo">Domazone</h3>
        </section>
      </header>
    </div>

    <div class="hero bg-primary text-light text-center">
      <div class="container">
        <h1>Available dictionary .app domains</h1>

        <!-- <div class="has-icon-right search centered">
          <input type="text" class="form-input input-lg search-input" placeholder="Search for domain">
          <i class="form-icon loading"></i>
        </div> -->
      </div>
    </div>

    <nuxt/>
  </div>
</template>

<style lang="scss">
$primary-color: red;

@import "spectre.css";
.navbar {
  padding: 10px 0;
}

h2.logo {
  margin: 0px !important;
}

.container{
  max-width: 1080px;
  padding: 0 5%
}

.hero {
  padding: 10% 0;

  .search {
    max-width: 500px;
  }

  .search-input {
    border-radius: 50px;
    padding: 25px;
  }
}

hr {
  border: 0;
  height: 0;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}
</style>
