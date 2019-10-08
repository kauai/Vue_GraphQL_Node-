<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>
        Name gator
        <i class="fa fa-check"></i>
      </h1>
      <br />
      <h6 class="text-secondary">Gerador de Nomes</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>
              Prefixos
              <i class="badge badge-info">{{ prefixes.length }}</i>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li v-for="prefix in prefixes" v-bind:key="prefix" class="list-group-item">
                    {{ prefix }}
                    <button v-on:click="deletePrefix(prefix)" class="btn btn-info">
                      <span class="fa fa-trash"></span>
                    </button>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    v-on:keyup.enter="addPrefix(prefix)"
                    v-model="prefix"
                    type="text"
                    placeholder="Digite o prefixo"
                    class="form-control"
                  />
                  <div class="input-group-append">
                    <button v-on:click="addPrefix(prefix)" class="btn btn-info">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="col-md">
            <h5>
              Sufixos
              <i class="badge badge-info">{{ sufixes.length }}</i>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li v-for="sufix in sufixes" v-bind:key="sufix" class="list-group-item">
                    {{ sufix }}
                    <button v-on:click="deleteSufix(sufix)" class="btn btn-info">
                      <span class="fa fa-trash"></span>
                    </button>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    v-on:keyup.enter="addSufix(sufix)"
                    v-model="sufix"
                    type="text"
                    placeholder="Digite o sufixo"
                    class="form-control"
                  />
                  <div class="input-group-append">
                    <button v-on:click="addSufix(sufix)" class="btn btn-info">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <br />
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">{{ domain }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
  name: "app",
  data: function() {
    return {
      prefix: "",
      sufix: "",
      prefixes: ["Php", "Html", "Javascript"],
      sufixes: ["Css", "Scss", "React", "Vuejs"],
      domains: ["Surf", "BodyBoard", "Skate", "Kite surf"]
    };
  },
  methods: {
    addPrefix(prefix) {
      this.prefixes.push(prefix);
      this.prefix = "";
      this.generate();
    },
    deletePrefix(prefix) {
      this.prefixes = this.prefixes.filter(item => item != prefix);
    },
    addSufix(sufix) {
      this.sufixes.push(sufix);
      this.sufix = "";
      this.generate();
    },
    deleteSufix(sufix) {
      this.sufixes = this.sufixes.filter(item => item != sufix);
    },
    generate() {
      this.domains = [];
      for (const prefix of this.prefixes) {
        for (const sufix of this.sufixes) {
          this.domains.push(prefix + sufix);
        }
      }
    }
  }
};
</script>

<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}
#main {
  background: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}

.list-group-item {
  display: flex;
  justify-content: space-between;
  align-items: end;
}
</style>
