<template>
    <div class="card" :class="{disabled: isDisabled}">
        <div class="card-inner" :class="{'is-flipped': isFlipped}" @click="onToggleFlipCard()">
            <div class="card-face card-face--front">
                <div class="card__content" ></div>
            </div>
            <div class="card-face card-face--back">
                <div class="card__content" :style="{ backgroundImage: `url(${require('@/assets/' +imgBackFaceUrl)})`}"></div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        card : {
            type : [Array, String, Number, Object],
        }, 
        imgBackFaceUrl: {
            type: String,
            required: true,
        }
    },
    data() {
        return {
            isFlipped:false,
            isDisabled:false,
        }
    },
    methods: {
        onToggleFlipCard(){
            if (this.isDisabled) return false;
            this.isFlipped= !this.isFlipped;
            if (this.isFlipped) this.$emit("onFlip", this.card);
        },
        onFlipBackCard(){
            this.isFlipped = false;
        },
        onDisableBackCard(){
            this.isDisabled = true;
        }
    },
}
</script>
<style lang="css" scoped>
    .card {
        display: inline-block;
        margin-right: 1rem;
        margin-bottom: 1rem;
        width: 90px;
        height: 120px;
    }
    .card-inner {
        width: 100%;
        height:100%;
        transition: transform 1s;
        transform-style: preserve-3d;
        cursor: pointer;
        position: relative;
    }
    .card-inner.is-flipped{
        transform: rotateY(-180deg);
    }
    .card.disable .card-inner{
        cursor: default;
    }
    .card-face {
        position: absolute;
        width: 100%;
        height:100%;
        backface-visibility: hidden;
        overflow: hidden;
        border-radius: 1rem ;
        padding: 1rem;
        box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
    }
    .card-face--front .card__content {
        background: url("../assets/images/icon_back.png") no-repeat center center;
        background-size: 40px 40px;
        height: 100%;
        width: 100%;
    }
    .card-face--back{
        background-color: var(--light);
        transform: rotateY(-180deg);
    }
    .card-face--back .card__content {
        background-size: contain;
        background-position: center center;
        background-repeat: no-repeat;
        height: 100%;
        width: 100%;
    }
</style>