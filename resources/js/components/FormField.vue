<template>
    <default-field :field="field" :errors="errors">
        <template slot="field">
            <div class="flex items-center">
                <time-picker
                    class="w-full form-control form-input form-input-bordered border-r-0 rounded-r-none"
                    :class="{ 'border-danger': hasError }"
                    :id="field.attribute"
                    :field="field"
                    :placeholder="placeholder"
                    :value="value"
                    :dusk="field.attribute"
                    :disabled="isReadonly"
                    :twelveHourTime="twelveHourTime"
                    :minuteIncrement="minuteIncrement"
                    @change="handleChange"
                />
                <button class="form-control form-input form-input-bordered border-l-0 rounded-l-none" @click.prevent="clearTime">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" width="24" height="24">
                        <path class="heroicon-ui" d="M16.24 14.83a1 1 0 0 1-1.41 1.41L12 13.41l-2.83 2.83a1 1 0 0 1-1.41-1.41L10.59 12 7.76 9.17a1 1 0 0 1 1.41-1.41L12 10.59l2.83-2.83a1 1 0 0 1 1.41 1.41L13.41 12l2.83 2.83z"/>
                    </svg>
                </button>
            </div>
        </template>
    </default-field>
</template>

<script>
import TimePicker from './../TimePicker'
import { Errors, FormField, HandlesValidationErrors } from 'laravel-nova'

export default {
    mixins: [HandlesValidationErrors, FormField],

    components: { TimePicker },

    computed: {
        placeholder() {
            return moment(new Date()).format('HH:ss')
        },

        twelveHourTime() {
            return this.field.twelveHourTime || false;
        },

        minuteIncrement() {
            return this.field.minuteIncrement || 5;
        }
    },

    methods: {
        onClear(event) {
            if(event.target.value === '') {
                this.flatpickr.close();
            }
        },
        clearTime () {
            this.value = '';
        }
    },

    beforeDestroy() {
        this.flatpickr.destroy()
    },
}
</script>
