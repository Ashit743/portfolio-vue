<script setup lang="ts">
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'
</script>

<template>
  <Avatar>
    <AvatarImage src="https://media.licdn.com/dms/image/v2/D5603AQFudCNxW9XvMw/profile-displayphoto-shrink_200_200/profile-displayphoto-shrink_200_200/0/1731948945527?e=1740614400&v=beta&t=3lQBlELExSKwbzD7WDuEuqxx36Cd3UFP062szfiOIIE" alt="@radix-vue" />
    <AvatarFallback>AD</AvatarFallback>
  </Avatar>
</template>