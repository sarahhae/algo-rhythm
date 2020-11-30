<template>
  <div class="form-group">
    <label for="exampleInputmusic">music</label>
    <div class="col-md-10">
      <input
        type="music"
        class="form-control"
        id="exampleInputmusic"
        aria-describedby="music"
        placeholder="search music"
        @input="keyPressed"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      newSet: []
    };
  },
  methods: {
    keyPressed(event) {
      var key = event.target.value;
      axios
        .get(
          "https://api.spotify.com/v1/search?q=" + key + "&amp;type=cloudcast"
        )
        .then(response => {
          this.newSet = response.data;
        })
        .catch(function(error) {
          console.log(error);
        });
      this.$emit("newDataSet", this.newSet);
    }
  }
};
</script>
