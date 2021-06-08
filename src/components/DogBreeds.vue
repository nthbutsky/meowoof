<template>
  <div class="dog-breeds__container">
    <p class="label">Select the breed</p>
    <select name="breeds-drop-down" class="dog-breeds" v-model="selected_breed">
      <option class="option-style" v-for="breed in breeds" :key="breed.name">
        {{ breed.name }}
      </option>
    </select>
    <div class="breed-info__container">
      <div class="temperament" v-if="showItem()">
        {{ temperament }}
        <div class="country" v-if="showItem()">
          Country of origin: {{ country_name }}
        </div>
      </div>
      <div class="image__container">
        <img class="image" :src="image" alt="" />
        <img class="flag" :src="country_flag_url" alt="" />
      </div>
      <p class="description" v-if="showItem()">Bred for: {{ description }}</p>
      <!-- <a class="wiki-link" :href="wiki_url" v-if="showItem()">WIKIPEDIA</a> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "DogBreeds",
  data() {
    return {
      country_flag_url: "",
      breeds: [],
      selected_breed: {},
      image: "",
      description: "",
      country_code: "",
      country_name: "",
      temperament: "",
      wiki_url: "",
    };
  },
  created() {
    this.getBreeds();
  },
  watch: {
    selected_breed: function () {
      this.getInfo();
    },
  },
  methods: {
    async getBreeds() {
      try {
        axios.defaults.headers.common["x-api-key"] =
          "ac1011c3-eae8-4b98-863c-f5db417fcbdd"; // Replace this with your API Key, as it's set to defaults it will be used from now onwards

        let response = await axios.get("https://api.thedogapi.com/v1/breeds/");
        this.breeds = response.data;
        console.log(
          "-- (" + this.breeds.length + ") Breeds from TheDogAPI.com"
        );
        this.selected_breed = this.breeds[0].name;
      } catch (err) {
        console.log(err);
      }
    },

    getInfo() {
      const selectedBreedArray = this.breeds.find(
        ({ name }) => name === this.selected_breed
      );
      this.image = selectedBreedArray.image.url;
      this.description = selectedBreedArray.bred_for;

      if (
        selectedBreedArray.country_code === undefined ||
        selectedBreedArray.country_code === ""
      ) {
        this.country_code = "";
      } else {
        this.country_code = selectedBreedArray.country_code.toLowerCase();
        this.country_flag_url = `https://cdnjs.cloudflare.com/ajax/libs/flag-icon-css/3.2.1/flags/1x1/${this.country_code}.svg`;
      }
      if (
        selectedBreedArray.origin === undefined ||
        selectedBreedArray.origin === ""
      ) {
        this.country_name = "Origin Unknown";
        this.country_flag_url = "";
      } else {
        this.country_name = selectedBreedArray.origin;
      }

      this.temperament = selectedBreedArray.temperament;
      // this.wiki_url = selectedBreedArray.wikipedia_url;
    },
    showItem() {
      if (this.image !== "") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.dog-breeds__container {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}
.label {
  font-size: 3rem;
  font-weight: 700;
  color: #888;
  margin: 5px 0;
}

.dog-breeds {
  font-family: "Exo 2", sans-serif;
  font-size: 18px;
  border: solid 1px #aaa;
  padding: 5px;
  border-radius: 10px;
  list-style: none;
  &:focus {
    outline: none;
  }
  &:hover {
    border-color: #888;
    background: #aaa;
  }
}
.option-style {
  background: white;
  &:focus {
    color: white;
  }
}

.breed-info__container {
  position: relative;
  padding: 10px;
  max-width: 600px;
  overflow: hidden;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -ms-flex-wrap: nowrap;
  flex-wrap: nowrap;
  -ms-flex-line-pack: center;
  align-content: center;
}

.image__container {
  position: relative;
}

.flag {
  margin-top: 10px;
  margin-left: 5px;
  position: absolute;
  top: 0;
  left: 0;
  width: 50px;
  border-radius: 15px;
  opacity: 75%;
}

.description,
.temperament {
  font-family: "Exo 2", sans-serif;
  padding: 5px;
  font-size: 18px;
  line-height: 1.5;
  border-radius: 15px;
  background: white;
  &.description {
    margin-top: 5px;
  }
  &.temperament {
    width: 100%;
  }
}

.wiki-link {
  font-size: 50px;
  text-decoration: none;
  color: black;
  padding: 10px;
  &:hover {
    text-decoration: underline;
    color: #888;
  }
}

.image {
  margin-top: 5px;
  width: 100%;
  border-radius: 20px;
}
</style>
