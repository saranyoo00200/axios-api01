<template>
  <div>
    <!-- logo , header , manual ,searvh button in jumbotron -->
    <div>
      <b-jumbotron
        bg-variant="secondary"
        text-variant="white"
        border-variant="dark"
      >
        <img class="sizeL" src="../assets/1412.png" />
        <template v-slot:header>MUSIC MAIX</template>
        <hr class="my-4 new1" />
        <b-row align-h="center">
          <b-col md="auto">
            <div>
              <b-button v-b-toggle.sidebar-no-header variant="light" size="sm"
                >Manual</b-button
              >
              <b-sidebar
                id="sidebar-no-header"
                title="Sidebar"
                bg-variant="dark"
                text-variant="light"
                aria-labelledby="sidebar-no-header-title"
                no-header
                shadow
              >
                <template v-slot:default="{ hide }">
                  <div class="p-3">
                    <h4 id="sidebar-no-header-title">คำแนะนำ</h4>
                    <p>
                      เพลงที่ Search บางครั้งก็ไม่ตรงตามชื่อที่ search อาจจะมี
                      title หนัง เข้ามาด้วย ดังนั้น user โปรด
                      พิมพ์ชื่อเพลงให้ถูกต้องโดยไม่ต้องพิมพ์คำว่า"เพลง"ด้านหน้า
                      เช่น เธอ ,ความเชื่อ เป็นต้น.
                    </p>
                    <nav class="mb-3">
                      <b-nav vertical>
                        <b-nav-item active @click="hide">Link</b-nav-item>
                        <b-nav-item href="#link-1" @click="hide"
                          >Link</b-nav-item
                        >
                        <b-nav-item href="#link-2" @click="hide"
                          >Link</b-nav-item
                        >
                      </b-nav>
                    </nav>
                    <b-button variant="light" block @click="hide"
                      >Close Sidebar</b-button
                    >
                  </div>
                </template>
              </b-sidebar>
            </div>
          </b-col>
          <b-col cols="6">
            <b-form-input
              size="sm"
              class="mr-sm-2"
              v-model="musicName"
              placeholder="Search Music"
            ></b-form-input>
          </b-col>
          <b-col md="auto">
            <b-button
              variant="light"
              @click="searchdata()"
              size="sm"
              class="my-2 my-sm-0"
              type="submit"
              >Search</b-button
            >
          </b-col>
        </b-row>
      </b-jumbotron>
    </div>
    <!--/ logo , header , manual ,searvh button in jumbotron -->
    <!-- card -->
    <div>
      <b-container v-if="load == true">
        <b-card-group columns>
          <b-card
            no-body
            class="overflow-hidden"
            style="max-width: 540px;"
            :per-page="perPage"
            :current-page="currentPage"
            v-for="data in resultData.slice(
              (currentPage - 1) * perPage,
              (currentPage - 1) * perPage + perPage
            )"
            :key="data.trackId"
          >
            <div>
              <b-card
                :title="data.trackName"
                :img-src="data.artworkUrl60"
                img-top
                tag="article"
                style="max-width: 97%;"
                class="mb-2"
                bg-variant="dark"
                text-variant="light"
              >
                <b-card-text>
                  <audio controls>
                    <source :src="data.previewUrl" type="audio/mpeg" />
                  </audio>
                </b-card-text>
                <b-card-text>{{ data.synopsis }}</b-card-text>
                <b-button
                  :href="data.trackViewUrl"
                  target="_blank"
                  variant="light"
                  >Click Music</b-button
                >
              </b-card>
            </div>
          </b-card>
        </b-card-group>
        <!--/ card /-->
        <div>
          <b-row>
            <!-- pagination -->
            <b-pagination
              v-model="currentPage"
              :total-rows="resultData.length"
              :per-page="perPage"
              class="mt-4"
            >
              <template v-slot:first-text
                ><span class="text-success">First</span></template
              >
              <template v-slot:prev-text
                ><span class="text-danger">Prev</span></template
              >
              <template v-slot:next-text
                ><span class="text-warning">Next</span></template
              >
              <template v-slot:last-text
                ><span class="text-info">Last</span></template
              >
              <template v-slot:ellipsis-text>
                <b-spinner small type="grow"></b-spinner>
                <b-spinner small type="grow"></b-spinner>
                <b-spinner small type="grow"></b-spinner>
              </template>
            </b-pagination>
          </b-row>
        </div>
        <!--/ pagination / -->
      </b-container>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      resultData: "",
      musicName: "",
      load: false,
      perPage: 3,
      currentPage: 1,
    };
  },
  methods: {
    searchdata() {
      axios
        .get("https://itunes.apple.com/search?term=" + this.musicName)
        .then(
          (response) => (
            (this.resultData = response.data.results),
            (this.load = true),
            (this.currentPage = 1)
          )
        )
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style>
.sizeL {
  width: 200px;
}
.headColor {
  color: light;
}
.new1 {
  border-top: 1px solid rgb(255, 255, 255);
}
</style>
