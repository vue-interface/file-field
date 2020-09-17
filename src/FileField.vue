<template>
    <div class="form-file" :class="formGroupClasses">
        <slot name="control">
            <input
                ref="field"
                v-bind-events
                v-bind="controlAttributes"
                type="file"
                :multiple="multiple"
                :value="value"
                @input="$emit('input', $event.target.files)">
        </slot>

        <slot name="label">
            <label :for="$attrs.id" :class="legacy ? legacyLabelClass : labelClass">
                <template v-if="legacy">{{ label || defaultLabel }}</template>
                <template v-else>
                    <span class="form-file-text">{{ label || defaultLabel }}</span>
                    <span class="form-file-button">Browse</span>
                </template>
            </label>
        </slot>

        <slot name="feedback">
            <div 
                v-if="invalidFeedback"
                class="invalid-feedback"
                invalid
                v-html="invalidFeedback" />
            <div 
                v-else-if="validFeedback"
                class="valid-feedback"
                valid
                v-html="validFeedback" />
        </slot>

        <slot name="help">
            <small v-if="helpText" ref="help">
                {{ helpText }}
            </small>
        </slot>
    </div>
</template>

<script>
import FormControl from '@vue-interface/form-control';

export default {

    mixins: [
        FormControl
    ],

    props: {

        /**
         * The class name assigned to the control element
         *
         * @property String
         */
        defaultControlClass: {
            type: String,
            default: 'form-file-input'
        },

        /**
         * The label
         *
         * @property String
         */
        label: {
            type: String,
            default: 'Choose file...'
        },

        /**
         * The class name assigned to the control element
         *
         * @property String
         */
        labelClass: {
            type: String,
            default: 'form-file-label'
        },

        /**
         * The legacy class name assigned to the control element
         *
         * @property String
         */
        legacyControlClass: {
            type: String,
            default: 'custom-file-input'
        },

        /**
         * The legacy class name assigned to the control element
         *
         * @property String
         */
        legacyLabelClass: {
            type: String,
            default: 'custom-file-label'
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

    },

    computed: {

        controlClass() {
            return this.custom ? this.customControlClass : (
                this.legacy ? this.legacyControlClass : this.defaultControlClass
            );
        }

    }
};
</script>

<style>
.file-field {
    position: relative;
}
</style>