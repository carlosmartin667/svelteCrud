<script>
  export let PersonaDetail = {
    id: 0,
    nombre: "",
    apellido: "",
    edad: "",
  };
  export let verPersona;
  
</script>

<main>
  {#if verPersona}
    <div class="row justify-content-center">
      <div class=" col-md-5 ">
        <ul class="list-group">
          <li class="list-group-item active">Detalles de persona</li>
          <li class="list-group-item">id:{PersonaDetail.id}</li>
          <li class="list-group-item">nombre: {PersonaDetail.nombre}</li>
          <li class="list-group-item">apellido: {PersonaDetail.apellido}</li>
          <li class="list-group-item">edad: {PersonaDetail.edad}</li>
        </ul>
        <br />
        <button
          class="btn btn-primary"
          on:click={() => (verPersona = false)}
        >
          cerrar
        </button>
      </div>
    </div>
  {/if}
</main>
