<template>
  <div id="div-quote" v-bind:style="{ display }"  >
    <div>
      <p class="quote">
        {{ quote }}
      </p>

      <p class="autor">
        {{ author }}
      </p>
    </div>

    <div class="div-icon">
      <img
        v-on:click="getRandomQuote"
        class="icon-refresh"
        src="../assets/desktop/icon-refresh.svg"
      />
    </div>
  </div>
</template>


<style scoped>
#div-quote {
  position: relative;
  display: flex;
  justify-content: space-between; 
  width: 600px;
  height: 10%;
  left: 10%;
  top: -15%;
  
}

.quote {
  font-family: Inter;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  color: #ffffff;
}

.autor {
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 18px;
  color: #ffffff;
}

.div-icon {
  position: relative;
  top: 20%;
  left: 1%;
}

.icon-refresh {
  position: relative;
  cursor: pointer;
}

@media only screen and (max-width:768px) {
  #div-quote {
  position: relative;
  display: flex;
  justify-content: space-between; 
  width: 80%;
  height: 10%;
  left: 10%;
  top: -15%;
}
}

@media only screen and (max-width:500px) {
.quote {
  font-family: Inter;
  font-style: normal;
  font-weight: normal;
  font-size: 15px;
  color: #ffffff;
}

.autor {
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 15px;
  color: #ffffff;
}
}
</style>

<script>
import axios from "axios";

export default {
  name: "Section1",

  props:{
      display: {
        type: String,
        default: "flex"
      } ,
  },

  data: function () {
    return {
      quote: null,
      author: null,
    };
  },



  methods: {
    getRandomQuote() {
      axios
        .request("https://type.fit/api/quotes")
        .then((response) => {
          const randomQuote = response.data[Math.floor(Math.random() * response.data.length)];

          this.quote = randomQuote.text;
          this.author = randomQuote.author;
        })
        .catch((error) => {
          console.log(error.response);
        });
    },
  },


  created: function(){
    this.getRandomQuote();
  }
};
</script>