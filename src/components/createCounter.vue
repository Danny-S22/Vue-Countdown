<template>
    <div class="container mb-3">
        <form action="">
            <div class="mb-3 p-4">
                <label for="" class="form-table">
                    Hours
                </label>
                <input type="text" class="form-control" v-model="hours" v-on:input="validateNumber('hours')">
                <label for="" class="form-table">
                    Minutes
                </label>
                <input type="text" class="form-control" v-model="minutes" v-on:input="validateNumber('minutes')">
                <label for="" class="form-table">
                    Seconds
                </label>
                <input type="text" class="form-control" v-model="seconds" v-on:input="validateNumber('seconds')">
                <button class="set-counter btn btn-primary btn-dark" @click.prevent="submitForm" :disabled="ifFormInvalid">
                    Set Counter
                </button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            hours: '',
            minutes: '',
            seconds: ''
        };
    },
    computed: {
        ifFormInvalid() {
            return this.hours === '' && this.minutes === '' && this.seconds === '';
        }
    },
    methods: {
        validateNumber(field) {
            this[field] = this[field].replace(/\D/g, '');
        },
        submitForm() {
            this.$emit('counter-created', {
                hours: this.hours,
                minutes: this.minutes,
                seconds: this.seconds
            });
        }
    }
}
</script>

<style scoped>
label {
    display: block;
    margin: 10px 0 5px;
}

.container {
    margin: 0 auto;
    width: 20%;
}

.set-counter {
    margin: 20px;
}
</style>