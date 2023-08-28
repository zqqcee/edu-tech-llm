<script setup>
import { ref } from 'vue';
definePageMeta({
    layout: "vuetify-app",
});
const articleSubTitle = ref("假设你是一名小学生，请你以“我的梦想之旅”为题，写一篇400字的作文，描述你梦想中的一次特别的旅行经历。你可以选择任何地方，虚构或真实，描述你在那里看到、听到和体验到的事情，以及这次旅行对你的影响。");

const articleEditableText = ref("asdfafadsfadsf");
let textReadonly = ref(true);

const toggleEditState = () => {
    textReadonly.value = !textReadonly.value;
}
const dialog = ref(false);
const handleTabKey = (event) => {
    if (event.key === 'Tab') {
        event.preventDefault();
        const textarea = event.target;
        const start = textarea.selectionStart;
        const end = textarea.selectionEnd;
        const indent = '  '; // 可以根据需要调整缩进的空格或制表符数量
        const indentText = indent.repeat(2); // 可以根据需要调整每次缩进的数量

        // 在选中文本的范围内插入缩进
        textarea.value =
            textarea.value.substring(0, start) +
            indentText +
            textarea.value.substring(end);
        // 调整光标位置
        textarea.selectionStart = textarea.selectionEnd = start + indent.length;
    }
}

</script>

<style>
.article-card {
    position: relative;
}

.multiline-subtitle {
    white-space: normal;
}

.multiline-content {
    overflow-y: scroll;
    white-space: pre-wrap;
}

.close-dialog-btn {
    position: fixed;
    bottom: 10px;
}

.paragraph-panel {
    padding-top: 10px;
}
</style>

<template>
    <div class=" h-screen bg-gray-00">
        <Header />
        <SearchBar />

        <div class="w-full h-full bg-blue d-flex justify-space-evenly article-card">
            <div class="ma-2">
                <v-card width="800" height="650">
                    <v-card-item>
                        <div class="text-h5">我的梦想之旅</div>
                        <v-card-subtitle class="multiline-subtitle">
                            {{ articleSubTitle }}
                        </v-card-subtitle>
                        <v-textarea clearable counter no-resize rows="19" class="multiline-content"
                            v-model="articleEditableText" :readonly="textReadonly" @keydown.tab.prevent="handleTabKey"
                            label="作文正文">
                        </v-textarea>
                        <div class="d-flex justify-space-around">
                            <v-btn color="indigo-darken-3" @click="toggleEditState" size="large" variant="flat"
                                class="text-none mb-4 edit-btn">
                                {{ textReadonly ? '编辑作文' : '保存作文' }}
                                <!-- <v-icon icon="fa:fas fa-edit"></v-icon> -->
                            </v-btn>

                            <div>
                                <v-dialog v-model="dialog" width="w-full" fullscreen :scrim="false">
                                    <template v-slot:activator="{ props }">
                                        <v-btn v-bind="props" class="text-none mb-4" color="indigo-darken-3" size="large"
                                            variant="flat">
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
                                        <v-btn class="close-dialog-btn" block color="gery" size="large"
                                            @click="dialog = false">关闭</v-btn>

                                    </v-card>

                                </v-dialog>
                            </div>

                        </div>





                    </v-card-item>
                </v-card>
            </div>

            <div class="ma-2">
                <v-card width="600" height="650">
                    <v-card-item>
                        <v-card-title>This is a title</v-card-title>

                        <v-card-subtitle>This is a subtitle</v-card-subtitle>
                    </v-card-item>

                    <v-card-text>
                        This is content
                    </v-card-text>
                </v-card>
            </div>
        </div>
    </div>
</template>