<template>
	<div class="container">
		<router-link to="/new_course"><button class="btn">新建班课</button></router-link>
		<div class="line">
			<div class="left"><h3>进行中的班课</h3></div>
	
		<div class="right"><h3>{{ courses.length }}个正在进行中的班课</h3></div>
		</div>
		<hr>
		<div class="course-conainer">
			<div class="course" v-for="(course, index) in courses" :key="index">
				<div class="course-cover">
					<router-link :to="'/course/' + course.courseId">
						<img :src="course.cover" />
					</router-link>
				</div>
				<div class="course-class">
					<p class="class">{{ course.courseClass }}</p>
				</div>
				<div class="course-name">
					
					<p class="title">{{ course.courseName }}</p>
				</div>
				<div class="my">
				
				<div class="course-code" v-if="loginUserId === course.userId">
					{{ course.courseCode }}
					
				</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
			name: 'Index',
	data() {
		return {
			loginUserId: 2,
			courses: [],
			courses1:[]
		};
	},
	methods: {
		deleteCourse: function(courseId,index) {
			var _this = this;
			this.$http({
				method: 'delete',
				url: 'http://localhost:8080/api/course/' + courseId
			}).then(function() {
				alert('班课删除成功');
				_this.courses1.splice(index,1);
			});
		}
	},
	created() {
		var _this = this;
		this.$http.get('http://localhost:8080/api/courses').then(function(response) {
			_this.courses = response.data;
		});
		this.$http.get('http://localhost:8080/api/courses1').then(function(response) {
			_this.courses1 = response.data;
		});
	}
};
</script>
<style scoped>
	.container {
	padding-top: 20px;
	width: 80%;
}
.line{
	display: flex;
	justify-content: space-between;
}
.left{
	font-size: 14px;
	color: #AAAAAA;
}
.course-conainer {
	
	display: flex;
	flex-wrap: wrap;
}
.course {
	margin-left: 1px;
	width: 233px;
	height: 322px;
	margin-right: 20px;
	border: 1px solid #fff;
	background-color: #fff;
	display: flex;
	flex-direction: column;
	padding-bottom: 40px;
}
.course-cover img {
	width: 100%;
	height: 220px;
}
.class{
	font-size: 14px;
	margin-left: 10px;
	
}
.title {
	font-size: 8px;
	color: #333;
}
.my{
	display: flex;
	justify-content: space-between;
	width: 233px;
	height: 40px;
}
.course-avatar{
	
}
img{
	width: 40px;
	height: 40px;
	border-radius: 10px;
}
.btn {
	width: 120px;
	height: 40px;
	border: 1px solid #fff;
	background-color: rgb(0, 187, 221);
	border-radius: 20px;
	outline: none;
	color: #fff;
	font-size: 16px;
}
.course-code {
	color: rgb(0, 187, 221);
}
</style>
