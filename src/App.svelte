<script>
	let playStatus = "play-outline";
	let groupPlayStatus = [
		"play-outline",
		"play-outline",
		"play-outline"
	];
	const numberOfLines = 80;
	let sizes = new Array(numberOfLines).fill(30);
	

	window.addEventListener("load", () => {
		const spectrumLines = document.getElementsByClassName("spectrum-line");
		setInterval(() => {
			for (let i = 0; i < spectrumLines.length; i++) {
				if (i == 1) continue;
				const max = 2;
				const min = 0;
				const random = Math.floor(Math.random() * (max - min + 1)) + min - (max / 2);
				for (let near = -5; near <= 5; near++) {
					const _near = i + near;
					const nearIndex = _near < 0 ? numberOfLines - (-_near % numberOfLines) : _near % numberOfLines;
					const target = spectrumLines[nearIndex];
					console.log(near);

					sizes[nearIndex] = Math.min(35, Math.max(18, sizes[nearIndex] + (random * (64 - near * near) / 64)));
					const size = sizes[nearIndex];
					target.style.width = `${size}%`;
					target.style.transformOrigin = `calc(100% + ${50 - size} / ${size} * 100%)`;
					target.style.transform = `rotate(calc(360deg / ${numberOfLines} * var(--i))) translate(calc(100% * (40 - ${size}) / ${size}))`;
				}
				
				// line.style.width = `${size}%`;
				// line.style.transformOrigin = `calc(100% + ${50 - size} / ${size} * 100%)`;
				// line.style.transform = `rotate(calc(360deg / ${numberOfLines} * var(--i))) translate(calc(100% * (40 - ${size}) / ${size}))`;
			}
		}, 50)
	});

	/**
	 * @returns {HTMLDivElement}
	 */
	const getMenu = () => {
		const menu = document.getElementById("menu");
		
		return menu;
	}
	
	/**
	 * @returns {HTMLDivElement}
	 */
	const getHighlight = () => {
		const highlight = document.getElementById("highlight");

		return highlight;
	}

	const clickPlayButton = () => {
		if (playStatus === "play-outline") playStatus = "stop-outline";
		else playStatus = "play-outline";
	}

	/**
	 * @param {MouseEvent} eventData 
	 */
	const clickGroupPlayButton = (eventData) => {
		const element = eventData.target;
		groupPlayStatus.forEach((_, index) => {
			if (!element.classList.contains(index.toString())) return;
			if (_ === "play-outline") groupPlayStatus[index] = "stop-outline";
			else groupPlayStatus[index] = "play-outline";
		});
	}

	const moveFxHighlightToRight = () => {
		const highlight = getHighlight();

		highlight.style.left = "calc(50% + 0.3vw)";
	}
	const moveFxHighlightToLeft = () => {
		const highlight = getHighlight();

		highlight.style.left = "0.3vw";
	}
	
	/**
	 * @param {MouseEvent} eventData 
	 */
	const openMenu = (eventData) => {
		/**
		 * @type {HTMLSpanElement}
		 */
		const menu = getMenu();
		const element = eventData.target;
		
		if (menu.style.left == "0px") {
			element.innerText = "menu";
			menu.style.left = "-25vw";
		}
		else {
			element.innerText = "close";
			menu.style.left = "0";
		}
	}
	
	/**
	 * @param {Event} eventData 
	 */
	const move = (eventData) => {
		const element = eventData.target;
		const slider = document.querySelector(`label[for="${element.id}"] > .slider`);
		
		slider.style.left = `${20 * element.value - 20}%`;
	}
	
	/**
	 * @param {MouseEvent} eventData 
	 */
	const lock = (eventData) => {
		/**
		 * @type {HTMLDivElement}
		 */
		const element = eventData.target;

		console.log("hi");

		if (element.getAttribute("name") == "lock-open-outline") element.setAttribute("name", "lock-closed-outline");
		else element.setAttribute("name", "lock-open-outline");
	}
</script>

