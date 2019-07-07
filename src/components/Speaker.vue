<template>
    <v-app id="inspire">
        <v-container fluid grid-list-md>
            <v-layout row wrap>
                <v-flex class="text-xs-center" xs12 md5>
                    <v-text-field
                        clearable=true
                        v-model="message"
                        hint="発話させたい文言を入力してください"
                        >
                    </v-text-field>
                    <v-btn fab color=primary @click="speak">
                        <v-icon dark>volume_up</v-icon>
                    </v-btn>
                </v-flex>

                <v-flex xs12 md5 >
                       <v-slider
                           label="音量"
                           v-model="volume"
                           min=0
                           max=1
                           step=0.1
                       >
                       </v-slider> 
                        <!-- 
                            速度の最大は10とAPI使用には書いてあるが、
                            試した感じ3.6を越えると正常に動かなかったため、
                            3.5を最大とする。
                        -->
                       <v-slider
                           label="速度"
                           v-model="rate"
                           min=0.1
                           max=3.5
                           step=0.1
                           :value="rate"
                       >
                       </v-slider> 
                       <v-slider
                           label="音程"
                           v-model="pitch"
                           min=0
                           max=2
                           step=0.1
                           :value="pitch"
                       >
                       </v-slider> 
                </v-flex>
            </v-layout>
        </v-container>
    </v-app>
</template>

<script lang="ts">
    import { Component, Prop, Vue } from 'vue-property-decorator';

    @Component
    export default class Speaker extends Vue{
        msg = new SpeechSynthesisUtterance();

        message: string = ""
        volume = 1.0; // 音量 min 0 ~ max 1
        rate = 1.0; // 速度 min 0 ~ max 10
        pitch = 1.0; // 音程 min 0 ~ max 2

        speak() {
            if(!this.msg.voice){
                const voices = speechSynthesis.getVoices();
                const voice = voices.find(_ => _.lang === 'ja-JP')
                if(voice)
                    this.msg.voice = voice;
            }
            this.msg.volume = this.volume;
            this.msg.rate = this.rate;
            this.msg.pitch = this.pitch
            this.msg.lang = 'ja-JP'
            this.msg.text = this.message

            console.log(this.msg)

            speechSynthesis.speak(this.msg)
        }
    }
</script>


<style scoped lang="less">
</style>


