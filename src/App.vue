<template>
    <section class="section">
        <div class="container">
            <div class="cen">
                <div class="title">T R I V I A</div>
                <!-- quest -->
                <div class="card">
                    <!-- question -->
                    <div class="card-head has-text-centered p-3">
                        <div class="subtitle is-4 p-6 qus ">
                            {{ db[Q].question }}
                        </div>
                    </div>
                    <!-- option -->
                    <div class="card-body p-5">
                        <!-- 1 -->
                        <div class="box" v-for="opt in opts" :key="opts" @click="sel">
                            <span class="icon-text">
                                <span class="icon is-medium">
                                    <span class="iconify" data-icon="mdi:alpha-a-box" data-inline="false"></span>
                                </span>
                                <span class="subtitle ml-3 opt1"> {{ opt }} </span>
                            </span>
                        </div>
                    </div>
                    <!-- submit -->
                    <div class="card-footer">
                        <div class="card-footer-item">
                            <!-- <div class="button btn mb-3 is-medium btn_sub">S U B M I T</div> -->
                            <!-- <div class="button btn mb-3 is-medium btn_nxt">N E X T</div> -->
                            <div class="button is-primary" @click="nxt">nxt</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
    name: 'App',
    components: {},
    data() {
        return {
            pt: 0,
            Q: 0,
            db: [],
            opts: []
        }
    },
    methods: {
      sel(e){
        e.classList.toggle("sel")
        console.log(e)
      },
        nxt() {
            console.log("next")
            let shuffleArray = (array) => {
                console.log(array)
                for (var i = array.length - 1; i > 0; i--) {
                    var j = Math.floor(Math.random() * (i + 1));
                    var temp = array[i];
                    array[i] = array[j];
                    array[j] = temp;
                }
                return array
            }
            let q = this.Q
            // question update
            this.opts = shuffleArray([this.db[q].incorrect_answers[0],this.db[q].incorrect_answers[1],this.db[q].incorrect_answers[2],this.db[q].correct_answer])
            // option update
            this.Q++
        }
    }
    ,
    async created() {
        let api = "https://opentdb.com/api.php?amount=10&type=multiple"
        let raw = await (fetch(api))
        let data = await (raw.json())
        this.db = await (data.results)
        this.opts = [this.db[0].incorrect_answers[0],this.db[0].incorrect_answers[1],this.db[0].incorrect_answers[2],this.db[0].correct_answer]
    }
}
</script>
<style>
#app {}
</style>