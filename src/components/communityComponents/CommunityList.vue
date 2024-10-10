<template>
	<MainTop />
	<div class="common-container">
		<div class="common-container-line">
			<div class="list-container">
				<div class="list-warpper">
					<div class="commponent-title">
						<h1 class="community-title">{{category == null ? "우리아이" : category}} 커뮤니티</h1>
						<p class="community-subtitle">우리아이를 돌아보세요!</p>
					</div>
				</div>
				<CommunityCategoryFilterSelector :showImage="category == null"/>
				<div class="list-container">
					<div class="list-Line">
						<div v-for="post in filteredPosts" :key="post.id" class="post-item">
							<router-link :to="{ name: 'CommunityDetail', params: { id: post.id } }" class="post-item-wrapper">
								<span class="post-category">{{ post.category }}</span>
								<div>
									<h3 class="list-title">{{ post.title }}</h3>
								</div>
								<div class="list-ediNdelNcount">
									<span class="post-view-count">조회수: {{ post.viewCount }}</span>
									<span class="post-author">{{ post.authorName }}</span>
								</div>
							</router-link>
						</div>
					</div>
				</div>
			</div>
			<div class="background-image"></div>
		</div>
	</div>
</template>
<script setup>
import '@/assets/css/community_list.css'
import '@/assets/css/post_list.css'
import MainTop from '@/components/MainTop.vue'

import api from '@/services/api';
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';
import CommunityCategoryFilterSelector from './CommunityCategoryFilterSelector.vue';

const posts = ref([])

const fetchPosts = async () => {
	try {
		const response = await api.getAllCommunityPosts()
		posts.value = response
	} catch (error) {
		console.error('Error fetching posts:', error)
	}
}

onMounted(async () => {
	await fetchPosts();
})

const route = useRoute();
const category = computed(() => route.params.category);

const filteredPosts = computed(() => {
	const category = route.params.category;
	if (category) {
		return posts.value.filter(post => post.category === category);
	}
	return posts.value;
});
</script>
