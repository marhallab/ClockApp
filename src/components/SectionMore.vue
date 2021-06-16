<template>
  <div id="div-more"  v-bind:style="{ display, backgroundColor:bgColor}">
    <div class="flex-container">
      <div class="div-column">
        <div class="div-info">
          <p class="info-title" v-bind:style="{color:textColor}">Current time zone</p>
          <p class="info-p"  v-bind:style="{color:textColor}" > {{ time_zone }}</p>
        </div>
        <div class="div-info">
          <p class="info-title"  v-bind:style="{color:textColor}" >Day of the year</p>
          <p class="info-p"  v-bind:style="{color:textColor}" >{{ day_year }}</p>
        </div>
      </div>

      <div class="div-divider-container">
        <div class="div-divider"> </div>
      </div>

      <div class="div-column column-left">
        <div class="div-info">
          <p class="info-title"  v-bind:style="{color:textColor}" >Day of the week</p>
          <p class="info-p"  v-bind:style="{color:textColor}" >{{ day_week }}</p>
        </div>
        <div class="div-info">
          <p class="info-title"  v-bind:style="{color:textColor}" > Week Number</p>
          <p class="info-p"  v-bind:style="{color:textColor}" >{{ week_number }}</p>
        </div>
      </div>

    </div>
  </div>
</template>

<style scoped>
#div-more {
  position: relative;
  background-color: white;
  display: none;
  height: 50%;
  justify-content: space-around;
  justify-items: center;
  top: 10%;
}
.flex-container {
  display: flex;
  justify-content: space-around;
  width: 100%;
  height: 100%;
}

.div-column {
  display: flex;
  justify-content: space-around;
  flex-direction: column;
  margin-top: 3%;
}
.column-left{
  left: 10%;
}

.div-info {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.info-title {
  font-family: Inter;
  font-style: normal;
  font-weight: normal;
  font-size: 15px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #303030;
}

.info-p {
  margin-top : 0; 
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 56px;
  color: #303030;
}
.div-divider{
  border-left: 2px solid grey;
  height: 250px;
  }
.div-divider-container{
  display: flex;
  justify-content: space-around;
  flex-direction: column;
}

@media only screen and (max-width: 768px) {

.div-divider-container{
  display: none;
}


.info-title {
  font-family: Inter;
  font-style: normal;
  font-weight: normal;
  font-size: 13px;
  letter-spacing: 2.6px;
  text-transform: uppercase;
  color: #303030;
}

.info-p {
  margin-top : 0; 
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 40px;
  color: #303030;
}

.div-column {
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  height: 80%;
}

#div-more {
  position: relative;
  background-color: white;
  display: none;
  height: 50%;
  justify-content: space-evenly;
  justify-items: center;
  top: 10%;
  padding-top: 3%;
  padding-bottom: 5%;
}
}

@media only screen and (max-width: 500px) {
  #div-more {
  position: relative;
  background-color: white;
  display: none;
  height: 50%;
  justify-content: space-around;
  justify-items: center;
  top: 15%;
}
.flex-container {
  display: flex;
  justify-content: stretch;
  width: 90%;
  height: 70%;
  flex-direction: column;
}

.div-column {
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  
}
.div-info {
  display: flex;
  justify-content: space-between;
  flex-direction: row;
}
 .info-title {
  font-family: Inter;
  font-style: normal;
  font-weight: normal;
  font-size: 10px;
  letter-spacing: 2.6px;
  text-transform: uppercase;
  color: #303030;
}

.info-p {
  margin-top : 0; 
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 20px;
  color: #303030;
}

}
</style>

<script>
export default {
  name: "Section3",
  
  props:{
    time_zone: String,
    day_year: Number,
    day_week: Number,
    week_number: Number,
    display: {
        type: String,
        default: "flex"
      } ,
    bgColor: String,
    textColor: String
  },

  methods: {
 
  },
};
</script>