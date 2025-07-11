<template>
    <div>
        <h2>18. Список игральных карт</h2>
        Массив объектов: [{ id: 1, suit: "Пики", value: "Король" }].<br>
        Отрисовка: Список карт в виде карточек.<br>
        Форма: Добавление новой карты (поля "масть", "значение").
    </div>
    <div>
        1. Массив объектов: Создайте массив с начальными данными (например, tasks, books, movies).
        <br>2. Отрисовка списка: Используйте v-for для отображения элементов массива.
        <br>3. Со звездочкой добавить form input и put запрос. Редактирование: Добавьте возможность редактирования
        существующих объектов через форму.
    </div>

    <div>
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

    <div>
        <h2>Список карт:</h2>
        <div v-for="card in foundCards" :key="card.id">
            {{ card.suit }} {{ card.value }}
        </div>
        <div v-if="foundCards.length === 0">
            Карт не найдено!
        </div>
    </div>
</template>

<script>
import cards from './assets/cards.js';

export default {
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
            this.searchPerformed = true
            if (this.cardSuit === "Любая") {
                // Ищем все карты с указанным значением в любой масти
                this.foundCards = this.cards.filter(card => 
                card.value.toLowerCase() === this.cardValue.toLowerCase()
                );
            } else {
            // Ищем конкретную карту по значению и масти
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