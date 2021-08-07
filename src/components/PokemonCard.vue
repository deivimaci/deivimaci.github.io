<template>
  <div class="card" @click="setFavourite(name)">
    <img class="image" :src="imageSrc" />
    <h2 class="name">{{ name }}</h2>
    <svg
      v-if="favourite === name"
      viewBox="0 0 300 275"
      xmlns="http://www.w3.org/2000/svg"
      version="1.1"
      class="star"
    >
      <polygon
        stroke="#fff"
        stroke-width="20"
        points="150,25 179,111 269,111 197,165  223,251 150,200 77,251 103,165 31,111 121,111"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: "PokemonCard",
  props: {
    name: String,
    imageSrc: String,
    favourite: String,
    setFavourite: Function,
  },
};
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
  border-radius: 7px;
  box-shadow: 0 4px 16px rgb(0 0 0 / 20%);
  cursor: pointer;
}

.image {
  max-width: 150px;
}

.name {
  margin-bottom: 10px;
  color: #000;
  text-align: center;
  text-transform: capitalize;
  font-weight: 500;
}

.star {
  width: 40px;
  height: 40px;
  padding: 10px;
  margin-bottom: 20px;
  border-radius: 40px;
  cursor: pointer;
  background-color: #fa2356;
  box-shadow: 0 4px 16px rgb(0 0 0 / 20%);
  transition: background-color 0.2s cubic-bezier(0.4, 0, 0.2, 1);

  &:hover {
    background-color: #d21d48;
  }
  &:active {
    background-color: #fa2356;
  }
}
</style>
