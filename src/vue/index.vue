<template>
    <div class="vue-pithy-rate">
        <div>
            <i
                v-for="i in 5"
                :key="i"
                :style="{color: starColor, fontSize: starSize + 'px'}"
                class="iconfont"
                :class="[getClass(i), disabled && i === Math.floor(score) + 1 ? 'icon-star-half' : '']"
                @mouseenter="disabled ? '' : (currentScore = i)"
                @mouseleave="disabled ? '' : (currentScore = '')"
                @click="disabled ? '' : setScore(i)"
            />
        </div>
        <span
            v-if="showScore"
            class="score-text"
            :style="{color: scoreColor}"
        >{{ currentScore || score }}分</span>
    </div>
</template>
<script>
export default {
    name: 'VuePithyRate',
    props: {
        score: {
            type: Number,
            default: 0
            // required: true
        },
        disabled: {
            type: Boolean,
            default: false
        },
        showScore: {
            type: Boolean,
            default: false
        },
        starColor: {
            type: String,
            default: '#000'
        },
        starSize: {
            type: Number,
            default: 16
        },
        scoreColor: {
            type: String,
            default: '#000'
        }
    },
    data() {
        return {
            currentScore: ''
        };
    },
    methods: {
        getClass(i) {
            // console.log(i);
            if (this.currentScore === '') {
                return i <= this.score ? 'icon-star-fill' : 'icon-star';
            } else {
                return i <= this.currentScore ? 'icon-star-fill' : 'icon-star';
            }
        },
        setScore(i) {
            this.$emit('handleUpdateScore', i); // 使用`.sync`修饰符，对score 进行“双向绑定
        }
    }
};
</script>
<style lang="scss" scoped>
@font-face {
    font-family: iconfont; /* Project id 3941812 */
    src: url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.woff2?t=1686215479016') format('woff2'),
        url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.woff?t=1686215479016') format('woff'),
        url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.ttf?t=1686215479016') format('truetype'),
        url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.svg?t=1686215479016#iconfont') format('svg');
}
.iconfont {
    font-family: iconfont !important;
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-style: normal;
}
.icon-star:before {
    content: '\e659';
}
.icon-star-half:before {
    content: '\e6b6';
}
.icon-star-fill:before {
    content: '\e86a';
}
.vue-pithy-rate {
    display: flex;
    align-items: center;
    .score-text {
        margin-left: 3px;
        font-size: 14px;
    }
}
</style>
