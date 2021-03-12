<template>
  <div class="repository">
    <a :href="url" :alt="title" target="_blank">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </a>
    <a :href="url + '/stargazers'" :alt="title" target="_blank">
      <div class="stars">
        <Star />
        <span class="star-count">{{ starCount }}</span>
      </div>
    </a>
  </div>
</template>
<script>
import Star from "~/components/Star.vue";

export default {
  props: ["url", "title", "description", "starCount"],
  components: {
    Star,
  },
};
</script>
<style lang="scss">
.repository {
  display: inline-block;
  margin: 0 20px 0 0;
  width: 350px;
  background-color: var(--bg-content-color);
  border-radius: var(--radius);
  box-shadow: 1px 1px 5px 0 rgba(0, 0, 0, 0.02),
    1px 1px 15px 0 rgba(0, 0, 0, 0.03);
  padding: 0 15px;
  position: relative;
  transition: all ease 0.3s;
  &:hover {
    transform: translateY(-5px);
    box-shadow: 1px 10px 30px 0 rgba(0, 0, 0, 0.1);
    transition: all ease 0.3s;
  }
  &:last-child {
    margin: 0;
  }
  h4 {
    margin: 15px 0 0;
  }
  p {
    margin: 10px 0 50px;
    font-size: 0.6em;
    text-overflow: ellipsis;
    overflow: hidden;
  }
  .star-count {
    font-size: 0.6em;
    vertical-align: middle;
    margin-left: 20%;
  }
  .stars {
    position: absolute;
    right: 8%;
    bottom: 1.5vh;
  }
  a {
    text-decoration: none;
    color: inherit;
  }
  @media screen and (max-width: 1024px) {
    width: 250px;
  }
}
</style>
