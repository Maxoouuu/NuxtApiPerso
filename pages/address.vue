<template>
    hello
    <nuxt-link to="/">Home Api</nuxt-link>
    <div class="container">
        <h1 class="status"></h1>
        <button class="find-state">Find my state</button>
    </div>
</template>

<script >
export default {
    /* https://www.youtube.com/watch?v=VK9F8BWrOgY */
    /* https://stackoverflow.com/questions/56180458/referenceerror-document-is-not-defined-in-svelte-3 */
    mounted() {

        const findMyState = () => {
            const status = document.querySelector('.status')

            const success = (position) => {
                console.log(position)
                const latitude = position.coords.latitude
                const longitude = position.coords.longitude
                /* console.log(latitude + ' ' +  longitude) */

                const geoApiUrl = `https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${latitude}&longitude=${longitude}&localityLanguage=en`

                /* Promesse */
                fetch(geoApiUrl)
                    .then(res => res.json())
                    .then(data => {
                        console.log(data)
                        /* Ecris là où il y a la class status la localité */
                        status.textContent = data.locality
                    })
            }

            const error = () => {
                status.textContent = 'Unable to retrieve your location'
            }

            navigator.geolocation.getCurrentPosition(success, error)
        }

        document.querySelector('.find-state').addEventListener('click', findMyState)
    }
}


</script>


