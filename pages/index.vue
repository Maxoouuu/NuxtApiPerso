

<template>
    <div>

        <header>
            <nuxt-link to="/address">Address</nuxt-link>
        </header>
        <input type="text" placeholder="login, id, node_id, url" id="in" v-model="text">
        <button type="button" v-on:click="getValue">Submit</button>
        <p>organization : {{ organization }}</p>
        <p>Text : {{ text }}</p>
        <!-- <p>organization.text : {{ organization.text }}</p> -->


        <p>organization.login : {{ organization.login }}</p>
        <p>organization.description : {{ organization.description }}</p>
    </div>
</template>
  
<script >

export default defineComponent({
    async setup() {

        const [{ data: organization }, { data: repos }] = await Promise.all([
            useFetch(`https://api.github.com/orgs/nuxt`),
            useFetch(`https://api.github.com/orgs/nuxt/repos`)
        ])

        return {
            organization,
            repos
        }
    },
    methods: {
        getValue() {
            /* Essayer avec {} pour la variable et $ pour l'appeler */
            // Sélectionner l'élément input et récupérer sa valeur
            var { text } = document.getElementById("in").value;
            // Afficher la valeur
            console.log(text)
        }
    }
})

</script>