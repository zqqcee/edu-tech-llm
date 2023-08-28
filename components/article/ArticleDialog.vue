<script setup>

const dialog = ref(false);
</script>
<template>
    <div>
        <v-dialog v-model="dialog" width="w-full" fullscreen :scrim="false">
            <template v-slot:activator="{ props }">
                <v-btn v-bind="props" class="text-none mb-4" color="indigo-darken-3" size="large" variant="flat">
                    逐段解析
                </v-btn>
            </template>

            <v-card class="d-flex align-space-around">
                <div class="paragraph-panel">
                    <v-expansion-panels>
                        <v-expansion-panel title="第一自然段"
                            text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus! Eaque cupiditate minima">
                        </v-expansion-panel>
                    </v-expansion-panels>
                </div>

                <div class="paragraph-panel">
                    <v-expansion-panels>
                        <v-expansion-panel title="第二自然段"
                            text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus! Eaque cupiditate minima">
                        </v-expansion-panel>
                    </v-expansion-panels>
                </div>


                <div class="paragraph-panel">
                    <v-expansion-panels>
                        <v-expansion-panel title="第三自然段"
                            text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus! Eaque cupiditate minima">
                        </v-expansion-panel>
                    </v-expansion-panels>
                </div>

                <div class="paragraph-panel">
                    <v-expansion-panels>
                        <v-expansion-panel title="第四自然段"
                            text="Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi, ratione debitis quis est labore voluptatibus! Eaque cupiditate minima">
                        </v-expansion-panel>
                    </v-expansion-panels>
                </div>
                <v-btn class="close-dialog-btn" block color="gery" size="large" @click="dialog = false">关闭</v-btn>

            </v-card>

        </v-dialog>
    </div>
</template>