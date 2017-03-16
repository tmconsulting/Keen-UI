<template>
    <section class="page page--ui-button">
        <h2 class="page__title">TMC Кнопки</h2>

        <p>Типы кнопок:</p>

        <ul>
            <li><b>Фирменый синий</b>:</li>
            <li><b>Фирменый зеленый</b>: </li>
        </ul>

        <p>А так же есть обычный стандартный цвет</p>

        <h3 class="page__section-title">
            Примеры <a href="https://github.com/JosephusPaye/Keen-UI/blob/master/docs-src/pages/UiButton.vue" target="_blank" rel="noopener">View Source</a>
        </h3>

        <div class="page__examples">
            <ui-radio-group
                name="size"
                :options="['small', 'normal', 'large']"
                v-model="size"
            >Размеры кнопок</ui-radio-group>

            <ui-radio-group
                name="icon_position"
                :options="['left', 'right']"
                v-model="iconPosition"
            >Выравнивание иконки</ui-radio-group>

            <ui-switch v-model="loading">
                Загрузка: <code>{{ loading ? 'on' : 'off' }}</code>
            </ui-switch>

            <div class="table-responsive">
                <table class="table table-bordered page__demo-table">
                    <tbody>
                        <tr>
                            <th></th>
                            <th>Тип: первостепенные</th>
                            <th>Тип: второстепенные</th>
                        </tr>

                        <tr>
                            <th>Цвет: Обычный</th>
                            <td>
                                <ui-button :size="size">Нормальная</ui-button>
                                <ui-button raised :size="size">Приподнятая</ui-button>
                                <ui-button :loading="loading" :size="size">Загрузка</ui-button>
                                <ui-button disabled :size="size">Недоступно</ui-button>
                                <ui-button icon="refresh" :icon-position="iconPosition" :size="size">С иконкой</ui-button>
                            </td>

                            <td>
                                <ui-button :size="size" type="secondary">Нормальная</ui-button>
                                <ui-button raised :size="size" type="secondary">Приподнятая</ui-button>
                                <ui-button :loading="loading" :size="size" type="secondary">Загрузка</ui-button>
                                <ui-button disabled :size="size" type="secondary">Недоступно</ui-button>
                                <ui-button icon="refresh" :icon-position="iconPosition" :size="size" type="secondary">С иконкой</ui-button>
                            </td>
                        </tr>

                        <tr>
                            <th>Color: Фирменный синий</th>
                            <td>
                                <ui-button color="primary" :size="size">Нормальная</ui-button>
                                <ui-button color="primary" raised :size="size">Приподнятая</ui-button>
                                <ui-button color="primary" :loading="loading" :size="size">Загрузка</ui-button>
                                <ui-button color="primary" disabled :size="size">Недоступно</ui-button>
                                <ui-button color="primary" icon="add" :icon-position="iconPosition" :size="size">With Icon</ui-button>
                            </td>

                            <td>
                                <ui-button color="primary" :size="size" type="secondary">Нормальная</ui-button>
                                <ui-button color="primary" raised :size="size" type="secondary">Приподнятая</ui-button>
                                <ui-button color="primary" :loading="loading" :size="size" type="secondary">Загрузка</ui-button>
                                <ui-button color="primary" disabled :size="size" type="secondary">Недоступно</ui-button>
                                <ui-button color="primary" icon="add" :icon-position="iconPosition" :size="size" type="secondary">С иконкой</ui-button>
                            </td>
                        </tr>

                        <tr>
                            <th>Color: Фирменный зеленый</th>
                            <td>
                                <ui-button color="accent" :size="size">Нормальная</ui-button>
                                <ui-button color="accent" raised :size="size">Приподнятая</ui-button>
                                <ui-button color="accent" :loading="loading" :size="size">Загрузка</ui-button>
                                <ui-button color="accent" disabled :size="size">Недоступно</ui-button>
                                <ui-button color="accent" icon="add" :icon-position="iconPosition" :size="size">С иконкой</ui-button>
                            </td>

                            <td>
                                <ui-button color="accent" :size="size" type="secondary">Нормальная</ui-button>
                                <ui-button color="accent" raised :size="size" type="secondary">Приподнятая</ui-button>
                                <ui-button color="accent" :loading="loading" :size="size" type="secondary">Загрузка</ui-button>
                                <ui-button color="accent" disabled :size="size" type="secondary">Недоступно</ui-button>
                                <ui-button color="accent" icon="add" :icon-position="iconPosition" :size="size" type="secondary">С иконкой</ui-button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <div class="page__demo">
            <h4 class="page__demo-title">Выпадающий список с пунктами меню</h4>

            <div class="page__demo-group">
                <ui-button color="primary" has-dropdown ref="dropdownButton" :size="size">
                    <ui-menu
                        contain-focus
                        has-icons
                        has-secondary-text
                        slot="dropdown"

                        :options="menuOptions"

                        @close="$refs.dropdownButton.closeDropdown()"
                    ></ui-menu>
                    Нажми для просмотра
                </ui-button>
            </div>

            <h4 class="page__demo-title">Кастомизированный с текстом</h4>

            <div class="page__demo-group">
                <ui-button has-dropdown :size="size">
                    <div class="custom-popover-content" slot="dropdown">
                        <p><b>Привет</b> всем!</p>
                        <p>Здесь может быть не только текст и выпадающие списки, но и кнопки.</p>
                    </div>

                    Нажми для просмотра
                </ui-button>
            </div>

            <h4 class="page__demo-title">Выпадашка с брендом</h4>

            <div class="page__demo-group">
                <ui-button has-dropdown :size="size" type="default">
                    <div class="tmc-brand-popover" slot="dropdown">
                       <div class="tmc-mainbrand">
                           <a href="/"><img class="tmc-mainbrand__photo" :src="image.logo" alt="">Travel Management Cansalting</a>
                           <div><ui-icon-button has-dropdown icon="more_vert" :size="size" color="white">
                               <div class="tmc-brand-popover" slot="dropdown">
                                   <ul class="tmc-mainbrand__links">
                                       <li><a href="/">Сменить компанию</a></li>
                                       <li><a href="/">Настройки</a></li>
                                   </ul>
                               </div>
                           </ui-icon-button></div>
                       </div>
                       <ul class="tmc-mainbrand__links">
                           <li><a href="/">Офисы</a></li>
                           <li><a href="/">Менеджеры</a></li>
                           <li><a href="/">Приложения</a></li>
                       </ul>
                        <div class="tmc-mainbrand__manager">
                            <a class="tmc-mainbrand__manager-face" href="/">
                                <img class="tmc-mainbrand__photo" :src="image.manager" alt="">
                                <span class="tmc-mainbrand__manager-name">
                                <p>Mariya Pelota</p>
                                <p class="tmc-mainbrand__manager-position">Passive Enginer</p>
                            </span>
                            </a>
                            <ui-icon-button has-dropdown icon="mail_outline" :size="size" color="black">
                                <div class="tmc-brand-popover" slot="dropdown">
                                    <ul class="tmc-mainbrand__links">
                                        <li><a href="/">Отправить письмо</a></li>
                                        <li><a href="/">Оставить сообщение</a></li>
                                    </ul>
                                </div>
                            </ui-icon-button>
                        </div>

                    </div>
                    Travel Management Consulting
                </ui-button>
            </div>
        </div>

        <h3 class="page__section-title">API</h3>

        <ui-tabs raised>
            <ui-tab title="Props">
                <div class="table-responsive">
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Type</th>
                                <th>Default</th>
                                <th>Description</th>
                            </tr>
                        </thead>

                        <tbody>
                            <tr>
                                <td>type</td>
                                <td>String</td>
                                <td><code>"primary"</code></td>
                                <td>
                                    <p>The type of button (determines the visual prominence).</p>
                                    <p>Use <code>primary</code> for a more prominent button, and <code>secondary</code> for a less prominent button.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>buttonType</td>
                                <td>String</td>
                                <td><code>"submit"</code></td>
                                <td>The <code>type</code> attribute of the button element.</td>
                            </tr>

                            <tr>
                                <td>color</td>
                                <td>String</td>
                                <td><code>"default"</code></td>
                                <td>
                                    <p>One of <code>primary</code>, <code>accent</code>, <code>green</code>, <code>orange</code>, <code>red</code> or <code>default</code>.</p>
                                    <p>In <code>type="primary"</code> buttons, this is the background color; in <code>type="secondary"</code> buttons, the text color.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>size</td>
                                <td>String</td>
                                <td><code>"normal"</code></td>
                                <td>
                                    <p>The size of the button. One of <code>small</code>, <code>normal</code>, or <code>large</code>.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>loading</td>
                                <td>Boolean</td>
                                <td><code>false</code></td>
                                <td>
                                    <p>Whether or not the button progress spinner is shown.</p>
                                    <p>Set to <code>true</code> to show the progress. This disables the button.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>raised</td>
                                <td>Boolean</td>
                                <td><code>false</code></td>
                                <td>
                                    <p>Whether or not the button has a drop shadow.</p>
                                    <p>Set to <code>true</code> to show a drop shadow.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>icon</td>
                                <td>String</td>
                                <td></td>
                                <td>
                                    <p>The button icon. Can be any of the <a href="https://design.google.com/icons/" target="_blank" rel="noopener">Material Icons</a>.</p>
                                    <p>You can set a custom or SVG icon using the <code>icon</code> slot.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>iconPosition</td>
                                <td>String</td>
                                <td><code>"left"</code></td>
                                <td>
                                    <p>The position of the icon relative to the button text. One of <code>left</code> or <code>right</code>.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>disableRipple</td>
                                <td>Boolean</td>
                                <td><code>false</code></td>
                                <td>
                                    <p>Whether or not the ripple ink animation is shown when the button is clicked.</p>
                                    <p>Can be set using the <a href="https://github.com/JosephusPaye/Keen-UI/blob/master/Customization.md#global-config" target="_blank" rel="noopener">global config</a>.</p>
                                    <p>Set to <code>true</code> to disable the ripple ink animation.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>hasDropdown</td>
                                <td>Boolean</td>
                                <td><code>false</code></td>
                                <td>
                                    <p>Whether or not the button contains a dropdown.</p>
                                    <p>Use the <code>dropdown</code> slot to add any dropdown content, including a <a href="#/ui-menu">UiMenu</a>.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>dropdownPosition</td>
                                <td>String</td>
                                <td class="no-wrap"><code>"bottom left"</code></td>
                                <td>
                                    <p>The position of the dropdown relative to the button.</p>
                                    <p>One of <code>top left</code>, <code>left top</code>, <code>left middle</code>, <code>left bottom</code>, <code>bottom left</code>, <code>bottom center</code>, <code>bottom right</code>, <code>right bottom</code>, <code>right middle</code>, <code>right top</code>, <code>top right</code>, or <code>top center</code>.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>openDropdownOn</td>
                                <td>String</td>
                                <td><code>"click"</code></td>
                                <td>
                                    <p>The type of event that will cause the dropdown to open. One of <code>click</code>, <code>hover</code>, <code>focus</code>, or <code>always</code>.</p>
                                    <p>For <code>always</code>, the dropdown is opened when rendered and it remains open.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>disabled</td>
                                <td>Boolean</td>
                                <td><code>false</code></td>
                                <td>
                                    <p>Whether or not the button is disabled.</p>
                                    <p>Set to <code>true</code> to disable the button.</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </ui-tab>

            <ui-tab title="Slots">
                <div class="table-responsive">
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Description</th>
                            </tr>
                        </thead>

                        <tbody>
                            <tr>
                                <td>(default)</td>
                                <td>Holds the button text and can contain HTML.</td>
                            </tr>

                            <tr>
                                <td>icon</td>
                                <td>
                                    <p>Holds the button icon and can contain any custom or SVG icon.</p>
                                </td>
                            </tr>

                            <tr>
                                <td>dropdown</td>
                                <td>
                                    <p>Holds the the dropdown content and can contain HTML.</p>
                                    <p>For a dropdown menu, add a <a href="#/ui-menu">UiMenu</a> component in this slot, and then call the <code>closeDropdown()</code> method when the <code>close</code> event is emitted on the menu.</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </ui-tab>

            <ui-tab title="Events">
                <div class="table-responsive">
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Description</th>
                            </tr>
                        </thead>

                        <tbody>
                            <tr>
                                <td class="no-wrap">dropdown-open</td>
                                <td>
                                    <p>Emitted when the button dropdown is opened.</p>
                                    <p>Listen for it using <code>@dropdown-open</code>.</p>
                                </td>
                            </tr>

                            <tr>
                                <td class="no-wrap">dropdown-close</td>
                                <td>
                                    <p>Emitted when the button dropdown is closed.</p>
                                    <p>Listen for it using <code>@dropdown-close</code>.</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </ui-tab>

            <ui-tab title="Methods">
                <div class="table-responsive">
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Description</th>
                            </tr>
                        </thead>

                        <tbody>
                            <tr>
                                <td class="no-wrap"><code>openDropdown()</code></td>
                                <td>
                                    <p>Call this method to open the button dropdown.</p>
                                </td>
                            </tr>

                            <tr>
                                <td class="no-wrap"><code>closeDropdown()</code></td>
                                <td>
                                    <p>Call this method to close the button dropdown.</p>
                                </td>
                            </tr>

                            <tr>
                                <td class="no-wrap"><code>toggleDropdown()</code></td>
                                <td>
                                    <p>Call this method to toggle the button dropdown.</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </ui-tab>
        </ui-tabs>
    </section>
