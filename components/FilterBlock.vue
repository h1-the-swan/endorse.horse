<template>
  <div id="filter-wrap">
    <div id="search-wrap">
      <input
        class="searchbox"
        type="text"
        :placeholder="placeholderMsg"
        v-model="options.search"
      />
      <div class="counter">{{ counterAnim }}</div>
    </div>

    <div class="filter-options">
      <div class="control-container">
        <div class="label">Hide Latest Episode</div>
        <div class="switch-wrap">
          <label for="spoiler-switch">
            <input
              type="checkbox"
              id="spoiler-switch"
              v-model="options.spoilerMode"
            />
            <span class="switch"></span>
            <span class="toggle"></span>
          </label>
        </div>
      </div>

      <div class="control-container">
        <div class="label">Include Small Wonders</div>
        <div class="switch-wrap">
          <label for="small-wonder-switch">
            <input
              type="checkbox"
              id="small-wonder-switch"
              v-model="options.smallWonderMode"
            />
            <span class="switch"></span>
            <span class="toggle"></span>
          </label>
        </div>
      </div>

      <div class="control-container">
        <div class="select-wrap">
          <select v-model="options.selectedCategory">
            <option
              v-for="category of categories"
              :key="category"
              :value="category"
              >{{ category }}</option
            >
          </select>
        </div>
      </div>

      <div class="btn-wrap control-container">
        <div class="btn-bg">
          <button
            class="left"
            @click="setSort('name')"
            :class="{ selected: options.sortBy == 'name' }"
          >
            A-Z
          </button>
          <svg
            class="arrow"
            viewBox="0 0 30 30"
            :class="options.sortAsc ? 'asc' : 'desc'"
          >
            <path
              class="arrow-icon"
              xmlns="http://www.w3.org/2000/svg"
              d="M0,15C0,6.7,6.7,0,15,0s15,6.7,15,15s-6.7,15-15,15S0,23.3,0,15z M17.7,22v-7h4.3c0.6,0,1-0.8,0.5-1.2l-6.9-6.9  c-0.3-0.3-0.7-0.3-1,0l-7,6.9C7.1,14.2,7.4,15,8.1,15h4.3v7c0,0.4,0.3,0.7,0.7,0.7h3.9C17.3,22.7,17.7,22.4,17.7,22z"
            />
          </svg>
          <button
            class="right"
            @click="setSort('ep_num')"
            :class="{ selected: options.sortBy == 'ep_num' }"
          >
            Ep #
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>
$f_size: 1em;
$tgl_width: 32px;
$tgl_height: $tgl_width / 2.5;
$primary: #15a2fe;
$primary_light: #6dd3ff;
$grey: #bbb;
$break-small: 765px;

.filter-options {
  padding: 16px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

select {
  appearance: none;
  border-radius: 20px;
  border: 0;
  color: white;
  background-color: $primary_light;
  font-weight: bold;
  padding: 6px 15px;
  font-size: $f_size;
  outline: 0;
  white-space: nowrap;
  width: 185px;
  transition: all 0.5s;
  box-sizing: content-box;
  border-radius: 20px;
  cursor: pointer;
  position: relative;
}

.select-wrap {
  display: inline-block;
  position: relative;
  &:after {
    content: "";
    position: absolute;
    top: 50%;
    right: 5%;
    -webkit-transform: translateY(-50%);
    transform: translateY(-50%);
    width: 2px;
    height: 0;
    border-top: 9px solid white;
    border-left: 8px solid transparent;
    border-right: 8px solid transparent;
    border-radius: 3px;
    pointer-events: none;
  }
}

#filter-wrap {
  width: 100%;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  display: block;
}
#search-wrap {
  border: 2px solid $grey;
  box-sizing: border-box;
  position: relative;
  text-align: left;
  display: block;

  .counter {
    font-size: 2.5em;
    font-weight: bold;
    color: #15a2fe;
    width: auto;
    text-align: right;
    position: absolute;
    display: inline-block;
    padding: 16px 16px 16px 0;
    margin: 0;
    border: 0;
    right: 0;
    height: 100%;
    line-height: 50px;

    @media screen and (max-width: $break-small) {
      font-size: 5.5vw;
    }
  }
}
.searchbox {
  border: 0;
  color: #15a2fe;
  position: relative;
  display: inline-block;
  font-size: $f_size * 2.5;
  font-weight: bold;
  width: 90%;
  padding: 16px 8px 16px 16px;
  outline: 0;
  text-align: left;
  box-sizing: border-box;
  @media screen and (max-width: $break-small) {
    font-size: 5.5vw;
    width: 80%;
  }

  &::placeholder {
    opacity: 0.3;
  }
}

