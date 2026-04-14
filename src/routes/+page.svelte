<script>
	import { onMount } from 'svelte';

	let activeSection = $state('home');

	onMount(() => {
		const sections = document.querySelectorAll('section[id]');
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						activeSection = entry.target.id;
					}
				}
			},
			{ threshold: 0.3 }
		);
		sections.forEach((s) => observer.observe(s));
		return () => observer.disconnect();
	});

	const projects = [
		{
			title: 'Web Application',
			description:
				'A full-stack web application built with modern technologies and best practices for scalable, maintainable code.',
			image: 'https://picsum.photos/seed/proj1/600/400',
			tags: ['Svelte', 'Node.js', 'Bootstrap']
		},
		{
			title: 'Data Visualizer',
			description:
				'Interactive data visualization dashboard with real-time updates and dynamic charts for insightful analytics.',
			image: 'https://picsum.photos/seed/proj2/600/400',
			tags: ['Python', 'R', 'D3.js']
		},
		{
			title: 'CLI Tool',
			description:
				'Command-line utility for automating development workflows and boosting productivity across teams.',
			image: 'https://picsum.photos/seed/proj3/600/400',
			tags: ['C++', 'Git', 'Linux']
		}
	];

	const skillCategories = [
		{ name: 'Languages', items: ['C++', 'JavaScript', 'Python', 'R'] },
		{ name: 'Frameworks', items: ['Svelte', 'Bootstrap', 'Node.js'] },
		{ name: 'Tools', items: ['Git/GitHub', 'VS Code', 'Linux', 'RStudio'] }
	];
</script>

