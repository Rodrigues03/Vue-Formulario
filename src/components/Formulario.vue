<template>
  <div class="row">
    <div class="col-12 mb-3">
        <progress-bar :porcentagem="porcentagem" />
    </div>

    <div class="col-12 col-md-4">
      <form @submit.prevent="registrarProjeto">
        <div class="mb-3">
          <label class="form-label">Projeto</label>
          <input
            v-model.trim="projeto"
            type="text"
            class="form-control"
            required
          />
        </div>

        <div class="mb-3">
          <label class="form-label">Atividade</label>
          <select v-model.trim="tipo" class="form-select" required>
            <option disabled selected value="">Selecione um tipo ...</option>
            <option>Aplicação Web com Vue.js</option>
            <option>Aplicação Web - Python</option>
            <option>Backend Service com Node.js</option>
            <option>Backend Service - Python</option>
            <option>App Mobile com React Native</option>
            <option>Mobile App Frameworks for Python</option>
          </select>
        </div>

        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-check-label">
            Urgente
          </label>
          <input
            v-model.trim="urgente"
            type="checkbox"
            class="form-check-input"
          />
        </div>

        <button type="submit" class="btn btn-primary">Salvar</button>
      </form>
    </div>
    <div class="col-12 col-md-8">
     <total-projetos 
     :numeroProjetos="numeroProjetos" 
     :projetos="projetos"
     :mudarEstado="mudarEstado"
     :limparData="limparData" 
     />
    </div>
  </div>
</template>
<script>
  import ProgressBar from './ProgressBar.vue';
  import TotalProjetos from './TotalProjetos.vue';
  export default {
    components: { ProgressBar, TotalProjetos },
    data: () => ({
      projeto: "",
      tipo: "",
      urgente: false,
      projetos: [],
    }),
    methods: {
      registrarProjeto() {
        // completado: false
        const projeto = {
          projeto: this.projeto,
          tipo: this.tipo,
          urgente: this.urgente,
          completado: false,
        };
        this.projetos.push(projeto);
        this.saveData()
  
        this.projeto = "";
        this.tipo = "";
        this.urgente = false;
      },
      mudarEstado(projeto, campo) {
        projeto[campo] = !projeto[campo];
        this.saveData();
      },
      saveData(){
        localStorage.setItem("projetos", JSON.stringify(this.projetos) );
      },
      limparData() {
        this.projetos = [];
        localStorage.clear();
      }
    },
  
    computed: {
      numeroProjetos() {
        return this.projetos.length;
      },
      porcentagem(){
        let completados = 0;
  
        this.projetos.map(projeto => {
          if(projeto.completado) completados++;
        });
  
        return (completados * 100) / this.numeroProjetos || 0;
      },
    },
    mounted(){
     this.projetos = JSON.parse(localStorage.getItem("projetos") ) || [];
    }
  };
  </script>
  