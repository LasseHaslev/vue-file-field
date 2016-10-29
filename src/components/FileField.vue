<template>
    <div class="VueFileField">
        <div v-if="!supported">Sorry, your browser is not supported.</div>
        <div class="VueFileField__dropzone" @click.prevent="findFile"
            @dragover.stop.prevent="addDragOver"
            @dragenter.stop.prevent="addDragOver"

            @dragleave.stop.prevent="removeDragOver"
            @dragend.stop.prevent="removeDragOver"
            @drop.stop.prevent="dropFile"
            :class="{
                'VueFileField__dropzone--drag': dragOver,
            }">
            <file-preview @remove-file="removeFile" v-for="file in files" :file="file"></file-preview>
        </div>
        <input class="VueFileField__input" v-if="multiple" @change="inputChanged" type="file" :name="name" :accept="accept" multiple>
        <input class="VueFileField__input" v-else @change="inputChanged" type="file" :name="name" :accept="accept">
    </div>
</template>
<script> 

import FilePreview from './FilePreview.vue';

export default {
    props: {
        name: {
            type: String,
            default: 'file',
        },

        accept: {
            type: String,
            default: '*',
        },

        multiple: {
            type: Boolean,
            default: false,
        }
    },

    data() {
        return {
            supported: true,
            fileInput: null,
            files: [],
            dragOver: false,
        }
    },

    mounted() {
        this.supported = !(!window.File || !window.FileReader || !window.FileList || !window.Blob)
        this.fileInput = this.$el.querySelector( '.VueFileField__input' );

        if ( ! this.fileInput.files ) {
            this.supported = false;
        }
    },

    methods: {
        inputChanged() {
            this.addFiles( this.fileInput.files );
        },
        addFiles( files ) {
            this.$set( this, 'files', [] );
            this.$nextTick( function() {
                this.$set( this, 'files', files );
            } );
        },
        removeFile( file ) {
            console.log( this.files );
            var index = this.files.indexOf( file );
            if ( index > -1 ) {
                this.files.splice( index, 1 );
            }
        },

        findFile() {
            this.fileInput.click();
        },

        addDragOver() {
            this.dragOver = true;
        },
        removeDragOver() {
            this.dragOver = false;
        },
        dropFile( evt ) {
            var files = evt.dataTransfer.files;
            if ( !this.multiple ) {
                files = [ evt.dataTransfer.files[0] ];
            }
            this.addFiles( files );
            this.removeDragOver();
        },
    },

    components: {
        FilePreview,
    }

}
</script>
