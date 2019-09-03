<template>
    <div>
        <div class="field name-on-card">
            <VInputText 
                v-bind:value="formPaymentData.nameOnCard"
                name="nameOnCard" 
                label="Name On Card:" 
                v-on:input="onInput"
                v-bind:error="this.getError('nameOnCard')"
            />
        </div>
        <div class="field name-on-card">
            <VInputText
                v-bind:value="(formPaymentData.cardNumber === 0)? '': formPaymentData.cardNumber.toString()"
                name="cardNumber"
                label="Card Number:"
                v-on:input="onInput"
                v-bind:error="this.getError('cardNumber')"
            />
        </div>
        <div class="expiration-date-container">
            <div class="field label">Expiration Date</div>
            <div>
                <div class="field expiration-date-month">    
                    <VInputSelect 
                        name="month"
                        label="MM"
                        v-bind:value="(formPaymentData.expirationDate.month === 0)? '': formPaymentData.expirationDate.month.toString()"
                        v-on:input="onInput"
                        v-bind:items="months"
                        v-bind:error="this.getError('month')"
                    />
                </div>
                <div class="field expiration-date-year ">    
                    <VInputSelect 
                        name="year"
                        label="YYYY"
                        v-bind:value="(formPaymentData.expirationDate.year === 0)? '': formPaymentData.expirationDate.year.toString()"
                        v-on:input="onInput"
                        v-bind:items="years"
                        v-bind:error="this.getError('year')"
                    />
                </div>
                <div class="field expiration-date-year ">    
                    <VInputText 
                        v-bind:value="(formPaymentData.CVV === 0)? '': formPaymentData.CVV.toString()"
                        name="CVV"
                        label="CVV:"
                        v-on:input="onInput"
                        v-bind:error="this.getError('CVV')"
                    />
                </div>
            </div>
        </div>
        <div class="button-container">
            <div class="button" v-on:click="submit">Check Out.</div>
        </div>
    </div>
</template>

<script>

import VInputText from './VInputText';
import VInputSelect from './VInputSelect';

export default {
    name: 'FormPayment',
    components: {
        VInputText,
        VInputSelect,
    },
    data () {
        return {
            months: [
                '01','02','03','04','05','06',
                '07','08','09','10','11','12'
            ],
            years: [],
            formPaymentData: {
                nameOnCard: '',
                cardNumber: 0,
                expirationDate: {
                    month: 0,
                    year: 0
                },
                CVV: 0
            },
            formErrors: []
        }
    },
    methods : {
        submit() {

            if (this.formPaymentData.nameOnCard === '') {
                this.insertError('nameOnCard','Required!');
            } else {
                this.resetError('nameOnCard')
            }

            if  ( 
                    (this.formPaymentData.cardNumber.toString() === '') || 
                    (this.formPaymentData.cardNumber === 0) 
            ) {
                this.insertError('cardNumber','Required!');
            } else if (this.formPaymentData.cardNumber.toString().length != 16) {
                this.insertError('cardNumber','Out of Range!');
            }  else {
                this.resetError('cardNumber');
            }

            if  ( 
                    (this.formPaymentData.expirationDate.month.toString() === '') || 
                    (this.formPaymentData.expirationDate.month === 0) 
            ) {
                this.insertError('month','Required!');
            }else {
                this.resetError('month');
            }

            if  ( 
                    (this.formPaymentData.expirationDate.year.toString() === '') || 
                    (this.formPaymentData.expirationDate.year === 0) 
            ) {
                this.insertError('year','Required!');
            }else {
                this.resetError('year');
            }

            if  ( 
                    (this.formPaymentData.CVV.toString() === '') || 
                    (this.formPaymentData.CVV === 0) 
            ) {
                this.insertError('CVV','Required!');
            } else if (this.formPaymentData.CVV.toString().length > 4) {
                this.insertError('CVV','Out of Range!');
            } else {
                this.resetError('CVV');
            }

            if (this.formErrors.length === 0) {
                this.$emit('submit',this.formPaymentData);
            }
        },
        insertError (field, message) {
            this.formErrors.push(
                {
                    field : field,
                    hasError: true,
                    message: message
                }
            );
        },
        getError(field) {
            let index = this.formErrors.findIndex ((error) => (error.field === field));
            if ( index > -1) {
                return this.formErrors[index];
            } else {
                return {
                    hasError: false,
                    message: ''
                }
            }
        },
        resetError (field) {
            this.formErrors = this.formErrors.filter(
                (error) => (error.field !== field)
            )
        },
        onInput (event) {
            const CVV_ONLY_NUMBER = /^\d+$/.test(event.value); 
            const CARD_NUMBER_ONLY_NUMBER = /^\d+$/.test(event.value); 
            
            switch(event.key){
                case 'nameOnCard':
                    this.resetError('nameOnCard');
                    this.formPaymentData.nameOnCard = event.value.toUpperCase();
                    break;
                case 'cardNumber':
                    this.resetError('cardNumber');
                    if ( (CARD_NUMBER_ONLY_NUMBER) || (event.value === '') ) {
                        this.formPaymentData.cardNumber = event.value;
                    }
                    break;
                case 'month': 
                    this.resetError('month');
                    this.formPaymentData.expirationDate.month = Number(event.value);
                    break;
                case 'year': 
                    this.resetError('year');
                    this.formPaymentData.expirationDate.year = Number(event.value);
                    break;
                case 'CVV': 
                    this.resetError('CVV');
                    if ( (CVV_ONLY_NUMBER) || (event.value === '') ) {
                        this.formPaymentData.CVV = Number(event.value);
                    }
                    break;
            }
        }
    },
    beforeMount () {
        const currentYear = new Date().getFullYear();
        for (let i = 0;i <= 9; i++) {
            this.years.push((currentYear+i).toString());
        }
    }
}
</script>

<style>
.expiration-date-container{
    width: 100%;
    margin-left: 10%;
}

.field {
    margin-top: 7%;
    color: #DDD;
    font-size: 0.5em;
}

.name-on-card {
    margin-left:10%;
    width: 80%;
}

.expiration-date-month {
    float: left;
    margin-top: 0%;
    margin-left: 0%;
    width: 20%;
}

.expiration-date-year {
    float: left;
    margin-top: 0%;
    margin-left: 10%;
    width: 20%;
}

.label {
    width: 100%;
}

.button-container {
    margin-top: 20%;
    margin-left: 17%;
}

.button {
    cursor: pointer;
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