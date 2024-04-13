<script>
  import svelteLogo from "./assets/svelte.svg";

  const personas = (async () => {
    const URL = "https://reqres.in/api/users?page=1";
    const response = await fetch(URL);
    return await response.json();
  })();
</script>

<main>
  <h1>
    Consumir API REST en Svelte
    <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
  </h1>

  <ul class="user-list">
    {#await personas}
      <div class="loader-container">
        <div class="loader">Cargando...</div>
      </div>
    {:then data}
      {#each data.data as persona (persona.id)}
        <li class="user-item">
          <img
            src={persona.avatar}
            alt={persona.first_name}
            class="user-avatar"
          />
          <div class="user-details">
            <p class="user-details__name">
              Nombre: {persona.first_name}
            </p>
            <p class="user-details__email">Email: {persona.email}</p>
          </div>
        </li>
      {/each}
    {/await}
  </ul>
</main>

<style>
  .logo {
    height: 2em;
    will-change: filter;
    filter: drop-shadow(0 0 1em #ff3e00aa);
  }
  h1 {
    text-align: center;
    color: #222;
    font-size: 40px;
    font-weight: 900;
  }
  .user-list {
    list-style: none;
    padding: 0;
    display: flex;
    flex-direction: column;
    background-color: #fff6ea;
    padding: 10px 40px;
    border-radius: 20px;
  }

  .user-item {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    background-color: #e2dbf6;
    padding: 5px 100px 5px 5px;
    color: #222;
    border-radius: 60px;
    font-size: 20px;
  }
  .user-item:hover {
    cursor: pointer;
    transform: scale(1.1); /* Escalamos el tamaño del elemento al hacer hover */
    transition: transform 0.3s ease; /* Aplicamos una transición suave de 0.3 segundos */
    background-color: #ded2ff;
  }
  .user-avatar {
    margin-right: 10px;
    border-radius: 50%;
    width: 100px;
    height: 100px;
  }

  .user-details {
    margin: 0;
  }

  .user-details__name,
  .user-details__email {
    margin: 0;
  }

  .loader-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .loader {
    font-size: 24px;
    color: #333;
  }
</style>
