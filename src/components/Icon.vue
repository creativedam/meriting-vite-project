<script setup>
import cellphoneIcon from '../assets/cellphone-icon.svg'
import clipboardIcon from '../assets/clipboard-icon.svg'
import facebookIcon from '../assets/facebook-icon.svg'
import instagramIcon from '../assets/instagram-icon.svg'
import medicalEyeLogo from '../assets/medical-eye-logo.svg'
import meritingLogo from '../assets/meriting-logo.svg'
import meritingLogoGrayscale from '../assets/meriting-logo-grayscale.svg'
import phoneApprovalChat from '../assets/phone-approval-chat.svg'
import telephoneIcon from '../assets/telephone-icon.svg'
import vueLogo from '../assets/vue.svg'
import whatsappIcon from '../assets/whatsapp-icon.svg'

defineProps({
  name: {
    type: String,
    required: true,
  },
  alt: {
    type: String,
    default: '',
  },
})
</script>

<template>
  <img
    v-if="name === 'cellphone'"
    :src="cellphoneIcon"
    :alt="alt || 'Cellphone icon'"
    class="icon"
  />
  <img
    v-else-if="name === 'clipboard'"
    :src="clipboardIcon"
    :alt="alt || 'Clipboard icon'"
    class="icon"
  />
  <img
    v-else-if="name === 'medical-eye'"
    :src="medicalEyeLogo"
    :alt="alt || 'Medical eye logo'"
    class="icon"
  />
  <img
    v-else-if="name === 'facebook'"
    :src="facebookIcon"
    :alt="alt || 'Facebook icon'"
    class="icon"
  />
  <img
    v-else-if="name === 'instagram'"
    :src="instagramIcon"
    :alt="alt || 'Instagram icon'"
    class="icon"
  />
  <img
    v-else-if="name === 'meriting-logo'"
    :src="meritingLogo"
    :alt="alt || 'Meriting Medical Centre logo'"
    class="icon"
  />
  <img
    v-else-if="name === 'meriting-logo-grayscale'"
    :src="meritingLogoGrayscale"
    :alt="alt || 'Meriting Medical Centre grayscale logo'"
    class="icon"
  />
  <img
    v-else-if="name === 'phone-approval-chat'"
    :src="phoneApprovalChat"
    :alt="alt || 'Phone approval chat illustration'"
    class="icon"
  />
  <img
    v-else-if="name === 'telephone'"
    :src="telephoneIcon"
    :alt="alt || 'Telephone icon'"
    class="icon"
  />
  <img
    v-else-if="name === 'whatsapp'"
    :src="whatsappIcon"
    :alt="alt || 'WhatsApp icon'"
    class="icon"
  />
  <img
    v-else-if="name === 'vue'"
    :src="vueLogo"
    :alt="alt || 'Vue logo'"
    class="icon"
  />
  <span v-else class="icon icon--missing" aria-hidden="true"></span>
</template>

<style scoped>
.icon {
  display: inline-block;
  max-width: 100%;
  height: auto;
  vertical-align: middle;
}

.icon--missing {
  width: 1em;
  height: 1em;
}
</style>
