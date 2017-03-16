<template>
    <li
        class="ui-menu-option"
        ref="menuOption"
        role="menu-item"

        :class="classes"
        :tabindex="(isDivider || disabled) ? null : '0'"
    >
        <slot v-if="!isDivider">
            <div class="ui-menu-option__content">
                <ui-icon
                    class="ui-menu-option__icon"

                    :icon-set="iconProps.iconSet"
                    :icon="icon"
                    :remove-text="iconProps.removeText"
                    :use-svg="iconProps.useSvg"

                    v-if="icon"
                ></ui-icon>

                <div class="ui-menu-option__text">{{ label }}</div>

                <div class="ui-menu-option__secondary-text" v-if="secondaryText">
                    {{ secondaryText }}
                </div>
            </div>
        </slot>

        <ui-ripple-ink
            trigger="menuOption"
            v-if="!disabled && !isDivider && !disableRipple"
        ></ui-ripple-ink>
    </li>
</template>

<script>
import UiIcon from './UiIcon.vue';
import UiRippleInk from './UiRippleInk.vue';

import config from './config';

export default {
    name: 'ui-menu-option',

    props: {
        type: String,
        label: String,
        icon: String,
        iconProps: {
            type: Object,
            default() {
                return {};
            }
        },
        secondaryText: String,
        disableRipple: {
            type: Boolean,
            default: config.data.disableRipple
        },
        disabled: {
            type: Boolean,
            default: false
        }
    },

    computed: {
        classes() {
            return {
                'is-divider': this.isDivider,
                'is-disabled': this.disabled
            };
        },

        isDivider() {
            return this.type === 'divider';
        }
    },

    components: {
        UiIcon,
        UiRippleInk
    }
};
</script>

<style lang="scss">
@import './styles/imports';

.ui-menu-option {
    display: block;
    font-family: $font-stack;
    position: relative;
    user-select: none;
    width: 100%;

    &.is-divider {
        background-color: rgba(black, 0.08);
        display: block;
        height: rem-calc(1px);
        margin: rem-calc(6px 0);
        padding: 0;
    }

    &:not(.is-divider) {
        color: $tmc-primary;
        cursor: pointer;
        font-size: $ui-dropdown-item-font-size;
        font-weight: normal;
        min-height: rem-calc(40px);
        outline: none;

        &:hover:not(.is-disabled),
        body[modality="keyboard"] &:focus {
            background-color: #EEEEEE; // rgba(black, 0.1);
        }

        &.is-disabled {
            color: $tmc-secondary-text;
            cursor: default;
            opacity: 0.5;

            .ui-menu-option__secondary-text {
                color: $tmc-secondary-text;
            }
        }
    }
}

.ui-menu-option__content {
    align-items: center;
    display: flex;
    height: rem-calc(40px);
    padding: rem-calc(0 16px);
}

.ui-menu-option__icon {
    color: $tmc-secondary-text;
    font-size: rem-calc(18px);
    margin-right: rem-calc(16px);
}

.ui-menu-option__text {
    @include text-truncation;
    flex-grow: 1;
}

.ui-menu-option__secondary-text {
    color: $tmc-hint;
    flex-shrink: 0;
    font-size: rem-calc(13px);
    margin-left: rem-calc(4px);
}
</style>
