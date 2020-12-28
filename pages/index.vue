<template>
  <div class="container">
    <div class="col-12 mt-5">
      <div class="col-12 mt-5">
        <b-button size="lg" variant="outline-primary" to="/lottery"  style="width:200px ;">Lottery Page</b-button>
      </div>
      <div class="col-12 mt-5">
      <b-button size="lg" variant="outline-success" to="/xo"  style="width:200px ;">XO Page</b-button>
    </div>
    </div>
  </div>
</template>

<script>
  export default {}
</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 500vh;
    /*display: flex;*/
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .title {
    font-family: 'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
    display: block;
    font-weight: 300;
    font-size: 100px;
    color: #35495e;
    letter-spacing: 1px;
  }

  .subtitle {
    font-weight: 300;
    font-size: 42px;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 15px;
  }

  .links {
    padding-top: 15px;
  }
</style>
