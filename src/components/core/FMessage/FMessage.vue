<template>
    <div class="f-message" :class="[classes, type]">
        <slot name="prefix">
            <template v-if="withIcon">
                <icon
                    v-if="type === 'success'"
                    data="@/assets/svg/message/check-circle.svg"
                    width="16"
                    height="16"
                    aria-hidden="true"
                />
                <icon
                    v-if="type === 'error'"
                    data="@/assets/svg/message/exclamation-circle.svg"
                    width="16"
                    height="16"
                    aria-hidden="true"
                />
                <icon
                    v-if="type === 'info'"
                    data="@/assets/svg/message/info-circle.svg"
                    width="16"
                    height="16"
                    aria-hidden="true"
                />
            </template>
        </slot>
        <span class="f-message-body"><slot></slot></span>
        <slot name="suffix"></slot>
    </div>
</template>

<script>
import { helpersMixin } from '../../../mixins/helpers.js';

export default {
    mixins: [helpersMixin],

    props: {
        type: {
            type: String,
            default: '',
            required: true,
        },
        withIcon: {
            type: Boolean,
            default: false,
        },
    },

    computed: {
        classes() {
            return {
                'with-icon': this.withIcon,
                'prefix-slot': this.hasSlot('prefix'),
                'suffix-slot': this.hasSlot('suffix'),
            };
        },
    },

    methods: {
        getMessage() {
            return this.$slots.default ? this.$slots.default[0].text : '';
        },
    },
};
</script>

<style lang="scss">
@import 'style';
</style>
