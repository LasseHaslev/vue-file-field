<template>
    <div class="VueFileUploader">
        <div v-if="!supported">Sorry, your browser is not supported.</div>
        <div class="VueFileUploader__dropzone" @click.prevent="findFile"
            @dragover.stop.prevent="addDragOver"
            @dragenter.stop.prevent="addDragOver"

            @dragleave.stop.prevent="removeDragOver"
            @dragend.stop.prevent="removeDragOver"
            @drop.stop.prevent="dropFile"
            :class="{
                'VueFileUploader__dropzone--drag': dragOver,
            }">
            <image-preview @remove-image="removeImage" v-for="image in files" :image="image"></image-preview>
        </div>
        <input class="VueFileUploader__input" v-if="multiple" @change="inputChanged" type="file" :name="name" :accept="accept" multiple>
        <input class="VueFileUploader__input" v-else @change="inputChanged" type="file" :name="name" :accept="accept">
    </div>
</template>
<script> 

import ImagePreview from './ImagePreview.vue';

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
        this.fileInput = this.$el.querySelector( '.VueFileUploader__input' );

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
        removeImage( image ) {
            console.log( this.files );
            var index = this.files.indexOf( image );
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
        ImagePreview,
    }

}
</script>
