<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list>
        <ion-item>
          <ion-label>
            <ion-button expand="block" color="danger" @click="logoutClicked"
              >Logout</ion-button>
          </ion-label>
        </ion-item>
        <ion-item>
          <ion-label>
            <ion-button
              expand="block"
              color="secondary"
              @click="updateUnlockMode('BiometricsWithPasscode')"
              >Use Biometrics</ion-button>
          </ion-label>
        </ion-item>
        <ion-item>
          <ion-label>
            <ion-button
              expand="block"
              color="secondary"
              @click="updateUnlockMode('InMemory')"
              >Use In Memory</ion-button>
          </ion-label>
        </ion-item>
        <ion-item>
          <ion-label>
            <ion-button
              expand="block"
              color="secondary"
              @click="updateUnlockMode('SecureStorage')"
              >Use Secure Storage</ion-button>
          </ion-label>
        </ion-item>
        <ion-item>
          <div>
            <div>{{ session?.email }}</div>
            <div>{{ session?.firstName }} {{ session?.lastName }}</div>
            <div>{{ session?.accessToken }}</div>
            <div>{{ session?.refreshToken }}</div>
          </div>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { useAuthentication } from '@/composables/authentication';
import { useSessionVault } from '@/composables/session-vault';
import {
  IonButton,
  IonContent,
  IonHeader,
  IonItem,
  IonLabel,
  IonList,
  IonPage,
  IonTitle,
  IonToolbar,
} from '@ionic/vue';
import { useRouter } from 'vue-router';

const { logout } = useAuthentication();
const { session, updateUnlockMode } = useSessionVault();
const router = useRouter();

const logoutClicked = async (): Promise<void> => {
  await logout();
  router.replace('/');
};
</script>