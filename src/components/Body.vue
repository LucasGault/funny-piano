<template>
    <div class="MainBody">
        <h1 class="title">The emoji piano</h1>
        <div class="emoji">
            <img v-if="emoji && !current" :src="emoji" alt="Random Emoji">
            <img v-if="emoji2 && current" :src="emoji2" alt="Random Emoji">
        </div>
        <div class="piano">
            <div class="toucheB C touche"></div>
            <div class="toucheN Cd touche"></div>
            <div class="toucheB D touche"></div>
            <div class="toucheN Dd touche"></div>
            <div class="toucheB E touche"></div>
            <div class="toucheB F touche"></div>
            <div class="toucheN Fd touche"></div>
            <div class="toucheB G touche"></div>
            <div class="toucheN Gd touche"></div>
            <div class="toucheB A touche"></div>
            <div class="toucheN Ad touche"></div>
            <div class="toucheB B touche"></div>
        </div>
        <div class="container_notes">
            <p class="notes" ref="do">DO</p>
            <p class="notes" ref="re">RÉ</p>
            <p class="notes" ref="mi">MI</p>
            <p class="notes" ref="fa">FA</p>
            <p class="notes" ref="sol">SOL</p>
            <p class="notes" ref="la">LA</p>
            <p class="notes" ref="si">SI</p>
        </div>
    </div>
</template>

<script lang="js">
    import { GiphyFetch } from '@giphy/js-fetch-api'
    export default {
        name: 'Body',
        data() {
            return {
                emoji: null,
                emoji2: null,
                rand: null,
                rand2: null,
                gf: null,
                tab: [],
                current: null
            }
        },
        mounted() {
            this.gf = new GiphyFetch('33cExsArNV2S2pW9p5y8R5MVALVXGKz7')
            const emoji = async () => {
                try {
                    const result = await this.gf.emoji({
                        limit: 97
                    })
                    result.data.forEach(el => {
                        this.tab.push(el.images.fixed_width.webp)
                    });
                } catch (error) {
                    console.error(`emoji`, error)
                }
            }
            emoji()
            this.addListeners()
        },
        beforeDestroy() {
            this.removeListeners()
        },
        methods: {
            addListeners() {
                const touche = document.querySelectorAll('.touche')
                touche.forEach(el => {
                    el.addEventListener('click', this.onClick)
                });
                document.addEventListener('keydown', this.onKeyDown)
                document.addEventListener('keyup', this.onKeyUp)
            },
            removeListeners() {
                const touche = document.querySelectorAll('.touche')
                touche.forEach(el => {
                    el.removeEventListener('click', this.onClick)
                });
                document.removeEventListener('keydown', this.onKeyDown)
                document.removeEventListener('keyup', this.onKeyUp)
            },
            onClick(ev) {
                this.rand = Math.floor(Math.random() * 97)
                this.rand2 = Math.floor(Math.random() * 97)
                this.ramdomEmoji()
                this.resetClavier()
                switch (ev.target.classList[1]) {
                    case "C":
                        this.addSon('C')
                        this.$refs.do.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "D":
                        this.addSon('D')
                        this.$refs.re.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "E":
                        this.addSon('E')
                        this.$refs.mi.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "F":
                        this.addSon('F')
                        this.$refs.fa.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "G":
                        this.addSon('G')
                        this.$refs.sol.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "A":
                        this.addSon('A')
                        this.$refs.la.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "B":
                        this.addSon('B')
                        this.$refs.si.style.opacity = 1
                        ev.target.classList.toggle("activeB")
                        break;
                    case "Cd":
                        this.addSon('C%23')
                        ev.target.classList.toggle("activeN")
                        break;
                    case "Dd":
                        this.addSon('D%23')
                        ev.target.classList.toggle("activeN")
                        break;
                    case "Fd":
                        this.addSon('F%23')
                        ev.target.classList.toggle("activeN")
                        break;
                    case "Gd":
                        this.addSon('G%23')
                        ev.target.classList.toggle("activeN")
                        break;
                    case "Ad":
                        this.addSon('A%23')
                        ev.target.classList.toggle("activeN")
                        break;
                    default:
                        break;
                }
            },
            resetClavier () {
                const notes = document.querySelectorAll('.notes')
                notes.forEach(note => {
                    note.style.opacity = 0.4
                });
                if (document.querySelector('.activeB')) {
                    const toucheAB = document.querySelector('.activeB')
                    toucheAB.classList.remove('activeB')
                }
                if (document.querySelector('.activeN')) {
                    const toucheAN = document.querySelector('.activeN')
                    toucheAN.classList.remove('activeN')
                }
            },
            ramdomEmoji() {
                this.current = !this.current
                this.emoji = this.tab[this.rand]
                this.emoji2 = this.tab[this.rand2]
            },
            onKeyDown(ev)  {
                if (this.isDown) return
                this.rand = Math.floor(Math.random() * 97)
                this.rand2 = Math.floor(Math.random() * 97)
                this.ramdomEmoji()
                this.resetClavier()
                switch (ev.keyCode) {
                    case 81: //Q
                        document.querySelector('.C').classList.toggle("activeB")
                        this.$refs.do.style.opacity = 1
                        this.addSon('C')
                        break;
                    case 90: //Z
                        document.querySelector('.Cd').classList.toggle("activeN")
                        this.addSon('C%23')
                        break;
                    case 83: //S
                        document.querySelector('.D').classList.toggle("activeB")
                        this.$refs.re.style.opacity = 1
                        this.addSon('D')
                        break;
                    case 69: //E
                        document.querySelector('.Dd').classList.toggle("activeN")
                        this.addSon('D%23')
                        break;
                    case 68: //D
                        document.querySelector('.E').classList.toggle("activeB")
                        this.addSon('E')
                        this.$refs.mi.style.opacity = 1
                        break;
                    case 70: //F
                        document.querySelector('.F').classList.toggle("activeB")
                        this.addSon('F')
                        this.$refs.fa.style.opacity = 1
                        break;
                    case 84: //T
                        document.querySelector('.Fd').classList.toggle("activeN")
                        this.addSon('F%23')
                        break;
                    case 71: //G
                        document.querySelector('.G').classList.toggle("activeB")
                        this.addSon('G')
                        this.$refs.sol.style.opacity = 1
                        break;
                    case 89: //Y
                        document.querySelector('.Gd').classList.toggle("activeN")
                        this.addSon('G%23')
                        break;
                    case 72: //H
                        document.querySelector('.A').classList.toggle("activeB")
                        this.addSon('A')
                        this.$refs.la.style.opacity = 1
                        break;
                    case 85: //U
                        document.querySelector('.Ad').classList.toggle("activeN")
                        this.addSon('A%23')
                        break;
                    case 74: //J
                        document.querySelector('.B').classList.toggle("activeB")
                        this.addSon('B')
                        this.$refs.si.style.opacity = 1
                        break;
                }
                this.isDown = true
            },
            onKeyUp () {
                this.isDown = false
            },
            addSon(son) {
                const audio = document.createElement('audio')
                audio.src = './assets/sounds/' + son +'.mp3'
                audio.play()
            },
        }
    }
