<template>
	<div>

		<nav class="navbar navbar-expand-lg navbar-dark bg-dark ">
			<div class="container">
				<!-- <a class="navbar-brand" href="#">Christian VUE Laravel</a> -->

				<router-link :to="{name: 'home'}" 
							class="navbar-brand">
					<strong>Christian VUE Laravel</strong>
				</router-link>
				<button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
					aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
					<span class="navbar-toggler-icon"></span>
				</button>
				<div class="collapse navbar-collapse" id="navbarNav">
					<ul class="navbar-nav">
						<li class="nav-item">
							<router-link class="nav-link" :to="{name:'home'}">Home</router-link>
						</li>
						<li class="nav-item">
							<router-link class="nav-link" :to="{name:'blog'}">Blog</router-link>
						</li>
					</ul>
				</div>
			</div>
		</nav>


		<transition name="slide-fade" mode="out-in">
			<!-- <router-view ::key="$route.fullPath"></router-view> -->
			<router-view :key="$route.path" />
		</transition>

	</div>
</template>


<script>

</script>