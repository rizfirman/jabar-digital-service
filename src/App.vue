<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
</script>

<template>
  <div class="container">
    <h1 class="d-flex justify-content-center mt-5">
      Formulir Bantuan COVID-19
    </h1>
    <div class="mt-5 mb-5">
      <div class="card border border-dark">
        <div class="container">
          <div class="row">
            <div class="col-lg-6">
              <div class="mb-3">
                <label for="nama" class="form-label mt-2"
                  >Nama <span class="text-danger ms-1">*</span></label
                >
                <input
                  type="text"
                  class="form-control"
                  id="nama"
                  v-model="nama"
                />
              </div>

              <div class="mb-3">
                <label for="nik" class="form-label"
                  >NIK<span class="text-danger ms-2">*</span></label
                >
                <input
                  type="number"
                  class="form-control"
                  id="nik"
                  v-model="nik"
                />
              </div>

              <div class="mb-3">
                <label for="kk" class="form-label"
                  >Kartu Keluarga<span class="text-danger ms-2">*</span></label
                >
                <input
                  type="number"
                  class="form-control"
                  id="kk"
                  v-model="kk"
                />
              </div>
              <div class="row mb-3">
                <div class="col-md-3">
                  <label for="umur" class="form-label"
                    >Umur<span class="text-danger ms-2">*</span></label
                  >
                  <input
                    type="number"
                    class="form-control"
                    id="umur"
                    v-model="umur"
                  />
                </div>
                <div class="col-md-9">
                  <label for="kelamin" class="mb-2"
                    >Jenis Kelamin<span class="text-danger ms-2">*</span></label
                  >
                  <select
                    id="kelamin"
                    class="form-select"
                    aria-label="Default select example"
                    v-model="kelamin"
                  >
                    <option selected value="">Pilih Jenis Kelamin</option>
                    <option value="Laki-laki">Laki-laki</option>
                    <option value="Perempuan">Perempuan</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="col-lg-6">
              <div class="row mb-2">
                <div class="col-md-6">
                  <div>
                    <label for="image" class="form-label mb-2 mt-2"
                      >Upload Foto KTP<span class="text-danger ms-2"
                        >*</span
                      ></label
                    >
                    <div
                      class="imagePreviewWrapper mb-3 border border-dark"
                      :style="{ 'background-image': `url(${previewImageKtp})` }"
                      @click="selectImageKTP"
                    ></div>

                    <input
                      ref="fileInputKTP"
                      type="file"
                      id="image"
                      @input="pickFileKtp"
                      accept="image/*"
                    />
                  </div>
                </div>
                <div class="col-md-6">
                  <div>
                    <label for="image" class="form-label mb-2 mt-2"
                      >Upload Foto Kartu Keluarga<span class="text-danger ms-2"
                        >*</span
                      ></label
                    >
                    <div
                      class="imagePreviewWrapper mb-3 border border-dark"
                      :style="{ 'background-image': `url(${previewImageKK})` }"
                      @click="selectImageKK"
                    ></div>

                    <input
                      ref="fileInputKK"
                      type="file"
                      id="image"
                      accept="image/*"
                      @input="pickFileKK"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="row">
            <div class="col-lg-6">
              <label for="provinsi" class="mb-2"
                >Provinsi<span class="text-danger ms-2">*</span></label
              >
              <select
                id="provinsi"
                class="form-select mb-3"
                aria-label="Default select example"
                v-model="provinsi"
              >
                <option selected value="">Pilih Provinsi</option>
                <option
                  v-for="(provinsi, index) in provinsiList"
                  :key="index"
                  :value="provinsi.id"
                >
                  {{ provinsi.name }}
                </option>
              </select>

              <label for="kota" class="mb-2"
                >Kab/Kota<span class="text-danger ms-2">*</span></label
              >
              <select
                id="kota"
                class="form-select mb-3"
                aria-label="Default select example"
                :disabled="!provinsi"
                v-model="kota"
              >
                <option selected value="">Pilih Kab/Kota</option>
                <option
                  v-for="(kota, index) in kotaList"
                  :key="index"
                  :value="kota.id"
                >
                  {{ kota.name }}
                </option>
              </select>

              <label for="desa" class="mb-2"
                >Kelurahan/Desa<span class="text-danger ms-2">*</span></label
              >
              <select
                id="desa"
                class="form-select mb-3"
                aria-label="Default select example"
                :disabled="!kota || !provinsi"
                v-model="desa"
              >
                <option selected value="">Pilih Kelurahan/Desa</option>
                <option
                  v-for="(desa, index) in desaList"
                  :key="index"
                  :value="desa.id"
                >
                  {{ desa.name }}
                </option>
              </select>
            </div>
            <div class="col-lg-6">
              <div class="row">
                <div class="col-md-6">
                  <label for="rt" class="form-label"
                    >RT<span class="text-danger ms-2">*</span></label
                  >
                  <input
                    type="number"
                    class="form-control"
                    id="rt"
                    v-model="rt"
                  />
                </div>
                <div class="col-md-6">
                  <label for="rw" class="form-label"
                    >RW<span class="text-danger ms-2">*</span></label
                  >
                  <input
                    type="number"
                    class="form-control"
                    id="rw"
                    v-model="rw"
                  />
                </div>
              </div>

              <div class="row mt-3">
                <div class="col-md-12">
                  <label for="penghasilan1" class="form-label"
                    >Penghasilan Sebelum Pandemi<span class="text-danger ms-2"
                      >*</span
                    ></label
                  >
                  <input
                    type="number"
                    class="form-control"
                    id="penghasilan1"
                    v-model="penghasilan1"
                  />
                </div>
              </div>

              <div class="row mt-3 mb-3">
                <div class="col-md-12">
                  <label for="penghasilan2" class="form-label"
                    >Penghasilan Sesudah Pandemi<span class="text-danger ms-2"
                      >*</span
                    ></label
                  >
                  <input
                    type="number"
                    class="form-control"
                    id="penghasilan2"
                    v-model="penghasilan2"
                  />
                </div>
              </div>
            </div>
          </div>

          <div class="row">
            <div class="col-lg-12">
              <div class="mb-3">
                <label for="alamat" class="form-label mt-2"
                  >Alamat <span class="text-danger ms-2">*</span></label
                >
                <textarea
                  type="text"
                  class="form-control"
                  id="alamat"
                  v-model="alamat"
                ></textarea>
              </div>

              <label for="alasan" class="mb-2"
                >Alasan Membutuhkan Bantuan<span class="text-danger ms-2"
                  >*</span
                ></label
              >
              <select
                id="alasan"
                class="form-select mb-3"
                aria-label="Default select example"
                v-model="alasan"
              >
                <option selected value="">
                  Pilih Alasan Membutuhkan Bantuan
                </option>
                <option value="1">Kehilangan pekerjaan</option>
                <option value="2">
                  Kepala keluarga terdampak atau korban Covid-19
                </option>
                <option value="3">
                  Tergolong fakir/miskin semenjak sebelum Covid-19, atau
                </option>
                <option value="4">Lainnya</option>
              </select>
            </div>
          </div>

          <div v-if="alasan === `4`" class="mb-3">
            <label for="lainnya" class="form-label mt-2"
              >Alasan Lainnya <span class="text-danger ms-2">*</span></label
            >
            <textarea
              type="text"
              class="form-control"
              id="lainnya"
              v-model="lainnya"
            ></textarea>
          </div>

          <div v-else>
            <div></div>
          </div>
          <div
            v-if="alasan === `4` && lainnya === ''"
            class="d-flex justify-content-center mb-5 mt-3"
          >
            <button
              type="button"
              class="btn btn-dark"
              @click="onSubmit"
              disabled
            >
              SUBMIT
            </button>
          </div>

          <div v-else class="d-flex justify-content-center mb-5 mt-3">
            <button
              type="button"
              class="btn btn-dark"
              @click="onSubmit"
              :disabled="
                nama === '' ||
                nik === '' ||
                umur === '' ||
                provinsi === '' ||
                kota === '' ||
                desa === '' ||
                rt === '' ||
                rw === '' ||
                penghasilan1 === '' ||
                penghasilan2 === '' ||
                alamat === '' ||
                alasan === '' ||
                fileKKString === '' ||
                fileKtpString === '' 
              "
            >
              SUBMIT
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      previewImageKtp: `https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTS2sRlULpZo5zSIWdlCAaHkCXrRUEG-9mFrc19z4J3PWeiuPArJgsy1VqOW9H6ybhdUps&usqp=CAU`,
      previewImageKK: `https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTS2sRlULpZo5zSIWdlCAaHkCXrRUEG-9mFrc19z4J3PWeiuPArJgsy1VqOW9H6ybhdUps&usqp=CAU`,
      nama: "",
      nik: "",
      kk: "",
      umur: "",
      kelamin: "",
      provinsiList: [],
      kotaList: [],
      desaList: [],
      provinsi: "",
      kota: "",
      desa: "",
      rt: "",
      rw: "",
      penghasilan1: "",
      penghasilan2: "",
      alasan: "",
      alamat: "",
      alasanLainnya: "",
      fileKtp: {},
      fileKK: {},
      fileKtpString: "",
      fileKKString: "",
      alasan: "",
      lainnya: "",
    };
  },
  computed: {},
  async mounted() {
    const urlProvinsi = `http://www.emsifa.com/api-wilayah-indonesia/api/provinces.json`;

    const responseProvinsi = await axios.get(urlProvinsi);
    this.provinsiList = responseProvinsi.data;
    console.log("prov", this.provinsiList);
  },
  //fetch url fr kotaList data when provinsi !== ""
  watch: {
    provinsi(newValue) {
      if (newValue !== "") {
        const urlKota = `http://www.emsifa.com/api-wilayah-indonesia/api/regencies/${newValue}.json`;
        console.log("urlKota", urlKota);
        const responseKota = axios
          .get(urlKota)
          .then((response) => {
            this.kotaList = response.data;
            console.log("kota", this.kotaList);
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
    kota(newValue) {
      if (newValue !== "") {
        const urlDesa = `http://www.emsifa.com/api-wilayah-indonesia/api/districts/${newValue}.json`;
        console.log("urlDesa", urlDesa);
        const responseDesa = axios
          .get(urlDesa)
          .then((response) => {
            this.desaList = response.data;
            console.log("desa", this.desaList);
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },

  methods: {
    selectImageKTP() {
      this.$refs.fileInputKTP.click();
    },
    selectImageKK() {
      this.$refs.fileInputKK.click();
    },
    pickFileKtp() {
      let input = this.$refs.fileInputKTP;
      let file = input.files;
      if (file && file[0] && file[0].size < 2000000) {
        if (file && file[0]) {
          let reader = new FileReader();
          reader.onload = (e) => {
            this.previewImageKtp = e.target.result;
          };
          reader.readAsDataURL(file[0]);
          this.$emit("input", file[0]);
          this.fileKtp = file[0];
          this.fileKtpString = file[0].name;
        }
      } else {
        alert("File terlalu besar!");
      }
    },
    pickFileKK() {
      let input = this.$refs.fileInputKK;
      let file = input.files;
      //limited file.size just 2mb
      if (file && file[0] && file[0].size < 2000000) {
        if (file && file[0]) {
          console.log(file);
          let reader = new FileReader();
          reader.onload = (e) => {
            this.previewImageKK = e.target.result;
          };
          reader.readAsDataURL(file[0]);
          this.$emit("input", file[0]);
          this.fileKK = file[0];
          this.fileKKString = file[0].name;
        }
      } else {
        alert("File size is too big");
      }
    },
    onSubmit() {
      let data = {
        nama: this.nama,
        nik: this.nik,
        kk: this.kk,
        umur: this.umur,
        kelamin: this.kelamin,
        provinsi: this.provinsi,
        kota: this.kota,
        desa: this.desa,
        rt: this.rt,
        rw: this.rw,
        penghasilan1: this.penghasilan1,
        penghasilan2: this.penghasilan2,
        alasan: this.alasan,
        alasanLainnya: this.alasanLainnya,
        fileKtp: this.fileKtp,
        fileKK: this.fileKK,
      };
      console.log(data);
    },
  },
};
</script>

<style scoped lang="css">
/* @import "./assets/base.css"; */

.imagePreviewWrapper {
  width: 250px;
  height: 250px;
  display: block;
  cursor: pointer;

  background-size: cover;
}
input[type="file"] {
  color: transparent;
}
</style>
