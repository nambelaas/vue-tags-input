<template>

  <div class="tags-input-wrapper">
    <div class="tags-length">You have {{ tags.length }} tags</div>
    <div class="tags-list-input">
      <span class="tag-item" v-for="(tag, index) in tags" :key="index">
        {{ tag }}
        <a href="#" class="remove-tag" @click.prevent="removeTags(index)">&times;</a>
      </span>
      <input class="tag-input" type="text" v-model.trim="newTag" @keydown.enter="addNewTag"
        @keydown.tab.prevent="addNewTag" @keydown.delete="removeLastTag" :class="{ 'tag-exists': isTagExists }" />
    </div>
  </div>



</template>

<script>
export default {
  props: {
    selectedTags: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      tags: [...this.selectedTags],
      newTag: ""
    }
  },
  computed: {
    isTagExists() {
      return this.tags.includes(this.newTag)
    }
  },
  watch: {
    newTag(newVal) {
      if (newVal.indexOf(",") > -1) {
        this.newTag = newVal.slice(0, -1)
        this.addNewTag()
      }
    }
  },
  methods: {
    addNewTag() {
      if (this.newTag && !this.isTagExists) {
        this.tags.push(this.newTag)
        this.newTag = ""
        this.$emit('change', this.tags)
      }
    },
    removeTags(index) {
      this.tags.splice(index, 1)
      this.$emit('change', this.tags)
    },
    removeLastTag() {
      if (this.newTag.length === 0) {
        this.removeTags(this.tags.length - 1)
      }
    }
  },
  emits: ['change']
}
</script>

<style scoped>
.tag-exists {
  color: red;
  text-decoration: line-through;
}

.tags-input-wrapper .tags-list-input {
  display: flex;
  gap: 10px;
  padding: 8px 10px;
  border: 1px solid #c5dbf0;
  margin-top: 10px;
}

.tags-list-input span.tag-item {
  padding: 6px 0.9rem;
  background-color: #5b70e9;
  color: white;
  border-radius: 6px;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.tags-list-input span.tag-item a.remove-tag {
  text-decoration: none;
  color: white;
  vertical-align: middle;
}

.tags-list-input input.tag-input {
  border: none;
  width: 100%
}

.tags-list-input input.tag-input:focus {
  outline: none;
}
</style>