<script>
	let projects = $state([
		{
			title: 'project 1',
			description: 'explanation',
			image: 'pic'
		},
		{
			title: 'project 2',
			description: 'explanation',
			image: 'pic'
		}
	]);

	let titleName = $state('');
	let desc = $state('');
	let image = $state(''); // FIX (ASK BIG DADDY MATT), image holds an image not words

	let givePrompts = $state(false);

	function addProject() {
		projects.push({
			title: titleName,
			description: desc,
			image: image
		});
		givePrompts = false;
	}

	function handleShowForm() {
		givePrompts = true;
	}

	function handleDeleteProject(index) {
		projects.splice(index, 1);
	}
</script>

<div class="pt-5 text-center">
	<h1 style="font-size: 90px; color:white">Manraj's Portfolio</h1>
	<p class="lead" style="color: white">Computer Science Student @ CSUF</p>
</div>

<nav class="navbar navbar-expand-lg bg-body-tertiary">
	<div class="container-fluid">
		<div class="navbar-collapse justify-content-center collapse" id="navbarNav">
			<ul class="navbar-nav justify-content-center">
				<li class="nav-item">
					<a class="nav-link" style="font-size: 20px;" href="#">Home</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" style="font-size: 20px;" href="#projects">Projects</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" style="font-size: 20px;" href="#resume">Resume</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" style="font-size: 20px;" href="#socials">Socials</a>
				</li>
			</ul>
		</div>
	</div>
</nav>

<div id="about" class="py-3 container">
	<div class="row align-items-center">
		<div class="col-md-6">
			<h2 class="mb-4" style="color: white">About Me</h2>
			<p class="lead" style="color: white">
				My name is Manraj Chahal I am a computer science Student @ CSUF.
			</p>
			<p style="color: white">I enjoy blah blah b...</p>
		</div>
		<div class="col-md-6 text-center">
			<img
				src="/headshot.jpg"
				class="rounded-circle shadow"
				style="width:250px; height: 250px; object-fit: cover;"
			/>
		</div>
	</div>
</div>

<div id="projects " class="py-5 container">
	<h2 class="mt-1 text-center" style="color: white">Projects</h2>

	<div class="prompt d-flex justify-content-center mb-2 mt-3">
		{#if givePrompts}
			<input placeholder="Title" bind:value={titleName} />
			<input placeholder="Description" bind:value={desc} />
			<input placeholder="Image (text for now ask Matt)" bind:value={image} />
			<button type="button" class="btn btn-secondary" onclick={addProject}>Finish</button>
		{:else}
			<button type="button" class="btn btn-secondary" onclick={handleShowForm}>ADD PROJECT</button>
		{/if}
	</div>
	<div class="row justify-content-center">
		{#each projects as project, index}
			<div class="col-sm-12 col-md-6 col-lg-4 mb-4 d-flex justify-content-center">
				<div class="project-card">
					<img src="https://picsum.photos/200/300" class="project-img" alt="..." />
					<div class="card-body">
						<h1 class="m-3" style="color: white">{project.title}</h1>
						<p class="m-3" style="color: white">{project.description}</p>
						<button
							onclick={() => handleDeleteProject(index)}
							type="button"
							class="btn-close position-absolute bottom-0 end-0 m-2"
							aria-label="Close"
						></button>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div>
<div id="resume" class="mt-5 container">
	<h2 class="text-center" style="color: white">Resume</h2>
	<p style="color: white">Matt is a sexc boy that I want to touch</p>
</div>

<div id="socials" class="py-5 text-center" style="color: white">
	<h2 class="mb-4">Connect with me!</h2>

	<a href="https://www.linkedin.com/in/manraj-chahal-4508153b7/" style="margin:10px;">
		<img src="/linkedin.png" alt="LinkedIn" style="width:50px; height: 50px;" />
	</a>
	<a href="https://github.com/ManrajC5" style="margin:10px;">
		<img src="/githubIcon.jpg" alt="GitHub" style="width:50px; height: 50px;" />
	</a>
</div>

<style>
	:global(body) {
		background: linear-gradient(#1d2129, #0e1322);
		color: #fcfdfe;
	}

	.project-card {
		background: rgba(75, 72, 72, 0.337);
		backdrop-filter: blur(10px);
		border-radius: 15px;
		overflow: hidden;
		width: 100%;
		max-width: 300px;
		box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
		transition:
			transform 0.3s,
			box-shadow 0.3s;
	}

	.project-img {
		width: calc(100% - 20px);
		height: 180px;
		object-fit: cover;
		border-radius: 10px;
		margin: 10px;
	}
	.project-card:hover {
		transform: translateY(-8px);
		box-shadow: 0 15px 30px rgba(0, 0, 0, 0.7);
	}
</style>
