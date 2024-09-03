<script lang="ts" setup>
const timestamp = useState('timestamp', () => new Date().getTime())

const isoTime = computed(() => new Date(timestamp.value).toISOString())

const updateTimestamp = () => {
  timestamp.value = new Date().getTime()
}

let intervalId: NodeJS.Timeout
onMounted(() => {
  updateTimestamp()
  intervalId = setInterval(() => {
    updateTimestamp()
  }, 10000)
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

<template>
  <div>
    <p>Time: {{ isoTime }}</p>
    <PostsList />
  </div>
</template>
