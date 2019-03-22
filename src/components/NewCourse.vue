<template>
	<div class="container">
			<input
			type="text"
			placeholder="请输入班课名称"
			v-model="course.courseName"
			class="inputbox"
		/>
		<input
			type="text"
			placeholder="请输入班级"
			v-model="course.courseClass"
			class="inputbox"
		/>
		<input type="text" placeholder="请输入图片地址" v-model="course.cover" class="inputbox" />
		<button @click="addCourse(course)" class="btn">确定</button>
	</div>
</template>

<script>
export default {
	name: 'NewCourse',
	data() {
		return {
			loginUserId: 1,
			course: {
				courseName: '',
				courseClass: '',
				cover: ''
			}
		};
	},
	methods: {
		addCourse: function(course) {
			var _this = this;
			this.$http({
				method: 'post',
				url: 'http://localhost:8080/api/course',
				data: {
					userId: _this.loginUserId,
					courseName: course.courseName,
					courseClass: course.courseClass,
					cover: course.cover,
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
	.container {
		margin: 0 auto;
	display: flex;
	flex-direction: column;
	padding-top: 20px;
	padding-left: 100px;
	background-color: #fff;
	margin-top: 20px;
}
.inputbox {
	width: 500px;
	height: 40px;
	margin-bottom: 40px;
	font-size: 14px;
}
.btn {
	width: 120px;
	height: 40px;
	border: 2px solid rgb(0, 187, 221);
	background-color: #fff;
	border-radius: 8px;
	outline: none;
	color: rgb(0, 187, 221);
	font-size: 16px;
}
</style>
