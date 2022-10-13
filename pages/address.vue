<template>
    <div>
        <nuxt-link to="/">Home Api</nuxt-link>
        <div>
            <button  @click="findMyState">Find my state</button>
            <p>{{ city }}</p>
        </div>
    </div>
</template>

<script setup>
const city = ref('')

const findMyState = () => {
    const success = (position) => {
        /* console.log(position) */
        const latitude = position.coords.latitude
        const longitude = position.coords.longitude
        /* console.log("latitude : " + latitude + ' ' + "longitude : " + longitude) */

        const geoApiUrl = `https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${latitude}&longitude=${longitude}&localityLanguage=en`

        fetch(geoApiUrl)
            .then(res => res.json())
            .then(data => {
                /* console.log(data) */
                city.value = data.city
            })
    }

    const error = () => {
        city = 'Impossible de récupérer votre emplacement'
    }

    navigator.geolocation.getCurrentPosition(success, error)
}
</script>