<script setup>
import { ref, computed } from "vue";

const counter = ref(0);
const initialCount = counter.value
const arrayNumFavs = ref([])

const incrementCounter = () => {
    counter.value++;
};

const decrementCounter = () => {
    counter.value--;
};

const resetCounter = () => {
    counter.value = initialCount;
};

const removeFavorite = (num) => {
    const index = arrayNumFavs.value.indexOf(num);
    if (index !== -1) {
        arrayNumFavs.value.splice(index, 1);
    }
};

const addFavorite = () => {
    arrayNumFavs.value.push(counter.value);
};

const bloqueoBoton = computed(() => {
    const numSearch = arrayNumFavs.value.find(num => num === counter.value)
    if (numSearch === 0) {
        return true
    }
    return numSearch ? true : false
})
</script>

<template>
    <div class="counter-container">
        <h1 class="counter">{{ counter }}</h1>
        <div class="button-container">
            <button v-on:click="incrementCounter" class="btn btn-action"><i class="bi bi-plus-lg"></i></button>
            <button v-on:click="resetCounter" class="btn btn-action"><i class="bi bi-arrow-clockwise"></i></button>
            <button v-on:click="decrementCounter" class="btn btn-action"><i class="bi bi-dash"></i></button>
        </div>
        <div class="favorites">
            <button v-on:click="addFavorite" class="btn btn-favorite" :disabled="bloqueoBoton">
                <i class="bi bi-star"></i> Agregar favoritos
            </button>
            <h2>Tus numeros favoritos:</h2>
        </div>
        <div class="favorite-num-container">
            <div class="favorite-num" v-for="(num, index) in arrayNumFavs" :key="index">
                {{ num }}
                <button @click="removeFavorite(num)" class="btn-remove-favorite">
                    <i class="bi bi-x-circle"></i>
                    <span class="sr-only"></span>
                </button>
            </div>
        </div>
    </div>
</template>

<style>
.counter-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

.counter {
    font-size: 3rem;
    margin-bottom: 20px;
}

.button-container {
    display: flex;
    gap: 10px;
}

.btn-action {
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 150px;
    padding: 10px 20px;
    transition: background-color 0.3s ease;
    cursor: pointer;
}

.btn-action:hover {
    background-color: #0056b3;
}

.favorites {
    margin-top: 20px;
}

.favorite-num-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 10px;
}

.favorite-num {
    display: flex;
    align-items: center;
    padding: 8px 12px;
    border-radius: 4px;
    margin: 5px;
    font-size: 1.2rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.btn-favorite {
    background-color: #077b21;
    color: rgb(255, 255, 255);
    border: none;
    border-radius: 150px;
    padding: 5px 10px;
    position: relative;
    left: 90px;
    margin-top: 10px;
    margin-bottom: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.btn-favorite:hover {
    background-color: #62b631;
}

@media screen and (max-width: 600px) {

    .counter-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: auto;
    }

    .btn-favorite {
        left: 50px;
    }

}
.num-text {
    flex-grow: 1;
}

.btn-remove-favorite {
    background-color: #e74c3c;
    color: rgb(255, 255, 255);
    border: none;
    border-radius: 50%;
    padding: 5px;
    margin-left: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1rem;
}

.btn-remove-favorite:hover {
    background-color: #c0392b;
}

</style>
