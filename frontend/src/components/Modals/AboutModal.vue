<template>
  <Dialog v-model:open="show" :size="'sm'">
    <template #body>
      <div class="p-4 pt-5">
        <div class="flex justify-center">
          <div class="flex flex-col items-center">
            <img
              v-if="brand.logo"
              :src="brand.logo"
              class="mb-3 size-12 rounded object-cover"
            />
            <CRMLogo v-else class="mb-3 size-12" />
            <h3 class="text-2xl-semibold text-ink-gray-9">
              {{ brand.name || 'GARP CRM' }}
            </h3>
          </div>
        </div>
        <hr class="border-t my-3 mx-2" />
        <div>
          <a
            v-for="link in links"
            :key="link.label"
            class="flex py-2 px-2 hover:bg-surface-gray-1 rounded cursor-pointer"
            target="_blank"
            :href="link.url"
          >
            <component
              :is="link.icon"
              v-if="link.icon"
              class="size-4 mr-2 text-ink-gray-7"
            />
            <span class="text-base text-ink-gray-8">
              {{ link.label }}
            </span>
          </a>
        </div>
        <hr class="border-t my-3 mx-2" />
        <p class="text-sm text-ink-gray-6 px-2 mt-2">
          <!-- Upstream copyright, licence and no-warranty notices live on the
               licences page; this link is how the dialog displays them. -->
          © AICONEC and contributors ·
          <a
            href="https://garp.aiconec.com/docs/licences"
            target="_blank"
            class="underline underline-offset-2 hover:text-ink-gray-8"
          >
            {{ __('Licences') }}
          </a>
        </p>
      </div>
    </template>
  </Dialog>
</template>
<script setup>
import CRMLogo from '@/components/Icons/CRMLogo.vue'
import LucideGlobe from '~icons/lucide/globe'
import LucideHeadset from '~icons/lucide/headset'
import LucideBookOpen from '~icons/lucide/book-open'
import { getSettings } from '@/stores/settings'

let show = defineModel({ type: Boolean })

const { brand } = getSettings()

let links = [
  {
    label: __('Website'),
    url: 'https://aiconec.com',
    icon: LucideGlobe,
  },
  {
    label: __('Documentation'),
    url: 'https://garp.aiconec.com/docs/modules/crm',
    icon: LucideBookOpen,
  },
  {
    label: __('Contact Support'),
    url: 'https://aiconec.com/support',
    icon: LucideHeadset,
  },
]
</script>
