<script>

const FormErrorHandler =  {
    data () {
        return {
            formErrors: []
        }
    },
    methods: {
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
            const INDEX_ERROR = this.formErrors.findIndex ((error) => (error.field === field));
            const  HAS_ERROR = INDEX_ERROR > -1;
            if ( HAS_ERROR ) {
                return this.formErrors[INDEX_ERROR];
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
        }
    }
}

export default FormErrorHandler;

</script>
