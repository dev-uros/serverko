<script setup>
import { copyToClipboard, useQuasar } from 'quasar'
import { ref } from 'vue'

const $q = useQuasar()
const clipboard = text => {
  copyToClipboard(text)
  $q.notify({
    message: 'Copied to clipboard',
    color: 'positive',
    icon: 'check_circle',
    iconColor: 'white',
    timeout: 1500
  })
}

const deleteServer = () => {
  $q.dialog({
    title: 'Server',
    message:
      'Are you sure you want to delete server (this action can not be undone)',
    cancel: true,
    ok: {
      push: true,
      color: 'red',
      label: 'delete'
    },
    cancel: {
      flat: true
    },
    focus: 'cancel',
    persistent: true
  }).onOk(() => {
    console.log('>>>> OK')
  })
}

const serverDialog = ref(false)
const projectDialog = ref(false)

const deleteProject = () => {
  $q.dialog({
    title: 'Project',
    message:
      'Are you sure you want to delete project (this action can not be undone)',
    cancel: true,
    ok: {
      push: true,
      color: 'red',
      label: 'delete'
    },
    cancel: {
      flat: true
    },
    focus: 'cancel',
    persistent: true
  }).onOk(() => {
    console.log('>>>> OK')
  })
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
            <q-card-actions align="center">
              <p class="text-h4">Server</p>
            </q-card-actions>
            <q-card-actions align="evenly">
              <q-btn
                rounded
                style="width: 45%"
                label="Edit"
                icon="edit"
                color="blue"
                @click="projectDialog = true"
              ></q-btn>
              <q-btn
                rounded
                style="width: 45%"
                label="Delete"
                icon="delete"
                color="red"
                @click="deleteServer"
              ></q-btn>
            </q-card-actions>
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
            <q-separator inset class="q-mt-md" />
            <q-card-actions align="center">
              <p class="text-h4">
                Projekti
                <q-btn
                  round
                  icon="add"
                  color="positive"
                  size="sm"
                  @click="projectDialog = true"
                ></q-btn>
              </p>
            </q-card-actions>
            <q-timeline color="secondary" class="q-pl-md q-pr-md">
              <q-timeline-entry icon="local_police">
                <template v-slot:title>
                  Komunalna milicija
                  <q-btn
                    round
                    icon="delete"
                    color="red"
                    size="sm"
                    class="q-mr-sm q-ml-sm"
                    @click="deleteProject"
                  />
                  <q-btn
                    round
                    icon="edit"
                    color="primary"
                    size="sm"
                    @click="projectDialog = true"
                  />
                </template>
                <p class="text-body2 text-weight-light">
                  Backoffice application for communal police of Belgrade
                </p>
                <p
                  class="text-body2 text-weight-light"
                  style="cursor: pointer"
                  @click="clipboard('/var/www/html/communal-police-backoffice')"
                >
                  Root: /var/www/html/communal-police-backoffice
                </p>
              </q-timeline-entry>
            </q-timeline>
          </q-expansion-item>
        </q-list>
        <q-page-sticky position="bottom-right" :offset="[18, 18]">
          <q-fab padding="5px" icon="unfold_more" direction="up" color="accent">
            <q-fab-action
              padding="2px"
              @click="serverDialog = true"
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
        <q-dialog v-model="serverDialog" persistent>
          <q-card style="width: 300px">
            <q-card-section>
              <div class="text-h6">
                Create New Server
                <q-btn
                  icon="close"
                  round
                  size="sm"
                  style="float: right"
                  flat
                  color="red"
                  v-close-popup
                />
              </div>
            </q-card-section>

            <q-card-section class="q-pt-none">
              <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
                <q-input
                  dense
                  v-model="name"
                  label="Server IP *"
                  hint="Enter server IP address"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Please type something'
                  ]"
                />

                <q-input
                  dense
                  type="text"
                  v-model="age"
                  label="Server password *"
                  hint="Enter server password"
                  lazy-rules
                  :rules="[
                    val =>
                      (val !== null && val !== '') || 'Please type your age',
                    val => (val > 0 && val < 100) || 'Please type a real age'
                  ]"
                />

                <q-input
                  dense
                  v-model="name"
                  label="Projects root directory"
                  hint="Enter projects root directory"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Please type something'
                  ]"
                />
                <div>
                  <q-btn label="Submit" type="submit" color="primary" />
                  <q-btn
                    label="Reset"
                    type="reset"
                    color="primary"
                    flat
                    class="q-ml-sm"
                  />
                </div>
              </q-form>
            </q-card-section>
          </q-card>
        </q-dialog>
        <q-dialog v-model="projectDialog" persistent>
          <q-card style="width: 300px">
            <q-card-section>
              <div class="text-h6">
                Create New Project for Server
                <q-btn
                  icon="close"
                  round
                  size="sm"
                  style="float: right"
                  flat
                  color="red"
                  v-close-popup
                />
              </div>
            </q-card-section>

            <q-card-section class="q-pt-none">
              <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
                <q-input
                  dense
                  v-model="name"
                  label="Project name *"
                  hint="Enter project name"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Please type something'
                  ]"
                />

                <q-input
                  dense
                  type="text"
                  v-model="age"
                  label="Project description *"
                  hint="Enter project description"
                  lazy-rules
                  :rules="[
                    val =>
                      (val !== null && val !== '') || 'Please type your age',
                    val => (val > 0 && val < 100) || 'Please type a real age'
                  ]"
                />

                <q-input
                  dense
                  v-model="name"
                  label="Project root directory"
                  hint="Enter project root directory"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Please type something'
                  ]"
                />
                <div>
                  <q-btn label="Submit" type="submit" color="primary" />
                  <q-btn
                    label="Reset"
                    type="reset"
                    color="primary"
                    flat
                    class="q-ml-sm"
                  />
                </div>
              </q-form>
            </q-card-section>
          </q-card>
        </q-dialog>
      </q-page>
    </q-page-container>
  </q-layout>
</template>
