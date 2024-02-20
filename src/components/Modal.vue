<template>
    <div id="modal__container" :class="{invisible: props.start}">
        <div id="modal-inner__container">
            <div id="panel">
                <div id="user-panel__container">
                    <span v-if="props.retry">
                        <button @click="$emit('play')">Play Again</button>
                    </span>
                    <span v-else>
                        <button @click="$emit('play')">Play Game</button>
                    </span>
                    
                </div>
                <div id="character__container">
                    <span id="word-bubble">
                        <p>{{ talk }}</p>
                    </span>
                    <img src="/viking.svg" alt="viking">
                </div>
            </div>
        </div>
    </div>
</template> 

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps({
    start: {
        type: Boolean,
        required: true
    },
    retry: {
        type: Boolean,
        required: false
    },
    input: {
        type: String,
        required: true
    }
})

const emit = defineEmits(['play'])

const talk = ref(props.input)

</script>

<style scoped>
#modal__container {
    display: block;
    visibility: visible;
    position: fixed;
    background-color: rgba(0, 0, 0, 0.39);
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    transition: 0.6s;
}
.invisible {
    display: none !important;
    visibility: hidden !important;
}

#modal-inner__container {
    position: absolute;
    width: 100%;
    max-width: 920px;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.301);
}
#panel {
    display: flex;
    width: 100%;
    background-color: #e6e9c6;
}
#user-panel__container {
    position: relative;
    width: 66%;
}

#user-panel__container button {
    position: absolute;
    top: 60%;
    right: 0;
    transform: translate(-50%, -50%);
    border: none;
    background-color: brown;
    color: #e6e9c6;
    border-radius: 2px;
    padding: 16px 28px;
    font-family: "Poppins";
    text-transform: uppercase;
    letter-spacing: 1px;
    font-size: 2.2rem;
    font-weight: bold;
    cursor: pointer;
}
#user-panel__container button:hover {
    opacity: .8;
}
#character__container {
    position: relative;
    max-width: 350px;
}
#word-bubble {
    position: absolute;
    width: 290px;
    height: 225px;
    border-radius: 50%;
    background-color: white;
    left: -120%;
    top: -25%;
    transition-delay: 0.3s;
    transition: 0.6s;
    text-align: center;
    z-index: 2;
    padding: 0 45px;
}
#word-bubble p {
    position: absolute;
    width: 100%;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: "Poppins";
    font-weight: bold;
    color: brown;
    line-height: 1.2;
    font-size: 1.9rem;
    z-index: 3;
    text-transform: uppercase;
}
#word-bubble::after {
    content: "";
    position: absolute;
    background-color: white;
    width: 40px;
    height: 40px;
    right: 20px;
    bottom: 30px;
    z-index: 1;
}
#character__container img {
    transform: rotate(22deg);
    object-fit: contain;
    object-position: center;
    width: 240px;
    height: auto;
    margin: 0 50px 35px 0;
}

</style>