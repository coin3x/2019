<template>
  <div
    class="session"
    :class="{'clickable': data.type !== 'BREAK' && data.type !== 'E' }"
    @click="data.type !== 'BREAK' && data.type !== 'E' ? openPop(data.id) : null"
  >
    <p class="tag">
      <span
        v-for="(tag, index) in data.tag"
        :key="`tag-${index}`"
      >
        {{ tag.zh }}
      </span>
    </p>
    <h2 class="session-title">{{ data.zh.title }}</h2>
    <p class="session-speaker">
      <span
        v-for="(speaker, index) in data.speakers"
        :key="speaker.name"
      >
        {{ speaker.zh.name }}
        {{ data.speakers.length - 1 !== index ? ' / ' : '' }}
      </span>
    </p>
    <p v-if="isMobile" class="room">
      {{ data.room }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object
    },
    isMobile: {
      default: false,
      type: Boolean
    }
  },
  methods: {
    openPop (id) {
      this.$router.push({ name: 'AgendaPopup', params: { sessionId: id } })
    }
  }
}
</script>
