<template>
  <ion-page>
    <ion-content>
      <div style="display: flex; justify-content: center; align-items: center">
        <img
          src="https://cdn-icons-png.flaticon.com/512/6213/6213814.png"
          alt="Registra tu vivienda"
          style="width: 600px; height: 600px; margin-top: 60px"
        />
      </div>
      <div style="text-align: center">
        <h3 style="margin: 100px">Registra tu vivienda App</h3>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonButtons,
  IonContent,
  IonHeader,
  IonMenuButton,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
