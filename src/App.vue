<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h2>Tres en Raya</h2>

    <table align="center" border="2">
      <tr>
        <td width="100" height="100" id="c0" v-on:click="pcelda(0)"></td>
        <td width="100" height="100" id="c1" v-on:click="pcelda(1)"></td>
        <td width="100" height="100" id="c2" v-on:click="pcelda(2)"></td>
      </tr>
      <tr>
        <td width="100" height="100" id="c3" v-on:click="pcelda(3)"></td>
        <td width="100" height="100" id="c4" v-on:click="pcelda(4)"></td>
        <td width="100" height="100" id="c5" v-on:click="pcelda(5)"></td>
      </tr>
      <tr>
        <td width="100" height="100" id="c6" v-on:click="pcelda(6)"></td>
        <td width="100" height="100" id="c7" v-on:click="pcelda(7)"></td>
        <td width="100" height="100" id="c8" v-on:click="pcelda(8)"></td>
      </tr>
    </table>
    <table align="center" border="0">
      <tr>
        <td width="300" align="center"><br />
          <a href="javascript:location.reload()">
            <button type="button" class="btn btn-primary">Reiniciar</button></a>
        </td>
      </tr>
    </table>

  </div>
</template>

<script>
  export default {
    name: 'app',
    data: () => ({
      mapa: [0, 0, 0, 0, 0, 0, 0, 0, 0, ],
      jugador: 1,
    }),

    methods: {

      dibujar: function () {
        var i;
        for (i = 0; i < 9; i++) {
          if (this.mapa[i] == 0) {
            document.getElementById("c" + i).style = "background-color: white";
          }
          if (this.mapa[i] == 1) {
            document.getElementById("c" + i).innerHTML = "X";
          }
          if (this.mapa[i] == 2) {
            document.getElementById("c" + i).innerHTML = "O";
          }
        }
      },

      pcelda: function (celda) {
        if (this.mapa[celda] == 0) {
          if (this.jugador == 1) {
            this.mapa[celda] = 1;
            this.jugador = 2;
          } else {
            this.mapa[celda] = 2;
            this.jugador = 1;
          }
        } else {
          alert("No puedes pulsar sobre una celda ya seleccionada por otro jugador");
        }
        this.dibujar();
        var r = this.ganador();
        switch (r) {
          case 0:
            break;
          case 1:
            alert("¡Ganó el jugador X!");
            break;
          case 2:
            alert("¡Ganó el jugador O!");
            break;
          case 3:
            alert("¡Empate!");
            break;
        }
      },

      ganador: function () {
        var numEspacios = 0;
        var i;
        for (i = 0; i < 9; i++) {
          if (this.mapa[i] == 0) numEspacios++;
        }
        // Las líneas horizontales
        if (this.mapa[0] == this.mapa[1] && this.mapa[1] == this.mapa[2] && this.mapa[0] != 0) return this.mapa[0];
        if (this.mapa[3] == this.mapa[4] && this.mapa[4] == this.mapa[5] && this.mapa[3] != 0) return this.mapa[3];
        if (this.mapa[6] == this.mapa[7] && this.mapa[7] == this.mapa[8] && this.mapa[6] != 0) return this.mapa[6];
        //Las líneas verticales
        if (this.mapa[0] == this.mapa[3] && this.mapa[3] == this.mapa[6] && this.mapa[0] != 0) return this.mapa[0];
        if (this.mapa[1] == this.mapa[4] && this.mapa[4] == this.mapa[7] && this.mapa[1] != 0) return this.mapa[1];
        if (this.mapa[2] == this.mapa[5] && this.mapa[5] == this.mapa[8] && this.mapa[2] != 0) return this.mapa[2];
        //Las diagonales
        if (this.mapa[0] == this.mapa[4] && this.mapa[4] == this.mapa[8] && this.mapa[0] != 0) return this.mapa[0];
        if (this.mapa[2] == this.mapa[4] && this.mapa[4] == this.mapa[6] && this.mapa[2] != 0) return this.mapa[2];

        if (numEspacios > 0) {
          return 0;
        } else {
          return 3;
        }

      }
    }
  }

</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  img {
    max-width: 150px;
    max-height: 150px;
    margin: 20px;
  }

  h1,
  h2 {
    font-weight: normal;
  }

  #c0,
  #c1,
  #c2,
  #c3,
  #c4,
  #c5,
  #c6,
  #c7,
  #c8 {
    font-size: 50px;
  }

</style>
