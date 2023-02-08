<script>
import animes from './data/file2.json'
export default {
  data() {
    return {
      items: animes.data
    };
  },
};
</script>

<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
      </div>
    </nav>
    <div class="row">
      <div
        v-for="item in items"
        :key="item.id"
        class="card mb-3"
        style="max-width: 540px"
      >
        <div class="row g-0">
          <div class="col-md-4">
            <img
              :src=item[3]
              class="img-fluid rounded-start"
              alt="..."
            />
          </div>
          <div class="col-md-8">
            <div class="card-body">
              <h5 class="card-title">{{ item[2] }}</h5>
              <li>Score: {{ item[9] }}</li>
              <li>Genre: {{ item[10] }}</li>
              <li>Source: {{ item[11] }}</li>
              <li>Season: {{ item[8] }} {{ item[7] }}</li>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
