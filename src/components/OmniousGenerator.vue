<template>
    <div class="generator-container">
        <h3>Click what you need right now</h3>
        <div class="button-container">
            <button @click="generatePositive" class="button positive">
                Positivity ☀️
            </button>
            <button @click="generateNegative" class="button negative">
                Negativity 🌙
            </button>
        </div>

        <div class="output-container">
            <hr class="separator" />
            <p class="generated-sentence">{{ currentSentence }}</p>
            <social-share-bar :sentence="currentSentence"></social-share-bar>
            <hr class="separator" />

            <div class="previous-sentences">
                <h3>Your last recent Generations</h3>
                <p v-for="(sentence, index) in previousSentences" :key="index">{{ sentence }}</p>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import SocialShareBar from './SocialShareBar.vue';

export default defineComponent({
    name: 'OminousGenerator',
    components: {
        SocialShareBar
    },
    data() {
        return {
            currentSentence: 'You will press the button. It\'s inevitable.',
            previousSentences: [] as string[],
            positiveFirstParts: [
                "Today you will.", "You are destined to.", "Luck will find you.", "Success chases you.", "Joy is inevitable.",
                "Happiness will hunt you down.", "Fortune favors you.", "Victory is your shadow.", "Achievement clings to you.",
                "Triumph will stalk you.", "Prosperity is coded in your destiny.", "Abundance seeks you out.", "You will be ok.",
                "Help is on the way.", "You are saved.", "Everything will turn out fine.", "You will succeed.",
                "Be nice to yourself.", "Just keep going.", "You are strong.", "Everything will turn out right.",
                "The world is better with you in it.", "Embrace the future.", "Your success is inevitable.", "You will find happiness.",
                "Trust in your path.", "You are unstoppable.", "Your dreams will come true.", "Love surrounds you.",
                "You are the chosen one.", "Prosperity awaits you.", "The light will guide you.", "Miracles gravitate towards you.",
                "Your potential is limitless.", "Abundant joy follows you.", "You radiate success.", "Your path is blessed.",
                "Opportunities seek you out.", "Your energy attracts fortune.", "You are a magnet for miracles.",
                "Success is in your footsteps.", "You are destined for greatness.", "Good fortune is in your future.",
                "Your journey leads to success.", "Wealth flows towards you.", "Your story inspires triumph.",
                "You are a beacon of hope.", "You are destined for prosperity.", "Fulfillment is within your grasp.",
                "You are a catalyst for positive change.", "Your aspirations will be realized.", "Greatness is your destiny.",
                "You will rise above challenges.", "Your spirit is unbreakable.", "You are a force of positivity."
            ],
            negativeFirstParts: [
                "Trouble will find you.",
                "Misery clings to you.",
                "Sorrow is on your trail.",
                "Hardship targets you.",
                "Anguish becomes your shadow.",
                "Struggle chooses you.",
                "Doom is drawn to you.",
                "Distress is in pursuit.",
                "Gloom is your constant follower.",
                "Peril is linked to your steps.",
                "Fear accompanies you.",
                "Disappointment is inevitable.",
                "Defeat lurks behind you.",
                "Loss is on your horizon.",
                "Regret will shadow you.",
                "Desolation follows your path.",
                "Failure is your constant companion.",
                "Despair wraps around you.",
                "Ruin awaits you.",
                "Suffering is in your future.",
                "Disaster will seek you out.",
                "Dread will engulf you.",
                "Rejection is drawn to you.",
                "Frustration will be your guide.",
                "Loneliness chooses you.",
                "Melancholy is your destiny.",
                "Neglect will find you.",
                "Pain will be your ally.",
                "Torment is yours to bear.",
                "Agony will accompany you.",
                "Bitterness will be your constant.",
                "Conflict will follow you.",
                "Turmoil will be your companion.",
                "Crisis seeks you out.",
                "Adversity is your fate.",
                "Misfortune will stick to you.",
                "Calamity will be your shadow.",
                "Woe will cling to you.",
                "Heartbreak finds its way to you.",
                "Discord will walk with you.",
                "Anger will fuel you.",
                "Resentment will be your echo.",
                "Anxiety will be your burden.",
                "Dismay will be your guest.",
                "Hopelessness will be your shadow.",
                "Tragedy will be your story.",
                "Catastrophe will hunt you down.",
                "Grief will be your constant.",
                "Havoc will be drawn to you.",
                "Destitution will be your partner.",
                "Deprivation will follow you.",
                "Isolation will be your fate.",
                "Dejection is your path.",
                "Discontent will be your theme.",
                "Mourning will be your song.",
                "Rage will burn within you.",
                "Wrath will consume you.",
                "Envy will be your drive.",
                "Jealousy will guide you."
            ],
            secondParts: ["Find joy in small things.", "Achieve great success.", "You have no choice.", "Do not resist.",
                "You cannot stop it.", "It is inevitable.", "... or else.", "Otherwise they will catch you.",
                "The weak already perished.", "Your presence is mandatory.", "Resistance is futile.", "Accept your fate.",
                "It is your destiny.", "Deviation leads to despair.", "Others will fall.", "Prepare for consequences.",
                "Surrender to its grip.", "Beware of your power.", "Resistance will bring suffering.", "But shadows linger.",
                "Escape is not an option.", "Denial is not feasible.", "You can't avoid success.", "Your victory is assured.",
                "There's no alternative.", "Acceptance is your only choice.", "The stars have decided.", "Your path is written.",
                "Destiny embraces you.", "The universe conspires in your favor.", "Fate has chosen you.", "There's no looking back.",
                "Your time has come.", "This is your moment.", "Your fate is sealed.", "The outcome is certain.",
                "Your triumph is unavoidable.", "The prophecy will be fulfilled.", "There's no escaping your destiny.",
                "Your glory is preordained.", "The script is written.", "Your success story is inevitable.", "The future is yours.",
                "Your legend is being written.", "There's no dodging fortune.", "Your breakthrough is imminent.",
                "Your victory is written in the stars.", "The cosmos aligns for you.", "Your destiny is undeniable.",
                "There's no avoiding it.",
                "It's a relentless pursuit.",
                "Escape is an illusion.",
                "You can't hide.",
                "It's an unyielding chase.",
                "There's no outrunning it.",
                "Evading it is impossible.",
                "You can't shake it off.",
                "It's an inescapable reality.",
                "Denial is pointless.",
                "You cannot escape fate.",
                "The shadows are closing in.",
                "It's a truth you can't deny.",
                "The cycle is unbreakable.",
                "Your efforts are futile.",
                "It's a destiny you can't avoid.",
                "The darkness is inevitable.",
                "There's no light at the end.",
                "You're trapped in this fate.",
                "It's a path you must walk.",
                "No one can save you now.",
                "You're bound to this end.",
                "It's a burden you must carry.",
                "There's no relief in sight.",
                "The end is already written.",
                "You're caught in this web.",
                "There's no turning back now.",
                "It's a fate sealed in shadow.",
                "The abyss stares back at you.",
                "You're sinking into despair.",
                "There's no climbing out.",
                "You're in the eye of the storm.",
                "The night grows darker.",
                "It's a downward spiral.",
                "You're on a collision course.",
                "The curse is unbreakable.",
                "The chains are unyielding.",
                "You're falling into the void.",
                "The vortex pulls you deeper.",
                "You're walking into the storm.",
                "The whisper of doom is near.",
                "The chill of fate is upon you.",
                "The hourglass is running out.",
                "You're dancing with shadows.",
                "The weight is unbearable.",
                "The bell tolls for you.",
                "The grip of fate tightens.",
                "You're at the edge of despair.",
                "The floodgates are open.",
                "The fire consumes all.",
                "You're in the jaws of defeat.",
                "The tide is unturnable.",
                "You're under the dark cloud.",
                "The winds of misfortune blow.",
                "The sands of time run out.",
                "The storm will not pass.",
                "The thorns grow sharper.",
                "The cold grips tighter.",
                "The darkness deepens."
            ]
        };
    },
    methods: {
        getRandomElement(array: string[]):string {
            return array[Math.floor(Math.random() * array.length)];
        },
        generateSentence(firstParts: string[], secondParts: string[]): string {
            const firstPart = this.getRandomElement(firstParts);
            const secondPart = this.getRandomElement(secondParts);
            return `${firstPart} ${secondPart}`;
        },
        addSentence(sentence: string) {
            this.previousSentences.unshift(sentence);
            if (this.previousSentences.length > 50) {
                this.previousSentences.pop();
            }
        },
        generatePositive() {
            const sentence = this.generateSentence(this.positiveFirstParts, this.secondParts);
            this.currentSentence = sentence;
            this.addSentence(sentence);
        },
        generateNegative() {
            const sentence = this.generateSentence(this.negativeFirstParts, this.secondParts);
            this.currentSentence = sentence;
            this.addSentence(sentence);
        }
    }
})
</script>
<style scoped>
.generator-container {
    text-align: center;
}

.button-container {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-bottom: 20px;
}

.button {
    padding: 15px 30px;
    font-size: 1.2em;
    cursor: pointer;
    border: none;
    border-radius: 5px;
}

.positive {
    background-color: #ffcc00;
    color: white;
}

.negative {
    background-color: #333;
    color: white;
}

.output-container {
    margin-top: 20px;
}

.generated-sentence {
    font-size: 1.5em;
    margin-bottom: 20px;
}

.separator {
    margin-bottom: 20px;
    width: 50%;
    margin: 2rem auto;
}

.previous-sentences h3 {
    font-size: 1.3rem;
    font-weight: bolder;
    color: #999999;
}

.previous-sentences p {
    font-size: 0.9rem;
    color: #666;
}
</style>
  