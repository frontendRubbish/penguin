<script lang="ts">

	let rightAnimation: boolean;
	let wrongAnimation: boolean;
	let showMessage = '';

	export function startRight() {
		rightAnimation = true;
		wrongAnimation = false;
		showMessage = 'Gut gemacht!';

		setTimeout( () => {
			rightAnimation = false;
		}, 800);

		setTimeout( () => {
			showMessage = '';
		}, 1200);
	}

	export function startWrong() {
		rightAnimation = false;
		wrongAnimation = true;
		showMessage = 'ups!';

		setTimeout( () => {
			wrongAnimation = false;
		}, 260);

		setTimeout( () => {
			showMessage = '';
		}, 800);
	}
</script>

<style>
@keyframes wiggle {
  0% {transform: rotateZ(0);}
  25% {transform: rotateZ(10deg)}
	50% {transform: rotateZ(0);}
  75% {transform: rotateZ(-10deg)}
	100% {transform: rotateZ(0);}
}

@keyframes cringe {
  0% {transform: scaleY(1);}
	50% {transform: scaleY(0.8);}
  100% {transform: scaleY(1);}
}

.penguin {
	position: relative;
}

.penguin .penguin__eye {
	opacity: 1;
}

.penguin .penguin__cheek,
.penguin .penguin__eye--right,
.penguin .penguin__eye--wrong {
	opacity: 0;
}

.penguin__eye {
	transition: opacity 240ms;
}
.penguin__cheek {
	transition: opacity 400ms;
}

.penguin--right {
	animation-name: wiggle;
  animation-duration: 200ms;
	animation-iteration-count: 4;
	transform: rotateZ(0);
}

.penguin--right .penguin__eye,
.penguin--wrong .penguin__eye {
	opacity: 0;
}

.penguin--right .penguin__eye--right {
	opacity: 1;
}

.penguin--right .penguin__cheek {
	opacity: 0.3;
}

.penguin--wrong {
	animation-name: cringe;
  animation-duration: 150ms;
	animation-delay: 50ms;
	animation-iteration-count: 1;
	transform: scaleY(1);
	transform-origin: bottom;
}

.penguin--wrong .penguin__eye--wrong {
	opacity: 1;
}

</style>

