<template>
	<div class="content-wrapper">
		<div class="category-buttons">
			<router-link v-for="category in categories" :key="category.value"
				:to="{ name: 'FilteredCommunity', params: { category: category.value } }">
				<div class="btn-container" :class="{ active: isActive }">
					<button>
						<div class="category-image-container">
							<img :src="category.imagePath" :alt="category.label" class="category-image" :class="{ hide: !props.showImage}">
							<span class="category-label">{{ category.label }}</span>
						</div>
					</button>
				</div>
			</router-link>
		</div>
	</div>
</template>

<script setup>
import '@/assets/css/common_container.css'

// 이미지 import
import img0to2 from '@/assets/images/community/category-under-2.png'
import img3to5 from '@/assets/images/community/category-under-5.png'
import img6to7 from '@/assets/images/community/category-under-7.png'
import img8to9 from '@/assets/images/community/category-under-9.png'
import img10to11 from '@/assets/images/community/category-over-10.png'
import imgOver12 from '@/assets/images/community/category-over-12.png'

const categories = [
	{ value: '영유아(0~2세)', label: '영유아(0~2세)', imagePath: img0to2 },
	{ value: '유아(3~5세)', label: '유아(3~5세)', imagePath: img3to5 },
	{ value: '취학 전 아동(6~7세)', label: '취학 전 아동(6~7세)', imagePath: img6to7 },
	{ value: '초등학교 저학년(8~9세)', label: '초등학교 저학년(8~9세)', imagePath: img8to9 },
	{ value: '초등학교 중학년(10~11세)', label: '초등학교 중학년(10~11세)', imagePath: img10to11 },
	{ value: '초등학교 고학년(12~13세)', label: '초등학교 고학년(12~13세)', imagePath: imgOver12 }
];

const props = defineProps({
	showImage: Boolean,
});

</script>

<style scoped>
.content-wrapper {
	width: 100%;
	padding: 20px 0;
}

.category-buttons {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
	gap: 20px;
	max-width: 100%;
	margin: 0 auto;
}

.btn-container {
	flex: 0 0 calc(50% - 10px);
	max-width: 300px;
}

.category-buttons button {
	background: none;
	border: none;
	cursor: pointer;
	transition: transform 0.2s, box-shadow 0.2s;
	width: 100%;
	height: 100%;
	padding: 10px;
	box-shadow: 0 3px 7px rgba(0, 0, 0, 0.2);
	border-radius: 10px;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: space-between;

}

.category-buttons button:hover {
	transform: translateY(-3px);
	box-shadow: 0 7px 15px rgba(173, 253, 43, 0.7);
}

.category-image-container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	width: 100%;
	height: 100%;
	/* 컨테이너 높이를 100%로 설정 */
	overflow: hidden;
	/* 이 줄을 추가합니다 */
}

.category-image {
	width: 70%;
	height: auto;
	/* 높이를 자동으로 조정 */
	object-fit: contain;
	margin-bottom: 10px;
	max-width: 100%;
}

.category-label {
	text-align: center;
	font-weight: bold;
	font-size: 0.9em;
	width: 100%;

}

.hide {
	display: none;
}

</style>
