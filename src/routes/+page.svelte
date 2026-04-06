<script>
	let projects = $state([
		{
			title: 'Project 1',
			description: 'A cool app I built.',
			image: 'https://picsum.photos/300/200'
		}
	]);

	let titleName = $state('');
	let desc = $state('');
	let imageUrl = $state('');

	let givePrompts = $state(false);

	function addProject() {
		if (titleName && desc) {
			projects.push({
				title: titleName,
				description: desc,
				image: imageUrl || 'https://picsum.photos/300'
			});
			titleName = '';
			desc = '';
			imageUrl = '';
			givePrompts = false;
		}
	}

	function handleDeleteProject(index) {
		projects.splice(index, 1);
	}
</script>

<div class="py-5 text-white text-center">
	<h1 class="display-1 fw-bold">Manraj's Portfolio</h1>
	<p class="lead">Computer Science Student @ CSUF</p>
</div>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark sticky-top shadow-sm">
	<div class="container-fluid">
		<div class="navbar-collapse justify-content-center">
			<ul class="navbar-nav">
				<li class="nav-item"><a class="nav-link px-3" href="#">Home</a></li>
				<li class="nav-item"><a class="nav-link px-3" href="#projects">Projects</a></li>
				<li class="nav-item"><a class="nav-link px-3" href="#resume">Resume</a></li>
				<li class="nav-item"><a class="nav-link px-3" href="#socials">Socials</a></li>
			</ul>
		</div>
	</div>
</nav>

<div id="about" class="py-5 text-white container">
	<div class="row align-items-center">
		<div class="col-md-6">
			<h2 class="mb-4 border-bottom pb-2">About Me</h2>
			<p class="lead">
				My name is Manraj Chahal, and I am a Computer Science Student at Cal State University of
				Fullerton.
			</p>
			<p class="text-secondary">
				I'm passionate about building efficient projects and exploring new web technologies.
			</p>
		</div>
		<div class="col-md-6 text-center">
			<img
				src="/headshot.jpg"
				alt="Manraj"
				class="rounded-circle shadow-lg border-secondary border border-3"
				style="width:250px; height: 250px; object-fit: cover;"
			/>
		</div>
	</div>
</div>

<div id="projects" class="pb-5 text-white container">
	<div class="row justify-content-center text-center">
		<h2 class="mb-4 display-5 fw-bold">My Projects</h2>

		<div class="d-flex justify-content-center mb-5">
			{#if givePrompts}
				<div class="card p-4 bg-dark border-secondary w-100" style="max-width: 500px;">
					<input class="form-control mb-2" placeholder="Project Title" bind:value={titleName} />
					<textarea class="form-control mb-2" placeholder="Description" bind:value={desc}
					></textarea>
					<input class="form-control mb-3" placeholder="Image URL" bind:value={imageUrl} />
					<div class="d-flex gap-2">
						<button type="button" class="btn btn-primary w-100" onclick={addProject}
							>Add Project</button
						>
						<button
							type="button"
							class="btn btn-outline-light"
							onclick={() => (givePrompts = false)}>Cancel</button
						>
					</div>
				</div>
			{:else}
				<button
					type="button"
					class="btn btn-lg btn-outline-light"
					onclick={() => (givePrompts = true)}>+ ADD PROJECT</button
				>
			{/if}
		</div>

		<div class="row justify-content-center">
			{#each projects as project, index}
				<div class="col-sm-12 col-md-6 col-lg-4 mb-4 d-flex justify-content-center">
					<div class="project-card position-relative">
						<img src={project.image} class="project-img" alt={project.title} />
						<div class="p-3 text-white">
							<h3 class="h5">{project.title}</h3>
							<p class="small opacity-75">{project.description}</p>
							<button
								onclick={() => handleDeleteProject(index)}
								class="btn-close btn-close-white position-absolute top-0 end-0 m-2"
								aria-label="Delete"
							></button>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</div>

<div id="resume" class="pb-5 text-white container">
	<div class="row justify-content-center text-center">
		<div class="col-lg-8">
			<h2 class="mb-4 display-5 fw-bold">Resume</h2>
			<p class="lead mb-4">
				Aspiring Software Engineer with a focus on full stack development and problem solving.
				Currently pursuing a B.S. in Computer Science at California State University of Fullerton.
			</p>

			<div class="mb-5">
				<span class="badge rounded-pill bg-primary px-3 py-2 m-1">C++</span>
				<span class="badge rounded-pill bg-info text-dark px-3 py-2 m-1">JavaScript</span>
				<span class="badge rounded-pill bg-secondary px-3 py-2 m-1">Python</span>
				<span class="badge rounded-pill bg-warning text-dark px-3 py-2 m-1">Svelte</span>
				<span class="badge rounded-pill bg-dark border-light px-3 py-2 m-1 border">Git/GitHub</span>
				<span class="badge rounded-pill bg-danger text-dark px-3 py-2 m-1">R/RStudio</span>
			</div>

			<div class="d-grid gap-3 d-sm-flex justify-content-sm-center">
				<a href="/Manraj_Chahal_Resume.pdf" target="_blank" class="btn btn-primary btn-lg px-5">
					View Full Resume (PDF)
				</a>
				<a href="" class="btn btn-outline-light btn-lg px-5"> Contact Me </a>
			</div>
		</div>
	</div>
</div>

<div id="socials" class="py-5 text-white bg-black bg-opacity-25 text-center">
	<h2 class="mb-4">Connect with me!</h2>
	<div class="d-flex justify-content-center gap-4">
		<a href="https://www.linkedin.com/in/manraj-chahal-4508153b7/" class="social-icon">
			<img src="/linkedin.png" alt="LinkedIn" width="40" height="40" />
		</a>
		<a href="https://github.com/ManrajC5" class="social-icon">
			<img src="/githubIcon.jpg" alt="GitHub" width="40" height="40" class="rounded" />
		</a>
	</div>
</div>

<style>
	:global(body) {
		background: linear-gradient(135deg, #1d2129, #0e1322);
		background-attachment: fixed;
		min-height: 100vh;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}

	.project-card {
		background: rgba(255, 255, 255, 0.05);
		backdrop-filter: blur(12px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 15px;
		overflow: hidden;
		width: 100%;
		transition:
			transform 0.3s ease,
			box-shadow 0.3s ease;
	}

	.project-card:hover {
		transform: translateY(-10px);
		box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
	}

	.project-img {
		width: 100%;
		height: 200px;
		object-fit: cover;
	}

	.social-icon {
		transition: transform 0.2s;
	}

	.social-icon:hover {
		transform: scale(1.2);
	}
</style>
