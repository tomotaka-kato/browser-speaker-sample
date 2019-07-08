<template>
    <v-layout row wrap justify-space-around >
        <v-flex class="text-xs-center" xs10 md5>
            <v-text-field
                clearable
                v-model="message"
                placeholder="発話させたい文言を入力してください"
                >
            </v-text-field>
                <v-btn fab color=primary @click="speak">
                    <v-icon dark>volume_up</v-icon>
                </v-btn>
        </v-flex>

        <v-flex xs10 md5 >
            <v-slider
                label="音量"
                v-model="volume"
                min=0
                max=1
                step=0.1
                >
            </v-slider> 
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

            <v-flex xs10 md11 v-if="errorMsg.length > 0" >
                <v-card>
                    <v-card-title primary-title>
                        <div>
                            <h3 class="headline mb-0">エラーメッセージ</h3>
                            <div> {{ errorMsg }} </div>
                        </div>
                    </v-card-title>
                </v-card>
            </v-flex>



    </v-layout>
</template>

<script lang="ts">
    import { Component, Prop, Vue } from 'vue-property-decorator';

    @Component
    export default class Speaker extends Vue{

        errorMsg: string = "aaa";
        msg = new SpeechSynthesisUtterance();

        message: string = "test"
        volume = 1.0;
        rate = 1.0;
        pitch = 1.0;

        speak() {
            try {
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
                this.message
                    ? this.msg.text = this.message
                    : this.msg.text = "サンプルメッセージです"

                console.log(`rate: ${this.rate}`)
                console.log(`pitch: ${this.pitch}`)
                console.log("")

                speechSynthesis.speak(this.msg)
                this.errorMsg = "";
            } catch(e) {
                console.error(e)
                this.errorMsg = e.toString()
            }
        }
    }
</script>

