<template>
  <q-layout view="hHh Lpr lFf">
    <q-layout-header>
      <q-toolbar
        color="dark"
        :inverted="$q.theme === 'ios'"
      >
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
        >
          <q-icon name="menu" />
        </q-btn>

        <q-toolbar-title @click.native="openWindow()">
          Attendance
          <div slot="subtitle">Electron v{{ version }}</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-layout-header>

    <q-layout-drawer
      v-model="leftDrawerOpen"
      :content-class="$q.theme === 'mat' ? 'bg-grey-2' : null"
    >
      <q-list
        no-border
        link
        inset-delimiter
      >
        <q-list-header>MENU</q-list-header>
        <q-item to="/">
          <q-item-side icon="school" />
          <q-item-main label="Chats" sublabel="Chats em atendimento" />
        </q-item>
        <q-item to="/bot">
          <q-item-side icon="code" />
          <q-item-main label="Bot" sublabel="Configuração do seu bot" />
        </q-item>
      </q-list>
    </q-layout-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'
import electron from 'electron'

const { app, BrowserWindow } = electron.remote;

const display = electron.screen.getAllDisplays();

console.log(display);

export default {
  name: 'MyLayout',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      version: app.getVersion()
    }
  },
  methods: {
    openURL,
    openWindow() {
      const win = new BrowserWindow();
      win.loadURL('https://schoolofnet.com');
    }
  }
}
</script>

<style>
</style>
