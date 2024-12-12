<template>
    <div class="note-body">
        <div class="header">
            <div class="title">
                <p v-if="loadingSkeleton == false">{{ localTitle }}</p>
                <p aria-hidden="true" v-if="loadingSkeleton == true">
                    <span class="placeholder col-12 placeholder-lg"></span>
                </p>
            </div>
            <div class="pre-title">
                <p v-if="loadingSkeleton == false">{{ localPreTitle }}</p>
                <p aria-hidden="true" v-if="loadingSkeleton == true">
                    <span class="placeholder col-12"></span>
                </p>
            </div>
        </div>
        <div class="memo-wrapper">
            <div class="memo">
                <p v-if="loadingSkeleton == false">{{ localMemo }}</p>
                <p aria-hidden="true" v-if="loadingSkeleton == true">
                    <span class="placeholder col-12 placeholder-xs"></span>
                    <span class="placeholder col-12 placeholder-xs"></span>
                    <span class="placeholder col-12 placeholder-xs"></span>
                    <span class="placeholder col-12 placeholder-xs"></span>
                    <span class="placeholder col-12 placeholder-xs"></span>
                </p>
            </div>
        </div>
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" :data-bs-target="'#redact'+localId">
            <p v-if="loadingSkeleton == false">Редактировать</p>
            <p aria-hidden="true" v-if="loadingSkeleton == true" style="width: 100%;">
                <span class="placeholder col-12"></span>
            </p>
        </button>
    </div>
    <div class="modal fade" :id="'redact'+localId" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <div class="title">
                        <input type="text" v-model="TitleRedact">
                    </div>
                    <div class="pre-title">
                        <input type="text" v-model="PreTitleRedact">
                    </div>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Закрыть"></button>
                </div>
                <div class="modal-body">
                    <div class="memo-wrapper">
                        <div class="memo">
                            <textarea v-model="MemoRedact"></textarea>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary"
                        @click="saveChanges(); redactCorrect('Заметка успешно изменена!', 'success');"
                        data-bs-dismiss="modal">Сохранить изменения</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        title: String,
        preTitle: String,
        memo: String,
        localId: Number,
        redact: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            loadingSkeleton: true,
            localTitle: this.title,
            localPreTitle: this.preTitle,
            localMemo: this.memo,
            TitleRedact: this.title,
            PreTitleRedact: this.preTitle,
            MemoRedact: this.memo
        }
    },
    methods: {
        saveChanges() {
            this.localTitle = this.TitleRedact,
                this.localPreTitle = this.PreTitleRedact,
                this.localMemo = this.MemoRedact
        },
        redactCorrect(message, type) {
            const redact = document.getElementById('redactAlert');
            const wrapper = document.createElement('div');
            wrapper.innerHTML = [
                `<div class="alert alert-${type} alert-dismissible" role="alert">`,
                `   <div>${message}</div>`,
                '   <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>',
                '</div>'
            ].join('');

            redact.append(wrapper);
        },
    },
    mounted() {
        setTimeout(() => {
            this.loadingSkeleton = false;
        }, 800);
    }
}
</script>
