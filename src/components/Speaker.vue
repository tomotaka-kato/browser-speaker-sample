<template>
    <div>
        {{ message }}
    </div>
</template>

<script lang="ts">
    import { Component, Prop, Vue } from 'vue-property-decorator';

    @Component
    export default class Speaker extends Vue{

        errorMsg: string = "aaa";
        msg = new SpeechSynthesisUtterance();

        message: string = "test"
        volume = 1.0; // 音量 min 0 ~ max 1
        rate = 1.0; // 速度 min 0 ~ max 10
        pitch = 1.0; // 音程 min 0 ~ max 2

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
                this.msg.text = this.message

                // console.log(`rate: ${this.rate}`)
                // console.log(`pitch: ${this.pitch}`)
                // console.log("")

                speechSynthesis.speak(this.msg)
                this.errorMsg = "";
            } catch(e) {
                console.error(e)
                this.errorMsg = e.toString()
            }
        }
    }
</script>


<style scoped lang="less">
</style>


