<template>
	<MainTop />
	<div class="common-container">
		<div class="common-container-line">
			<div class="list-container">
				<div class="list-warpper">
					<div class="commponent-title">
						<h1 class="community-title">우리아이 커뮤니티</h1>
						<p class="community-subtitle">우리아이를 돌아보세요!</p>
					</div>
				</div>
				<CommunityCategoryFilterSelector :showImage = "true"/>
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
import { ref, onMounted } from 'vue'
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
</script>
