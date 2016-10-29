<template>
    <div class="VueFileUploader">
        <div class="VueFileUploader__dropzone">
            <image-preview v-for="image in files" :image="image"></image-preview>
        </div>
        <div v-if="!supported"></div>
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
            default: 'image',
        },

        accept: {
            type: String,
            default: 'image/*',
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
    },

    components: {
        ImagePreview,
    }

}
</script>
