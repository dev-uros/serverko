<script setup>
import { copyToClipboard } from 'quasar'

const clipboard = text => {
  copyToClipboard(text)
}
console.log('👋 This message is being logged by "App.vue", included via Vite')
</script>

<template>
  <q-layout>
    <q-page-container>
      <q-page padding>
        <q-list padding class="rounded-borders">
          <q-expansion-item
            dense
            dense-toggle
            expand-separator
            icon="dns"
            label="206.32.91"
          >
            <q-list dense>
              <q-item>
                <q-item-section>
                  <q-item-label>206.32.91</q-item-label>
                  <q-item-label caption>Ip</q-item-label>
                </q-item-section>
                <q-item-section avatar>
                  <q-btn
                    flat
                    icon="content_copy"
                    size="sm"
                    @click="clipboard('127.01.01')"
                  ></q-btn>
                </q-item-section>
              </q-item>
              <q-item>
                <q-item-section>
                  <q-item-label>Bobasmrad2@</q-item-label>
                  <q-item-label caption>Password</q-item-label>
                </q-item-section>
                <q-item-section avatar>
                  <q-btn
                    flat
                    icon="content_copy"
                    size="sm"
                    @click="clipboard('Bobasmrad2@')"
                  ></q-btn>
                </q-item-section>
              </q-item>
              <q-item>
                <q-item-section>
                  <q-item-label>/var/www/html</q-item-label>
                  <q-item-label caption>Projects root directory</q-item-label>
                </q-item-section>
                <q-item-section avatar>
                  <q-btn
                    flat
                    icon="content_copy"
                    size="sm"
                    @click="clipboard('/var/www/html')"
                  ></q-btn>
                </q-item-section>
              </q-item>
            </q-list>
            <q-timeline color="secondary" style="padding: 15px">
              <q-timeline-entry title="Komunalna milicija" icon="local_police">
                <p class="text-body2 text-weight-light">
                  Backoffice application for communal police of Belgrade
                </p>
                <p class="text-body2 text-weight-light">
                  Root: /var/www/html/communal-police-backoffice
                </p>
              </q-timeline-entry>

              <q-timeline-entry title="A-voucher" icon="redeem">
                <p class="text-body2 text-weight-light">
                  Backoffice application for A-vocher topup service
                </p>
                <p class="text-body2 text-weight-light">
                  Root: /var/www/html/a-voucher
                </p>
              </q-timeline-entry>
            </q-timeline>
          </q-expansion-item>
        </q-list>
        <q-page-sticky position="bottom-right" :offset="[18, 18]">
          <q-fab padding="5px" icon="unfold_more" direction="up" color="accent">
            <q-fab-action
              padding="2px"
              @click="onClick"
              color="primary"
              icon="add_circle"
            >
              <q-tooltip
                class="bg-primary"
                anchor="center left"
                self="center right"
                :offset="[10, 10]"
              >
                Kreiraj
              </q-tooltip></q-fab-action
            >
            <q-fab-action
              padding="2px"
              @click="onClick"
              color="primary"
              icon="download"
            >
              <q-tooltip
                class="bg-positive"
                anchor="center left"
                self="center right"
                :offset="[10, 10]"
              >
                Exportuj
              </q-tooltip></q-fab-action
            >
          </q-fab>
        </q-page-sticky>
      </q-page>
    </q-page-container>
  </q-layout>
</template>
