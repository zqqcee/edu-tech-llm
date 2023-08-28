<template>
    <v-container class="search-bar">
        <v-row align="center">
            <v-col cols="6">
                <v-text-field hide-details="auto" class="topic-input" label="作文主题"></v-text-field>
            </v-col>
            <v-col cols="4">
                <v-select class="md-2" label="请选择教师级别" hide-details="auto"
                    :items="['专家', '高级', '中级', '初级', '同龄']"></v-select>
            </v-col>

            <v-col cols="2">
                <v-btn variant="tonal" class="rounded-lg" height="3rem" width="11rem" color="black">
                    开始生成
                </v-btn>
            </v-col>
        </v-row>
    </v-container>
</template>

<style scoped>
.topic-input {
    width: 100%;
}

.search-bar {
    max-width: 100%;
    display: flex;
}
</style>