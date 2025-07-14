<template >
    <div>
        <h2>Список карт:</h2>
        <p>Найдено {{ foundCards.length }} карт:</p>
        <div class="cardsList">
            <div v-for="card in foundCards" :key="card.id" class="card-item">
                <div class="card-value">{{ getShortValue(card.value) }}</div>
                <img :src="getSuitImage(card.suit)" class="card-suit"> 
            </div>
        </div>
        <div v-if="foundCards.length === 0">
            Карт не найдено!
        </div>
    </div>
</template>
<script>
export default {
    props:{
        foundCards:{
            type: Array,
            required: true,
            default: () => []
        }
    },
    methods:{
        getSuitImage(suit) {
            try {
                return new URL(`/src/assets/suits/${suit}.png`, import.meta.url).href
            } catch {
                console.error(`Изображение для масти ${suit} не найдено`);
                return ''; // или путь к изображению-заглушке
            }
        },
        getShortValue(value) {
            const abbreviations = {
                'Валет': 'В',
                'Дама': 'Д',
                'Король': 'К',
                'Туз': 'Т'
            };
            return abbreviations[value] || value; // Возвращаем сокращение или оригинал, если нет в списке
        }
    }
     
}
</script>
<style scoped>
    .cardsList {
    display: flex;
    flex-wrap: wrap;
    gap: 50px;
    justify-content: flex-start;
}

.card-item {
    background-color: white;
    border: none;
    box-shadow: 1px 1px 1px gray;
    border-radius: 20px;
    height: 300px;
    width: 200px;
    padding: 10px;
    padding-left: 10px;
    text-align: start;
    font-size: xx-large;
    color: #333;
    flex: 0 0 auto;
    box-sizing: border-box;
}

.card-value {
  font-size: 24px;
  font-weight: bold;
  padding-left: 13px;

}

.card-suit {
  width: 40px;
  height: 40px;
  object-fit: contain;
}
</style>