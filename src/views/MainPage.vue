<template>
    <NewNote @note-created="addNote" />
    <div class="wrapper">
        <div class="filters">
            <div class="new-note">
                <div class="dropdown">
                    <button class="btn btn-secondary dropdown-toggle" id="dropdownMenuButton2" type="button"
                        data-bs-toggle="dropdown" aria-expanded="false" v-if="loadingSkeleton == false">
                        Создать
                    </button>
                    <ul class="dropdown-menu dropdown-menu-dark" aria-labelledby="dropdownMenuButton2">
                        <li><a class="dropdown-item btn btn-primary" data-bs-toggle="modal"
                            data-bs-target="#createNote">Заметку</a></li>
                        <li><a class="dropdown-item btn btn-primary" data-bs-toggle="modal"
                            data-bs-target="#createDoc">Документ</a></li>
                        <li><a class="dropdown-item btn btn-primary" data-bs-toggle="modal"
                            data-bs-target="#createUrl">Ссылку</a></li>
                        <li>
                            <hr class="dropdown-divider">
                        </li>
                        <li><a class="dropdown-item btn btn-primary" data-bs-toggle="modal"
                            data-bs-target="#createFolder">Папку</a></li>
                    </ul>
                </div>
                <p aria-hidden="true" v-if="loadingSkeleton == true" style="margin: 0;">
                    <span class="placeholder col-12 placeholder-xs new-note-skeleton"></span>
                </p>
            </div>
        </div>
        <div class="notes-block" v-if="redact === false">
            <NoteMain v-for="(note, index) in NoteMain" :key="index" :title="note.title" :preTitle="note.preTitle"
                :memo="note.memo" :localId="note.localId" />
        </div>
    </div>
</template>

<script>
import NewNote from '@/components/NewNote.vue';
import NoteMain from '@/components/NoteMain.vue';

export default {
    components: {
        NoteMain,
        NewNote,
    },
    data() {
        return {
            loadingSkeleton: true,
            NoteMain: [
                {
                    title: "Привет",
                    preTitle: "привет",
                    memo: "Lorem ipsum delectus aliquam quia a molestiae eaque voluptatum doloribus omnis nulla. Nam molestiae, dolorem nisi voluptatibus iusto dolor, est dignissimos laudantium maiores, quos error esse veniam. Quaerat, id dolorem enim, aut laboriosam libero consequuntur minus unde totam incidunt repudiandae nesciunt vitae! Laborum aliquid dolorum, voluptatibus dolores cumque quos maiores commodi in perspiciatis nihil. Quis quia molestias facere tempora provident qui praesentium dolor inventore nisi illum fuga id, nostrum repudiandae distinctio quisquam itaque! Nesciunt expedita vero totam tenetur!"
                },
                {
                    title: "Привет",
                    preTitle: "привет",
                    memo: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime, numquam itaque rerum delectus aliquam quia aut ullam, odit, obcaecati consequuntur non autem explicabo sequi culpa ipsa porro cum molestiae eaque voluptatum doloribus omnis nulla. Nam molestiae, dolorem nisi voluptatibus iusto dolor, est dignissimos laudantium maiores, quos error esse veniam. Quaerat, id dolorem enim, aut laboriosam libero consequuntur minus unde totam incidunt repudiandae nesciunt vitae! Laborum aliquid dolorum, voluptatibus dolores cumque quos maiores commodi in perspiciatis nihil. Quis quia molestias facere tempora provident qui praesentium dolor inventore nisi illum fuga id, nostrum repudiandae distinctio quisquam itaque! Nesciunt expedita vero totam tenetur!"
                },
                {
                    title: "Привет",
                    preTitle: "привет",
                    memo: "Lorem aliquam"
                },
            ].map((product, index) => ({
                ...product,
                localId: index + 1
            })),
            redact: false,
            buttonIsDark: false,
        }
    },
    methods: {
        addNote(newNote) {
            this.NoteMain.push(newNote);
        },
        toggleRedact() {
            this.redact = !this.redact
        },
        toggleButton() {
            this.buttonIsDark = !this.buttonIsDark;
        },
    },
    mounted() {
        document.body.style.overflow = 'hidden';
        setTimeout(() => {
            this.loadingSkeleton = false;
            document.body.style.overflow = 'auto';
        }, 800)
    }
}
</script>