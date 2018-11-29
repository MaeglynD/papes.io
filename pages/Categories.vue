<template>
  <div class="cat-container">
    <div class="cat-bg-container"></div>
    <div class="cat-gradient">
      <h1>Coming Soon...</h1>
    </div>
    </div>
  </div>
</template>

<style scoped>
.cat-container{
  width: 100%;
  padding-bottom: 600px;
}

.trend-dia-container{
  max-width: 1500px;
}

.cat-bg-container{
  min-height: 300px;
  max-height: 500px;
  height: 20vw;
  background: url("../static/cat-bg.png") bottom center/cover no-repeat;
}
.cat-gradient{
  width: 100%;
  height: 300px;
  margin-top: -300px;
  background: rgb(23,24,26); /* Old browsers */
  background: -moz-linear-gradient(top, rgba(23,24,26,0) 0%, rgba(23,24,26,1) 100%); /* FF3.6-15 */
  background: -webkit-linear-gradient(top, rgba(23,24,26,0) 0%,rgba(23,24,26,1) 100%); /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(to bottom, rgba(23,24,26,0) 0%,rgba(23,24,26,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
}
.cat-gradient h1{
  font-weight: 300;
  font-size: 52px;
  text-align: Center;
  padding-top: 100px;
}
</style>
