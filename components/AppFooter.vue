<template>
    <a-layout-footer class="footer">
        {{title}}
    </a-layout-footer>
</template>

<script>
export default {
    data(){
        return {
            title: ""
        }
    },
    props: {
        id: null
    },
    async fetch(){
        if(!this.id)
            return;

        const response = await this.$prismic.api.getSingle("footer");

        this.title = this.$prismic.asText(response.data.footer_title)
    }
}
</script>

<style>
.footer {
   position:absolute;
   bottom:0;
   width:100%;
   height:70px;   /* Height of the footer */
   /* background:#6cf; */
   text-align: center;
}
</style>