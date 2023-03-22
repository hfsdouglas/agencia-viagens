<template>
    <div class="container rounded border border-primary">
        <div class="row">
            <div class="col-12 mt-4">
                <div class="form-floating">
                    <select class="form-select border border-primary" name="country-origin" id="country-origin" v-model="originCountry" @change="selectedCountry('origin')">
                        <option v-for="item in countries" :key="item" :value="item.country">{{ item.country }}</option>
                    </select>
                    <label for="country-origin">País de Origem</label>
                </div>
            </div>
        </div>
        <div class="row mt-2">
            <div class="col-12">
                <div class="form-floating">
                    <select class="form-select border border-primary" name="country-origin" id="country-origin">
                       <option v-for="item in originCities" :key="item" :value="item.city">{{ item.city }}</option>
                    </select>
                    <label for="country-origin">Cidade de Origem</label>
                </div>
            </div>
        </div>
        <div class="row mt-4">
            <div class="col-12">
                <div class="form-floating">
                    <select class="form-select border border-primary" name="country-origin" id="country-origin" v-model="destinyCountry" @change="selectedCountry('destiny')">
                        <option v-for="item in countries" :key="item" :value="item.country">{{ item.country }}</option>
                    </select>
                    <label for="country-origin">País de Destino</label>
                </div>
            </div>
        </div>
        <div class="row mt-2">
            <div class="col-12">
                <div class="form-floating">
                    <select class="form-select border border-primary" name="country-origin" id="country-origin">
                        <option v-for="item in destinyCities" :key="item" :value="item.city">{{ item.city }}</option>
                    </select>
                    <label for="country-origin">Cidade de Destino</label>
                </div>
            </div>
        </div>
        <div class="row mt-4">
            <div class="col-6">
                <label for="">Adultos</label>
                <div class="d-flex justify-content-center">
                    <button class="btn btn-primary">-</button>
                    <input type="number" class="form-control mx-2 border border-primary">
                    <button class="btn btn-primary">+</button>
                </div>
            </div>
            <div class="col-6">
                <label for="">Crianças</label>
                <div class="d-flex justify-content-center">
                    <button class="btn btn-primary">-</button>
                    <input type="number" class="form-control mx-2 border border-primary">
                    <button class="btn btn-primary">+</button>
                </div>
            </div>
        </div>
        <div class="row mt-2">
            <div class="col-6">
                <div class="form-check">
                    <input class="form-check-input" type="radio" name="economy" id="economy">
                    <label class="form-check-label" for="economy">Econômica</label>
                </div>
            </div>
            <div class="col-6">
                <div class="form-check">
                    <input class="form-check-input" type="radio" name="executive" id="executive">
                    <label class="form-check-label" for="executive">Executiva</label>
                </div>
            </div>
        </div>
        <div class="row mt-2 mb-4">
            <div class="col-12">
                <label class="form-label" for="milhas-range">Utilizar {{ milhas }} milhas</label>
                <input type="range" class="form-range" name="milhas-range" id="milhas-range">
            </div>
        </div>
    </div>
</template>

<script>
    import { ref, onMounted } from 'vue'; 
export default {
    setup() {
        var milhas = 0;
        var countries = ref([]);
        var originCities = ref([]);
        var originCountry = ref([]);
        var destinyCountry = ref([]);
        var destinyCities = ref([]);

        onMounted(() => {
            fetch('http://localhost:3000/countries').then(response => {
                response.json().then(items => {
                    countries.value = items;
                });
            });
        });
        
        function selectedCountry (fn) {
            let countriesArray = JSON.parse(JSON.stringify(countries.value));
            
            if (fn === 'origin') {
                let country = countriesArray.filter(item => item.country === originCountry.value); 
                country.map(arrayCities => {
                    originCities.value = arrayCities.cities.filter(item => item.city);
                });            
            } else {
                let country = countriesArray.filter(item => item.country === destinyCountry.value); 
                country.map(arrayCities => {
                    destinyCities.value = arrayCities.cities.filter(item => item.city);
                });
            }
        }

        return { 
            countries, 
            originCities, 
            selectedCountry,
            originCountry,
            destinyCountry,
            destinyCities,
            milhas 
        };
    }
}
</script>

<style scoped>
    .container {
        max-width: 350px;
        margin: 10px;
    }
</style>