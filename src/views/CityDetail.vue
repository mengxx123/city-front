<template>
    <my-page title="地区查询" backable>
        <ui-article>
            <table>
                <tr>
                    <th>地区名称</th>
                    <th>邮政编码</th>
                </tr>
                <tr v-for="county in counties">
                    <td>
                        {{ county.name }}
                        <!-- <router-link :to="'/cities/' + county.code">{{ county.name }}</router-link> -->
                    </td>
                    <td>
                        {{ county.code }}
                    </td>
                </tr>
            </table>
        </ui-article>
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                counties: []
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                let cityCode = this.$route.params.code
                this.$http.get(`http://node.api.yunser.com/cities/${cityCode}/counties`).then(
                    response => {
                        let data = response.data
                        console.log(data)
                        if (data.code === 0) {
                            console.log(data)
                            this.counties = data.data
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
