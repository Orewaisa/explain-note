<template>
  <head>
    <title>Объяснительная</title>
  </head>

  <main>
    <Header />
    <h1 class="ubuntu-regular">Объяснительная записка</h1>

    <FormNote />
  </main>
</template>

<style lang="less">
  @import "@/assets/styles/main.less";
  h1 {
    text-align: center;
    margin: 20px 0px;

    @media (max-width: 450px) {
      font-size: 20px;
    }
  }
</style>
