<template>
  <div>
    <div class="container">
      <div class="d-flex justify-content-center">
        <div class="card text-center border-0">
          <div class="card-body">
            <div class="form-floating mb-3">
              <input
                type="text"
                class="form-control"
                id="messageInput"
                placeholder="example@mail.com"
                v-model="message"
              />
              <label for="messageInput">Encrypted Message</label>
            </div>
            <div class="col-12">
              <button
                class="btn btn-primary"
                type="submit"
                @click="encryptMessage()"
                :disabled="loading"
              >
                Encrypt Message
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>

<script setup lang="ts">
import WebCryptoService from "../services/crypto";
import MessageService from "../services/message";

import { ref, onMounted } from "vue";
const message = ref("" as string);
const loading = ref(false);

onMounted(async () => {
  await decryptMessage();
})

async function encryptMessage() {
  const encryptedString = await WebCryptoService.encrypt(message.value);
  MessageService.setEncryptedMessage(encryptedString);
}

async function decryptMessage() {
  await WebCryptoService.loadCryptoPublicKey();
  await WebCryptoService.deriveEncryptionKey();
  console.log(WebCryptoService.getCryptoPrivateKey());
  console.log(WebCryptoService.getCryptoPublicKey());
  const encryptedMessage = MessageService.getEncryptedMessage() as string;
  if (encryptedMessage != "")
    message.value = await WebCryptoService.decrypt(encryptedMessage);
}
</script>
