<script>
	let playStatus = "play_circle";
	let groupPlayStatus = [
		"play_arrow",
		"play_arrow",
		"play_arrow"
	]

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
		if (playStatus === "play_circle") playStatus = "stop_circle";
		else playStatus = "play_circle";
	}

	/**
	 * @param {MouseEvent} eventData 
	 */
	const clickGroupPlayButton = (eventData) => {
		const element = eventData.target;
		groupPlayStatus.forEach((_, index) => {
			if (!element.classList.contains(index.toString())) return;
			if (_ === "play_arrow") groupPlayStatus[index] = "stop";
			else groupPlayStatus[index] = "play_arrow";
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
				<img src="../images/close.svg" alt="" id="close" width="17px">
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
			<span class="material-symbols-outlined" id="menu-button" on:mouseup={openMenu}>
				menu
			</span>
		</section>
		<section id="play-section">
			<span class="material-symbols-outlined" id="play-button" on:mouseup={clickPlayButton}>
				{playStatus}
			</span>
		</section>
		<section id="undo-section">
			<span class="material-symbols-outlined">
				undo
			</span>
			<span class="material-symbols-outlined">
				redo
			</span>
		</section>
		<section id="setting-section">
			<span class="material-symbols-outlined">
				public
			</span>
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
				<div style="--color: #b96bc6"></div>
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
						<span class="material-symbols-outlined group-player-icon 0" on:mousedown={clickGroupPlayButton}>
							{groupPlayStatus[0]}
						</span>
						<span>play</span>
					</div>
				</div>
				<div class="group-player" style="--color: #5696d8">
					<div class="group-player-header">
						<span>sound<br>group 2</span>
					</div>
					<div class="group-player-bottom">
						<span class="material-symbols-outlined group-player-icon 1" on:mousedown={clickGroupPlayButton}>
							{groupPlayStatus[1]}
						</span>
						<span>play</span>
					</div>
				</div>
				<div class="group-player" style="--color: #1fb5ad">
					<div class="group-player-header">
						<span>sound<br>group 3</span>
					</div>
					<div class="group-player-bottom">
						<span class="material-symbols-outlined group-player-icon 2" on:mousedown={clickGroupPlayButton}>
							{groupPlayStatus[2]}
						</span>
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

	#menu-section {
		z-index: 1;
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
		height: 45%;

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
		height: fit-content;
	}

	.group-player-icon {
		position: relative;
		margin: 0;
		margin-top: 1.2vh;
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
</style>