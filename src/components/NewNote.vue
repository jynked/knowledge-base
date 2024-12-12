<template>
  <div class="modal fade" id="createNote" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="createNote">Создание новой заметки</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="title">
            <p>Как бы вы хотели озаглавить вашу новую заметку?</p>
            <input type="text" v-model="newNote.title">
          </div>
          <div class="pre-title">
            <p>Подзаголовок (если нужно)</p>
            <input type="text" v-model="newNote.preTitle">
          </div>
          <div class="memo">
            <p>Ваши мысли:</p>
            <input type="text" v-model="newNote.memo">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" data-bs-dismiss="modal"
            @click="appendAlert('Новая заметка успешно создана!', 'success', 'note');">
            Создать заметку </button>
        </div>
      </div>
    </div>
  </div>
  <div class="modal fade" id="createDoc" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="createNote">Создание нового документа</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="title">
            <p>Как бы вы хотели озаглавить вашу новую заметку?</p>
            <input type="text" v-model="newNote.title">
          </div>
          <div class="pre-title">
            <p>Подзаголовок (если нужно)</p>
            <input type="text" v-model="newNote.preTitle">
          </div>
          <div class="memo">
            <p>Ваши мысли:</p>
            <input type="text" v-model="newNote.memo">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" data-bs-dismiss="modal"
            @click="appendAlert('Новый документ успешно создан!', 'success', 'document');">
            Создать документ </button>
        </div>
      </div>
    </div>
  </div>
  <div class="modal fade" id="createUrl" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="createNote">Создание новой ссылки</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="title">
            <p>Как бы вы хотели озаглавить вашу новую заметку?</p>
            <input type="text" v-model="newNote.title">
          </div>
          <div class="pre-title">
            <p>Подзаголовок (если нужно)</p>
            <input type="text" v-model="newNote.preTitle">
          </div>
          <div class="memo">
            <p>URL страницы</p>
            <input type="url" v-model="newNote.memo">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" data-bs-dismiss="modal"
            @click="appendAlert('Новая ссылка успешно создана!', 'success', 'url');">
            Создать ссылку </button>
        </div>
      </div>
    </div>
  </div>
  <div class="modal fade" id="createFolder" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="createNote">Создание новой папки</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="title">
            <p>Как бы вы хотели озаглавить вашу новую папку?</p>
            <input type="text" v-model="newNote.title">
          </div>
          <div class="pre-title">
            <p>Подзаголовок (если нужно)</p>
            <input type="text" v-model="newNote.preTitle">
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" data-bs-dismiss="modal"
            @click="appendAlert('Новая папка успешно создана!', 'success', 'folder');">
            Создать папку </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newNote: {
        title: '',
        preTitle: '',
        memo: ''
      }
    }
  },
  methods: {
    appendAlert(message, type, elementType) {
      const alertPlaceholder = document.getElementById('addAlert');
      const wrapper = document.createElement('div');
      if (!this.newNote.title.trim()) {
        alert("Ошибка: Заголовок не может быть пустым.");
        return;
      } else if (elementType !== 'folder' && !this.newNote.memo.trim()) {
        alert("Ошибка: Основной текст не может быть пустым.");
        return;
      } else {
        setTimeout(() => {
          wrapper.innerHTML = [
            `<div class="alert alert-${type} alert-dismissible" role="alert">`,
            `   <div>${message}</div>`,
            '   <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>',
            '</div>'
          ].join('');

          alertPlaceholder.append(wrapper);
        }, 800)

        this.$emit('note-created', { ...this.newNote });
        this.$emit('element-type', { elementType });
        this.newNote.title = '';
        this.newNote.preTitle = '';
        this.newNote.memo = '';
      }
    },
  }
}
</script>
