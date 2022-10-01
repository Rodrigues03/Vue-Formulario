<template>
<div class="row my-2">
 <div class="col-6">
  <h3>Total de Projetos: {{ numeroProjetos }}</h3>
 </div>
 <div class="col-6 text-end">
  <button @click="limparData" class="btn bg-primary text-white ">Limpar Projetos</button>
</div>
</div>

  <div class="table-responsive">
    <table class="table table-dark">
      <thead>
        <tr>
          <th>#</th>
          <th>Projeto</th>
          <th>Tipo</th>
          <th>Urgente</th>
          <th>Completado</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(projeto, index) in projetos" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ projeto.projeto }}</td>
          <td>{{ projeto.tipo }}</td>
          <td
            @click="mudarEstado(projeto, 'urgente')"
            :class="projeto.urgente ? 'bg-success' : 'bg-danger'"
          >
            {{ projeto.urgente ? "Sim" : "Não" }}
          </td>
          <td
            @click="mudarEstado(projeto, 'completado')"
            :class="projeto.completado ? 'bg-success' : 'bg-danger'"
          >
            {{ projeto.completado ? "Completo" : "Incompleto" }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ["numeroProjetos", "projetos", "mudarEstado", "limparData"],
};
</script>