<div class="relative">
	{#if showMessage !== ''}
		<div class="absolute border-2 border-black bg-white rounded-full -right-2 p-2 text-xl">
			{showMessage}
		</div>
	{/if}
	<div class="penguin" class:penguin--right={rightAnimation} class:penguin--wrong={wrongAnimation}>
		<svg version="1.1" id="Layer_1" x="0px" y="0px" viewBox="0 0 864 864" xml:space="preserve">

		<path fill-rule="evenodd" clip-rule="evenodd" fill="#FFE500" d="M407.417,339.05c-17.105-2.285-31.119-9.324-40.922-22.996
			c-2.344-3.268-2.945-9.029-2.062-13.154c4.178-19.53,14.376-35.8,29.081-49.226c9.124-8.33,18.043-9,27.533-1.044
			c16.049,13.456,25.517,31.126,30.408,51.299c0.496,2.05,0.034,4.793-0.98,6.676C441.149,327.895,426.271,336.756,407.417,339.05z"/>
		<g>
			<path d="M373.31,24.862c17.101,0,34.202,0,51.303,0c11.208,1.305,22.463,2.294,33.615,3.971 
				c43.212,6.497,82.654,22.05,116.928,49.627c43.604,35.084,70.673,81.508,90.523,132.775
				c17.466,45.114,27.804,92.067,36.037,139.606c7.021,40.544,24.779,75.456,56.059,103.02c4.665,4.111,7.935,9.807,11.85,14.77
				c0,2.565,0,5.131,0,7.696c-4.078,9.404-11.069,15.264-20.944,18.174c-6.729,1.983-13.257,4.69-19.798,7.268
				c-19.138,7.542-33.46,19.099-36.646,41.212c-1.45,10.063-4.699,19.894-7.447,29.741c-9.464,33.896-19.266,67.683-36.965,98.491
				c-17.031,29.641-40.101,52.515-72.948,64.041c-10.567,3.707-21.478,6.435-32.641,9.731c2.942,1.569,5.649,2.809,8.134,4.396
				c2.508,1.602,4.944,3.385,7.149,5.378c7.534,6.815,7.856,12.952-0.437,18.948c-6.617,4.785-14.16,9.702-21.936,11.184
				c-16.681,3.179-33.748,4.497-50.709,5.979c-17.494,1.528-33.826-3.352-49.386-10.896c-8.808-4.271-16.417-9.657-12.553-21.805
				c-1.684,0-2.727,0-3.769,0c-3.818,0-7.636,0-11.67,0c3.237,9.382,2.271,13.571-5.653,18.991c-5.397,3.691-11.26,7.415-17.464,9.088
				c-24.308,6.556-49.223,9.36-74.135,5.143c-11.124-1.882-22.081-6.541-32.285-11.607c-12.536-6.226-13.15-15.896-2.971-25.469
				c1.041-0.979,2.067-1.973,3.746-3.579c-4.704-0.971-8.596-2.001-12.554-2.554c-36.645-5.119-65.436-23.076-87.448-52.632
				c-14.366-19.29-25.885-40.133-35.549-62.064c-13.45-30.526-22.762-62.423-30.818-94.694c-4.02-16.102-14.051-24.23-30.225-26.932
				c-9.047-1.51-18.736-3.887-26.228-8.789c-9.241-6.047-16.498-15.127-24.611-22.896c0-2.138,0-4.275,0-6.413
				c5.708-7.332,14.118-10.077,22.425-12.619c9.074-2.776,16.003-8.072,20.67-16.087c3.95-6.783,7.782-13.739,10.675-21.013
				c12.005-30.18,15.643-62.272,20.672-94.01c6.138-38.731,12.905-77.318,24.541-114.859c11.497-37.096,28.259-71.227,55.693-99.482
				c19.939-20.536,42.971-37.04,66.919-52.354c27.933-17.862,57.728-31.083,91.094-34.885
				C353.479,27.321,363.391,26.062,373.31,24.862z M628.209,432.421c-0.924-47.901-4.447-95.569-12.581-142.788
				c-6.494-37.698-15.476-74.771-33.362-108.971c-10.803-20.658-24.24-39.185-45.301-50.928c-11.279-6.289-22.829-7.251-34.336-1.775
				c-8.239,3.922-15.979,8.964-23.704,13.878c-18.719,11.904-37.431,23.829-55.87,36.158c-7.104,4.75-13.482,4.091-20.189-0.059
				c-2.538-1.57-5.19-3.013-7.515-4.861c-13.362-10.628-26.507-21.531-39.975-32.023c-31.055-24.191-63.482-24.367-94.332,0.047
				c-20.167,15.96-34.913,36.569-44.186,60.341c-24.179,61.976-37.815,126.542-43.482,192.691c-3.285,38.346-3.22,76.815,2.363,115.07
				c5.624,38.529,15.977,75.508,36.896,108.806c23.687,37.702,56.276,63.93,100.044,74.47c45.143,10.87,90.733,18.604,137.506,14.788
				c30.161-2.461,58.842-9.783,84.718-26.095c33.19-20.922,54.28-51.488,67.91-87.433
				C622.507,541.803,629.891,487.781,628.209,432.421z"/>
			

				<circle cx="482.522" cy="220" r="24" class="penguin__eye" />
				<circle cx="321.96" cy="220" r="24" class="penguin__eye" />

				<line x1="303" y1="230" x2="341" y2="230" stroke="#000000" stroke-width="20" class="penguin__eye penguin__eye--wrong"/>
				<line x1="464" y1="230" x2="502" y2="230" stroke="#000000" stroke-width="20" class="penguin__eye penguin__eye--wrong"/>

				<path d="M 303 230 C 303 190, 341 190, 341 230" stroke="#000000" stroke-width="1" class="penguin__eye penguin__eye--right"/>
				<path d="M 464 230 C 464 190, 502 190, 502 230" stroke="#000000" stroke-width="1" class="penguin__eye penguin__eye--right"/>

				<circle cx="522.522" cy="320" r="50" fill="#fc92b0" class="penguin__cheek"/>
				<circle cx="296" cy="320" r="50" fill="#fc92b0" class="penguin__cheek"/>

			</g>
		</svg>
	</div>
</div>