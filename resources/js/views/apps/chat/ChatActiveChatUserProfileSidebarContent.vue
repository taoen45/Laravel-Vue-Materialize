<script setup>
import { PerfectScrollbar } from 'vue3-perfect-scrollbar'
import { useChat } from './useChat'
import { useChatStore } from '@/views/apps/chat/useChatStore'

const emit = defineEmits(['close'])

const store = useChatStore()
const { resolveAvatarBadgeVariant } = useChat()
</script>

<template>
  <template v-if="store.activeChat">
    <!-- Close Button -->
    <div
      class="me-3 pt-3"
      :class="$vuetify.locale.isRtl ? 'text-left' : 'text-right'"
    >
      <IconBtn @click="$emit('close')">
        <VIcon
          icon="ri-close-line"
          class="text-medium-emphasis"
          size="24"
        />
      </IconBtn>
    </div>

    <!-- User Avatar + Name + Role -->
    <div class="text-center px-6 mt-n2">
      <VBadge
        location="bottom right"
        offset-x="13"
        offset-y="7"
        bordered
        :color="resolveAvatarBadgeVariant(store.activeChat.contact.status)"
        class="chat-user-profile-badge mb-4"
      >
        <VAvatar
          size="84"
          :variant="!store.activeChat.contact.avatar ? 'tonal' : undefined"
          :color="!store.activeChat.contact.avatar ? resolveAvatarBadgeVariant(store.activeChat.contact.status) : undefined"
        >
          <VImg
            v-if="store.activeChat.contact.avatar"
            :src="store.activeChat.contact.avatar"
          />
          <span
            v-else
            class="text-3xl"
          >{{ avatarText(store.activeChat.contact.fullName) }}</span>
        </VAvatar>
      </VBadge>
      <h5 class="text-h5">
        {{ store.activeChat.contact.fullName }}
      </h5>
      <p class="text-body-1 mb-0">
        {{ store.activeChat.contact.role }}
      </p>
    </div>

    <!-- User Data -->
    <PerfectScrollbar
      class="ps-chat-user-profile-sidebar-content text-medium-emphasis pb-5 px-5"
      :options="{ wheelPropagation: false }"
    >
      <!-- About -->
      <div class="my-6">
        <p
          for="textarea-user-about"
          class="text-base text-disabled mb-1"
        >
          ABOUT
        </p>
        <p class="text-body-1 mb-0">
          {{ store.activeChat.contact.about }}
        </p>
      </div>

      <!-- Personal Information -->
      <div class="mb-6">
        <p class="text-base text-disabled mb-1">
          PERSONAL INFORMATION
        </p>

        <div class="d-flex align-center pa-2">
          <VIcon
            class="me-2"
            size="22"
            color="high-emphasis"
            icon="ri-mail-line"
          />
          <h6 class="text-h6 font-weight-regular">
            lucifer@email.com
          </h6>
        </div>
        <div class="d-flex align-center pa-2">
          <VIcon
            class="me-2"
            size="22"
            color="high-emphasis"
            icon="ri-phone-line"
          />
          <h6 class="text-h6 font-weight-regular">
            +1(123) 456 - 7890
          </h6>
        </div>
        <div class="d-flex align-center pa-2">
          <VIcon
            class="me-2"
            size="22"
            icon="ri-time-line"
            color="high-emphasis"
          />
          <h6 class="text-h6 font-weight-regular">
            Mon - Fri 10AM - 8PM
          </h6>
        </div>
      </div>

      <!-- Options -->
      <div class="pb-5">
        <p class="text-base text-disabled mb-1">
          OPTIONS
        </p>
        <div class="d-flex align-center pa-2">
          <VIcon
            class="me-2"
            size="22"
            color="high-emphasis"
            icon="ri-bookmark-line"
          />
          <h6 class="text-h6 font-weight-regular">
            Add Tag
          </h6>
        </div>
        <div class="d-flex align-center pa-2">
          <VIcon
            class="me-2"
            size="22"
            color="high-emphasis"
            icon="ri-user-star-line"
          />
          <h6 class="text-h6 font-weight-regular">
            Important Contact
          </h6>
        </div>
        <div class="d-flex align-center pa-2">
          <VIcon
            class="me-2"
            size="22"
            color="high-emphasis"
            icon="ri-image-2-line"
          />
          <h6 class="text-h6 font-weight-regular">
            Shared Media
          </h6>
        </div>
        <div class="d-flex align-center pa-2">
          <VIcon
            size="22"
            color="high-emphasis"
            icon="ri-forbid-2-line"
            class="me-2"
          />
          <h6 class="text-h6 font-weight-regular">
            Block Contact
          </h6>
        </div>
      </div>

      <VBtn
        block
        color="error"
        append-icon="ri-delete-bin-7-line"
        class="mt-15"
      >
        Delete Contact
      </VBtn>
    </PerfectScrollbar>
  </template>
</template>
