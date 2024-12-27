<script setup lang="ts">
import {
  NavigationMenu,
  NavigationMenuItem,
  NavigationMenuLink,
  NavigationMenuList,
  navigationMenuTriggerStyle,
} from '@/components/ui/navigation-menu'
import darkLight from './ui/dark-light/dark-light.vue';
import ashitAvatar from './ashitAvatar.vue';


</script>

<template>
  <NavigationMenu>
    <NavigationMenuList>
      <NavigationMenuItem>
        <NavigationMenuLink href="/docs/introduction" :class="navigationMenuTriggerStyle()">
          Ashit's Portfolio
        </NavigationMenuLink>
      </NavigationMenuItem>
      <NavigationMenuItem>
        <NavigationMenuLink href="/docs/introduction" :class="navigationMenuTriggerStyle()">
          Projects
        </NavigationMenuLink>
      </NavigationMenuItem>
    </NavigationMenuList>
    <darkLight/>
  </NavigationMenu>
</template>