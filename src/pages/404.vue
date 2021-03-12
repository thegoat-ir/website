<template>
  <Layout :showLogo="false" :showFooter="false">
    <div id="not-found">
      <p>404: not found</p>
    </div>
  </Layout>
</template>
<style lang="scss">
#not-found {
  width: 85%;
  text-align: center;
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  font-size: 2em;
}
</style>

<script>
export default {
  metaInfo: {
    title: "Not found - The Goat",
  },
};
</script>