.arrow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 30px;
  padding: 0;
  margin: 0;

  .arrow-icon {
    fill: white;
    transition: all 1s cubic-bezier(0.215, 1.545, 0.53, 0.945);
    transform-origin: center;
    margin: 0;
    padding: 0;
    -webkit-backface-visibility: hidden;
    -webkit-transform: translateZ(0) scale(1, 1);
    transform: translateZ(0);
  }

  &.desc {
    .arrow-icon {
      fill: white;
      -webkit-backface-visibility: hidden;
      -webkit-transform: translateZ(0) scale(1, 1);
      transition: all 1s cubic-bezier(0.215, 1.545, 0.53, 0.945);
      transform: translateZ(0);
      transform-origin: center;
      transform: rotate(180deg);
    }
  }
}

.btn-wrap {
  position: relative;
  display: inline-block;
  border-radius: 100px;
  padding: 0;
  box-sizing: border-box;
  text-align: right;

  @media (max-width: 720px) {
    display: block;
    width: 100%;
    text-align: center;
  }
}

.btn-bg {
  position: relative;
  background-color: $grey;
  display: inline-block;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border-radius: 20px;
}

button {
  border: 0;
  color: white;
  background-color: $grey;
  font-weight: bold;
  padding: 6px 15px;
  font-size: $f_size;
  outline: 0;
  white-space: nowrap;
  width: $tgl_width;
  transition: all 0.5s;
  box-sizing: content-box;
  border-radius: 20px;
  cursor: pointer;

  @media (max-width: 1000px) {
    width: 62px;
  }

  &.selected {
    background-color: $primary;
    color: white;
    border-radius: 20px;

    &.left {
      padding-right: 45px;
    }

    &.right {
      padding-left: 45px;
    }

    span {
      display: inline;
    }
  }
}

input[type="checkbox"] {
  display: none;

  &:checked ~ .toggle {
    background: $primary;
    left: ($tgl_width - ($tgl_height * 1.4 - $tgl_height) / 2) - $tgl_height;
    transition: 0.5s;
  }

  &:checked ~ .switch {
    background: $primary_light;
    transition: 0.5s;
  }
}

.switch {
  display: block;
  width: $tgl_width;
  height: $tgl_height;
  background: $grey;
  border-radius: $tgl_height / 2;
  position: absolute;
  top: 0;
  transition: 0.5s;
  cursor: pointer;
}

.toggle {
  height: $tgl_height * 1.4;
  width: $tgl_height * 1.4;
  border-radius: 50%;
  background: white;
  position: absolute;
  top: ($tgl_height * 1.4 - $tgl_height) / -2;
  left: ($tgl_height * 1.4 - $tgl_height) / -2;
  box-shadow: 0 $tgl_width / 50 $tgl_width / 25 rgba(black, 0.4);
  transition: 0.5s;
  cursor: pointer;
}

.switch-wrap {
  display: inline-block;
  margin: 0;
  width: $tgl_width;
  height: $tgl_height;
  position: relative;
  text-align: right;
}

.label {
  display: inline-block;
  margin: 0 ($tgl_height) 0 0;
  padding: 0;
  position: relative;
  box-sizing: border-box;
  text-align: left;

  @media (max-width: 600px) {
    width: 170px;
  }
}

.control-container {
  padding: 0;
  display: inline-block;
  box-sizing: border-box;
  text-align: left;

  @media (max-width: 1000px) {
    width: 50%;
    padding: 10px 0;
    text-align: center;
  }

  @media (max-width: 600px) {
    width: 100%;
    padding: 10px 0;
  }
}
</style>
