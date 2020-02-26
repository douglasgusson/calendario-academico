<template>
  <div class="calendario">
    <h1>{{ title }}</h1>
    <label for="busca">Busca</label>
    <input type="text" id="busca" placeholder="Buscar..." v-model="search" />
    <div class="container">
      <div class="card" v-bind:key="i" v-for="(data, i) in filteredList()">
        <dl>
          <dt>Procedimento</dt>
          <dd>{{ data.procedimento }}</dd>
          <dt>Período</dt>
          <dd>{{ data.periodo[0] | dateFormat }} à {{ data.periodo[1] | dateFormat }}</dd>
        </dl>
      </div>
    </div>
  </div>
</template>

<script>
import json from "../data/si.json";

export default {
  name: "Calendario",
  props: {
    title: String
  },
  data() {
    return {
      search: "",
      dados: json
    };
  },
  filters: {
    dateFormat: function(value) {
      if (!value) return "";
      let d = new Date(value);
      return d.toLocaleDateString();
    },
    periodoFormat: function(value) {
      let di = new Date(value[0]);
      let df = new Date(value[1]);
      if (value[0] == value[0]) return di.toLocaleDateString();
      return `${di.toLocaleDateString()} à ${df.toLocaleDateString()}`;
    }
  },
  methods: {
    filteredList: function() {
      this.search = this.search
        .toLowerCase()
        .normalize("NFD")
        .replace(/[\u0300-\u036f]/g, "");
      if (this.search)
        return this.dados.filter(item =>
          item.procedimento
            .toLowerCase()
            .normalize("NFD")
            .replace(/[\u0300-\u036f]/g, "")
            .includes(this.search)
        );
      else return this.dados;
    }
  }
};
</script>

<style scoped>
label {
  display: block;
}

input {
  width: 95%;
  padding: 1em 0;
  margin: 1em auto;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.card {
  border: 1px solid #eee;
  margin: 1em;
  padding: 2em;
  box-shadow: 3px 3px 5px #ccc;
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 40%;
}

dt {
  font-weight: bold;
  margin: 0.4em 0;
}

dd {
  margin: 0;
}
</style>
