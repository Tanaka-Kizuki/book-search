<template>
  <div class="container">
    <div>
      <h1>Book Search</h1>
      <input type="text" v-model="isbn">
      <button class="button" v-on:click="search">Search</button>
      <div v-if="show">
        <table>
          <tr><th>書籍詳細</th></tr>
          <tr>
            <th>署名</th>
            <th>{{ title }}</th>
          </tr>
          <tr>
            <th>表紙</th>
            <th><img v-bind:src="cover"></th>
          </tr>
          <tr>
            <th>著名</th>
            <th>{{ author }}</th>
          </tr>
          <tr>
            <th>出版社</th>
            <th>{{ publisher }}</th>
          </tr>
          <tr>
            <th>出版年</th>
            <th>{{ pubdate }}</th>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
const axios = require("axios");
export default {
  data:()=>({
    title:"",
    author:"",
    publisher:"",
    pubdate:"",
    cover:"",
    isbn:"",
    show:false,
  }),
  methods:{
    search(){
      const url = "https://api.openbd.jp/v1/get?isbn=" + this.isbn;
      axios.get(url)
      .then((res) => {
        this.title = res.data[0].summary.title;
        this.author = res.data[0].summary.author;
        this.publisher = res.data[0].summary.publisher;
        this.pubdate = res.data[0].summary.pubdate;
        this.cover = res.data[0].summary.cover;
        this.show = true;
      })
    }
  }
}
// const isbn = "978-4-7741-8967-3";
// const url = "https://api.openbd.jp/v1/get?isbn=" + isbn;
// export default {
//   asyncData({ params, error }) {
//     return axios
//       .get(url)
//       .then((res) => {
//         return { title: res.data[0].summary.title };
//       })
//       .catch((e) => {
//         error({ title: e.response.status, message: "ERROR!!" });
//       });
//   },
// };
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

/* .title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 10px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
} */
</style>
