<template>
  <div class="content-wrapper mb-5">
    <section class="content-header">
      <div class="container-fluid"></div>
    </section>

    <section class="content">
      <div class="card card-outline card-info">
        <div class="card-header">
          <h3 class="card-title">
            <i class="nav-icon fas fa-folder"></i> CATEGORIES
          </h3>
          <div class="card-tools">
            <button
              type="button"
              class="btn btn-tool"
              data-card-widget="collapse"
              title="Collapse"
            >
              <i class="fas fa-minus"></i>
            </button>
            <button
              type="button"
              class="btn btn-tool"
              data-card-widget="remove"
              title="Remove"
            >
              <i class="fas fa-times"></i>
            </button>
          </div>
        </div>
        <div class="card-body">
          <div class="form-group">
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <nuxt-link
                  :to="{ name: 'admin-category-create' }"
                  class="btn btn-info btn-sm"
                  style="padding-top: 8px"
                >
                  <i class="fa fa-plus-circle"></i> TAMBAH</nuxt-link
                >
              </div>
              <input
                type="text"
                class="form-control"
                placeholder="cari berdasarkan nama tag"
              />
              <div class="input-group-append">
                <button class="btn btn-info">
                  <i class="fa fa-search"></i>
                  CARI
                </button>
              </div>
            </div>
          </div>

          <!-- table -->
          <b-table
            striped
            bordered
            hover
            :items="categories"
            :fields="fields"
            show-empty
          >
            <template v-slot:cell(image)="data">
              <img class="img-fluid" width="50" :src="data.item.image" />
            </template>
          </b-table>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  //layout
  layout: "admin",

  //meta
  head() {
    return {
      title:
        "Categories - Kopiitamku.web.id - Belajar Koding Bahasa Indonesia Terlengkap",
    };
  },

  //data function
  data() {
    return {
      //table header
      fields: [
        {
          label: "Gambar",
          key: "image",
          tdClass: "text-center",
        },
        {
          label: "Nama Category",
          key: "name",
        },
        {
          label: "Actions",
          key: "actions",
          tdClass: "text-center",
        },
      ],
    };
  },

  async asyncData({ $axios }) {
    //fetching categories
    const categories = await $axios.$get("/api/admin/categories");

    return {
      categories: categories.data.data,
    };
  },
};
</script>

<style></style>
