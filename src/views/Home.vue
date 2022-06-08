<template>
	<header id="header">
		<div class="container">
			<h1><a href="index.html">{{ h1 }}</a></h1>
			<!-- <a href="index.html" class="mr-auto"><img src="assets/logo.png" alt="" class="img-fluid"></a> -->
			<h2 v-html="dashText"></h2>
			<nav id="navbar" class="navbar">
				<ul>
					<li><a class="nav-link active" href="#header">Trang chủ</a></li>
					<li><a class="nav-link" href="#about">Giới Thiệu</a></li>
					<li><a class="nav-link" href="#resume">Học Vấn</a></li>
					<li><a class="nav-link" href="#services">Kinh Nghiệm</a></li>
					<li><a class="nav-link" href="#portfolio">Công Việc</a></li>
					<li><a class="nav-link" href="#contact">Liên Hệ</a></li>
				</ul>
				<i class="bi bi-list mobile-nav-toggle"></i>
			</nav>
			<div class="social-links">
				<a v-for="item in [...socials, ...dashUrls]" :href="item.href" target="_blank" :class="item.name"><i :class="item.icon"></i></a>
			</div>
		</div>
	</header>
	<section id="about" class="about">
		<div class="about-me container">
			<div class="section-title">
				<h2>Giới Thiệu</h2>
				<p>Giới Thiệu Chung Về Tôi</p>
			</div>
			<div class="row">
				<div class="col-lg-4" data-aos="fade-right">
					<img src="/me.jpg" class="img-fluid" alt="">
				</div>
				<div class="col-lg-8 pt-4 pt-lg-0 content" data-aos="fade-left">
					<h3>{{ position }}</h3>
					<p class="fst-italic">{{ overall }}</p>
					<div class="row">
						<div class="col-lg-6" v-for="cols in chevron">
							<ul>
								<li v-for="cvr in cols"><i class="bi bi-chevron-right"></i> <strong>{{ cvr.text }}:</strong> <span>{{ cvr.val }}</span></li>
							</ul>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="counts container">
			<div class="row">
				<div class="col-lg-3 col-md-6 mt-5 mt-lg-0" v-for="item in counts">
					<div class="count-box">
						<i :class="item.icon"></i>
						<span data-purecounter-start="0" :data-purecounter-end="item.count" data-purecounter-duration="1" class="purecounter"></span>
						<p>{{ item.text }}</p>
					</div>
				</div>
			</div>
		</div>
		<div class="skills container">
			<div class="section-title">
				<h2>Kỹ năng</h2>
			</div>
			<div class="row skills-content">
				<div class="col-lg-6" v-for="cols of skills">
					<div class="progress" v-for="skill in cols">
						<span class="skill">{{ skill.name }} <i class="val">{{ skill.val }}%</i></span>
						<div class="progress-bar-wrap">
							<div class="progress-bar" role="progressbar" :aria-valuenow="skill.val" aria-valuemin="0" aria-valuemax="100"></div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="interests container">
			<div class="section-title">
				<h2>Sở Thích</h2>
			</div>
			<div class="row">
				<div class="col-lg-3 col-md-4 mt-4" v-for="item in interests">
					<div class="icon-box">
						<i :class="item.icon" :style="'color:'+ item.color"></i>
						<h3>{{ item.text }}</h3>
					</div>
				</div>
			</div>
		</div>
	</section>
	<section id="resume" class="resume">
		<div class="container">
			<div class="section-title">
				<h2>Học Vấn</h2>
				<p>Quá trình và kết quả học tập</p>
			</div>
			<div class="row">
				<div class="col-lg-6" v-for="col in resume">
					<div v-for="groupItems in col">
						<h3 class="resume-title">{{ groupItems.group }}</h3>
						<div class="resume-item" v-for="info in groupItems.items">
							<h4>{{ info.title }}</h4>
							<h5 v-if="info.date">{{ info.date }}</h5>
							<p><em>{{ info.description }}</em></p>
							<p v-if="!Array.isArray(info.details)">{{ info.details }}</p>
							<p v-if="Array.isArray(info.details)">
								<ul>
									<li v-for="li in info.details">{{ li }}</li>
								</ul>
							</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
	<section id="services" class="services">
		<div class="container">
			<div class="section-title">
				<h2>Kinh Nghiệm</h2>
				<p>Các công việc đã và đang thực hiện</p>
			</div>
			<div class="row">
				<div class="col-lg-4 col-md-6 d-flex align-items-stretch mt-4" v-for="exp in experiences">
					<div class="icon-box">
						<div class="icon"><i :class="exp.icon"></i></div>
						<h4><a href="">{{ exp.title }}</a></h4>
						<p>{{ exp.text }}</p>
					</div>
				</div>
			</div>
		</div>
	</section>
	<section id="portfolio" class="portfolio">
		<div class="container">
			<div class="section-title">
				<h2>Công Việc</h2>
				<p>Các công việc đảm nhiệm</p>
			</div>
			<div class="row">
				<div class="col-lg-12 d-flex justify-content-center">
					<ul id="portfolio-flters">
						<li data-filter="*" class="filter-active">Tất cả</li>
						<li v-for="category in portfolio.cats" :data-filter="'.filter-' + category.toLowerCase()">{{ category }}</li>
					</ul>
				</div>
			</div>
			<div class="row portfolio-container">
				<div v-for="item in portfolio.list" :class="['col-lg-4', 'col-md-6', 'portfolio-item', 'filter-' + item.cat.toLowerCase()]">
					<div class="portfolio-wrap">
						<img :src="item.img" class="img-fluid" alt="">
						<div class="portfolio-info">
							<h4>{{ item.title }}</h4>
							<p>{{ item.text }}</p>
							<div class="portfolio-links">
								<a :href="item.img" data-gallery="portfolioGallery" class="portfolio-lightbox" :title="item.title"><i class="bx bx-plus"></i></a>
								<a v-if="item.details" :href="item.details" data-gallery="portfolioDetailsGallery" data-glightbox="type: external" class="portfolio-details-lightbox" :title="item.title"><i class="bx bx-link"></i></a>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
	<section id="contact" class="contact">
		<div class="container">
			<div class="section-title">
				<h2>Liên hệ</h2>
				<p>Hãy liên hệ với tôi thông qua</p>
			</div>
			<div class="row mt-2">
				<div class="col-md-6 mt-4 d-flex align-items-stretch" v-for="item in contact">
					<div class="info-box">
						<i :class="item.icon"></i>
						<h3>{{ item.title }}</h3>
						<p v-for="it in item.content" v-html="it"></p>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>
