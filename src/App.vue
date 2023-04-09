<script>
import animes from './data/animes.json'
export default {
  data() {
    return {
      allItems: animes.data,
      filteredItems: animes.data,
      items: animes.data.slice(0, 10),
      page: 1,
      maxPages: Math.ceil(animes.data.length/10),
      sources: ['all sources', 'manga',  'original', 'visual_novel', 'novel', '4_koma_manga', 'light_novel', 'web_manga', 'web_novel', 'game', 'other', 'music', 'book', 'mixed_media', 'picture_book', 'card_game', 'radio'],
      selectedsource: 'all sources'
    };
  },
  watch: {
    selectedsource(newSource, old) {
      console.log('masuk sini')
      if (newSource === 'all sources') {
        this.filteredItems = this.allItems
      } else {
        this.filteredItems = this.allItems.filter(item => item[11] === newSource)
      }
      this.items = this.filteredItems.slice(0,10)
      this.page = 1
      this.maxPages = Math.ceil(this.filteredItems.length/10)
    }
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
    <div class="row justify-content-start mt-4">
      <div class="col-3">
        <select v-model="selectedsource" class="form-select" aria-label="Default select example">
          <option v-for="source in sources" :key="source">{{ source }}</option>
        </select>
      </div>
    </div>
    <div class="row mt-2">
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
              <h5 class="card-title fw-semibold">{{ item[2] }}</h5>
              <table class="table table-borderless">
                <tbody>
                  <tr>
                    <td colspan="4">
                      <table class="table mb-0">
                        <th scope="row">Rank:</th>
                        <td>{{ item[14] }}</td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <td></td>
                        <th scope="row">Score:</th>
                        <td>{{ item[9] }}</td>
                      </table>
                    </td>
                    <!-- <th scope="row">Rank:</th>
                    <td>{{ item[14] }}</td>
                    <th scope="row">Score:</th>
                    <td>{{ item[9] }}</td> -->
                  </tr>
                  <tr>
                    <th scope="row">Genre:</th>
                    <td>{{ item[10] }}</td>
                  </tr>
                  <tr>
                    <th scope="row">Season:</th>
                    <td>{{ item[8] }} {{ item[7] }}</td>
                  </tr>
                  <tr>
                    <th scope="row">Source:</th>
                    <td>{{ item[11] }}</td>
                  </tr>
                </tbody>
              </table>
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
