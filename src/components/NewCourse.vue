<template>
	<div class="container">
		<div class="f">
			<p>课程:<input type="text" placeholder="请输入班课名称" v-model="courseName" class="input-box" /></p>

		</div>
		<div class="f">
			<p>班级:<input type="text" placeholder="请输入班级" v-model="courseClass" class="input-box" /></p>

		</div>
		<div class="card">
			<p>请给本课程添加一个大气的封面</p>
			<div class="pic">
				<div class="preview" @click="handleClick()">
					<img :src="imgUrl" class="cover" v-if="!show" />
					<img src="../assets/add.png" class="icon-plus" v-if="show" />
					<input type="file" @change="getFile($event)" style="display: none;" id="coverFile" />
				</div>

			</div>

		</div>

		<div class="button"><button @click="addCourse()" class="btn">确定</button></div>
	</div>
</template>

<script>
	export default {
		name: 'NewCourse',
		data() {
			return {
				loginUserId: 1,
				courseName: '',
				courseClass: '',
				file: '',
				imgUrl: '',
				show: true
			};
		},

		methods: {
			//点击图片预览区，即模拟点击文件选择组件
			handleClick: function() {
				document.getElementById('coverFile').click();
			},
			//图片预览
			getFile: function() {
				this.file = event.target.files[0];
				var windowURL = window.URL || window.webkitURL;
				this.imgUrl = windowURL.createObjectURL(this.file);
				this.show = false;
			},
			addCourse: function() {
				var _this = this;
				this.$http({
					method: 'post',
					url: 'http://localhost:8080/api/course',
					data: {
						userId: _this.loginUserId,
						courseName: _this.courseName,
						courseClass: _this.courseClass,
						cover: _this.imgUrl,
						finished: 0
					}
				}).then(function() {
					alert('新增班课成功');
					_this.$router.push('/');
				});
			}
		}
	};
</script>

<style scoped>
	p {
		font-family: "微软雅黑";
		font-size: 22px;
		margin-bottom: 5px;

	}

	.container {
		display: flex;
		flex-direction: column;
		padding-top: 50px;
		align-items: center;
		background: #fff;
		margin-top: 20px;

	}

	.input-box {
		width: 500px;
		height: 30px;
		margin-bottom: 30px;
		font-size: 14px;
	}

	.card {
		width: 500px;
		height: 230px;
		


	}

	.pic {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.btn {
		width: 120px;
		height: 40px;
		order: 2px solid rgb(0, 187, 221);
		background-color: whitesmoke;
		border-radius: 8px;
		outline: none;
		color: rgb(0, 187, 221);
		font-size: 16px;
		margin-right: 20px;

	}



	.preview {
		width: 150px;
		height: 150px;
		border: 2px dashed blueviolet;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.icon-plus {
		width: 70px;
		height: 70px;

	}

	.cover {
		width: 100%;
		height: 100%;

	}
</style>
