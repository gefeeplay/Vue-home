<template>
    <site-desc></site-desc>

    <div class="block inputForm">
        <h2>Показать конкретные карты:</h2>
        Выберите значение карты:
        <input
        class="my-input"
        v-model="cardValue"  
        placeholder="6, 8, 10, король, валет и т.д."
        required
        >
        Выберите масть:
        <select
        class="my-input"
        v-model="cardSuit"  
        >
        <option value="Любая" selected>Любая</option>
        <option value="Пики">Пики</option>
        <option value="Крести">Крести</option>
        <option value="Червы">Червы</option>
        <option value="Бубны">Бубны</option>
        </select>
        <button class="my-btn" @click="showCard">Найти</button>
    </div>

    <list-of-cards :found-cards="foundCards"></list-of-cards>
</template>

<script>
import cards from './assets/cards.js';
import ListOfCards from './components/listOfCards.vue';
import SiteDesc from './components/SiteDesc.vue';

export default {
    components:{
        SiteDesc,
        ListOfCards
    },
    data(){
        return{
            cards: cards,
            cardValue: '',
            cardSuit: 'Любая',
            foundCards: [],
            searchPerformed: false,
        }
    },
    methods:{
        showCard(){
            // Если не указано значение И масть "Любая" - выводим всю колоду
            if (this.cardValue === '' && this.cardSuit === 'Любая') {
                this.foundCards = [...this.cards];
                return
            }
            
            // Если не указано значение, но выбрана масть - выводим все карты этой масти
            if (this.cardValue === '') {
                this.foundCards = this.cards.filter(card => 
                this.cardSuit === 'Любая' || card.suit === this.cardSuit
                );
                return
            }
            
            // Нормализация введенного значения (для удобства поиска)
            const normalizedValue = this.cardValue.toLowerCase();
            
            // Если масть "Любая" - ищем по значению во всех мастях
            if (this.cardSuit === 'Любая') {
                this.foundCards = this.cards.filter(card => 
                card.value.toLowerCase() === this.cardValue.toLowerCase()
                );
            } 
            // Иначе ищем конкретную карту
            else {
                this.foundCards = this.cards.filter(card => 
                card.value.toLowerCase() === this.cardValue.toLowerCase() && 
                card.suit === this.cardSuit
                );
            }
        }
    }    
}
</script>

<style scoped>

</style>