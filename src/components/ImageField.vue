<template>
    <div class="VueFileUploader">
        <div class="VueFileUploader__dropzone">
            <image-preview @remove-image="removeImage" v-for="image in files" :image="image"></image-preview>
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
        removeImage( image ) {
            console.log( this.files );
            var index = this.files.indexOf( image );
            if ( index > -1 ) {
                this.files.splice( index, 1 );
            }
        },
    },

    components: {
        ImagePreview,
    }

}
</script>
