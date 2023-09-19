<template>
    <a v-if="isExternaLink" :href="link.to" target="_blank" class="normal-link" >{{ link.name }}</a>

    <router-link
        v-else
        :to="route"
        v-slot="{ isActive }"
    >
        <a 
            :class=" isActive ? 'is-active' : 'normal-link'"
        >
            {{ link.name }}
        </a>
        <!-- <a 
            :href="href"
            :class=" isActive ? 'is-active' : 'normal-link'"
        >
            {{ link.name }}
        </a> -->
    </router-link>
</template>

<script>
    export default {
        props: {
            link: {
                type: Object,
                required: true,
            }
        },
        computed: {
            isExternaLink() {
                return this.link.to.startsWith('http')
            },
            route() {
                return this.link.id === undefined ?
                { name: this.link.to } 
                :
                { name: this.link.to, params: { id: this.link.id }}
            }
        }
    }

</script>

<style scoped>

.is-active {
    color: #42b983;
}
.normal-link{
    color: #c6c5c5;
}

</style>