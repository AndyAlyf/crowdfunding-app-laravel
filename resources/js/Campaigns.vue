<template>
    <div>
        <v-container class="ma-0 pa-0" grid-list-sm>
            <v-subheader>
                All Campaign
            </v-subheader>
            <v-layout wrap>
                <v-flex v-for="(campaign,index) in campaigns"
                        :key="'campaign-'+index"
                        xs6
                >
                    <!-- <v-card :to="'/campaign/'+campaign.id" class="m-2" >
                        <v-img :src="campaign.image" class="white--text" aspect-ratio="2.5">
                            <v-card-title class="fill-height align-end" v-text="campaign.title"></v-card-title>
                        </v-img>
                    </v-card> -->
                    <campaign-item v-bind:campaign="campaign" />
                </v-flex>
            </v-layout>
            <v-pagination
                v-model="page"
                @input="go"
                :length="lengthPage"
                :total-visible="6">
            </v-pagination>
        </v-container>
    </div> 
</template>

<script>
export default {
    data: () => ({
        campaigns: [],
        page: 0,
        lengthPage: 0
    }),
    created(){
        this.go()
    },
    methods: {
        go(){
            let url = 'api/campaign?page=' + this.page
            axios.get(url)
                .then((response) => {
                    let { data } = response.data
                    console.log(data)
                    this.campaigns = data.campaigns.data
                    this.page = data.campaigns.current_page
                    this.lengthPage = data.campaigns.last_page
                })
                .catch((error) => {
                    let { response } = error
                    console.log(response)
                })
        }
    }
}
</script>