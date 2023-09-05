<script setup>
import { ref } from 'vue';
const articleSubTitle = ref("假设你是一名小学生，请你以“我的梦想之旅”为题，写一篇400字的作文，描述你梦想中的一次特别的旅行经历。你可以选择任何地方，虚构或真实，描述你在那里看到、听到和体验到的事情，以及这次旅行对你的影响。");

const articleEditableText = ref("asdfafadsfadsf");
let textReadonly = ref(true);

const toggleEditState = () => {
    textReadonly.value = !textReadonly.value;
}
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

const imgFile = ref(null);
const onFileChange = (e) => {
    imgFile.value = e.target.files;

}
const uploadFile = async () => {
    if (!imgFile.value) {
        return;
    }
    const { data: count } = await useFetch('http://localhost:9001/api/chat/get_texts_ocr');
    console.log(count);
    console.log(1);
}



</script>

<style>
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

.test {
    width: 10%;
}
</style>
<template>
    <v-card width="800" height="650">
        <v-card-item>
            <div class="text-h5">我的梦想之旅</div>
            <v-card-subtitle class="multiline-subtitle">
                {{ articleSubTitle }}
            </v-card-subtitle>
            <v-textarea clearable counter no-resize rows="19" class="multiline-content" v-model="articleEditableText"
                :readonly="textReadonly" @keydown.tab.prevent="handleTabKey" label="作文正文">
            </v-textarea>
            <div class="d-flex justify-space-around">
                <v-file-input show-size counter multiple label="上传文件" @change="onFileChange"></v-file-input>
                <v-btn color="indigo-darken-3" size="large" variant="flat" @click="uploadFile"
                    class="text-none mb-4 edit-btn">
                    上传文件
                </v-btn>
                <v-btn color="indigo-darken-3" @click="toggleEditState" size="large" variant="flat"
                    class="text-none mb-4 edit-btn">
                    {{ textReadonly ? '编辑作文' : '保存作文' }}
                </v-btn>

                <ArticleDialog />

            </div>

        </v-card-item>
    </v-card>
</template>