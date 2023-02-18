<script>
import animes from './data/animes.json'
export default {
  data() {
    return {
      allItems: animes.data,
      filteredItems: animes.data,
      items: animes.data.slice(0, 10),
      page: 1,
      maxPages: Math.ceil(animes.data.length/10)
    };
  },
  methods: {
    changePage(newPage) {
      this.page = newPage
      this.items = this.filteredItems.slice((newPage-1)*10, newPage*10)
    }
  }
};
</script>

<template>
  <div class="container">
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Anime from MAL</a>
      </div>
    </nav>
    <div class="row">
      <div
        v-for="item in items"
        :key="item.id"
        class="card mb-4"
        style="max-width: 540px"
      >
        <div class="row g-0">
          <div class="col-md-4">
            <img
              :src=item[3]
              class="img-fluid rounded-start img-responsive"
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
    <nav aria-label="Page navigation example">
      <ul class="pagination justify-content-center">
        <li v-if="this.page > 1"  @click="changePage(1)" class="page-item"><a class="page-link fw-semibold" href="#">First</a></li>
        <li v-if="this.page > 1"  @click="changePage(this.page - 1)" class="page-item"><a class="page-link" href="#">Previous</a></li>
        <li v-if="this.page > 2" class="page-item"><a class="page-link">...</a></li>
        <li v-if="this.page > 1"  @click="changePage(this.page - 1)" class="page-item"><a class="page-link" href="#">{{ page - 1 }}</a></li>
        <li class="page-item"><a class="page-link fw-bold">{{ page }}</a></li>
        <li v-if="this.page < maxPages"  @click="changePage(this.page + 1)" class="page-item"><a class="page-link" href="#">{{ page + 1 }}</a></li>
        <li v-if="this.page < maxPages - 1" class="page-item"><a class="page-link">...</a></li>
        <li v-if="this.page < maxPages" @click="changePage(this.page + 1)" class="page-item"><a class="page-link" href="#">Next</a></li>
        <li v-if="this.page < maxPages"  @click="changePage(maxPages)" class="page-item"><a class="page-link fw-semibold" href="#">Last</a></li>
      </ul>
    </nav>
  </div>
</template>

<style scoped>
.img-responsive {
  width: 100%;
  height: auto;
}
</style>
