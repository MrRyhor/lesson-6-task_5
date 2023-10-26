<template>
    <a :href="itemData.link" target="_blank">
        <div class="imgContainer">
            <img :src="itemData.imgSrc" alt="product" />
        </div>
        <h3>{{ itemData.title }}</h3>
        <h1>{{ itemData.price }}</h1>
    </a>
</template>
<script>
export default {
    props: {
        itemData: {
            type: Object,
            default: () => ({}),
        },
    },
}
</script>
<style lang="scss" scoped>
a {
    text-decoration: none;
}
.imgContainer {
    display: flex;
    align-items: center;
    justify-content: center;

    img {
        width: 200px;
    }
}
h3 {
    margin-top: 10px;
    color: blue;
}
h1 {
    margin-top: 30px;
    color: red;
}
</style>
