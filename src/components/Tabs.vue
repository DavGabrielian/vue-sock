<template>
    <div>
        <h2>Reviews</h2>
        <span 
        class="tab" 
        :class="{activeTab: selectedTab === tab}"
        v-for="tab, index in tabs" 
        :key="index"
        @click="selectedTab = tab"
        >
            {{tab}}
        </span>
        <div v-if="selectedTab === 'Reviews'">
            <p v-if="!reviews.length">There are no reviews yet.</p>
            <ol>
                <li v-for="review,index in reviews" :key="index">
                <p>{{ review.name }}</p>
                <p>Rating: {{ review.rating }}</p>
                <p>{{ review.review }}</p>
                </li>
            </ol>
        </div>
        <div v-else>
            <Review @review-submitted="addReviw"/>
        </div>
    </div>
</template>

<script>
import Review from '../components/Review.vue'

export default {
    name: 'Tabs',
    components: {
        Review
    },
    props: {
        reviews: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            tabs: ['Reviews', 'Make a Review'],
            selectedTab: 'Reviews'
        }
    }
}
</script>

<style>

</style>