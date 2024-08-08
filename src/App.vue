<script>
export default {
  data: () => ({
    jsFrameworks: ["React.Js", "Vue.Js", "Angular"],
    otherFrameworks: []
  }),
  methods: {
    handleChange(tags) {
      this.jsFrameworks = [...tags]
    }
  }
}
</script>

<template>
  <h1>
    Hello world
  </h1>
  <p>{{ jsFrameworks }}</p>
  <tags-input :selectedTags="jsFrameworks" @change="handleChange" />
  <p>{{ otherFrameworks }}</p>
  <tags-input :selectedTags="otherFrameworks" @change="otherFrameworks = [...$event]" />
</template>

<style scoped>
h1 {
  color: rgb(79, 214, 214)
}
</style>
