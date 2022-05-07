<template>
    <v-app>
        <v-main>
            <div>{{ selecteds }}</div>
            <v-container>
                <v-select
                    :items="users"
                    item-text="name"
                    v-model="selecteds"
                    label="Selecione os usuários"
                    rounded
                    multiple>
                    <template v-slot:prepend-item>
                        <v-list-item ripple @mousedown.prevent @click="toggle">
                            <v-list-item-action>
                                <v-icon
                                    :color="
                                        selecteds.length > 0 ? 'indigo darken-4' : ''
                                    ">
                                    {{ icon }}
                                </v-icon>
                            </v-list-item-action>

                            <v-list-item-content>
                                <v-list-item-title> Selecionar todos </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                    </template>
                </v-select>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
    export default {
        name: 'App',
        data() {
            return {
                users: [
                    { name: 'Tiago', age: 22 },
                    { name: 'Cintia', age: 24 },
                    { name: 'Liz', age: 23 },
                    { name: 'Everton', age: 26 },
                    { name: 'Eline', age: 20 }
                ],
                selecteds: []
            };
        },
        computed: {
            likesAllUser() {
                return this.selecteds.length === this.users.length;
            },
            likesSomeUser() {
                return this.selecteds.length > 0 && !this.likesAllUser;
            },
            icon() {
                if (this.likesAllUser) return 'mdi-close-box';

                if (this.likesSomeUser) return 'mdi-minus-box';

                return 'mdi-checkbox-blank-outline';
            }
        },
        methods: {
            toggle() {
                this.$nextTick(() => {
                    if (this.likesAllUser) {
                        this.selecteds = [];
                    } else {
                        this.selecteds = this.users.slice();
                    }
                });
            }
        }
    };
</script>
