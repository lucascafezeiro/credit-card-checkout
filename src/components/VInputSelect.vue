<template>
    <div>
        <div class="select-input-container">
            <VInputText
                class="input"
                v-bind:label="label"
                v-bind:value="currentValue"
                v-bind:name="name"
                v-bind:type="type"
                v-on:focus="openList"
                v-on:blur="closeList"
                v-on:input="onInput"
                v-on:arrow-down="changeItem('down')"
                v-on:arrow-up="changeItem('up')"
                v-on:enter="onEnter"
                v-bind:error="error"
            />
            <div class="icon">▼</div>
        </div>        
        <div class="dropdownlist-container">
            <div 
                class="dropdownlist" 
                v-bind:style="[overrideStyles]"
            >
                <div 
                    class="dropdownlist-item"
                    v-for="item in this.currentList"
                    v-bind:key="item.value"
                    v-on:mousedown="selectItem(item.value)"
                    v-bind:class="{ active: item.isActive }"
                >
                    {{item.value}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import VInputText from './VInputText'

export default {
    name: 'VInputSelect',
    components: {
        VInputText
    },
    data () {
        return {
            overrideStyles : {
                display: 'none'
            },
            currentStart: 0,
            currentValue: '',
            currentKey: -1,
            currentList: [{
                value: '',
                isActive: false
            }]
        }
    },
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
        items : {
            type: Array,
            required: true
        },
        size : {
            type: Number,
            required: false,
            default: 4
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
    },
    methods : {
        openList () {
            this.overrideStyles.display = 'block';
        },
        closeList () {
            this.overrideStyles.display = 'none';
        },
        onInput (input) {
            this.currentStart = this.items.findIndex((item) => (item.substring(0,input.value.length) === input.value));
            if (this.currentStart === -1) {
                this.closeList();
            } else {
                this.openList();
                this.currentValue = input.value;
                this.currentKey = 0;
                this.updateCurrentList();
                this.currentList[this.currentKey].isActive = true;
            }
            this.$emit('input', {key: this.name, value: input.value});
        },
        updateCurrentList () {
            this.currentList = [];
            for (let i = this.currentStart; ( (i < this.items.length) && (i < (this.size+this.currentStart)) ) ;i++){
                this.currentList.push({value: this.items[i], isActive: false});
            }
        },
        selectItem(item) {
            this.currentValue = item;
            this.$emit('input', {key: this.name, value: item});
        },
        onEnter () {
            this.closeList();
            this.$emit('input', {key: this.name, value: this.currentValue});
        },
        changeItem(event) {
            const IS_LAST_ITEM_CURRENT_LIST = ((this.currentKey+1) % this.size === 0) && (this.currentKey >= 0);
            const IS_LAST_ITEM_ALL_LIST = (this.currentValue === this.items[this.items.length-1]);
            const IS_FIRST_ITEM_ALL_LIST = (this.currentValue === this.items[0]);

            if (this.currentKey > -1) {
                this.currentList[this.currentKey].isActive = false;
            }

            if (event == 'down') {
                if (!IS_LAST_ITEM_ALL_LIST) {
                    if ( IS_LAST_ITEM_CURRENT_LIST ) {
                        this.currentStart++;
                        this.updateCurrentList();
                    } else if (this.currentKey < this.items.length-1) {
                        this.currentKey++;
                    }
                }
            } else if (event == 'up') {
                if (this.currentKey === 0) {
                    if (!IS_FIRST_ITEM_ALL_LIST) {
                        this.currentStart--;
                        this.updateCurrentList();
                    }
                } else {
                    this.currentKey--;
                } 
            }
            this.currentList[this.currentKey].isActive = true;
            this.currentValue = this.currentList[this.currentKey].value;
        }
    },
    beforeMount () {
        this.currentValue = this.value;
        this.updateCurrentList();
    }
}
</script>

<style scoped>

.select-input-container{
    display: flex;
    align-items: center;
}

.input {
    float: left;
}

.icon {
    float: left;
    margin-left: -7pt;
    margin-bottom: 2px;
}

.dropdownlist-container {
    position: relative;
}

.dropdownlist {
	overflow: hidden;
	position: absolute;
    top:-12px;
	left: 0px;
	width: 100%;
	background-color: rgb(17, 28, 44);
}

.dropdownlist-item {
    cursor: pointer;
    text-align: center;
    margin-top: 1px;
    font-size: 13px;
}

.dropdownlist-item:hover {
    background-color: rgb(20, 40, 70);
}

.active {
    background-color: rgb(20, 40, 70);
}

::-webkit-scrollbar {
    width: 12px;
}
  
::-webkit-scrollbar-thumb {
    -webkit-border-radius: 10px;
    border-radius: 10px;
    background: rgba(12, 20, 46, 0.8); 
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.5); 
}

</style>