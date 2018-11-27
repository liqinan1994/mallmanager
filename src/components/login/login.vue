<template>
	<div class="login-wrap">
		<el-form class="login-form" label-position="top" label-width="80px" :model="formData">
			<h2>登录</h2>
		  <el-form-item label="名字">
		    <el-input v-model="formData.username"></el-input>
		  </el-form-item>
		  <el-form-item label='密码'>
		    <el-input v-model="formData.password"></el-input>
		  </el-form-item>
		  <el-button type="success" class="login-btn" @click="handleLogin">登录</el-button>
		</el-form>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				formData: {
					username: '',
					password: ''
				}
			}
		},
		methods: {
			async handleLogin() {
				var res = await this.$http.post('login',this.formData)

				console.log(res);
				const {meta:{status,msg},data} = res.data;

				if(status == 200) {
					const token = localStorage.setItem('token',data.token)
					this.$router.push({
						name: 'home'
					});
					this.$message.success(msg)
				} else {
					this.$message.warning(msg)
				}

			}
		}
	};
</script>

<style>
	.login-wrap {
		height: 100%;
		background-color: #324152;
		display: flex;
		justify-content: center;
		align-items: center;

	}
	.login-wrap .login-form {
		width: 400px;
		background-color: #fff;
		border-radius: 5px;
		padding: 30px; 
	}
	.login-wrap .login-btn {
		width: 100%;

	}
</style>