<main>
	<div id="menu">
		<div id="user-ui">
			<div id="user-inform">
				<img src="../images/default-avatar.png" alt="" width="25px" id="avatar">
				<label for="avatar" id="avatar-text">로그인 해주세요.</label>
				<label for="avatar-text" id="login-text">Sign in</label>
			</div>
			<div id="button">
				<img src="../images/settings.svg" alt="" id="settings" width="17px">
				<img src="../images/close.svg" alt="" id="close" width="17px" on:mouseup={openMenu}>
			</div>
			<div id="signup-button">
				<label for="">Sign up</label>
			</div>
		</div>
	
		<div id="tools">
			<div class="tool">
				<img src="../images/pen.svg" alt="" width="20px">
				<label for="tool">Edit file</label>
			</div>
			<hr width="80%" color="#382C62">
			<div class="tool">
				<img src="../images/file.svg" alt="" width="20px">
				<label for="tool">Save file</label>
			</div>
			<hr width="80%" color="#382C62">
			<div class="tool">
				<img src="../images/music.svg" alt="" width="20px">
				<label for="tool">Load a song</label>
			</div>
			<hr width="80%" color="#382C62">
			<div class="tool">
				<img src="../images/community.svg" alt="" width="20px">
				<label for="tool">Community</label>
			</div>
			<hr width="80%" color="#382C62">
			<hr style="border: 0px; height: 1.1px; background: #382C62;" width="80%">
			<img src="../images/cantabile.png" alt="" width="30%" id="menu-logo">
		</div>
	</div>

	<nav>
		<section id="menu-section">
			<ion-icon name="menu-outline" id="menu-button" on:mouseup={openMenu}></ion-icon>
		</section>
		<section id="play-section">
			<!-- <span class="material-symbols-outlined" id="play-button" on:mouseup={clickPlayButton}>
				{playStatus}
			</span> -->
			<ion-icon name={playStatus} id="play-button" on:mouseup={clickPlayButton}></ion-icon>
		</section>
		<section id="undo-section">
			<ion-icon name="arrow-back-outline"></ion-icon>
			<ion-icon name="arrow-forward-outline"></ion-icon>
		</section>
		<section id="setting-section">
			<ion-icon name="earth-outline"></ion-icon>
		</section>
		

	</nav>

	<div id="station">
		<div id="work-station">
			<div id="lines">
				<div></div>
				<div></div>
				<div></div>
			</div>
			<div id="loop-station">
				<div style="--color: #b96bc6" id="fake">
					<div id="spectrum">
					</div>
					<div class="spectrum-line" style="--i: 0"></div>
					<div class="spectrum-line" style="--i: 1"></div>
					<div class="spectrum-line" style="--i: 2"></div>
					<div class="spectrum-line" style="--i: 3"></div>
					<div class="spectrum-line" style="--i: 4"></div>
					<div class="spectrum-line" style="--i: 5"></div>
					<div class="spectrum-line" style="--i: 6"></div>
					<div class="spectrum-line" style="--i: 7"></div>
					<div class="spectrum-line" style="--i: 8"></div>
					<div class="spectrum-line" style="--i: 9"></div>
					<div class="spectrum-line" style="--i: 10"></div>
					<div class="spectrum-line" style="--i: 11"></div>
					<div class="spectrum-line" style="--i: 12"></div>
					<div class="spectrum-line" style="--i: 13"></div>
					<div class="spectrum-line" style="--i: 14"></div>
					<div class="spectrum-line" style="--i: 15"></div>
					<div class="spectrum-line" style="--i: 16"></div>
					<div class="spectrum-line" style="--i: 17"></div>
					<div class="spectrum-line" style="--i: 18"></div>
					<div class="spectrum-line" style="--i: 19"></div>
					<div class="spectrum-line" style="--i: 20"></div>
					<div class="spectrum-line" style="--i: 21"></div>
					<div class="spectrum-line" style="--i: 22"></div>
					<div class="spectrum-line" style="--i: 23"></div>
					<div class="spectrum-line" style="--i: 24"></div>
					<div class="spectrum-line" style="--i: 25"></div>
					<div class="spectrum-line" style="--i: 26"></div>
					<div class="spectrum-line" style="--i: 27"></div>
					<div class="spectrum-line" style="--i: 28"></div>
					<div class="spectrum-line" style="--i: 29"></div>
					<div class="spectrum-line" style="--i: 30"></div>
					<div class="spectrum-line" style="--i: 31"></div>
					<div class="spectrum-line" style="--i: 32"></div>
					<div class="spectrum-line" style="--i: 33"></div>
					<div class="spectrum-line" style="--i: 34"></div>
					<div class="spectrum-line" style="--i: 35"></div>
					<div class="spectrum-line" style="--i: 36"></div>
					<div class="spectrum-line" style="--i: 37"></div>
					<div class="spectrum-line" style="--i: 38"></div>
					<div class="spectrum-line" style="--i: 39"></div>
					<div class="spectrum-line" style="--i: 40"></div>
					<div class="spectrum-line" style="--i: 41"></div>
					<div class="spectrum-line" style="--i: 42"></div>
					<div class="spectrum-line" style="--i: 43"></div>
					<div class="spectrum-line" style="--i: 44"></div>
					<div class="spectrum-line" style="--i: 45"></div>
					<div class="spectrum-line" style="--i: 46"></div>
					<div class="spectrum-line" style="--i: 47"></div>
					<div class="spectrum-line" style="--i: 48"></div>
					<div class="spectrum-line" style="--i: 49"></div>
					<div class="spectrum-line" style="--i: 50"></div>
					<div class="spectrum-line" style="--i: 51"></div>
					<div class="spectrum-line" style="--i: 52"></div>
					<div class="spectrum-line" style="--i: 53"></div>
					<div class="spectrum-line" style="--i: 54"></div>
					<div class="spectrum-line" style="--i: 55"></div>
					<div class="spectrum-line" style="--i: 56"></div>
					<div class="spectrum-line" style="--i: 57"></div>
					<div class="spectrum-line" style="--i: 58"></div>
					<div class="spectrum-line" style="--i: 59"></div>
					<div class="spectrum-line" style="--i: 60"></div>
					<div class="spectrum-line" style="--i: 61"></div>
					<div class="spectrum-line" style="--i: 62"></div>
					<div class="spectrum-line" style="--i: 63"></div>
					<div class="spectrum-line" style="--i: 64"></div>
					<div class="spectrum-line" style="--i: 65"></div>
					<div class="spectrum-line" style="--i: 66"></div>
					<div class="spectrum-line" style="--i: 67"></div>
					<div class="spectrum-line" style="--i: 68"></div>
					<div class="spectrum-line" style="--i: 69"></div>
					<div class="spectrum-line" style="--i: 70"></div>
					<div class="spectrum-line" style="--i: 71"></div>
					<div class="spectrum-line" style="--i: 72"></div>
					<div class="spectrum-line" style="--i: 73"></div>
					<div class="spectrum-line" style="--i: 74"></div>
					<div class="spectrum-line" style="--i: 75"></div>
					<div class="spectrum-line" style="--i: 76"></div>
					<div class="spectrum-line" style="--i: 77"></div>
					<div class="spectrum-line" style="--i: 78"></div>
					<div class="spectrum-line" style="--i: 79"></div>
					<div id="black"></div>
				</div>
				<div style="--color: #b96bc6"></div>
				<div style="--color: #b96bc6"></div>
				<div style="--color: #5696d8"></div>
				<div style="--color: #5696d8"></div>
				<div style="--color: #5696d8"></div>
				<div style="--color: #1fb5ad"></div>
				<div style="--color: #1fb5ad"></div>
				<div style="--color: #1fb5ad"></div>
			</div>
			<div id="group-player-section">
				<div class="group-player" style="--color: #b96bc6">
					<div class="group-player-header">
						<span>sound<br>group 1</span>
					</div>
					<div class="group-player-bottom">
						<ion-icon name={groupPlayStatus[0]} class="group-player-icon 0" on:mouseup={clickGroupPlayButton}></ion-icon>
						<span>play</span>
					</div>
				</div>
				<div class="group-player" style="--color: #5696d8">
					<div class="group-player-header">
						<span>sound<br>group 2</span>
					</div>
					<div class="group-player-bottom">
						<ion-icon name={groupPlayStatus[1]} class="group-player-icon 1" on:mouseup={clickGroupPlayButton}></ion-icon>
						<span>play</span>
					</div>
				</div>
				<div class="group-player" style="--color: #1fb5ad">
					<div class="group-player-header">
						<span>sound<br>group 3</span>
					</div>
					<div class="group-player-bottom">
						<ion-icon name={groupPlayStatus[2]} class="group-player-icon 2" on:mouseup={clickGroupPlayButton}></ion-icon>
						<span>play</span>
					</div>
				</div>
			</div>
		</div>
		<div id="effect-station">
			<header id="effect-station-header">
				<div id="speaker-button">
					<span class="material-symbols-outlined">
						volume_up
					</span>
					<span class="text">output</span>
				</div>
				<div id="fx-change-button">
					<div id="highlight"></div>
					<input type="radio" name="fx-change" id="fx-change" style="display: none" checked>
					<label for="fx-change" id="fx-button" on:mouseup={moveFxHighlightToLeft}>
						<span class="text">fx</span>
					</label>
					<input type="radio" name="fx-change" id="equalizer-change" style="display: none" checked>
					<label for="equalizer-change" id="equalizer-button" on:mouseup={moveFxHighlightToRight}>
						<span class="material-symbols-outlined">
							graphic_eq
						</span>
					</label>
				</div>
			</header>
			<div id="effect-body">
				<label for="pitch">
					<hr style="--i: 0">
					<hr style="--i: 1">
					<hr style="--i: 2">
					<hr style="--i: 3">
					<input id="pitch" type="range" min="1" max="5" value="1" on:input={move}>
					<div class="slider">
						<hr class="row">
						<hr class="column">
						<div class="text">
							pitch
						</div>
						<ion-icon name="lock-open-outline" on:mouseup={lock}></ion-icon>
						<ion-icon name="move-outline"></ion-icon>
					</div>
				</label>
				<label for="filter">
					<hr style="--i: 0">
					<hr style="--i: 1">
					<hr style="--i: 2">
					<hr style="--i: 3">
					<input id="filter" type="range" min="1" max="5" value="1" on:input={move}>
					<div class="slider">
						<hr class="row">
						<hr class="column">
						<div class="text">
							filter
						</div>
						<ion-icon name="lock-open-outline" on:mouseup={lock}></ion-icon>
						<ion-icon name="move-outline"></ion-icon>
					</div>
				</label>
				<label for="reverb">
					<hr style="--i: 0">
					<hr style="--i: 1">
					<hr style="--i: 2">
					<hr style="--i: 3">
					<input id="reverb" type="range" min="1" max="5" value="1" on:input={move}>
					<div class="slider">
						<hr class="row">
						<hr class="column">
						<div class="text">
							reverb
						</div>
						<ion-icon name="lock-open-outline" on:mouseup={lock}></ion-icon>
						<ion-icon name="move-outline"></ion-icon>
					</div>
				</label>
			</div>
		</div>
	</div>
