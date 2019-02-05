<template>
    <my-page title="地区查询" >
        <ul>
            <li v-for="city in cities">
                <router-link :to="'/cities/' + city.code">{{ city.name }}</router-link>
            </li>
        </ul>
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                cities: []
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                let provinceCode = this.$route.params.code
                this.$http.get(`http://node.api.yunser.com/provinces/${provinceCode}/cities`).then(
                    response => {
                        let data = response.data
                        console.log(data)
                        if (data.code === 0) {
                            console.log(data)
                            this.cities = data.data
                        }
                    },
                    response => {
                        console.log(response)
                    })
            }
        }
    }
</script>

<style scoped>
</style>
