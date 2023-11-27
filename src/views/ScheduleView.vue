<script setup>
import Calender from '../components/Calender.vue'
import '../assets/schedule.css'
</script>

<template>
    <div id="top">
        <button v-if="(m==='01') && (y==='2022')" class="btn arrow unupdated" id="left_btn" onclick="alert('첫 번째 페이지입니다.')"><span>◀</span></button>
        <button v-else-if="(m==='01')" class="btn arrow" id="left_btn" @click="setmonth(String(parseInt(y)-1),'12')"><span>◀</span></button>
        <button v-else class="btn arrow" id="left_btn" @click="setmonth(y,String(parseInt(m)-1).padStart(2,'0'))"><span>◀</span></button>
        <div id="title" style="display:inline-block">
            <button id="btn_drop">
                <div class="btn" @click="setScroll()">
                    <span id="selectedYear">{{ y }}. {{ m }}</span>
                    <!-- <span id="selectedMonth">{{ m }}</span> -->
                </div>
                <div class="drop">
                    <div class="drop_box" id="year_box">
                        <p v-for="i in years" :id="i" @click="setyear(i)"><span>{{ i }}</span></p>
                    </div>
                    <div class="drop_box" id="month_box">
                        <p v-for="i in 12" :key="i" :id="String(i).padStart(2,'0')" @click="setmonth(year,String(i).padStart(2,'0'))"><span>{{ String(i).padStart(2,'0') }}</span></p>
                    </div>
                </div>
            </button>
        </div>
        <div style="display:inline-block">
            <button v-if="(m==='01') && (y==='2022')" class="btn arrow unupdated" id="left_btn_h" onclick="alert('첫 번째 페이지입니다.')"><span>◀</span></button>
            <button v-else-if="(m==='01')" class="btn arrow" id="left_btn_h" @click="setmonth(String(parseInt(y)-1),'12')"><span>◀</span></button>
            <button v-else class="btn arrow" id="left_btn_h" @click="setmonth(y,String(parseInt(m)-1).padStart(2,'0'))"><span>◀</span></button>
            <button v-if="(m==='12') && (y==='2023')" class="btn arrow unupdated" onclick="alert('업데이트 예정')"><span>▶</span></button>
            <button v-else-if="(m==='12')" class="btn arrow" @click="setmonth(String(parseInt(y)+1),'01')"><span>▶</span></button>
            <button v-else class="btn arrow" @click="setmonth(y,String(parseInt(m)+1).padStart(2,'0'))"><span>▶</span></button>
        </div>
    </div>
    <div id="table">
    <Calender :edYM="[y,m]" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            years: ['2022','2023'],
            year: '0',
            y: '0',
            m: '0'
        }
    },
    mounted() {
        var dt = new Date();
        this.y = String(dt.getFullYear());
        this.m = String(dt.getMonth()+1).padStart(2,'0');

        this.setmonth(this.y,this.m)
        this.setyear(this.y)
        //var y = '';
        //var m = '';
        
        // var ingYear = this.$route.params.ingYear;
        // var ingMonth = this.$route.params.ingMonth;
        // try {
        //     if (this.years.includes(ingYear)) {
        //         this.y = ingYear;
        //         try {
        //             var k = parseInt(ingMonth);
        //             if ((0 < k) && (k < 13)) {
        //                 this.m = String(k).padStart(2,'0');
        //             } else {
        //                 this.m = '01'
        //             }
        //         } catch(e) {
        //             this.m = '01'
        //         }
        //     } else {
        //         var dt = new Date();
        //         this.y = String(dt.getFullYear());
        //         this.m = String(dt.getMonth()+1).padStart(2,'0');
        //     }
        // } catch(e) {
        //     var dt = new Date();
        //     this.y = String(dt.getFullYear());
        //     this.m = String(dt.getMonth()+1).padStart(2,'0');
        // } finally {
        //     //this.loadSch(this.y,this.m)
        //     this.setmonth(this.y,this.m)
        //     this.year = this.y
        // }
    },
    methods: {
        setyear(yyyy) {
            $('#year_box > .selected').removeClass('selected')
            $('#'+yyyy).addClass('selected')
            this.year = yyyy
        },
        loadSch(yyyy,mm) {
            console.log(yyyy+mm)
            if (yyyy=='2022' && parseInt(mm) < 5) {
                //loadSch('2022','05')
                alert('존재하지 않는 페이지입니다.')
            } else {
                // $.ajax({
                //     url: './txt/'+yyyy+'/'+mm+'.txt',
                //     dataType: 'text'
                // }).done(setCalender);
                //$('#selectedMonth').text(mm)
                //$('#selectedYear').text(yyyy+'.')
                $('#month_box > .selected').removeClass('selected')
                $('#'+mm).addClass('selected')
                //this.setyear(yyyy);
                //setButton(yyyy,mm);
            }
        },
        setScroll() {
            $('.drop').width($('#btn_drop').width()+25);
            $("#month_box").scrollTop( $("#month_box > .selected").offset().top - $("#01").offset().top - 75 + $("#01").height()/2 );
            $("#year_box").scrollTop( $("#year_box > .selected").offset().top - $("#2022").offset().top );
        },
        setmonth(a,b) {
            this.y = a
            this.m = b
            $('#month_box > .selected').removeClass('selected')
            $('#'+b).addClass('selected')
        }
    }
}
</script>