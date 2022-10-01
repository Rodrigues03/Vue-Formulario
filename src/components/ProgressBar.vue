.<template>
  <h3 class="text-center">Progreso: {{porcentagem}}%</h3>
      <div class="progress">
        <div class="progress-bar progress-bar-striped progress-bar-animated bg-success"
        role="progressbar"
        :aria-valuenow="porcentagem"
        aria-valuemin="0"
        aria-valuemax="100"
        :style="`width: ${porcentagem}%`"
        ></div>
      </div>
</template>

<script>
export default {
    props: {
        porcentagem: Number,
    }

}
</script>
