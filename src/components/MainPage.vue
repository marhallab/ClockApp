<template>
  <div
    id="main-page-app"
    :style="{
      backgroundImage: 'url(' + require('../assets/desktop/' + bgImageUrl),
    }"
  >
    <div id="flex-container">
      <Section1 :display="sectionQuote.display" />

      <div id="flex-container-row">
        <Section2
          :time="sectionTime.time"
          :timeZone="sectionTime.timeZone"
          :location="sectionTime.location"
          :icon_time="sectionTime.icon_time"
          :welcome_message="sectionTime.welcome_message"
        />
        <div class="div-button">
          <button type="button" v-on:click="openCloseDiv">
            <p id="text-button">{{ buttonState }}</p>
            <img
              id="icon-arrow"
              :style="{ transform: 'rotate(' + rotation + 'deg)' }"
              src="../assets/desktop/icon-arrow-up.svg"
            />
          </button>
        </div>
      </div>

      <Section3
        :time_zone="sectionMore.time_zone"
        :day_year="sectionMore.day_year"
        :day_week="sectionMore.day_week"
        :week_number="sectionMore.week_number"
        :display="sectionMore.display"
        :bgColor="sectionMore.bgColor"
        :textColor="sectionMore.textColor"
      />
    </div>
  </div>
</template>

<style scoped>
#main-page-app {
  width: 100%;
  height: 100%;
  background: no-repeat center center fixed;
  box-sizing: border-box;
  overflow: hidden;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

#flex-container {
  backdrop-filter: brightness(0.65);
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  height: 100%;
}

#flex-container-row {
  display: flex;
  position: relative;
  justify-content: space-between;
  flex-direction: row;
  bottom: 3%;
}

.div-button {
  position: relative;
  width: 100px;
  height: 100px;
  top: 120%;
  right: 10%;
}

.div-button button {
  background-color: white;
  border-radius: 28px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 5px;
  cursor: pointer;
  padding-left: 25%;
  padding-right: 10%;
}

#icon-arrow {
  margin-left: 5px;
}

#text-button {
  font-family: Inter;
  font-style: normal;
  font-weight: bold;
  font-size: 13px;
  letter-spacing: 5px;
  text-transform: uppercase;
  color: #000000;
  opacity: 0.5;
}

@media only screen and (max-width: 768px) {
  #flex-container-row {
    display: flex;
    position: relative;
    justify-content: space-between;
    flex-direction: column;
    top: 1%;
  }

  .div-button {
    position: relative;
    width: 100px;
    height: 100px;
    top: 50%;
    left: 10%;
  }
}
@media only screen and (max-width: 500px) and (max-height: 850px) {
  .div-button {
    position: relative;
    width: 100px;
    height: 100px;
    top: 40%;
    left: 10%;
  }

  .div-button button {
    background-color: white;
    border-radius: 28px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1px;
    cursor: pointer;
    padding-left: 20%;
    padding-right: 10%;
  }

  #text-button {
    font-family: Inter;
    font-style: normal;
    font-weight: bold;
    font-size: 10px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: #000000;
    opacity: 0.5;
  }
}
</style>

<script>
import Section1 from "./SectionQuote";
import Section2 from "./SectionTime";
import Section3 from "./SectionMore";
import axios from "axios";

