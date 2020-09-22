<template>
  <div id="app" class="container">
    <div class="col">
      <h1>Validação de Autômato Finito Determininístico</h1>

      <b-tabs content-class="mt-3">
        <b-tab title="Autômato 1" active>
          <p>
            <b-row class="my-1">
              <b-col sm="12">
                <img src="./assets/automato-1.png" alt style="    width: 350px;" />
                <hr>
                <b-form-input
                  id="tab-1"
                  :state="automato1()"
                  v-model="palavra"
                  placeholder="Insira uma palavra"
                ></b-form-input>
              </b-col>
            </b-row>
          </p>
        </b-tab>
        <b-tab title="Autômato 2">
          <p>
            <b-row class="my-1">
              <b-col sm="12">
                <img src="./assets/automato-2.png" alt style="    width: 350px;" />
                <hr>
                <b-form-input
                  id="tab-2"
                  :state="automato2()"
                  placeholder="Insira uma palavra"
                  v-model="palavra"
                ></b-form-input>
              </b-col>
            </b-row>
          </p>
        </b-tab>
        <b-tab title="Autômato 3">
          <p>
            <b-row class="my-1">
              <b-col sm="12">
                <img src="./assets/automato-3.png" alt style="    width: 350px;" />
                <hr>  
                <b-form-input
                  id="tab-3"
                  :state="automato3()"
                  v-model="palavra"
                  placeholder="Insira uma palavra"
                ></b-form-input>
              </b-col>
            </b-row>
          </p>
        </b-tab>
      </b-tabs>
    </div>
    <div class="col">
      <div class="row">
        <img class="mx-auto" src="./assets/vue-boot.png" alt style="width:150px" />
      </div>
      <div class="row mx-auto">
        <a class="mx-auto" href="https://github.com/JoabeRamone">Joabe Ramone</a>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data: function () {
    return {
      palavra: null,
    };
  },
  methods: {
    entradaPalavra(edges, estadosF) {
      let arestas = edges;
      let estadoAtual = 0;
      let lista = [];
      var estadosFinais = estadosF;

      if (this.palavra === null || this.palavra === "") return null;

      lista = this.palavra.split("");

      try {
        lista.forEach(function (value) {
          estadoAtual = arestas.get(value)[estadoAtual][1];
        });
        return estadosFinais[estadoAtual];
      } catch (e) {
        return false;
      }
    },

    automato1() {
      let edges = new Map();
      var estadosFinais = [true, false];
      edges.set("0", [
        [0, 1, "0"],
        [1, 0, "0"],
      ]);
      edges.set("1", [
        [0, 0, "1"],
        [1, 1, "1"],
      ]);
      return this.entradaPalavra(edges, estadosFinais);
    },
    automato2() {
      let edges = new Map();
      var estadosFinais = [false, false, true, false];

      edges.set("a", [
        [0, 1, "a"],
        [1, 0, "a"],
        [2, 3, "a"],
        [3, 2, "a"],
      ]);
      edges.set("b", [
        [0, 3, "b"],
        [1, 2, "b"],
        [2, 1, "b"],
        [3, 0, "b"],
      ]);

      return this.entradaPalavra(edges, estadosFinais);
    },
    automato3() {
      let edges = new Map();
      var estadosFinais = [false, true, false, false, true, false, true];

      edges.set("a", [
        [0, 1, "a"],
        [1, 1, "a"],
        [2, 1, "a"],
        [3, 1, "a"],
        [4, 1, "a"],
        [5, 1, "a"],
        [6, 1, "a"],
      ]);
      edges.set("b", [
        [0, 2, "b"],
        [1, 2, "b"],
        [2, 4, "b"],
        [3, 2, "b"],
        [4, 4, "b"],
        [5, 2, "b"],
        [6, 2, "b"],
      ]);
      edges.set("c", [
        [0, 3, "c"],
        [1, 3, "c"],
        [2, 3, "c"],
        [3, 5, "c"],
        [4, 3, "c"],
        [5, 6, "c"],
        [6, 6, "c"],
      ]);

      return this.entradaPalavra(edges, estadosFinais);
    },
  },
};
</script>

<style>
</style>