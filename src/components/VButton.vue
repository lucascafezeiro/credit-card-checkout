<template>
    <button v-bind:type="type" class="button" v-on:click="$emit('click')">
        <slot>Send</slot>
    </button>
</template>

<script>
export default {
    name: 'VButton',
    props: {
        type: {
            type: String,
            required: false,
            default: 'button'
        }
    }

}
</script>

<style scoped>
.button {
    cursor: pointer;
    border: none;
    background-color: #407CE7;
    color: #FFF;
    font-size: 0.8em;
    width: 80%;
    height: 45px;
    border-radius: 5pt;
    display: flex;
    align-items: center;
    justify-content: center;
    -webkit-box-shadow: 0px 0px 36px -5px rgba(64,125,231,1); /* Chrome all / Safari all */
    -moz-box-shadow: 0px 0px 36px -5px rgba(64,125,231,1); /* Firefox all             */
    box-shadow: 0px 0px 36px -5px rgba(64,125,231,1); /* Likely future           */
    -webkit-user-select: none; /* Chrome all / Safari all */
    -moz-user-select: none;    /* Firefox all             */
    -ms-user-select: none;     /* IE 10+                  */
    user-select: none;        /* Likely future           */
}
</style>