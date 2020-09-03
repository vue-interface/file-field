<template>
    <div :class="formGroupClasses">
        <slot name="label">
            <label v-if="label" ref="label" :for="$attrs.id" class="custom-file-label" v-html="label" />
        </slot>

        <slot name="control">
            <input
                ref="field"
                v-bind-events
                v-bind="controlAttributes"
                type="file"
                :value="value"
                @change="$emit('change', $event.target.files)">
        </slot>

        <slot name="feedback">
            <div 
                v-if="validFeedback"
                class="valid-feedback"
                valid
                v-html="invalidFeedback" />
            <div 
                v-else-if="invalidFeedback"
                class="invalid-feedback"
                invalid
                v-html="invalidFeedback" />
        </slot>

        <slot name="help">
            <small v-if="helpText" ref="help">
                {{ helpText }}
            </small>
        </slot>
    </div>
</template>

<script>
import InputField from '@vue-interface/input-field';

export default {

    name: 'FileField',

    extends: InputField,

    model: {
        event: 'change'
    },

    props: {

        /**
         * An array of event names that correlate with callback functions
         *
         * @property Function
         */
        bindEvents: {
            type: Array,
            default() {
                return ['focus', 'blur', 'input', 'click', 'keyup', 'keydown', 'progress'];
            }
        },

        /**
         * The class name assigned to the control element
         *
         * @property String
         */
        defaultControlClass: {
            type: String,
            default: 'custom-file-input'
        },

        /**
         * An array of valid extensions
         *
         * @property String
         */
        extensions: Array,

        /**
         * The type attribute
         *
         * @property String
         */
        multiple: Boolean,

        /**
         * The height attribute for the control element
         *
         * @property String
         */
        height: [Number, String],

        /**
         * The width attribute for the control element
         *
         * @property String
         */
        width: [Number, String]

    }

};
</script>

<style>
.file-field {
    position: relative;
}
</style>