<template>
    <div>
        <div class="hero is-fullheight-with-navbar">
            <div class="hero-body">
                <div class="container">

                    <div class="columns">
                        <div class="column is-6 is-offset-3">
                            <div class="w-box">
                
                                <div class="instruction">
                                    <p class="title is-5">COMPREHENSIVE EXAM – GENERAL DIRECTIONS</p>
                                    <ol>
                                        <li>You will take two different sets of tests for your exam – one for the Professional Education test and another for the Majorship test.</li>
                                        <li>Each exam shall be comprised of 100 test items randomly generated by our system.</li>
                                        <li>Each test item has its own timer. The timer shall depend on the length and difficulty of the test item. The timer is placed at the bottom right corner of your screen(bottom for mobile).</li>
                                        <li>Avoid refreshing your browser. It may cause you to start your exam all over again.</li>
                                        <li>After answering each test item, click submit.</li>
                                        <li>CHEATING IS STRICTLY PROHIBITED.</li>
                                    </ol>

                                </div>

                                <div class="buttons mt-5 is-centered">
                                    <a href="/section" class="button is-primary is-outlined is-rounded">
                                        NEXT &nbsp;
                                        <b-icon icon="chevron-right"></b-icon>
                                    </a>
                                </div>

                               <b-loading :is-full-page="false" v-model="isLoading" :can-cancel="true"></b-loading>
                            </div>
                        </div>
                    </div>




                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    props: ['isNotScheduled', 'alreadyVisitedSection', 'isExist'],

    data() {
        return {


            isLoading: false,


        }
    },

    methods: {
    
   
    },


}
</script>

<style scoped>



    /*.instruction{*/
    /*    display: flex;*/
    /*    justify-content: center;*/
    /*    text-align: justify;*/
    /*    font-size: 20px;*/
    /*    font-weight: bold;*/
    /*    margin: 15px;*/
    /*    border-bottom: 1px solid darkgreen;*/
    /*    padding: 15px;*/
    /*}*/

    .w-box{
        border-top: 5px solid green;
        background: white;
        border-radius: 10px;
        padding: 15px 25px;
        box-shadow:
            0 2.8px 2.2px rgba(0, 0, 0, 0.034),
            0 6.7px 5.3px rgba(0, 0, 0, 0.048),
            0 12.5px 10px rgba(0, 0, 0, 0.06),
            0 22.3px 17.9px rgba(0, 0, 0, 0.072),
            0 41.8px 33.4px rgba(0, 0, 0, 0.086),
            0 100px 80px rgba(0, 0, 0, 0.12)
            ;
    }

    .horizontal-word {
        width: 100%;
        text-align: center;
        border-bottom: 1px solid darkgreen;
        line-height: 0.1em;
        margin: 10px 0 20px;
        font-weight: bold;
    }

    .horizontal-word > span {
        background: #fff;
        padding: 0 10px;
        color: darkgreen;
    }


    .instruction{
        margin-top: 30px;
    }

    .instruction ol{
       padding: 0px 20px;
    }

    .instruction > ol > li{
        padding: 0px 10px;
    }

</style>
