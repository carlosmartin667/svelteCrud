<script>
  import Detalles from "./components/variables.svelte";
  export let name;
  let ListPersonas = [];
  let Persona = {
    id: 0,
    nombre: "",
    apellido: "",
    edad: "",
  };

  let PersonaDetail = {
    id: 0,
    nombre: "",
    apellido: "",
    edad: "",
  };
  let editarPerosnaEstado = false;
  let verPersona = false;
  const agregarPersona = (e) => {
    e.preventDefault();
    const newPersona = {
      id: ListPersonas.length,
      nombre: Persona.nombre,
      apellido: Persona.apellido,
      edad: Persona.edad,
    };
    ListPersonas = ListPersonas.concat(newPersona);
    clearPerosna();
    console.log(Persona);
  };

  const EditarPersona = (e) => {
    const PersonaEditar = {
      id: Persona.id,
      nombre: Persona.nombre,
      apellido: Persona.apellido,
      edad: Persona.edad,
    };
    console.log(Persona.id);
    const PesonaIndex = ListPersonas.findIndex((p) => p.id === Persona.id);
    console.log(PesonaIndex);
    ListPersonas[PesonaIndex] = PersonaEditar;
    clearPerosna();
    editarPerosnaEstado = false;
  };
  const EscuhaPersona = (e) => {
    e.preventDefault();
    if (!editarPerosnaEstado) {
      agregarPersona(e);
    } else {
      EditarPersona(e);
    }
  };

  const clearPerosna = () => {
    Persona = {
      id: "",
      nombre: "",
      apellido: "",
      edad: "",
    };
  };
  const deletePerosna = (id) => {
    console.log(id);
    ListPersonas = ListPersonas.filter((item) => item.id != id);
  };
  const editarPerosna = (personaEditable) => {
    Persona = personaEditable;
    editarPerosnaEstado = true;
  };

  const detallesPersona = (personaDetalles) => {
    verPersona = true;
    
    PersonaDetail = personaDetalles;
    return PersonaDetail;
  };
</script>

<main>
  <div class="container">
    <div class="row">
      <h1>Hello {name}!</h1>

      <div class="col-4 p-3">
        <form on:submit={EscuhaPersona}>
          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <span class="input-group-text" id="Nombre">Nombre</span>
            </div>
            <input
              type="text"
              class="form-control"
              placeholder="Nombre"
              aria-label="Nombre"
              aria-describedby="Nombre"
              bind:value={Persona.nombre}
            />
          </div>
          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <span class="input-group-text" id="Apellidos">Apellidos</span>
            </div>
            <input
              type="text"
              class="form-control"
              placeholder="Apellidos"
              aria-label="Apellidos"
              aria-describedby="Apellidos"
              bind:value={Persona.apellido}
            />
          </div>
          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <span class="input-group-text" id="Edad">Edad</span>
            </div>
            <input
              type="text"
              class="form-control"
              placeholder="Edad"
              aria-label="Edad"
              aria-describedby="Edad"
              bind:value={Persona.edad}
            />
          </div>
          {#if !editarPerosnaEstado}
            <button class="btn btn-primary ">agregar</button>
          {:else}
            <button class="btn btn-primary ">Editar</button>
          {/if}
        </form>
      </div>
      {#if ListPersonas.length > 0}
        <div class="col-8">
          <table class="table table-striped  table-bordered">
            <thead>
              <tr>
                <th scope="col">#id</th>
                <th scope="col">Nombre</th>
                <th scope="col">Apellido</th>
                <th scope="col">Edad</th>
                <th />
              </tr>
            </thead>
            <tbody>
              {#each ListPersonas as item}
                <tr>
                  <th scope="row">{item.id}</th>
                  <td>{item.nombre}</td>
                  <td>{item.apellido}</td>
                  <td>{item.edad}</td>
                  <td>
                    <button
                      type="button"
                      class="btn btn-danger"
                      on:click={deletePerosna(item.id)}>Eliminar</button
                    >
                    <button
                      type="button"
                      class="btn btn-warning"
                      on:click={editarPerosna(item)}
                    >
                      Editar</button
                    >
                    <button
                      type="button"
                      class="btn btn-warning"
                      on:click={detallesPersona(item)}
                    >
                      detalles</button
                    >
                  </td>
                </tr>
              {/each}
            </tbody>
          </table>
        </div>
      {/if}

      <Detalles {PersonaDetail} bind:verPersona={verPersona} />
    </div>
  </div>
</main>

<style>
</style>
