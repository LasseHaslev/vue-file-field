<template>
    <div class="VueFileUploader__image" v-if="imageData">

        <div class="VueFileUploader__image__content"
             :style="{
                'background-image': 'url(' + imageData + ')',
             }">
            <div @click="remove" class="VueFileUploader__remove">X</div>
        </div>
    </div>
</template>
<script> 
export default {

    props: {
        'image': {
            default:null
        }
    },

    data() {
        return {
            imageData: null,
        }
    },

    mounted() {
        this.readFile( this.image );
    },

    methods: {
        readFile( file ) {
            var fileReader = new FileReader();
            fileReader.readAsDataURL( file );
            fileReader.onload = this.onFileReaderLoad;
        },

        onFileReaderLoad( evt ) {
            this.imageData = evt.target.result;
        },

        remove() {
            console.log( 'remove' );
        },
    }

}
</script>
