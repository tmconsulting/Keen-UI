<template>
    <transition name="ui-alert--transition-toggle">
        <div class="ui-alert" :class="classes" role="alert">
            <div class="ui-alert__body">
                <div class="ui-alert__icon" v-if="!removeIcon">
                    <slot name="icon">
                        <ui-icon v-if="type === 'info'">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M12.984 9V6.984h-1.97V9h1.97zm0 8.016v-6h-1.97v6h1.97zm-.984-15c5.53 0 9.984 4.453 9.984 9.984S17.53 21.984 12 21.984 2.016 17.53 2.016 12 6.47 2.016 12 2.016z"/></svg>
                        </ui-icon>

                        <ui-icon v-if="type === 'success'">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M9.984 17.016l9-9-1.406-1.453-7.594 7.594-3.563-3.563L5.016 12zm2.016-15c5.53 0 9.984 4.453 9.984 9.984S17.53 21.984 12 21.984 2.016 17.53 2.016 12 6.47 2.016 12 2.016z"/></svg>
                        </ui-icon>

                        <ui-icon v-if="type === 'warning'">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M12.984 14.016v-4.03h-1.97v4.03h1.97zm0 3.984v-2.016h-1.97V18h1.97zm-12 3L12 2.016 23.016 21H.986z"/></svg>
                        </ui-icon>

                        <ui-icon v-if="type === 'error'">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M12.984 12.984v-6h-1.97v6h1.97zm0 4.032V15h-1.97v2.016h1.97zm-.984-15c5.53 0 9.984 4.453 9.984 9.984S17.53 21.984 12 21.984 2.016 17.53 2.016 12 6.47 2.016 12 2.016z"/></svg>
                        </ui-icon>
                    </slot>
                </div>

                <div class="ui-alert__content">
                    <slot></slot>
                </div>

                <div class="ui-alert__dismiss-button">
                    <ui-close-button
                        size="small"

                        @click="dismissAlert"

                        v-if="dismissible"
                    ></ui-close-button>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
import UiCloseButton from './UiCloseButton.vue';
import UiIcon from './UiIcon.vue';

export default {
    name: 'ui-alert',

    props: {
        type: {
            type: String,
            default: 'info' // 'info', 'success', 'warning', or 'error'
        },
        removeIcon: {
            type: Boolean,
            default: false
        },
        dismissible: {
            type: Boolean,
            default: true
        }
    },

    computed: {
        classes() {
            return [
                `ui-alert--type-${this.type}`
            ];
        }
    },

    methods: {
        dismissAlert() {
            this.$emit('dismiss');
        }
    },

    components: {
        UiCloseButton,
        UiIcon
    }
};
</script>

<style lang="scss">
@import './styles/imports';

$ui-alert-color             : darken (tmc-primary, 0.75) !default;
$ui-alert-font-size         : rem-calc(15px) !default;
$ui-alert-margin-bottom     : rem-calc(16px) !default;

.ui-alert {
    display: flex;
    font-family: $font-stack;
    font-size: $ui-alert-font-size;
    line-height: 1.4;
    margin-bottom: $ui-alert-margin-bottom;
    overflow: hidden;
    position: relative;
    transition: margin-bottom 0.3s;
    width: 100%;
    a {
        text-decoration: none;

        &:hover,
        &:focus {
            text-decoration: underline;
        }
    }
}

.ui-alert__icon {
    align-self: flex-start;
    flex-shrink: 0;
    margin-right: rem-calc(12px);
}

.ui-alert__body {
    align-items: center;
    color: $tmc-primary;
    display: flex;
    flex-direction: row;
    margin-bottom: 0;
    margin-top: 0;
    min-height: rem-calc(48px);
    padding: rem-calc(12px 16px);
    transition: opacity 0.3s, margin-top 0.4s;
    width: 100%;
}

.ui-alert__content {
    flex-grow: 1;
}

.ui-alert__dismiss-button {
    align-self: flex-start;
    flex-shrink: 0;
    margin-bottom: rem-calc(-4px);
    margin-left: rem-calc(8px);
    margin-right: rem-calc(-8px);
    margin-top: rem-calc(-4px);
}

// ================================================
// Types
// ================================================

.ui-alert--type-info {
    .ui-alert__body {
        background-color: rgba($tmc-links, 0.1);
        border-left:3px solid $tmc-links;
    }

    .ui-alert__icon {
        color: $tmc-links;
    }

    a {
        color: $tmc-links;
    }
}

.ui-alert--type-success {
    .ui-alert__body {
        background-color: rgba($tmc-accent, 0.12);
        border-left:3px solid $tmc-accent;
    }

    .ui-alert__icon {
        color: $tmc-accent;
    }

    a {
        color: $tmc-accent;
    }
}

.ui-alert--type-warning {
    .ui-alert__body {
        background-color: rgba($tmc-attention, 0.1);
        border-left:3px solid $tmc-attention;
    }

    .ui-alert__icon {
        color: $tmc-attention;
    }

    a {
        color: $tmc-attention;
    }
}

.ui-alert--type-error  {
    .ui-alert__body {
        background-color: rgba($tmc-invalid, 0.12);
        border-left:3px solid $tmc-invalid;
    }

    .ui-alert__icon {
        color: $tmc-invalid;
    }

    a {
        color: $tmc-invalid;
    }
}

// ================================================
// Transition
// ================================================

.ui-alert--transition-toggle-enter,
.ui-alert--transition-toggle-leave-active {
    margin-bottom: 0;

    .ui-alert__body {
        margin-top: rem-calc(-56px);
        opacity: 0;
    }
}
</style>
