<template>
    <div class="ui-toolbar" :class="classes">
        <div class="ui-toolbar__left">
            <div class="ui-toolbar__nav-icon" v-if="!removeNavIcon">
                <slot name="icon">
                    <ui-icon-button
                        size="large"
                        type="secondary"

                        :color="textColor"
                        :icon="navIcon"

                        @click="navIconClick"
                    ></ui-icon-button>
                </slot>
            </div>

            <div class="ui-toolbar__brand" v-if="brand || $slots.brand">
                <slot name="brand">
                    <div class="ui-toolbar__brand-text">{{ brand }}</div>
                </slot>
            </div>
        </div>

        <div class="ui-toolbar__body" :class="{ 'has-brand-divider': hasBrandDivider }">
            <slot>
                <div class="ui-toolbar__title" v-if="title">{{ title }}</div>
            </slot>
        </div>

        <div class="ui-toolbar__right">
            <slot name="actions"></slot>
        </div>

        <ui-progress-linear
            class="ui-toolbar__progress"
            :color="progressColor"
            v-show="loading"
        ></ui-progress-linear>
    </div>
</template>

<script>
import UiIconButton from './UiIconButton.vue';
import UiProgressLinear from './UiProgressLinear.vue';

export default {
    name: 'ui-toolbar',

    props: {
        type: {
            type: String,
            default: 'default' // 'default', 'colored' or 'clear' - colored is brand primary color
        },
        textColor: {
            type: String,
            default: 'black' // 'black' or 'white'
        },
        title: String,
        brand: String,
        removeBrandDivider: {
            type: Boolean,
            default: false
        },
        navIcon: {
            type: String,
            default: 'menu'
        },
        removeNavIcon: {
            type: Boolean,
            default: false
        },
        raised: {
            type: Boolean,
            default: true
        },
        progressPosition: {
            type: String,
            default: 'bottom' // 'top' or 'bottom'
        },
        loading: {
            type: Boolean,
            default: false
        }
    },

    computed: {
        classes() {
            return [
                `ui-toolbar--type-${this.type}`,
                `ui-toolbar--text-color-${this.textColor}`,
                `ui-toolbar--progress-position-${this.progressPosition}`,
                { 'is-raised': this.raised }
            ];
        },

        progressColor() {
            return (this.textColor === 'black') ? 'primary' : 'white';
        },

        hasBrandDivider() {
            return this.removeBrandDivider ? false : (this.brand || this.$slots.brand);
        }
    },

    methods: {
        navIconClick() {
            this.$emit('nav-icon-click');
        }
    },

    components: {
        UiIconButton,
        UiProgressLinear
    }
};
</script>

<style lang="scss">
@import './styles/imports';

$ui-toolbar-font-size   : rem-calc(18px) !default;
$ui-toolbar-height      : rem-calc(56px) !default;

.ui-toolbar {
    align-items: center;
    display: flex;
    font-family: $font-stack;
    font-size: $ui-toolbar-font-size;
    height: $ui-toolbar-height;
    padding-left: rem-calc(16px);
    position: relative;

    &.is-raised {
        box-shadow: 0 0 2px rgba(black, 0.12), 0 2px 2px rgba(black, 0.2);
    }

    &:not(.is-raised).ui-toolbar--type-default {
        border-bottom: rem-calc(1px) solid $divider-color;
    }

    .ui-icon-button {
        height: rem-calc(48px);
        width: rem-calc(48px);
    }
}

.ui-toolbar__left {
    align-items: center;
    display: flex;
    flex-shrink: 0;
}

.ui-toolbar__nav-icon {
    margin-left: rem-calc(-16px);
    margin-right: rem-calc(8px);
}

.ui-toolbar__brand {
    min-width: rem-calc(160px);
}

.ui-toolbar__brand-text {
    flex-grow: 1;
    padding-right: rem-calc(8px);
}

.ui-toolbar__body {
    display: flex;
    flex-grow: 1;

    &.has-brand-divider {
        border-left-style: solid;
        border-left-width: rem-calc(1px);
        padding-left: rem-calc(24px);
    }
}

.ui-toolbar__right {
    flex-shrink: 0;
    margin-left: auto;
}

.ui-toolbar__progress {
    bottom: 0;
    height: rem-calc(3px);
    left: 0;
    position: absolute;
    right: 0;
}

// ================================================
// Types
// ================================================

.ui-toolbar--type-default {
    background-color: white;
}

.ui-toolbar--type-colored {
    background-color: lighten($tmc-primary, 5%);
}

.ui-toolbar--type-clear {
    background-color: transparent;
    border: none;
    box-shadow: none;
}

// ================================================
// Text colors
// ================================================

.ui-toolbar--text-color-black {
    color: $tmc-primary;

    .ui-toolbar__body {
        border-left-color: rgba(black, 0.15);
    }
}

.ui-toolbar--text-color-white {
    color: white;

    .ui-toolbar__body {
        border-color: rgba(white, 0.4);
    }
}

// ================================================
// Progress positions
// ================================================

.ui-toolbar--progress-position-top {
    .ui-toolbar__progress {
        top: 0;
    }
}
</style>
