<script>
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';
	import { Happy1, Happy2, Neutral1, Neutral2, Sad1, Sad2 } from '$lib';

	$: mood = $page.url.searchParams.get('mood') || 'Neutral';

	let image1, image2;

	$: {
		switch (mood) {
			case 'Sad':
				image1 = Sad1;
				image2 = Sad2;
				break;
			case 'Neutral':
				image1 = Neutral1;
				image2 = Neutral2;
				break;
			case 'Happy':
				image1 = Happy1;
				image2 = Happy2;
				break;
		}
	}

	function retakeSurvey() {
		goto('/');
	}
</script>

<div class="flex min-h-screen flex-col items-center bg-gray-50 px-4 py-12 sm:px-6 lg:px-8">
	<div class="w-full max-w-7xl space-y-8">
		<h1 class="text-center text-4xl font-bold tracking-tight text-gray-900">
			Clothing Recommendation <span class="text-indigo-600">({mood})</span>
		</h1>

		<div class="flex flex-col items-center justify-center gap-6 sm:flex-row sm:gap-8">
			<div class="group relative">
				<img
					src={image1}
					alt="Recommendation 1"
					class="h-64 w-64 rounded-lg object-cover shadow-lg transition-transform duration-300 group-hover:scale-105"
				/>
			</div>
			<div class="group relative">
				<img
					src={image2}
					alt="Recommendation 2"
					class="h-64 w-64 rounded-lg object-cover shadow-lg transition-transform duration-300 group-hover:scale-105"
				/>
			</div>
		</div>

		<div class="flex justify-center">
			<button
				on:click={retakeSurvey}
				class="rounded-md bg-indigo-600 px-8 py-3 font-medium text-white shadow-sm
                       transition-colors duration-300 hover:bg-indigo-700 focus:outline-none focus:ring-2
                       focus:ring-indigo-500 focus:ring-offset-2"
			>
				Retake Survey
			</button>
		</div>
	</div>
</div>
