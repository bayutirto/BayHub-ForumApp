<template>
    <v-app id="inspire">
        <v-container fluid>
            <v-form @submit.prevent="create">
                <v-layout row wrap>
                    <v-flex md8>
                    <h2 class="title mx-12 my-9 grey--text">Ask a question</h2>
                    <v-card
                        class="mx-12 mb-12"
                        max-width="1000"
                    >
                        <v-card-text>
                            <p><span class="font-weight-bold"> Title</span>
                            <br> Be specific and imagine you’re asking a question to another person
                            </p>

                            <v-text-field
                                label="Your question title"
                                hint="For example, Is there an R function for finding the index of an element in a vector?"
                                outlined
                                v-model="form.title"
                                type="text"
                                required
                            ></v-text-field>

                            <p><span class="font-weight-bold"> Category</span>
                            <br> Select a category to specify your question
                            </p>
                            <v-select
                                :items="categories"
                                item-text="name"
                                item-value="id"
                                label="Select your category"
                                outlined
                                v-model="form.category_id"
                                autocomplete
                            ></v-select>

                            <p><span class="font-weight-bold"> Body</span>
                            <br> Include all the information someone would need to answer your question
                            </p>

                            <vue-simplemde v-model="form.body"></vue-simplemde>

                        </v-card-text>
                        <v-card-actions>
                        <v-btn
                            tile
                            color="blue darken-1"
                            class="ma-2"
                            dark
                            type="submit"
                        >
                            Review your question
                        </v-btn>
                        </v-card-actions>
                    </v-card>

                    </v-flex>

                    Sidebar
                </v-layout>
            </v-form>
        </v-container>
    </v-app>
</template>

<script>
export default {
    data(){
        return {
            form :{
                title:null,
                category_id:null,
                body:null
            },
            categories:{},
            errors:{},
        }
    },
    created(){
        axios.get('/api/category')
        .then(res => this.categories = res.data.data)

    },
    methods:{
        create(){
            axios.post('api/question',this.form)
            .then(res => this.$router.push(res.data.path))
            .catch(error => this.errors = error.response.data.error)
        }
    }

}
</script>

<style>

</style>