</main>

<style>
	:root {
		--nav-color: #292146;
		--work-station-color: #0d0320;
		--effect-station-color: #352c61;

		--nav-height: 12vh
	}

	main {
		position: relative;
	}

	nav {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		align-items: center;

		height: var(--nav-height);

		background-color: var(--nav-color);

		z-index: 0;
	}
	
	nav > section {
		display: flex;
		flex-direction: row;
		
		position: relative;
		align-items: center;
	}

	nav ion-icon {
		font-size: calc(var(--nav-height) - 5vh);
		margin-left: 4vh;

		color: white;
	}

	#undo-section {
		justify-content: right;
	}

	#setting-section {
		justify-content: right;
		margin-right: 4vh;
	}

	.material-symbols-outlined {
		font-size: calc(var(--nav-height) - 6vh);
		margin-left: 4vh;
		
		color: white;
	}

	#station {
		display: grid;
		grid-template-rows: 1;
		grid-template-columns: 7fr 5fr;

		width: 100vw;
		height: calc(100vh - var(--nav-height));

		position: relative;
		z-index: 0;
	}
	
	#work-station {
		display: flex;
		flex-direction: row;
		
		justify-content: space-evenly;
		align-items: center;
		
		position: relative;
		overflow: hidden;
		
		background-color: var(--work-station-color);
	}

	#lines {
		display: grid;
		grid-template-rows: repeat(3, 1fr);

		width: 100%;
		height: 100%;

		background-color: transparent;

		position: absolute;

		left: 0;
		top: 0;
	}

	#lines > div {
		border-bottom: 1px solid #666;
	}

	#loop-station {
		display: grid;
		grid-template-rows: repeat(3, 1fr);
		grid-template-columns: repeat(3, 1fr);
		column-gap: 4vh;
		height: 100%;
		align-items: center;
		width: calc(100vh - var(--nav-height) + 2vh);
	}

	#loop-station > div {
		background-color: transparent;
		border-radius: 100%;
		border: 1px solid var(--color);
		transform: scale(0.95);
		aspect-ratio: 1 / 1;
	}

	#group-player-section {
		display: grid;
		grid-template-rows: repeat(3, 1fr);

		width: 6vw;
		height: calc(100vh - var(--nav-height));

		position: relative;
		align-items: center;
	}

	.group-player {
		display: grid;
		grid-template-rows: 4.5fr 5.5fr;

		width: 100%;
		height: 90%;

		background-color: #241a3e;
		border-radius: 10px;
		position: relative;
		overflow: hidden;
	}

	.group-player-header {
		display: flex;
		justify-content: center;
		align-items: center;
		
		width: 100%;
		height: 100%;

		text-align: center;
		text-transform: uppercase;
		font-size: 10px;
		color: white;

		background-color: var(--color);
	}

	.group-player-bottom {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;

		width: 100%;
		height: 100%;
	}

	.group-player-icon {
		position: relative;
		margin: 0;
		margin-top: 1.2vh;
		font-size: 22px;
		color: white;
	}

	.group-player-icon + span {
		text-transform: uppercase;
		font-size: 10px;
		color: white;
	}

	#effect-station {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: var(--effect-station-color);
	}

	#effect-station-header {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		margin-top: 2vw;

		width: 85%;
	}

	#effect-body {
		display: grid;
		grid-template-rows: repeat(3, 1fr);
		gap: 1vw;

		margin: 2vw 0;

		width: 85%;
		height: 100%;
	}

	#effect-body > label {

		position: relative;

		background: var(--nav-color);
		border-radius: 15px;
	}

	#effect-body > label > input {
		position: absolute;
		left: 7.5%;
		top: 0;
		
		width: 85%;
		height: 100%;

		opacity: 0;
	}

	#effect-body > label > hr {
		position: absolute;
		left: calc(20% * var(--i) + 20%);
		top: 25%;

		width: 1px;
		height: 50%;

		background: #ffffff55;
		border: none;
		margin: 0;
		padding: 0;
	}

	.slider {
		display: grid;
		grid-template-rows: 1fr 1fr;
		grid-template-columns: 1fr 1fr;
		justify-items: center;
		align-items: center;

		position: absolute;
		left: 0;
		top: 0;

		width: 20%;
		height: 100%;

		background: #231a3d;
		border-radius: 15px;
		border: 0.5px solid #ffffff99;

		color: white;
		text-transform: uppercase;
		font-size: 11px;

		transition: .2s;
	}

	.slider > ion-icon {
		font-size: 14px;

		transition: .2s;
	}

	.slider > ion-icon:hover {
		transform: scale(1.2);
	}

	.slider > .row {
		position: absolute;
		left: 0;
		top: calc(50% - 0.5px);
		margin: 0;

		width: 100%;
		height: 1px;

		background: #ffffff22;
		border: none;
	}

	.slider > .column {
		position: absolute;
		left: calc(50% - 0.5px);
		top: calc(50% + 1px);
		margin: 0;

		width: 1px;
		height: calc(50% - 1px);

		background: #ffffff22;
		border: none;
	}

	.slider > .text {
		grid-column: 1 / 3;

	}

	#speaker-button {
		display: flex;
		justify-content: row;
		align-items: center;
		gap: 0.3vw;

		color: white;
		text-transform: uppercase;
	}

	#effect-station .material-symbols-outlined {
		margin: 0;
	}
	
	#speaker-button > .text {
		font-size: 13px;
		font-weight: bold;
	}
	
	#fx-change-button {
		display: grid;
		position: relative;
		grid-template-columns: 1fr 1fr;
		align-items: center;
		justify-items: center;
		color: white;
		text-transform: uppercase;
		background-color: var(--nav-color);
		width: 10vw;
		height: 7vh;
		border-radius: 0.8vw;

	}

	#highlight {
		position: absolute;
		width: calc(50% - 0.6vw);
		height: calc(100% - 0.6vw);
		left: 0.3vw;
		top: 0.3vw;
		border-radius: 0.5vw;
		transition: left .2s ease;
		background-color: #7269ae;
		z-index: 0;
	}

	#fx-button, #equalizer-button {
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1;
	}

	#equalizer-button > span {
		font-size: 16px;
	}

	#fx-button > .text {
		font-size: 10px;
	}
	


	/* menu */

	#menu {
		position: absolute;
		left: -25vw;
		top: 0;
		transition: .5s ease;
		z-index: 1;
		background-color: #2F2749;
		width: 25vw;
		height: 100vh;
		border-radius: 0 1em 1em 0;
	}

	#user-ui {
		width: 100%;
		height: 25vh;
		background: linear-gradient(to top, #7A3C92, #30273F);
		border-radius: 0 1em 1em 0;
		margin-bottom: 3vh;
	}

	#avatar {
		position: absolute;
		left: 3vw;
		top: 6vh;
	}

	#avatar-text {
		color: #ffffff;
		font-family: NanumGothic;
		font-size: 8px;
		position: absolute;
		left: 3vw;
		top: 16.5vh;
	}

	#login-text {
		color: #cccccc;
		font-family: pretendard;
		font-size: 7px;
		position: absolute;
		left: 3vw;
		top: 20vh;
	}

	#signup-button {
		position: absolute;
		display: flex;
		justify-content: center;

		left: 19vw;
		top: 16vh;
		padding: 5px 10px;
		border: 1px solid #ffffff;
		border-radius: 50px;
	}

	#signup-button:active {
		transform: translateY(0.3vh);
	}

	#signup-button label {
		color: #ffffff;
		font-family: pretendard;
		font-size: 7px;
	}

	#button {
		position: absolute;
		left: 19.6vw;
		top: 4vh;
		transition: 0.3s;
	}


	#close, #settings {
		filter: invert(98%) sepia(67%) saturate(0%) hue-rotate(125deg) brightness(111%) contrast(101%);
	}

	#close:active, 
	#settings:active {
		/* animation-duration: 0.1s; */
		transform: translateY(0.3vh);
	}

	#tools {
		width: 100%;
	}

	.tool {
		display: flex;    
		flex-direction: row;
		align-items: center;
		height: 8vh;
	}

	.tool:active {
		opacity: 0.8;
	}

	.tool img {
		position: relative;
		left: 2.3vw;
	}

	.tool label {
		position: relative;
		font-family: NanumGothic;
		font-size: 9px;
		color: #ffffff;
		left: 3.5vw;
	}

	#menu-logo {
		position: relative;
		top: 9vh;
	}


	/* fake */

	#spectrum {
		position: relative;
		left: 25%;
		top: 25%;

		width: 50%;
		height: 50%;

		background: #ffffff22;
		border-radius: 50%;
	}

	.spectrum-line {

		position: absolute;
		width: 30%;
		height: 1px;


		background: rgb(255, 218, 251);
		transform-origin: calc(100% + 2 / 3 * 100%);
		transform: rotate(calc(360deg / 80 * var(--i))) translateX(calc(100% * 1 / 3));
		/* rotate(calc(360deg / 40 * var(--43i))) */
		/* translateX(calc(100% * 1 / 3)) */
	}

	#loop-station > div:nth-child(1) {
		box-shadow: 0 0 20px rgb(217, 0, 255);
	}

	#black {
		position: absolute;

		left: 50%;
		top: 50%;

		width: 50%;
		height: 50%;

		background: #000;

		transform: translate(-50%, -50%);
		border-radius: 100%;
	}
</style>