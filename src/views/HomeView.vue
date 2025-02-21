<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import Status from '../components/ui/status/Status.vue'
import Button from '../components/ui/bttons/Button.vue'
import Link from '../components/ui/links/Link.vue'

const buttonData = {
  text: 'Hello, World!',
  type: 'default'
}

const link = {
  text: 'Привет',
  isActive: true,
  type: 'default'
}

</script>

<template>
  <main>
<!--    <TheWelcome />-->
    <Button
      :isActive=false
      :type="buttonData.type"
      :text="buttonData.text"
    />
    <Link
        :isActive=true
        :type="link.type"
        :text="link.text"
    />
    <Link
        :isActive=false
        :type="link.type"
        :text="link.text"
    />
  </main>
</template>
