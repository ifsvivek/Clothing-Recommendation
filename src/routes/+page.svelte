<script>
	import { goto } from '$app/navigation';

	const questions = [
		'How do you feel about your day?',
		'How energetic are you today?',
		'How calm are you?',
		'How stressed do you feel?',
		'How motivated are you?'
	];

	const options = [
		['Very Sad', 'Sad', 'Neutral', 'Happy'],
		['Very Tired', 'Tired', 'Energetic', 'Very Energetic'],
		['Very Agitated', 'Agitated', 'Calm', 'Very Calm'],
		['Overwhelmed', 'Stressed', 'Relaxed', 'Very Relaxed'],
		['Unmotivated', 'Less Motivated', 'Motivated', 'Very Motivated']
	];

	let selectedOptions = new Array(5).fill(null);

	function submitSurvey() {
		if (selectedOptions.some((opt) => opt === null)) return;

		const avgScore = selectedOptions.reduce((a, b) => a + b, 0) / selectedOptions.length;

		let mood;
		if (avgScore < 1.5) {
			mood = 'Sad';
		} else if (avgScore < 2.5) {
			mood = 'Neutral';
		} else {
			mood = 'Happy';
		}

		goto(`/recommendation?mood=${encodeURIComponent(mood)}`);
	}
</script>

<div class="min-h-screen bg-gray-50 px-4 py-12 sm:px-6 lg:px-8">
	<div class="mx-auto max-w-2xl rounded-xl bg-white p-6 shadow-md sm:p-8">
		<h1 class="mb-8 text-center text-3xl font-bold text-gray-900">Mood Survey</h1>

		{#each questions as question, index}
			<div class="mb-8 last:mb-6">
				<h3 class="mb-4 text-lg font-medium text-gray-900">{question}</h3>
				<div class="space-y-3">
					{#each options[index] as option, optionIndex}
						<label
							class="flex cursor-pointer items-center space-x-3 rounded-lg p-3 transition-colors hover:bg-gray-50"
						>
							<input
								type="radio"
								name={`question-${index}`}
								value={optionIndex}
								checked={selectedOptions[index] === optionIndex}
								on:change={() => (selectedOptions[index] = optionIndex)}
								class="h-4 w-4 border-gray-300 text-indigo-600 focus:ring-indigo-500"
							/>
							<span class="text-gray-700">{option}</span>
						</label>
					{/each}
				</div>
			</div>
		{/each}

		<button
			on:click={submitSurvey}
			disabled={selectedOptions.some((opt) => opt === null)}
			class="w-full rounded-md border border-transparent bg-indigo-600 px-4 py-3 text-lg font-medium text-white
                   shadow-sm transition-colors hover:bg-indigo-700 focus:outline-none focus:ring-2
                   focus:ring-indigo-500 focus:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50
                   disabled:hover:bg-indigo-600"
		>
			Submit Survey
		</button>
	</div>
</div>
