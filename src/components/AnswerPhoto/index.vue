<template>
  <div class="checklist-answers-options-photo">
    <div v-if="loading" class="checklist-answers-options-photo-loading">
      <i class="fas fa-sync-alt"></i>
    </div>
    <div
      v-else
      class="checklist-answers-options-photo-content"
      @click="selectPhoto"
      @dragover="dragOverFiles"
      @dragleave="dragLeaveFiles"
      @drop="dropFiles"
      :class="{ active: dropActive }"
    >
      <img :src="image" v-if="image && !dropActive" />
      <span
        v-if="!image || (image && dropActive)"
        class="checklist-answers-options-photo-content-title"
        >FOTO</span
      >
      <span
        v-if="!image || (image && dropActive)"
        class="checklist-answers-options-photo-content-text"
        >{{ dropActive ? `Solte Aqui` : `Clique Aqui` }}</span
      >
    </div>
  </div>
</template>
<script>
import Swal from 'sweetalert2';

export default {
  name: 'AnswerPhoto',
  data() {
    return {
      image: null,
      filename: null,
      filetype: null,
      loading: false,
      dropActive: false,
    };
  },
  methods: {
    dragOverFiles(e) {
      e.stopPropagation();
      e.preventDefault();
      e.dataTransfer.dropEffect = 'copy';
      this.dropActive = true;
    },
    dragLeaveFiles() {
      this.dropActive = false;
    },
    dropFiles(e) {
      this.dropActive = false;
      e.stopPropagation();
      e.preventDefault();
      if (!e.dataTransfer.files.length) {
        return;
      }

      const file = e.dataTransfer.files[0];
      if (file.type === 'image/jpeg' || file.type === 'image/png') {
        this.loading = true;
        this.filename = file.name;
        this.filetype = file.type;
        this.readFile(file);
      } else {
        Swal.fire('Atenção', 'Arquivo não suportado!', 'warning');
      }
    },
    selectPhoto() {
      const input = document.createElement('input');
      input.type = 'file';
      input.accept = '.jpg, .jpeg, .png|image/*';
      input.addEventListener('change', this.selectedFiles);
      input.click();
    },
    selectedFiles(e) {
      if (!e.target.files.length) {
        return;
      }

      const file = e.target.files[0];
      if (file.type === 'image/jpeg' || file.type === 'image/png') {
        this.loading = true;
        this.filename = file.name;
        this.filetype = file.type;
        this.readFile(file);
      } else {
        Swal.fire('Atenção', 'Arquivo não suportado!', 'warning');
      }
    },
    readFile(file) {
      const fileReader = new FileReader();
      fileReader.onload = (e) => this.loadImage(e.target.result);
      fileReader.readAsDataURL(file);
    },
    loadImage(data) {
      const image = new Image();
      image.onload = () => this.render(image);
      image.src = data;
    },
    render(image) {
      const wRatio = 600 / image.width;
      const hRatio = 600 / image.height;
      const ratio = wRatio > hRatio ? wRatio : hRatio;
      const imgWidth = image.width * ratio;
      const imgHeight = image.height * ratio;

      const canvas = document.createElement('canvas');
      canvas.width = imgWidth;
      canvas.height = imgHeight;

      const ctx = canvas.getContext('2d');
      ctx.drawImage(image, 0, 0, imgWidth, imgHeight);
      this.image = canvas.toDataURL('jpeg', 90);
      this.loading = false;
      // this.update(canvas);
    },
  },
};
</script>