</template>

<script>
import UiButton from 'src/UiButton.vue';
import UiIconButton from 'src/UiIconButton.vue';
import UiMenu from 'src/UiMenu.vue';
import UiRadioGroup from 'src/UiRadioGroup.vue';
import UiSwitch from 'src/UiSwitch.vue';
import UiTab from 'src/UiTab.vue';
import UiTabs from 'src/UiTabs.vue';

const menuOptions = [
    {
        id: 'edit',
        label: 'Edit',
        icon: 'edit',
        secondaryText: 'Ctrl+E'
    },
    {
        id: 'duplicate',
        label: 'Duplicate',
        icon: 'content_copy',
        secondaryText: 'Ctrl+D'
    },
    {
        id: 'share',
        label: 'Share',
        icon: 'share',
        secondaryText: 'Ctrl+Shift+S',
        disabled: true
    },
    {
        type: 'divider'
    },
    {
        id: 'delete',
        label: 'Delete',
        icon: 'delete',
        secondaryText: 'Del'
    }
];

export default {
    data() {
        return {
            image: {
                logo: 'img/Logo.png',
                manager: 'img/ManagerPhoto.png'
            },
            size: 'normal',
            iconPosition: 'left',
            loading: true,
            menuOptions
        };
    },

    components: {
        UiButton,
        UiIconButton,
        UiMenu,
        UiRadioGroup,
        UiSwitch,
        UiTab,
        UiTabs
    }
};
</script>

