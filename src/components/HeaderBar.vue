<script setup>
import { RouterLink } from "vue-router"
</script>

<template>
    <!-- 캘린더로 가는 버튼 필요 -->
    <header>
        <div>
            <RouterLink to="/"><img id="home" src="../assets/home.svg"></RouterLink>
        </div>
        <div>
            <button class="btn main" id="btn_simple" @click="simple()">간단하게 보기</button>
            <button class="btn main" id="btn_darklight" @click="darklight()" style="width: 100px">라이트 모드</button>
        </div>
    </header>
</template>

<script>
export default {
    methods: {
        simple() {
            var isSimple = ((localStorage.getItem('isSimple') || 'false') === 'true')
            if (isSimple){
                $('body').removeClass('simple')
                $('#btn_simple').text('간단하게 보기')
                isSimple=false
            }
            else {
                $('body').addClass('simple')
                $('#btn_simple').text('자세하게 보기')
                isSimple=true
            }
            localStorage.setItem('isSimple',isSimple)
        },
        darklight() {
            var isLight = ((localStorage.getItem('isLight') || 'false') === 'true')
            if (isLight){
                $('body').removeClass('light').addClass('dark');
                $('#btn_darklight').text('라이트 모드')
                isLight=false
            }
            else {
                $('body').removeClass('dark').addClass('light');
                $('#btn_darklight').text('다크 모드')
                isLight=true
            }
            localStorage.setItem('isLight',isLight)
        }
    }
}
</script>