</script>


<style lang="postcss" scoped>
    .MainBody {
        @apply text-center pt-10 h-screen w-screen;
        background: linear-gradient(135deg, #FF9D6C 0%, #BB4E75 100%);
    }
    .title {
        @apply bg-black-bg text-white mx-auto font-normal rounded-xl text-3xl py-3 px-8 w-auto inline-block;
        line-height: 33.6px;
    }
    .emoji {
        @apply mx-auto mt-12 mb-24;
        width: 200px;
        height: 200px;
    }
    @screen lg {
        .emoji {
            @apply mx-auto mt-8 mb-16;
        }
    }
    .piano {
        @apply mx-auto bg-black flex justify-between relative p-3 mx-6;
        border-radius: 10px;
        height: 189px;
        width: 368px;
    }
    .toucheB {
        @apply bg-white;
        height: 166px;
        width: 45px;
    }
    .toucheN {
        @apply bg-black absolute;
        height: 120px;
        width: 20px;
        border-radius: 0px 0px 5px 5px;
        top: 6.5%;
    }
    .toucheB:first-child {
        border-radius: 5px 0px 0px 5px;
    }
    .toucheB:last-child {
        border-radius: 0px 5px 5px 0px;
    }
    .toucheB:hover {
        @apply bg-yellow-touche;
    }
    .toucheN:hover {
        @apply bg-purple-touche;
    }
    .activeB {
        @apply bg-yellow-touche;
    }
    .activeN {
        @apply bg-purple-touche;
    }
    .activeNote {
        opacity: 1;
    }
    .piano div:nth-child(2) {
        left: 12.81%;
    }
    .piano div:nth-child(4) {
        left: 26.55%;
    }
    .piano div:nth-child(7) {
        left: 54.05%;
    }
    .piano div:nth-child(9) {
        left: 67.8%;
    }
    .piano div:nth-child(11) {
        left: 81.54%;
    }
    .container_notes {
        @apply mx-auto flex pt-12 justify-between mx-10;
    }
    .notes {
        @apply text-xl;
        color: rgba(255, 255, 255);
        opacity: 0.4;
    }
    @screen md {
        .piano {
            @apply mx-auto;
            height: 276px;
            width: 531px;
        }
        .toucheB {
            height: 252px;
            width: 69px;
        }
        .toucheN {
            height: 184px;
            width: 30px;
            top: 4.35%;
        }
        .container_notes {
            @apply mx-auto;
            width: 462px;
        }
    }
    @media (max-width: 375px) {
        .container_notes {
            @apply invisible;
        }
        .piano {
            height: 162px;
            width: 311px;
        }
        .toucheB {
            height: 138px;
            width: 37.5px;
        }
        .toucheN {
            height: 108px;
            width: 18px;
            top: 7.4%;
        }
    }
    @media (max-width: 320px) {
        .container_notes {
            @apply invisible;
        }
        .piano {
            height: 141px;
            width: 270px;
        }
        .toucheB {
            height: 116px;
            width: 33px;
        }
        .toucheN {
            height: 85px;
            width: 15px;
            top: 8.5%;
        }
    }
</style>