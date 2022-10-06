<script>

    let user = "";
    let pass = "";
    let fail = undefined;

    function logear() {
        if(user != "" && pass != ""){
            fetch(
                `http://localhost:4000/api/login/signin`,
                { 
                  method:'POST',
                  headers: {'Content-Type': 'application/json'},
                  body: JSON.stringify({ usuario: user,
                      contraseña: pass})
                })
                .then(res => res.json())
                .then(apiResponse => {
                  console.log(apiResponse)
                  localStorage.setItem("token", apiResponse.token);
                  if(apiResponse.token) {fail = undefined; location.href = "http://127.0.0.1:5173/gestion/carreras"} 
                  else{
                    fail = apiResponse
                    localStorage.setItem("token", undefined)
                    console.log(localStorage)
                    JSON.stringify(fail)}
                })
        }else{
            res.sendStatus(409)
        }
    }

</script>

<body>

  <div class="login">

    <h1 class="text-center">Bienvenido Adiministrador!</h1>

  
      <div class="form-group">
      <label class="form-label" for="usuario">Usuario</label>
      <input class="form-control" bind:value={user} />
      </div>

      <div class="form-group">
        <label class="form-label" for="password">Contraseña</label>
        <input class="form-control" type="password" bind:value={pass} />
      </div>
      <br>
      <button type="submit" class="btn btn-primary w-100" on:click={logear}> Log In </button>

      <a class="btn btn-outline-primary w-100" href="/">
        Volver
      </a>
      <div>
        {#if fail}
          <h3>
            <strong>{fail.message}</strong>
          </h3> 
        {/if}
      </div>
  </div>
</body>

<style>
	*{
	  margin: 0;
	  padding: 0;
	  box-sizing: border-box;
  }
  
  body{
	  height: 100vh;
	  display: flex;
	  align-items: center;
	  justify-content: center;
	  background: #e8f2fc;
  }
  
  .login{
	  width: 330px;
	  height: min-content;
	  padding: 20px;
	  border-radius: 12px;
	  background: rgb(196, 197, 219);
  }
  
  .login h1{
	  font-size: 36px;
	  margin-bottom: 25px;
  }
  
  
  </style>