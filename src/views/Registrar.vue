<template>
  <ion-page>
    <!-- <ion-content>
      <div style="margin: 50px">
        <h3>Formulario para registrar vivencias</h3>
        <p>Ingrese el moments.titulo:</p>
        <input type="text" v-model="name" placeholder="Ingrese el nombre" />
      </div>
    </ion-content> -->
    <ion-content>
      <form @submit.prevent="submitForm" style="width: 1000px; margin: 50px">
        <div>
          <p>titulo</p>
          <input v-model="titulo" required />
        </div>

        <div>
          <p>Fecha</p>
          <input type="date" v-model="fecha" required />
        </div>

        <div>
          <p>Descripción</p>
          <input v-model="descripcion" required />
        </div>
        <!-- <ion-item>
          <ion-label>Foto</ion-label>
          <ion-button fill="outline" @click="capturePhoto"
            >Tomar foto</ion-button
          >
          <img v-if="photoData" :src="photoData" alt="Captured Photo" />
        </ion-item> -->

        <!-- <ion-item>
          <ion-label>Audio</ion-label>
          <ion-button
            fill="outline"
            @click="recordAudio"
            :disabled="isRecording"
          >
            {{ isRecording ? "Grabando..." : "Grabar audio" }}
          </ion-button>
          <audio v-if="audioData" :src="audioData" controls></audio>
        </ion-item> -->

        <ion-button type="submit" expand="block">Enviar</ion-button>
      </form>
      <div style="margin: 50px">
        <h3>Listado de vivencias</h3>
        <ion-button type="submit" v-if="items.length > 0" @click="deteleAll()"
          >Eliminar vivencias</ion-button
        >
        <div v-for="(item, index) in items" :key="index">
          <div>
            <div class="white-border">
              <p>
                {{ index + 1 }} - {{ item.titulo }} - {{ item.fecha }} -
                {{ item.descripcion }}
              </p>
              <ion-button style="margin-bottom: 10px" @click="editItem(index)"
                >Detalles</ion-button
              >
            </div>
          </div>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import {
  IonInput,
  IonButtons,
  IonContent,
  IonHeader,
  IonMenuButton,
  IonPage,
  IonTitle,
  IonToolbar,
  IonDatetime,
} from "@ionic/vue";
export default defineComponent({
  data() {
    return {
      items: [] as Array<Item>,

      titulo: "",
      fecha: "",
      descripcion: "",
      photoData: null,
      audioData: null,
      isRecording: false,
    };
  },
  methods: {
    saveItems() {
      localStorage.setItem("items", JSON.stringify(this.items));
    },
    submitForm() {
      console.log(this.titulo, this.fecha, this.descripcion);

      const newMoments = {
        titulo: this.titulo,
        fecha: this.fecha,
        descripcion: this.descripcion,
      };
      this.items.push(newMoments);
      this.saveItems();

      this.titulo = "";
      this.fecha = "";
      this.descripcion = "";
    },
    editItem(index: number) {
      const item = this.items[index];
      const itemData = JSON.parse(JSON.stringify(item));
      this.titulo = itemData.titulo;
      this.fecha = itemData.fecha;
      this.descripcion = itemData.descripcion;
    },
    deteleAll() {
      localStorage.removeItem("items");
      window.location.reload();
    },
  },
});
interface Item {
  titulo: string;
  fecha: string;
  descripcion: string;
}
</script>

<style scoped>
/* Styles for all input elements */
input {
  color: #333;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 8px;
  font-size: 14px;
  width: 200px;
}

/* Styles for focused input elements */
input:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.white-border {
  border: 2px solid white;
  padding: 10px;
}
</style>
