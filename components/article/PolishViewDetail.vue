<script setup>
import { ref } from 'vue';
import Keypoint from './Keypoint.vue';
import Poetry from './Poetry.vue';
import Idiom from './Idiom.vue';
import Quotes from './Quotes.vue';
import TopicAnalysis from './TopicAnalysis.vue';
const polishSelection = ref(1);//control the click style of the nav bar
const polishView = ref('keypoint');//control the polish view to display

const polishViewMapper = {
    'keypoint': Keypoint,
    'idiom': Idiom,
    'poetry': Poetry,
    'quotes': Quotes,
    'topicAnalysis': TopicAnalysis,
};

const changePolishView = (e) => {
    polishView.value = e;
}

</script>

<style></style>

<template>
    <v-card width="600" height="650">
        <v-card-item>
            <v-card-title>
                <v-layout class="overflow-visible" style="height: 56px;">
                    <v-bottom-navigation v-model="polishSelection" color="teal" grow>
                        <v-btn @click="changePolishView('keypoint')">
                            写作要点
                        </v-btn>
                        <v-btn @click="changePolishView('idiom')">
                            相关成语
                        </v-btn>
                        <v-btn @click="changePolishView('poetry')">
                            古典诗词
                        </v-btn>
                        <v-btn @click="changePolishView('topicAnalysis')">
                            主题赏析
                        </v-btn>
                        <v-btn @click="changePolishView('quotes')">
                            名人名言
                        </v-btn>
                    </v-bottom-navigation>
                </v-layout>
            </v-card-title>
        </v-card-item>

        <v-card-text>
            <component :is="polishViewMapper[polishView]">
            </component>
        </v-card-text>
    </v-card>
</template>