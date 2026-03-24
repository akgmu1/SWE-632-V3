<script setup lang="ts">
import {
  ArchiveBoxIcon,
  BugAntIcon,
  HomeIcon,
  PencilSquareIcon,
  PlusIcon,
  PresentationChartLineIcon,
  TrashIcon,
} from '@heroicons/vue/24/outline'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/solid'
import { type Ref, ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import { notifications } from './notification'

const IS_DEV = import.meta.env.DEV
const drawerCheckbox: Ref<HTMLInputElement | null> = ref(null)
</script>

<template>
  <div class="drawer lg:drawer-open">
    <input ref="drawerCheckbox" id="my-drawer-1" type="checkbox" class="drawer-toggle" />
    <div class="drawer-content">
      <!-- The primary content here -->
      <div class="navbar bg-base-100 shadow-sm block lg:hidden">
        <div class="flex justify-start items-center">
          <label for="my-drawer-1" class="btn btn-square btn-ghost">
            <Bars3Icon class="size-6" />
          </label>
          <RouterLink to="/">
            <div class="flex pt-2 justify-center items-center gap-2">
              <img src="/logo.png" class="size-9 rounded" />
              <div class="text-2xl font-semibold">Task Manager</div>
            </div>
          </RouterLink>
        </div>
      </div>
      <div class="px-4">
        <RouterView />
      </div>
    </div>
    <div class="drawer-side">
      <label for="my-drawer-1" aria-label="close sidebar" class="drawer-overlay"></label>
      <div class="bg-base-300 min-h-full">
        <div class="hidden lg:block">
          <RouterLink to="/">
            <div class="flex pt-2 justify-center items-center gap-2">
              <img src="/logo.png" class="size-9 rounded" />
              <div class="text-2xl font-semibold">Task Manager</div>
            </div>
          </RouterLink>
        </div>
        <ul class="menu w-64 p-4 gap-2 lg:gap-1">
          <!-- Sidebar content here -->
          <li class="block rounded lg:hidden bg-base-content/7 lg:bg-none">
            <button @click="drawerCheckbox!.checked = false" class="w-full">
              <XMarkIcon class="size-5" />
              Close
            </button>
          </li>
          <li class="bg-base-content/7 rounded lg:bg-transparent">
            <RouterLink
              to="/"
              active-class="bg-primary text-primary-content"
              @click="drawerCheckbox!.checked = false"
            >
              <HomeIcon class="size-5" />
              Home
            </RouterLink>
          </li>
          <li class="bg-base-content/7 rounded lg:bg-transparent">
            <RouterLink
              to="/create"
              active-class="bg-primary text-primary-content"
              @click="drawerCheckbox!.checked = false"
            >
              <PlusIcon class="size-5" />
              Create Task
            </RouterLink>
          </li>
          <li class="bg-base-content/7 rounded lg:bg-transparent">
            <RouterLink
              to="/edit"
              active-class="bg-primary text-primary-content"
              @click="drawerCheckbox!.checked = false"
            >
              <PencilSquareIcon class="size-5" />
              Edit Task
            </RouterLink>
          </li>
          <li class="bg-base-content/7 rounded lg:bg-transparent">
            <RouterLink
              to="/delete"
              active-class="bg-primary text-primary-content"
              @click="drawerCheckbox!.checked = false"
            >
              <TrashIcon class="size-5" />
              Delete Task
            </RouterLink>
          </li>
          <li class="bg-base-content/7 rounded lg:bg-transparent">
            <RouterLink
              to="/categories"
              active-class="bg-primary text-primary-content"
              @click="drawerCheckbox!.checked = false"
            >
              <ArchiveBoxIcon class="size-5" />
              Manage Categories
            </RouterLink>
          </li>
          <li class="bg-base-content/7 rounded lg:bg-transparent">
            <RouterLink
              to="/stats"
              active-class="bg-primary text-primary-content"
              @click="drawerCheckbox!.checked = false"
            >
              <PresentationChartLineIcon class="size-5" />
              Statistics
            </RouterLink>
          </li>
          <template v-if="IS_DEV">
            <li class="bg-base-content/7 rounded lg:bg-transparent">
              <RouterLink
                to="/debug"
                active-class="bg-primary text-primary-content"
                @click="drawerCheckbox!.checked = false"
              >
                <BugAntIcon class="size-5" />
                Debug
              </RouterLink>
            </li>
          </template>
        </ul>
      </div>
    </div>
  </div>

  <!-- Notifications -->
  <div class="toast toast-end toast-bottom">
    <div
      v-for="n in notifications"
      class="alert"
      :class="{
        'alert-success': n.type === 'success',
        'alert-info': n.type === 'info',
        'alert-warning': n.type === 'warning',
        'alert-error': n.type === 'error',
      }"
    >
      {{ n.message }}
    </div>
  </div>
</template>
