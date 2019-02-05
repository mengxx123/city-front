<template>
    <my-page title="地区查询">
        <ul>
            <li v-for="province in provinces">
                <router-link :to="'/provinces/' + province.code">{{ province.name }}</router-link>
            </li>
        </ul>
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                provinces: []
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                this.$http.get('http://node.api.yunser.com/provinces').then(
                    response => {
                        let data = response.data
                        console.log(data)
                        if (data.code === 0) {
                            console.log(data)
                            this.provinces = data.data
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
