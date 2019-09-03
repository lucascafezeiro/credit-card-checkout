<template>
    <div>
        <div class="input">
            <div class="label">{{ label }}</div>
            <input 
                class="error"
                v-bind:value="value"
                v-bind:name="name"
                v-bind:type="type"
                v-on:input="$emit('input', {key: name,value: $event.target.value})"
                v-on:focus="$emit('focus')"
                v-on:blur="$emit('blur')"
                v-on:keyup.arrow-down="$emit('arrow-down')"
                v-on:keyup.arrow-up="$emit('arrow-up')"
                v-on:keyup.enter="$emit('enter')"
                v-bind:class="{'hasError': error.hasError}"
            />
        </div>
        <div class="errorMessage"> 
            <span v-if="error.hasError" >{{error.message}}</span>
        </div>
        </div>
</template>

<script>

export default {
    name: 'VInputText',
    props: {
        value : {
            type: String,
            required: false
        },
        name : {
            type: String,
            required: true
        },
        type: {
            type: String,
            required: false,
            default: 'text'
        },
        label : {
            type: String,
            required: true
        },
        error: {
            type: Object,
            required: false,
            default () { 
                return {
                    hasError: false,
                    message: ''
                }
            }
        }
    }
}
</script>

<style scoped>
input{   
    background: transparent; 
    border-top: none;
    border-left: none;
    border-right: none;
    border-bottom: 1px solid #DDD;
    color: #DDD;
    width: 100%;
}

input:focus { 
    outline: none !important;
}

.hasError {
    border-bottom: 1px solid rgb(141, 10, 10);
    color:  rgb(141, 10, 10);
}

.errorMessage{
    height: 12px;
    color:  rgb(141, 10, 10);
}


</style>