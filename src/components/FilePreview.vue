<template>
    <div class="VueFileField__file" v-if="fileData">

        <div class="VueFileField__file__content"
             :style="{
                'background-image': isImage ? 'url(' + fileData + ')' : false,
             }">
            <!-- <div @click="remove" class="VueFileField__remove">X</div> -->
        </div>
            <div class="VueFileField__file__info">
                <div class="VueFileField__file__size">{{ formatBytes( file.size, 0 ) }}</div>
            </div>
    </div>
</template>
<script> 
export default {

    props: {
        'file': {
            default:null
        }
    },

    data() {
        return {
            fileData: null,
            isImage: false,
        }
    },

    mounted() {
        this.readFile( this.file );
    },

    methods: {
        readFile( file ) {

            var imageType = /^image\//;
            if (imageType.test(file.type)) {
                this.isImage = true;
            }

            var fileReader = new FileReader();
            fileReader.readAsDataURL( file );
            fileReader.onload = this.onFileReaderLoad;
        },

        onFileReaderLoad( evt ) {
            this.fileData = evt.target.result;
        },

        remove() {
            this.$emit( 'remove-file', this.file );
        },

        formatBytes( bytes, decimals ) {
            if(bytes == 0) return '0 Byte';
            var k = 1000; // or 1024 for binary
            var dm = decimals + 1 || 3;
            var sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'];
            var i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + sizes[i];
        }
    }

}
</script>