<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark fixed-top portfolio-nav">
	<div class="container">
		<a class="navbar-brand logo-text" href="#home">Manraj Chahal</a>
		<button
			class="navbar-toggler border-0"
			type="button"
			data-bs-toggle="collapse"
			data-bs-target="#navMenu"
		>
			<span class="navbar-toggler-icon"></span>
		</button>
		<div class="navbar-collapse justify-content-end collapse" id="navMenu">
			<ul class="navbar-nav gap-1">
				{#each ['home', 'about', 'projects', 'skills', 'resume', 'contact'] as section}
					<li class="nav-item">
						<a class="nav-link px-3" class:active={activeSection === section} href="#{section}">
							{section.charAt(0).toUpperCase() + section.slice(1)}
						</a>
					</li>
				{/each}
			</ul>
		</div>
	</div>
</nav>

<!-- Hero -->
<section
	id="home"
	class="min-vh-100 d-flex align-items-center justify-content-center px-3 text-center"
>
	<div class="container">
		<p class="text-uppercase ls-wide accent-text fw-semibold mb-3">Hello, I'm</p>
		<h1 class="display-3 display-md-1 fw-bold mb-3 hero-name">Manraj Chahal</h1>
		<p class="lead text-secondary mb-4">Computer Science Student @ CSUF</p>
		<div class="accent-line mb-4 mx-auto"></div>
		<div class="d-flex gap-2 gap-sm-3 justify-content-center flex-wrap">
			<a href="#projects" class="btn btn-gradient px-3 px-sm-4">View Projects</a>
			<a
				href="/Manraj_Chahal_Resume.pdf"
				target="_blank"
				class="btn btn-outline-secondary px-3 px-sm-4"
			>
				Download Resume
			</a>
		</div>
	</div>
</section>

<!-- About -->
<section id="about" class="py-section">
	<div class="container">
		<div class="mb-5 text-center">
			<p class="section-label">ABOUT ME</p>
			<h2 class="display-5 fw-bold text-white">Get to know me</h2>
		</div>
		<div class="row align-items-center g-4 g-lg-5">
			<div class="col-lg-5 mb-4 mb-lg-0 text-center">
				<div class="photo-wrapper">
					<div class="photo-border"></div>
					<img src="/headshot.jpg" alt="Manraj Chahal" class="photo-img" />
				</div>
			</div>
			<div class="col-lg-7 text-lg-start text-center">
				<p class="text-secondary fs-6 fs-md-5 lh-lg">
					My name is Manraj Chahal, and I am a Computer Science Student at Cal State University of
					Fullerton. I'm passionate about building efficient projects and exploring new web
					technologies.
				</p>
				<p class="text-secondary fs-6 fs-md-5 lh-lg">
					I enjoy tackling complex problems and turning ideas into reality through clean,
					maintainable code. When I'm not coding, you can find me exploring the latest in tech or
					collaborating on exciting open-source projects.
				</p>
				<div class="d-flex gap-4 gap-sm-5 mt-4 justify-content-center justify-content-lg-start">
					<div>
						<h3 class="fw-bold accent-text mb-0">5+</h3>
						<small class="text-secondary">Projects</small>
					</div>
					<div>
						<h3 class="fw-bold accent-text mb-0">3+</h3>
						<small class="text-secondary">Technologies</small>
					</div>
					<div>
						<h3 class="fw-bold accent-text mb-0">2025</h3>
						<small class="text-secondary">Grad Year</small>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Projects -->
<section id="projects" class="py-section bg-darker">
	<div class="container">
		<div class="mb-5 text-center">
			<p class="section-label">PORTFOLIO</p>
			<h2 class="display-5 fw-bold text-white">Featured Projects</h2>
		</div>
		<div class="row g-4 justify-content-center">
			{#each projects as project}
				<div class="col-md-6 col-lg-4">
					<div class="project-card h-100">
						<img src={project.image} alt={project.title} class="project-card-img" />
						<div class="p-4">
							<h5 class="fw-semibold text-white mb-2">{project.title}</h5>
							<p class="text-secondary small mb-3">{project.description}</p>
							<div class="d-flex gap-2 flex-wrap">
								{#each project.tags as tag}
									<span class="tag-badge">{tag}</span>
								{/each}
							</div>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Skills -->
<section id="skills" class="py-section">
	<div class="container">
		<div class="mb-5 text-center">
			<p class="section-label">SKILLS</p>
			<h2 class="display-5 fw-bold text-white">Technologies I Work With</h2>
		</div>
		<div class="row g-4">
			{#each skillCategories as category}
				<div class="col-sm-6 col-md-4">
					<div class="skill-card">
						<h5 class="fw-semibold text-white mb-3">{category.name}</h5>
						<div class="gradient-divider mb-3"></div>
						<div class="d-flex gap-2 flex-wrap">
							{#each category.items as item}
								<span class="skill-tag">{item}</span>
							{/each}
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- Resume -->
<section id="resume" class="py-section bg-darker">
	<div class="container text-center">
		<p class="section-label">RESUME</p>
		<h2 class="display-5 fw-bold text-white mb-4">Education & Experience</h2>
		<p class="text-secondary fs-5 mb-4 mx-auto" style="max-width: 700px;">
			Aspiring Software Engineer with a focus on full stack development and problem solving.
			Currently pursuing a B.S. in Computer Science at California State University of Fullerton.
		</p>
		<a href="/Manraj_Chahal_Resume.pdf" target="_blank" class="btn btn-gradient btn-lg px-5">
			View Full Resume (PDF)
		</a>
	</div>
</section>

<!-- Footer / Contact -->
<section id="contact" class="py-5 bg-footer text-center">
	<div class="container">
		<h3 class="fw-semibold text-white mb-3">Let's Connect</h3>
		<p class="text-secondary mb-4">
			Feel free to reach out for collaborations or just a friendly hello!
		</p>
		<div class="d-flex justify-content-center gap-3 mb-4">
			<a
				href="https://www.linkedin.com/in/manraj-chahal-4508153b7/"
				class="social-circle"
				aria-label="LinkedIn"
			>
				<img src="/linkedin.png" alt="LinkedIn" width="22" height="22" />
			</a>
			<a href="https://github.com/ManrajC5" class="social-circle" aria-label="GitHub">
				<img src="/githubIcon.jpg" alt="GitHub" width="22" height="22" class="rounded" />
			</a>
		</div>
		<hr class="border-secondary mx-auto opacity-10" style="max-width: 300px;" />
		<p class="text-secondary small mt-3 mb-0">&copy; 2025 Manraj Chahal. All rights reserved.</p>
	</div>
</section>

<style>
	:global(body) {
		background: #0f172a;
		font-family:
			'Inter',
			'Segoe UI',
			system-ui,
			-apple-system,
			sans-serif;
		color: #e2e8f0;
		overflow-x: hidden;
	}

	/* -- Navbar -- */
	.portfolio-nav {
		background: rgba(15, 23, 42, 0.92);
		backdrop-filter: blur(16px);
		border-bottom: 1px solid rgba(255, 255, 255, 0.06);
		transition: background 0.3s;
	}

	.logo-text {
		font-family: 'Satisfy', cursive;
		font-weight: 400;
		font-style: normal;
		font-size: 1.5rem;
		background: linear-gradient(135deg, #3b82f6, #8b5cf6);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
	}

	.portfolio-nav .nav-link {
		color: #94a3b8;
		font-weight: 500;
		font-size: 0.9rem;
		transition: color 0.2s;
	}

	.portfolio-nav .nav-link:hover,
	.portfolio-nav .nav-link.active {
		color: #3b82f6;
	}

	/* -- Accent & Utilities -- */
	.accent-text {
		color: #3b82f6;
	}

	.ls-wide {
		letter-spacing: 0.35em;
		font-size: 0.95rem;
	}

	.section-label {
		color: #3b82f6;
		font-weight: 600;
		font-size: 0.8rem;
		letter-spacing: 0.35em;
		margin-bottom: 0.75rem;
	}

	.py-section {
		padding-top: 6rem;
		padding-bottom: 6rem;
	}

	.bg-darker {
		background: #0b0f1e;
	}

	.bg-footer {
		background: #080c18;
	}

	/* -- Hero -- */
	.hero-name {
		background: linear-gradient(180deg, #ffffff 30%, #94a3b8 100%);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
	}

	.accent-line {
		width: 120px;
		height: 4px;
		border-radius: 2px;
		background: linear-gradient(90deg, #3b82f6, #8b5cf6);
	}

	/* -- Buttons -- */
	.btn-gradient {
		background: linear-gradient(135deg, #3b82f6, #8b5cf6);
		color: #fff;
		border: none;
		font-weight: 600;
		border-radius: 8px;
		transition:
			transform 0.2s,
			box-shadow 0.2s;
	}

	.btn-gradient:hover {
		transform: translateY(-2px);
		box-shadow: 0 8px 24px rgba(59, 130, 246, 0.3);
		color: #fff;
	}

	.btn-outline-secondary {
		border-color: #94a3b8;
		color: #94a3b8;
		border-radius: 8px;
		font-weight: 600;
	}

	.btn-outline-secondary:hover {
		background: rgba(148, 163, 184, 0.1);
		border-color: #cbd5e1;
		color: #cbd5e1;
	}

	/* -- About Photo -- */
	.photo-wrapper {
		position: relative;
		display: inline-block;
	}

	.photo-border {
		position: absolute;
		top: 20px;
		left: 50%;
		transform: translateX(-45%);
		width: 100%;
		max-width: 300px;
		aspect-ratio: 6 / 7;
		border-radius: 16px;
		border: 2px solid transparent;
		background: linear-gradient(180deg, #3b82f6, #8b5cf6) border-box;
		-webkit-mask:
			linear-gradient(#fff 0 0) padding-box,
			linear-gradient(#fff 0 0);
		mask:
			linear-gradient(#fff 0 0) padding-box,
			linear-gradient(#fff 0 0);
		-webkit-mask-composite: xor;
		mask-composite: exclude;
	}

	.photo-img {
		position: relative;
		width: 100%;
		max-width: 300px;
		aspect-ratio: 6 / 7;
		object-fit: cover;
		border-radius: 16px;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
	}

	/* -- Project Cards -- */
	.project-card {
		background: rgba(30, 41, 59, 0.6);
		border: 1px solid rgba(255, 255, 255, 0.08);
		border-radius: 16px;
		overflow: hidden;
		transition:
			transform 0.3s,
			box-shadow 0.3s;
	}

	.project-card:hover {
		transform: translateY(-8px);
		box-shadow: 0 12px 32px rgba(0, 0, 0, 0.4);
	}

	.project-card-img {
		width: 100%;
		height: 200px;
		object-fit: cover;
	}

	.tag-badge {
		background: rgba(59, 130, 246, 0.15);
		color: #3b82f6;
		font-size: 0.75rem;
		font-weight: 500;
		padding: 0.3rem 0.75rem;
		border-radius: 20px;
	}

	/* -- Skill Cards -- */
	.skill-card {
		background: rgba(30, 41, 59, 0.4);
		border: 1px solid rgba(255, 255, 255, 0.06);
		border-radius: 16px;
		padding: 2rem;
		height: 100%;
	}

	.gradient-divider {
		height: 2px;
		background: linear-gradient(90deg, rgba(59, 130, 246, 0.6), transparent);
		border-radius: 1px;
	}

	.skill-tag {
		background: #0f172a;
		color: #94a3b8;
		border: 1px solid rgba(255, 255, 255, 0.1);
		font-size: 0.85rem;
		font-weight: 500;
		padding: 0.5rem 1rem;
		border-radius: 8px;
	}

	/* -- Social -- */
	.social-circle {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 48px;
		height: 48px;
		border-radius: 50%;
		background: rgba(255, 255, 255, 0.08);
		border: 1px solid rgba(255, 255, 255, 0.12);
		transition:
			transform 0.2s,
			background 0.2s;
	}

	.social-circle:hover {
		transform: scale(1.1);
		background: rgba(59, 130, 246, 0.2);
	}

	/* -- Navbar collapse on mobile -- */
	:global(.navbar-collapse) {
		background: rgba(15, 23, 42, 0.98);
		border-radius: 0 0 12px 12px;
		padding: 0.5rem 0;
	}

	@media (min-width: 992px) {
		:global(.navbar-collapse) {
			background: transparent;
			padding: 0;
		}
	}

	/* -- Smooth scroll offset for fixed nav -- */
	:global(html) {
		scroll-behavior: smooth;
		scroll-padding-top: 80px;
	}

	/* -- Mobile responsive -- */
	@media (max-width: 767.98px) {
		.py-section {
			padding-top: 3.5rem;
			padding-bottom: 3.5rem;
		}

		.hero-name {
			font-size: 2.5rem;
		}

		.ls-wide {
			letter-spacing: 0.2em;
			font-size: 0.8rem;
		}

		.photo-border {
			top: 15px;
			max-width: 220px;
		}

		.photo-img {
			max-width: 220px;
		}

		.project-card-img {
			height: 160px;
		}

		.skill-card {
			padding: 1.5rem;
		}
	}

	@media (min-width: 768px) and (max-width: 991.98px) {
		.hero-name {
			font-size: 3.5rem;
		}

		.photo-border {
			max-width: 260px;
		}

		.photo-img {
			max-width: 260px;
		}
	}
</style>
