<template>
    <div>
        <v-card :to="'/campaign/'+campaign.id"
        class="m-1">
            <v-img
                :src="campaign.image"
                class="white--text"
                aspect-ratio="0.8"
            >
                <v-card-title 
                    class="fill-height align-end"
                    v-text="campaign.title"
                ></v-card-title>
            </v-img>

            <v-card-actions>
                <v-progress-linear
                    v-model="progress"
                    color="blue-grey"
                    height="7"
                    v-if="progress < 100"
                ></v-progress-linear>
                <v-progress-linear
                    v-model="progress"
                    color="success"
                    height="7"
                    v-else
                ></v-progress-linear>
            </v-card-actions>

            <v-card-actions>
                <v-icon>mdi-cash</v-icon>
                <span>Rp. {{ campaign.required.toLocaleString('id-ID') }}</span>
                <v-spacer></v-spacer>
                <span>{{ progress }}%</span>
            </v-card-actions>
        </v-card>
    </div> 
</template>

<script>
export default {
    name: 'campaign-item',
    props: ['campaign'],
    computed: {
        progress() {
            return (Math.round(this.campaign.collected / this.campaign.required * 100))
        }
    }
}
</script>