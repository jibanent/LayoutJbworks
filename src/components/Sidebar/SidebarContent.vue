<template>
  <vue-perfect-scrollbar :settings="settings">
    <nav class="idb-sidebar-nav">

      <ul class="idb-nav list-unstyled p-0">
        <template v-for="(menu, index) in sideBarLinks.routes">
          <li
            v-if="menu.child_routes!=null"
            :key="index"
            :class="[ 'nav-item', { 'active': menu.active } ]"
            @click="toggleActive(index)"
          >
            <a href="javascript:void(0)" class="nav-link">
              <i :class="menu.menu_icon" class="menu-icon" />
              <span class="menu-title">{{ textTruncate($t(menu.menu_title)) }}</span>
            </a>
            <ul class="list-unstyled sub-menu" @click="toggleActive(index)">
              <router-link v-for="(subMenu, key) in menu.child_routes" :key="key" :to="subMenu.path" tag="li">
                <a href="javascript:void(0)" class="sub-menu-nav-link">
                  <span>{{ textTruncate($t(subMenu.menu_title)) }}</span>
                </a>
              </router-link>
            </ul>
          </li>
          <router-link
            v-else
            :key="index"
            :to="menu.path"
            tag="li"
            class="nav-item"
            @click.native="toggleActive(index)"
          >
            <a class="nav-link">
              <i :class="menu.menu_icon" class="mr-15" />
              <span class="menu-title">{{ textTruncate($t(menu.menu_title)) }}</span>
            </a>
          </router-link>
        </template>
      </ul>
    </nav>
    <div class="idb-server-progress p-30">
      <div class="progress-wrap mb-30">
        <h5 class="text-white">{{ $t('message.todaySales') }}</h5>
        <b-progress :value="30" :max="50" class="mb-15" variant="warning" height="5px" />
        <p class="fs-12">15200 {{ $t('message.itemsSold') }}</p>
      </div>
      <div class="progress-wrap mb-30">
        <h5 class="text-white">{{ $t('message.customerTarget') }}</h5>
        <b-progress :value="70" :max="100" class="mb-15" height="5px" variant="danger" />
        <p class="fs-12">78% {{ $t('message.ofTheMonth') }}</p>
      </div>
    </div>
  </vue-perfect-scrollbar>
</template>

<script>
import sideBarLinks from './menu.js'
import { textTruncate } from 'Helpers/helpers'

export default {
  data() {
    return {
      settings: {
        maxScrollbarLength: 220
      },
      sideBarLinks
    }
  },
  methods: {
    textTruncate(text) {
      return textTruncate(text, 18)
    },
    toggleActive(index) {
      for (const selectedRoute in this.sideBarLinks.routes) {
        if (selectedRoute == index) {
          this.sideBarLinks.routes[selectedRoute].active = !this.sideBarLinks.routes[selectedRoute].active
        } else {
          this.sideBarLinks.routes[selectedRoute].active = false
        }
      }
    }
  }

}
</script>
