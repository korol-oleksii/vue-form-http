<template>
  <div class="container">
    <h1>Курсова робота з HTTP та формою</h1>

    <div class="cards">
      <form class="card" @submit.prevent="addTypeElement">
        <div class="form-control">
          <label for="type" class="label">Тип блоку</label>
          <select id="type" v-model="selectValue" ref="selectText" @change="updateSelectedText">
            <option value="title">Додати заголовок</option>
            <option value="avatar">Додати фото (посилання)</option>
            <option value="subtitle">Додати підзаголовок</option>
            <option value="description">Додати опис</option>
          </select>
        </div>

        <div class="form-control">
          <label for="val" class="label">Значення</label>
          <textarea v-model.trim="nameValue" id="val" rows="5" class="input"></textarea>
        </div>

        <button class="button primary" :disabled="minLength">{{ selectedText }}</button>
      </form>

      <app-resume></app-resume>
    </div>

    <app-loader v-if="isLoading"></app-loader>

    <app-comment v-else
      :comments="comments"
      @load="loadComments"
    ></app-comment>

  <app-auto-hint-confirm :autoHintForce="autoHintForce"></app-auto-hint-confirm>

  </div>
</template>

<script>
//const token = 'RDN5l8fKoicTLonYPVPwMpVvl7As5PMdAYBlCjes' //for fireBase
//https://jsonplaceholder.typicode.com/comments?_limit=42 //test api with comments

import AppResume from '@/components/AppResume.vue'
import AppComment from '@/components/AppComment.vue'
import AppLoader from '@/components/AppLoader.vue'
import AppAutoHintConfirm from '@/components/AppAutoHintConfirm.vue'
import axios from 'axios'

export default {
  data() {
    return {
      nameValue: '',
      selectValue: 'title',
      selectedText: '',
      resumeData: {
        title: '',
        avatar: '',
        contentBlocks: [], // Масив для підзаголовків і описів
      },
      comments: [],
      isLoading: false,
      autoHintForce: null,
    };
  },
  provide() {
    return {
      resumeData: this.resumeData,
    };
  },
  mounted() {
    this.updateSelectedText(); // Ініціалізація після монтування
  },
  methods: {
    addTypeElement() {
      if (this.nameValue.trim()) {
        const trimmedValue = this.nameValue.trim();

        // Збереження в залежності від обраного типу
        if (this.selectValue === 'title') {
          this.resumeData.title = trimmedValue;
        } else if (this.selectValue === 'avatar') {
          this.resumeData.avatar = trimmedValue;
        } else {
          // Додаємо до contentBlocks для subtitle або description
          this.resumeData.contentBlocks.push({
            type: this.selectValue, // Зберігаємо тип (subtitle або description)
            value: trimmedValue,   // Зберігаємо значення
          });
        }

        this.resumeData.id = this.selectValue // Створюємо id для керування наявності елементів

        // Очистка полів після додавання
        this.nameValue = '';
        this.selectValue = 'title';
        this.selectedText = 'Додати заголовок';
      }

      // Лог для перевірки
      // console.log(this.resumeData);
    },
    updateSelectedText() {
      this.selectedText = this.$refs.selectText.selectedOptions[0].innerText; // Отримуємо текст з select > options
    },
    async loadComments() {
      try {
        this.isLoading = true;
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
        this.comments = Object.keys(data).map(key => {
          return {
            id: key,
            ...data[key],
          }
        })

        this.autoHintForce = {
          type: 'primary',
          text: 'Коментарі успішно завантажені'
        }
        setTimeout(() => this.autoHintForce = null, 1000);

        this.isLoading = false;
      } catch (e) {

        this.autoHintForce = {
          type: 'danger',
          text: 'Виникла помилка! Спробуйте пізніше...'
        }
        setTimeout(() => this.autoHintForce = null, 2000);

        this.isLoading = false
        console.log(e.message)
      }
    },
  },
  computed: {
    minLength() {
      return this.nameValue.length < 4
    },
  },
  components: { AppResume, AppComment, AppLoader, AppAutoHintConfirm },
}
</script>

<style lang="scss" scoped></style>
