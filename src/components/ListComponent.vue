<script>
import axios from 'axios';

export default {
  data () {
    return {
      leftColElements: null,
      rightColElements: null
    }
  },
  mounted () {
    axios
        .get('https://jsonplaceholder.typicode.com/posts')
        .then(response => {
          this.leftColElements = response.data.splice(0, response.data.length / 2);
          this.rightColElements = response.data;
        })
  }
}
</script>

<template>
  <div class="container">
    <div class="elements-list">
      <ul class="elements-col-left">
        <li v-for="(item, index) in leftColElements">{{ index + 1 }} {{ item.title }}</li>
      </ul>
      <ul class="elements-col-right">
        <li v-for="(item, index) in rightColElements">{{ index + 51 }} {{ item.title }}</li>
      </ul>
    </div>
  </div>
</template>

<style lang="scss">
@import '../assets/variables';

.elements-list {
  display: flex;
  gap: 20px;

  @media screen and (max-width:720px) {
    display: block;
  }

  ul {
    padding: 0;
    margin: 0;
    list-style: none;
    -webkit-box-shadow: 0px 0px 21px -7px rgba(0,0,0,0.3);
    -moz-box-shadow: 0px 0px 21px -7px rgba(0,0,0,0.3);
    box-shadow: 0px 0px 21px -7px rgba(0,0,0,0.3);
    border-radius: 10px;
    overflow: hidden;

    @media screen and (max-width:720px) {
      margin-bottom: 30px;
    }

    &:first-child {
      li:nth-child(odd) {
        background-color: $secondary;
      }
    }

    &:last-child {
      li:nth-child(even) {
        background-color: $secondary;
      }

      @media screen and (max-width:720px) {
        li:nth-child(even) {
          background-color: #ffffff;
        }

        li:nth-child(odd) {
          background-color: $secondary;
        }
      }
    }

    li {
      min-height: 60px;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      padding: 5px 20px;

      &:hover {
        cursor: pointer;
        background-color: $light !important;
      }
    }
  }
}

</style>