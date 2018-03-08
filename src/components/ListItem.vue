<template>
	<div class="item" ref="item">
		<img :src="data.logo" alt="logo" class="server-logo">
		<h2 class="server-name">{{ data.name }}<span>（{{ data.version }}）</span></h2>
		<a class="server-download" :href="data.downloadUrl" target="_blank">下载整合包</a>
		<span class="server-group">QQ群：<a :href="data.qqGroupUrl" target="_blank"
		                                  v-if="data.qqGroupUrl">{{ data.qqGroup}}</a><span
			v-else>{{ data.qqGroup }}</span></span>
		<a v-if="detail" href="javascript:void(0);" class="server-detail-btn" @click="viewDetail">收起详情</a>
		<a v-else href="javascript:void(0);" class="server-detail-btn" @click="viewDetail">查看详情</a>
		<div v-show="detail" class="server-detail">
			<p>验证方式：{{ verifyMethodText[data.verifyMethod] }} <a v-if="data.verifyMethod === 'tongyi'"
			                                                     :href="data.tongyiRegisterUrl" target="_blank">注册账号</a>
			</p>
			<p v-if="data.maxPlayer">最大人数：{{ data.maxPlayer }}</p>
			<p>服务器地址：{{data.ip}}
				<button class="copy-ip" :data-clipboard-text="data.ip">复制</button>
			</p>
			<div class="server-announcement" v-html="markdown"></div>
		</div>
	</div>
</template>

<script>
	import showdown from 'showdown';
	import Clipboard from 'clipboard';

	let converter = new showdown.Converter();
	new Clipboard('.copy-ip');
	export default {
		name: 'ListItem',
		props: ['data', 's', 'index'],
		data () {
			return {
				verifyMethodText: {
					none: '无验证',
					mojang: '正版验证',
					tongyi: '统一验证'
				},
				detail: false,
				markdown: ''
			}
		},
		methods: {
			viewDetail: function () {
				if (typeof this.parsed === 'undefined') {
					if (this.data.announcement) {
						this.$http.get('./static/markdown/' + this.data.announcement).then((data) => {
							this.markdown = converter.makeHtml(data.body);
							this.parsed = true;
						});
					} else {
						this.parsed = true;
					}
				}
				this.detail = !this.detail;
			}
		},
		mounted () {
			if (this.s === this.index) {
				this.viewDetail();
				window.scroll(0, this.$refs.item.offsetTop);
			}
		}
	}
</script>

<style>
	a {
		text-decoration: none;
	}

	.item {
		background-color: #e9e9e9;
		padding: 16px;
		-webkit-border-radius: 4px;
		-moz-border-radius: 4px;
		border-radius: 4px;
		position: relative;
		margin: 8px 0;
	}

	.detailed {
		height: auto;
	}

	.server-logo {
		display: inline-block;
		width: 80px;
		height: 80px;
	}

	.server-name {
		position: absolute;
		left: 112px;
		top: 16px;
		font-size: 20px;
		font-weight: bold;
		margin: 0;
	}

	.server-download {
		position: absolute;
		left: 112px;
		top: 47px;
		background-color: #66ccff;
		-webkit-border-radius: 2px;
		-moz-border-radius: 2px;
		border-radius: 2px;
		border: none;
		padding: 4px 12px;
		outline: none;
		cursor: pointer;
		color: #fff;
		font-size: 14px;
	}

	.server-name span {
		font-size: 16px;
		font-weight: normal;
	}

	.server-group {
		position: absolute;
		top: 80px;
		left: 112px;
	}

	.server-detail-btn {
		position: absolute;
		font-size: 12px;
		top: 90px;
		right: 16px;
	}

	.server-detail {
		margin-top: 20px;
	}

	.copy-ip {
		background-color: #66ccff;
		font-size: 12px;
		padding: 2px 4px;
		border: none;
		outline: none;
		color: #fff;
		-webkit-border-radius: 2px;
		-moz-border-radius: 2px;
		border-radius: 2px;
		cursor: pointer;
	}
</style>
