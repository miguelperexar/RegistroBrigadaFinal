<template>
    <div class="row">
        <Home class="col-8" />
        <Lateral class="col-4"/>
    </div>
</template>
<script>
import Home from '../components/Home.vue';

export default {
    data() {
        return {
            titulo: "Proyecto´vue, bien mamalon",
            logo: "https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Google_2015_logo.svg/1280px-Google_2015_logo.svg.png"
        };
    },
    components: { Home }
}
</script>
<style scoped></style>