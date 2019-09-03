<template>
    <div>
        <div v-on:click="$emit('decrement')" class="number-input-item number-input-button">-</div>
        <div class="number-input-item number-input-value">{{value}}</div>
        <div v-on:click="$emit('increment')" class="number-input-item number-input-button">+</div>
    </div>
</template>

<script>
export default {
    name: 'NumberInput',
    props: {
        value: {
            type: Number,
            required: true,
            validator: function (value) {
                return (value >=1);
            }
        }
    }
}
</script>

<style scoped>

.number-input-item {
    text-align: center;
    float: left;
    color: #555;

}

.number-input-button{
    cursor: pointer;
    height: 100%;
    width: 30%;
    user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
    -webkit-user-select: none;
    -o-user-select: none;
}

.number-input-value{
    text-align: center;
    width: 40%;   
}

</style>