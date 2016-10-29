<template>
    <div>
        <div v-if="!supported"></div>
        <input v-if="multiple" @change="inputChanged" type="file" :name="name" multiple>
        <input v-else @change="inputChanged" type="file" :name="name">
        <image-preview v-for="image in files" :image="image"></image-preview>
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

        extensions: {
            type: String,
            default: 'jpg,jpeg,png,gif',
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
        this.fileInput = this.$el.querySelector( 'input[type=file]' );

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
