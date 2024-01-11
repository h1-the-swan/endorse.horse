<template>
  <div class="topic-row">
    <div :class="alignLeftOrRight">
      <div class="host-head" v-if="endorser === 'Emily'">
        <img src="@/assets/emily-head.png" />
      </div>
      <div class="bubble" :class="hostBubble">
        <h3 class="name" :class="{ propercase: shouldICapitalise }">
          <a v-if="link" target="_blank" :href="link">
            <span v-html="service_or_item"></span>
            <i class="material-icons">link</i>
          </a>
          <span v-else>{{ service_or_item }}</span>
        </h3>
        <span v-if="category">{{ category }}</span>
        <br />
        <span>{{ episode_date }}</span>
        <!-- <p class="topic-name"><a target="_blank" :href="ep_url">{{ep_title}}</a></p> -->
      </div>
      <div class="host-head" v-if="endorser === 'Lisa'">
        <img src="@/assets/lisa-head.png" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps<{
  episode_date: string;
  service_or_item: string;
  endorser: string;
  category: string;
  notes?: string;
  link?: string;
}>()
const hostBubble = computed(() => {
  return {
    griffin: props.endorser === "Emily",
    rachel: props.endorser === "Lisa"
  }
})
const alignLeftOrRight = computed(() => {
  return {
    left: props.endorser === "Emily",
    right: props.endorser === "Lisa"
  }
})
const shouldICapitalise = computed(() => {
  const addressPattern = /\b\w{1,63}\.\w{1,63}/i;
  return addressPattern.test(props.service_or_item) ? false : true
})
</script>

<style lang="scss" scoped>
$f_size: 1em;
$tgl_width: 32px;
$tgl_height: $tgl_width / 2.5;
$primary: #15A2FE;
$primary_light: #6dd3ff;
$grey: #bbb;
$rach_colour: rgb(254, 225, 133);
$grif_colour: rgb(252, 132, 120);
$break-small: 500px;


h3 {
  font-size: $tgl_width;
  margin: 0;
  display: block;
  padding: 8px 0 0 0;
  -webkit-font-smoothing: antialiased;
  letter-spacing: 0.2px;

  @media screen and (max-width: $break-small) {
    font-size: 5vw;
    line-height: 1;
  }

  i {
    font-size: 80%;
    transform: translateY(8%);

    @media screen and (max-width: $break-small) {
      transform: translateY(5%);
    }
  }

  // i {
  //   line-height: 1.3em;
  //   display: inline;
  //   vertical-align: bottom;
  //   @media screen and (max-width: $break-small) {
  //     line-height: .85em;
  //     font-size: 1em;
  //   }
  // }
  a {
    color: inherit;
    text-decoration: none;
    border: 0;
  }
}

p {
  margin: ($tgl_width/8) 0 0 0;
  padding: 4px 0;
  font-style: italic;

  a {
    color: inherit;
    text-decoration: none;
    line-height: 1.5;
  }

  @media screen and (max-width: $break-small) {
    font-size: 16px;
  }
}

.propercase {
  text-transform: capitalize;
}

h3 {
  display: inline;

  a:hover {
    color: black;
  }
}


.griffin {
  background-color: $grif_colour;
  color: #562D29;
  padding: 20px 40px 10px 25px;
  border-radius: ($tgl_width * 2) ($tgl_width * 2) ($tgl_width * 2) 10px;

  .topic-name {
    a:hover {
      border-bottom: 2px solid #574305;
    }
  }
}

.rachel {
  background-color: $rach_colour;
  color: #574305;
  padding: 20px 25px 10px 40px;
  border-radius: ($tgl_width * 2) ($tgl_width * 2) 10px ($tgl_width * 2);



  .topic-name {
    a:hover {
      border-bottom: 2px solid #574305;
    }
  }
}

.bubble {
  display: inline-block;
  margin: 20px 0 0;
  max-width: 75%;
  min-width: 20%;
  box-sizing: border-box;
}

.left {
  text-align: left;
  transform-origin: left;
}

.right {
  text-align: right;
  transform-origin: right;
}

.topic-row {
  border: 0;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  position: relative;
  width: 100%; //min-width: 260px;
  display: block;
  transform: scale(0.8);

}

.host-head {
  display: inline-block;
  vertical-align: bottom;
  width: 9%;
  min-width: 48px;
  height: auto;
  box-sizing: border-box;
}

img {
  width: 100%;
  object-fit: contain;
  box-sizing: border-box;
  display: block;
  padding: 0 2px;

}
</style>
