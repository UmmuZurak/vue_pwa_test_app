<template>
  <div class="landing-page sidebar-collapse">
    <nav class="navbar navbar-transparent navbar-color-on-scroll fixed-top navbar-expand-lg" color-on-scroll="100" id="sectionsNav">
      <div class="container">
        <div class="navbar-translate">
          <a class="navbar-brand" href="#">
            <img src="../assets/download.png" alt="" style="width: 200px" />
          </a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" aria-expanded="false" aria-label="Toggle navigation">
            <span class="sr-only">Toggle navigation</span>
            <span class="navbar-toggler-icon"></span>
            <span class="navbar-toggler-icon"></span>
            <span class="navbar-toggler-icon"></span>
          </button>
        </div>
        <div class="collapse navbar-collapse">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <a href="#" class="nav-link"> Home </a>
            </li>
            <li class="nav-item">
              <a href="#" class="nav-link"> About </a>
            </li>
            <li class="nav-item">
              <a href="#" class="nav-link"> FAQS </a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div class="page-header header-filter" data-parallax="true" style="background-image: url('../assets/img/background.jpg')">
      <div class="container">
        <div v-if="deferredPrompt" class="alert alert-info margin-top w-100 mr-3 rounded desktop">
          <div class="container">
            <div class="alert-icon">
              <i class="material-icons">info_outline</i>
            </div>
            <button type="button" class="close" data-dismiss="alert" aria-label="Close">
              <span aria-hidden="true"><i class="material-icons">clear</i></span>
            </button>
            <b>Info alert:</b> You can install the Jetstream app by clicking on the install button. It won't take up space on your phone and also works offline!
            <div class="d-flex justify-content-end mt-3">
              <b class="mr-4 hover">INSTALL</b>
              <b class="mr-5 hover" data-dismiss="alert" aria-label="Close">DISMISS</b>
            </div>
            <!-- <div class="d-flex justify-content-center mt-3"><button @click="install" class="btn btn-light mr-3">INSTALL</button> <button class="btn btn-danger" type="button" data-dismiss="alert" aria-label="Close">DISMISS</button></div> -->
          </div>
        </div>
        <div v-if="deferredPrompt" class="alert alert-info w-100 mr-3 mt-5 rounded mobile">
          <div class="container">
            <div class="alert-icon">
              <i class="material-icons">info_outline</i>
            </div>
            <!-- <button type="button" class="close" data-dismiss="alert" aria-label="Close">
              <span aria-hidden="true"><i class="material-icons">clear</i></span>
            </button> -->
            <b>Info alert:</b> You can install the Jetstream app by clicking on the install button. It won't take up space on your phone and also works offline!
            <div class="d-flex justify-content-end mt-3">
              <b class="mr-4 hover">INSTALL</b>
              <b class="mr-5 hover" data-dismiss="alert" aria-label="Close">DISMISS</b>
            </div>
            <!-- <div class="d-flex justify-content-center mt-3"><button @click="install" class="btn btn-light mr-3">INSTALL</button> <button class="btn btn-danger" type="button" data-dismiss="alert" aria-label="Close">DISMISS</button></div> -->
          </div>
        </div>
        <div class="row">
          <div class="col-md-6">
            <h1 class="title">About Jetstream</h1>
            <h4>Jetstream is a technology enabled logistics company. We aim to give businesses in emerging markets more control over their global supply chains.</h4>
            <br />
            <!-- <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank" class="btn btn-danger btn-raised btn-lg"> <i class="fa fa-play"></i> Watch video </a> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      deferredPrompt: null,
    };
  },
  created() {
    window.addEventListener("beforeinstallprompt", (e) => {
      e.preventDefault();
      // Stash the event so it can be triggered later.
      this.deferredPrompt = e;
    });
    window.addEventListener("appinstalled", () => {
      this.deferredPrompt = null;
    });
  },
  methods: {
    async dismiss() {
      this.deferredPrompt = null;
    },
    async install() {
      this.deferredPrompt.prompt();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.desktop {
  display: block;
}

.mobile {
  display: none;
}

.margin-top {
  /* margin-top: -300px; */
  position: absolute;
  bottom: 300px;
}

.hover {
  cursor: pointer;
}

@media only screen and (max-width: 767px) {
  .desktop {
    display: none;
  }

  .mobile {
    display: block;
  }

  .title {
    font-size: 30px;
  }
}
</style>
