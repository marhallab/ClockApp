<template>
  <div class="div-date">
    <div class="flex-container">
      <div class="div-welcome">
        <img
          id="icon-time"
          :src="require('../assets/desktop/' + icon_time)"
          alt=""
        />
        <p id="welcome-message">{{ welcome_message }}</p>
      </div>

      <div class="div-time">
        <p id="time">{{ time }}</p>
        <p id="timeZone">{{ timeZone }}</p>
      </div>
      <p id="location">{{ location }}</p>
    </div>
  </div>
</template>


<style scoped>
.div-date {
  position: relative;
  width: 540px;
  height: 200px;
  left: 10%;
}

.flex-container {
  display: flex;
  justify-content: space-around;
  flex-flow: column wrap;
}
.div-welcome {
  display: flex;
  align-items: stretch;
  flex-direction: row;
}

#icon-time {
  margin-right: 10px;
  margin-top: 20px;
  width: 24px;
  height: 24px;
}

#welcome-message {
  font-family: Inter;
  font-style: normal;
  font-weight: normal;
  font-size: 20px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: #ffffff;
}

.div-time {
  display: flex;
  width: 600px;
  height: 200px;
}

#time {
  margin-top: 100px;
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  line-height: 1px;
  font-size: 200px;
  color: #ffffff;
  float: left;
}

#timeZone {
  margin-top: 130px;
  margin-left: 10px;
  font-family: Inter;
  font-style: normal;
  font-weight: 300px;
  font-size: 40px;
  text-transform: uppercase;
  color: #ffffff;
  float: left;
}

#location {
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  letter-spacing: 4.8px;
  text-transform: uppercase;
  color: #ffffff;
}

@media only screen and (max-width: 768px) {
  #welcome-message {
    font-family: Inter;
    font-style: normal;
    font-weight: normal;
    font-size: 18px;
    letter-spacing: 3.6px;
    text-transform: uppercase;
    color: #ffffff;
  }

  #time {
    margin-top: 100px;
    font-family: Inter;
    font-style: normal;
    font-weight: bold;
    line-height: 1px;
    color: #ffffff;
    float: left;
    font-size: 175px;
    letter-spacing: -4.375px;
  }

  #timeZone {
    margin-top: 130px;
    font-family: Inter;
    font-style: normal;
    font-weight: 300px;
    font-size: 32px;
    text-transform: uppercase;
    color: #ffffff;

  }

  #location {
    font-family: Inter;
    font-style: normal;
    font-weight: bold;
    font-size: 18px;
    letter-spacing: 3.6px;
    text-transform: uppercase;
    color: #ffffff;
  }
}

@media only screen and (max-width: 500px) {
 
  #icon-time {
    margin-right: 10px;
    margin-top: 10%;
    width: 24px;
    height: 24px;
  }

  #welcome-message {
    margin-top: 10%;
    font-family: Inter;
    font-style: normal;
    font-weight: normal;
    font-size: 20px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: #ffffff;
  }
  #time {
    margin-top: 120px;
    font-family: Inter;
    font-style: normal;
    font-weight: bold;
    line-height: 1px;
    color: #ffffff;
    float: left;
    font-size: 120px;
    letter-spacing: -2.5px;
  }

  #timeZone {
    margin-top: 140px;
    font-family: Inter;
    font-style: normal;
    font-weight: 300px;
    font-size: 20px;
    text-transform: uppercase;
    color: #ffffff;
    float: left;
    
  }

  #location {
    font-family: Inter;
    font-style: normal;
    font-weight: bold;
    font-size: 15px;
    margin-top: 10px;
    letter-spacing: 3.6px;
    text-transform: uppercase;
    color: #ffffff;
  }
}
</style>

<script>
//import axios from "axios";

export default {
  name: "Section2",

  props: {
    time: String,
    timeZone: String,
    location: String,
    icon_time: String,
    welcome_message: String,
  },

  data: function () {
    return {
      current: null,
    };
  },

  methods: {},

  beforeMount: function () {
    // this.getTime();
  },
};
</script>