<style lang="scss">
@import '~styles/imports';

.page--ui-button {
    .ui-radio-group,
    .ui-switch {
        margin-bottom: rem-calc(16px);
    }

    .ui-switch {
        display: inline-flex;
    }

    .ui-button {
        margin-bottom: rem-calc(12px);
        margin-right: rem-calc(8px);
    }

    .page__demo-group {
        margin-bottom: rem-calc(18px);
    }

    .page__demo-table {
        max-width: rem-calc(600px);

        .ui-button {
            display: flex;

            &.ui-button--size-normal {
                min-width: rem-calc(100px);
            }

            &.ui-button--size-large {
                min-width: rem-calc(124px);
            }
        }
    }
}

.custom-popover-content {
    padding: rem-calc(16px);
    max-width: rem-calc(360px);

    p:first-child {
        margin-top: 0;
    }

    p:last-child {
        margin-bottom: 0;
    }
}
.tmc-brand-popover{
    max-width: rem-calc(360px);
    font-family: $font-stack;

    min-width: rem-calc(168px);
    outline: none;
    overflow-x: hidden;
    overflow-y: auto;

p:first-child {
    margin-top: 0;
}

p:last-child {
    margin-bottom: 0;
}
}
.tmc-mainbrand{
    @include flexbox();
    justify-content: space-between;
    padding: rem-calc(25px 20px);
    background: $tmc-accent;
    margin:0;
    a{
        @include flexbox();
        justify-content:space-between;
        align-items:center;
        color:$md-white;
        &:hover{
            opacity:0.8;
         }
        margin:0 10px 0 0;
    }
    img{
        margin:0 10px 0 0;
    }
}
.tmc-mainbrand__links{
    height: 100%;
    list-style: none;
    margin:0;
    padding:0;
    li{

        a{
            padding:16px 20px;
            display: block;
            color:$tmc-primary;
            &:hover{
                background: $tmc-default;
                color:$tmc-links;
             }
        }
    }
}
.tmc-mainbrand__photo{
    height: 34px;
    width: 34px;
    border-radius: $tmc-radius-50;
    margin: 0 10px 0 0;
}
.tmc-mainbrand__manager{
    @include flexbox();
    justify-content:space-between;
    align-items:center;
    border-top:1px solid $tmc-default;
    padding: rem-calc(25px 20px);
    margin:0;
}
.tmc-mainbrand__manager-face{
    @include flexbox();
    align-items:center;
    flex-direction: row;
}
.tmc-mainbrand__manager-name{
    @include flexbox();
    flex-direction: column;
    color:$tmc-primary;
    &:hover{
    color:$tmc-links;
     }
    p{
        padding: 0;
        margin: 0;
    }
    .tmc-mainbrand__manager-position{
        font-size: 13px;
    }
}
</style>
