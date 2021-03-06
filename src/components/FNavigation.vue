<template>
    <div class="f-navigation">
        <nav>
            <slot>
                <ul class="no-markers" v-if="cItems">
                    <li v-for="item in cItems" :key="item.id">
                        <a v-if="item.url.indexOf('http') === 0" :href="item.url" target="_blank">
                            {{ item.title }}
                        </a>
                        <router-link v-else :to="item.url">{{ item.title }}</router-link>
                    </li>
                </ul>
            </slot>
        </nav>
    </div>
</template>

<script>
    import { helpersMixin } from "../mixins/helpers.js";

    export default {
        mixins: [
            helpersMixin
        ],

        props: {
            /**
             * Array of navigation links.
             *
             * One item is an object with keys:
             * `url` - link url
             * `title` - link title
             */
            items: {
                type: Array,
                default() {
                    return [];
                }
            }
        },

        computed: {
            cItems() {
                this.setIds(this.items);

                return this.items;
            }
        }
    }
</script>

<style lang="scss">
    .f-navigation {
        display: inline-block;

        nav {
            ul {
                text-align: right;
                li {
                    display: inline-block;
                    margin-left: 4px;

                    @include links() {
                        color: $secondary-color-lighter;
                        font-weight: bold;
                        letter-spacing: normal;
                        display: inline-block;
                        padding: 16px 20px;
                        text-decoration: none;
                        transition: all $transition-length ease;
                        border-radius: $border-radius;

                        &.router-link-exact-active, &:hover {
                            color: #fff;
                            text-decoration: none;
                        }
                    }
                }
            }
        }
    }

    @include media-max(900px) {
        .f-navigation {
            nav {
                ul {
                    li {
                        @include links() {
                            font-size: 0.9em;
                            padding-left: 10px;
                            padding-right: 10px;
                        }
                    }
                }
            }
        }
    }

    @include media-max($bp-menu) {
        .f-navigation {
            nav {
                ul {
                    li {
                        display: block;

                        @include links() {
                            font-size: 1.5em;
                            padding-left: 20px;
                            padding-right: 20px;
                        }
                    }
                }
            }
        }
    }
</style>
