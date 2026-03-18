<template>
	<div class="article-item-wrapper">
		<div class="article-card m-box" v-for="item in articleList" :key="item.id">
			<!-- 置顶标识 -->
			<div class="top-badge" v-if="item.top">
				<i class="star icon"></i>置顶
			</div>

			<!-- 标题区域 -->
			<div class="article-header">
				<h2 class="article-title">
					<a href="javascript:;" @click.prevent="toArticle(item)">
						{{ item.title }}
					</a>
				</h2>
				<router-link :to="`/category/${item.category.name}`" class="category-tag">
					{{ item.category.name }}
				</router-link>
			</div>

			<!-- 元信息 -->
			<div class="article-meta">
				<span class="meta-item">
					<i class="calendar icon"></i>
					{{ dateFormat(item.gmtCreate, 'YYYY/MM/DD') }}
				</span>
				<span class="meta-item">
					<i class="eye icon"></i>
					{{ item.views }}
				</span>
			</div>

			<!-- 文章描述 -->
			<div class="article-description typo" v-html="item.description" />

			<!-- 标签 -->
			<div class="article-tags">
				<router-link :to="`/tag/${tag.name}`" class="tag-item" :class="tag.color"
					v-for="(tag, index) in item.tags" :key="index">
					{{ tag.name }}
				</router-link>
			</div>
		</div>
	</div>
</template>

<script>
import { dateFormat } from "@/util/dateTimeFormatUtils";

export default {
	name: "articleItem",
	props: {
		articleList: {
			type: Array,
			required: true
		}
	},
	methods: {
		toArticle(article) {
			this.$store.dispatch('goArticlePage', article)
		},
		dateFormat: dateFormat
	}
}
</script>

<style scoped>
.article-item-wrapper {
	display: flex;
	flex-direction: column;
	gap: 24px;
}

.article-card {
	position: relative;
	padding: 28px 32px;
	background: #fff;
	border-radius: 12px;
	box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
	transition: all 0.3s ease;
	overflow: hidden;
}

.article-card:hover {
	box-shadow: 0 6px 24px rgba(0, 0, 0, 0.12);
	transform: translateY(-2px);
}

/* 置顶标识 */
.top-badge {
	position: absolute;
	top: 16px;
	right: 16px;
	padding: 4px 12px;
	background: linear-gradient(135deg, #ff6b6b, #ee5253);
	color: #fff;
	border-radius: 20px;
	font-size: 12px;
	font-weight: 500;
	letter-spacing: 0.5px;
}

/* 标题区域 */
.article-header {
	display: flex;
	align-items: center;
	gap: 12px;
	margin-bottom: 16px;
	flex-wrap: wrap;
}

.article-title {
	margin: 0;
	flex: 1;
	min-width: 0;
}

.article-title a {
	font-size: 22px;
	font-weight: 600;
	color: #2c3e50;
	font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
	line-height: 1.4;
	text-decoration: none;
	transition: color 0.2s ease;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
	overflow: hidden;
}

.article-title a:hover {
	color: #409EFF;
}

.category-tag {
	padding: 6px 14px;
	background: linear-gradient(135deg, #667eea, #764ba2);
	color: #fff;
	border-radius: 6px;
	font-size: 13px;
	font-weight: 500;
	text-decoration: none;
	white-space: nowrap;
	transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.category-tag:hover {
	transform: translateY(-1px);
	box-shadow: 0 2px 8px rgba(102, 126, 234, 0.4);
}

/* 元信息 */
.article-meta {
	display: flex;
	gap: 20px;
	margin-bottom: 18px;
	color: #8590a6;
	font-size: 14px;
}

.meta-item {
	display: flex;
	align-items: center;
	gap: 6px;
}

.meta-item i {
	font-size: 14px;
	opacity: 0.8;
}

/* 文章描述 */
.article-description {
	color: #555;
	font-size: 15px;
	line-height: 1.8;
	margin-bottom: 18px;
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 3;
	-webkit-box-orient: vertical;
}

.article-description :deep(p) {
	margin: 0;
}

/* 标签 */
.article-tags {
	display: flex;
	flex-wrap: wrap;
	gap: 8px;
}

.tag-item {
	padding: 5px 12px;
	border-radius: 6px;
	font-size: 13px;
	font-weight: 500;
	text-decoration: none;
	transition: all 0.2s ease;
	color: #fff;
}

.tag-item:hover {
	transform: translateY(-1px);
	filter: brightness(1.1);
}

/* 响应式 */
@media (max-width: 768px) {
	.article-card {
		padding: 20px 20px;
		border-radius: 8px;
	}

	.article-title a {
		font-size: 18px;
	}

	.article-description {
		font-size: 14px;
		-webkit-line-clamp: 2;
	}

	.top-badge {
		top: 12px;
		right: 12px;
		padding: 3px 10px;
		font-size: 11px;
	}
}
</style>