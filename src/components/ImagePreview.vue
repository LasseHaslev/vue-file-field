<template>
    <div>
        {{ image.name }}
        <img v-if="imageData" :src="imageData" alt="">
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
    }

}
</script>