export default {
  name: "MainPage",

  data: function () {
    return {
      rotation: 180,

      isUp: true,

      buttonState: "MORE",

      bgImageUrl: String,

      windowHeight: window.innerHeight,
      windowWidth: window.innerWidth,

      sectionQuote: {
        display: String,
      },

      sectionTime: {
        location: String,
        current: Date,
        time: String,
        timeZone: String,
        icon_time: String,
        welcome_message: String,
      },

      sectionMore: {
        day_year: Number,
        day_week: Number,
        week_number: Number,
        time_zone: String,
        display: String,
        bgColor: String,
        textColor: String,
      },
    };
  },

  components: {
    Section1,
    Section2,
    Section3,
  },

  methods: {
    openCloseDiv() {
      this.rotation += 180;

      if (this.isUp === true) {
        this.isUp = false;
        this.sectionQuote.display = "none";
        this.sectionMore.display = "flex";
        this.buttonState = "LESS";
      } else {
        this.isUp = true;
        this.sectionQuote.display = "flex";
        this.sectionMore.display = "none";
        this.buttonState = "MORE";
      }
    },

    getLocation() {
      axios
        .request("https://freegeoip.app/json/")
        .then((response) => {
          this.sectionTime.location =
            "in " +
            response.data.region_name +
            ", " +
            response.data.country_name;
          this.sectionMore.time_zone = response.data.time_zone;
        })
        .catch((error) => {
          console.log(error.response);
        });
    },

    getTime() {
      axios
        .request("http://worldtimeapi.org/api/ip")
        .then((response) => {
          this.current = new Date(response.data.datetime);
          if (this.current.getMinutes().valueOf() < 10) {
            this.sectionTime.time =
              this.current.getHours() + ":0" + this.current.getMinutes();
          } else {
            this.sectionTime.time =
              this.current.getHours() + ":" + this.current.getMinutes();
          }

          this.sectionTime.timeZone = response.data.abbreviation;

          this.sectionMore.day_year = response.data.day_of_year;

          this.sectionMore.day_week = response.data.day_of_week;

          this.sectionMore.week_number = response.data.week_number;

          this.getWelcome();
        })
        .catch((error) => {
          console.log(error.response);
        });
    },

    getWelcome() {
      if (this.current.getHours().valueOf() > 18) {
        this.sectionTime.icon_time = "icon-moon.svg";
        if (innerHeight <= 850 && innerWidth <= 500) {
          this.sectionTime.welcome_message = "Good evening";
        } else {
          this.sectionTime.welcome_message = "Good evening, it's currently";
        }

        this.getBackgroundImage("n");
      } else if (
        this.current.getHours().valueOf() > 6 &&
        this.current.getHours().valueOf() < 18
      ) {
        this.sectionTime.icon_time = "icon-sun.svg";
        if (innerHeight <= 850 && innerWidth <= 500) {
          this.sectionTime.welcome_message = "Good morning";
        } else {
          this.sectionTime.welcome_message = "Good morning, it's currently";
        }
        this.getBackgroundImage("d");
      } else {
        this.sectionTime.icon_time = "icon-moon.svg";

        if (innerHeight <= 850 && innerWidth <= 500) {
          this.sectionTime.welcome_message = "Good evening";
        } else {
          this.sectionTime.welcome_message = "Good evening, it's currently";
        }
        this.getBackgroundImage("n");
      }
    },
    getBackgroundImage(Time) {
      if (Time == "n") {
        this.bgImageUrl = "bg-image-nighttime.jpg";
        this.changeColorsSectionMore("n");
      } else if (Time == "d") {
        this.bgImageUrl = "bg-image-daytime.jpg";
        this.changeColorsSectionMore("d");
      }
    },

    changeColorsSectionMore(Time) {
      if (Time == "d") {
        this.sectionMore.bgColor = "rgba(255, 255, 255, 0.75)";
        this.sectionMore.textColor = "#303030";
      } else if (Time == "n") {
        this.sectionMore.bgColor = "rgba(0, 0, 0, 0.75)";
        this.sectionMore.textColor = "#FFFFFF";
      }
    },

    onResize() {
      this.windowHeight = window.innerHeight;
      this.windowWidth = window.innerWidth;
    },
  },

  beforeMount: function () {
    this.getLocation();
    this.getTime();
  },

  beforeCreate: function () {
    this.$nextTick(() => {
      window.addEventListener("resize", this.onResize());
    });
  },

  beforeDestroy() {
    window.removeEventListener("resize", this.onResize);
    window.removeEventListener("scroll", this.onScrollFunction);
  },
};
</script>