<script>
import infos from "../info.js";

export default {
	data() {
		return {
			...infos,
			portfolioLightbox: null,
			portfolioDetailsLightbox: null,
		};
	},
	mounted() {
		document.title = this.title;
		(function () {
			"use strict";

			/**
			 * Easy selector helper function
			 */
			const select = (el, all = false) => {
				el = el.trim();
				if (all) {
					return [...document.querySelectorAll(el)];
				} else {
					return document.querySelector(el);
				}
			};

			/**
			 * Easy event listener function
			 */
			const on = (type, el, listener, all = false) => {
				let selectEl = select(el, all);

				if (selectEl) {
					if (all) {
						selectEl.forEach((e) => e.addEventListener(type, listener));
					} else {
						selectEl.addEventListener(type, listener);
					}
				}
			};

			/**
			 * Scrolls to an element with header offset
			 */
			const scrollto = (el) => {
				window.scrollTo({
					top: 0,
					behavior: "smooth",
				});
			};

			/**
			 * Mobile nav toggle
			 */
			on("click", ".mobile-nav-toggle", function (e) {
				select("#navbar").classList.toggle("navbar-mobile");
				this.classList.toggle("bi-list");
				this.classList.toggle("bi-x");
			});

			/**
			 * Scrool with ofset on links with a class name .scrollto
			 */
			on(
				"click",
				"#navbar .nav-link",
				function (e) {
					let section = select(this.hash);
					if (section) {
						e.preventDefault();

						let navbar = select("#navbar");
						let header = select("#header");
						let sections = select("section", true);
						let navlinks = select("#navbar .nav-link", true);

						navlinks.forEach((item) => {
							item.classList.remove("active");
						});

						this.classList.add("active");

						if (navbar.classList.contains("navbar-mobile")) {
							navbar.classList.remove("navbar-mobile");
							let navbarToggle = select(".mobile-nav-toggle");
							navbarToggle.classList.toggle("bi-list");
							navbarToggle.classList.toggle("bi-x");
						}

						if (this.hash == "#header") {
							header.classList.remove("header-top");
							sections.forEach((item) => {
								item.classList.remove("section-show");
							});
							return;
						}

						if (!header.classList.contains("header-top")) {
							header.classList.add("header-top");
							setTimeout(function () {
								sections.forEach((item) => {
									item.classList.remove("section-show");
								});
								section.classList.add("section-show");
							}, 350);
						} else {
							sections.forEach((item) => {
								item.classList.remove("section-show");
							});
							section.classList.add("section-show");
						}

						scrollto(this.hash);
					}
				},
				true
			);

			/**
			 * Activate/show sections on load with hash links
			 */
			window.addEventListener("load", () => {
				if (window.location.hash) {
					let initial_nav = select(window.location.hash);

					if (initial_nav) {
						let header = select("#header");
						let navlinks = select("#navbar .nav-link", true);

						header.classList.add("header-top");

						navlinks.forEach((item) => {
							if (item.getAttribute("href") == window.location.hash) {
								item.classList.add("active");
							} else {
								item.classList.remove("active");
							}
						});

						setTimeout(function () {
							initial_nav.classList.add("section-show");
						}, 350);

						scrollto(window.location.hash);
					}
				}
			});

			/**
			 * Skills animation
			 */
			let skilsContent = select(".skills-content");
			if (skilsContent) {
				new Waypoint({
					element: skilsContent,
					offset: "80%",
					handler: function (direction) {
						let progress = select(".progress .progress-bar", true);
						progress.forEach((el) => {
							el.style.width = el.getAttribute("aria-valuenow") + "%";
						});
					},
				});
			}

			/**
			 * Porfolio isotope and filter
			 */
			window.addEventListener("load", () => {
				let portfolioContainer = select(".portfolio-container");
				if (portfolioContainer) {
					let portfolioIsotope = new Isotope(portfolioContainer, {
						itemSelector: ".portfolio-item",
						layoutMode: "fitRows",
					});

					let portfolioFilters = select("#portfolio-flters li", true);

					on(
						"click",
						"#portfolio-flters li",
						function (e) {
							e.preventDefault();
							portfolioFilters.forEach(function (el) {
								el.classList.remove("filter-active");
							});
							this.classList.add("filter-active");

							portfolioIsotope.arrange({
								filter: this.getAttribute("data-filter"),
							});
						},
						true
					);
				}
			});

			const portfolioLightbox = GLightbox({ selector: ".portfolio-lightbox", });
			const portfolioDetailsLightbox = GLightbox({ selector: ".portfolio-details-lightbox", width: "90%", height: "90vh", });
		})();

		(() => {
			let sources = [
				"/vendor/purecounter/purecounter.js",
			];
			for (let source of sources) {
				let scr = document.createElement("script");
				scr.src = source;
				document.body.appendChild(scr);
			}
		})();
	}
}
</script>