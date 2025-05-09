<script lang="ts">
  import { onMount } from 'svelte';

  let performanceAnalysis = `
    <div class="metrics-grid">
      <span class="metrics">5.07km</span>
      <span class="metrics">36:38</span>
      <span class="metrics">4:20/km</span>
      <span class="metrics">HR 170</span>
      <span class="metrics">↑ 30m</span>
    </div>
    <p>Strong performance with consistent pacing. Heart rate indicates good aerobic effort. Cadence could be improved for better efficiency.</p>
  `;

  let goalBasedInsight = `
    <p>Progress toward goals:</p>
    <ul class="compact-list">
      <li>✓ Consistent 4:20/km pace</li>
      <li>✓ Good HR management</li>
      <li>✓ Regular training</li>
    </ul>
  `;

  let option1 = {
    title: "Speed & Cadence",
    content: `
      <div class="workout-details">
        <span>6 × 800m @ 5k pace</span>
        <span>2min recovery</span>
        <span>Target: 3:45-4:00/km</span>
      </div>
    `
  };

  let option2 = {
    title: "Threshold Run",
    content: `
      <div class="workout-details">
        <span>30min @ threshold</span>
        <span>HR: 170-175</span>
        <span>Steady effort</span>
      </div>
    `
  };

  let option3 = {
    title: "Long Run",
    content: `
      <div class="workout-details">
        <span>90-120min easy</span>
        <span>HR: 150-160</span>
        <span>Conversational pace</span>
      </div>
    `
  };

  let advancedSuggestions = `
    <div class="tips-grid">
      <span>💪 2x weekly strength</span>
      <span>🔄 Rest between hard sessions</span>
      <span>🥤 Stay hydrated</span>
    </div>
  `;

  let emailContent: string;

  onMount(async () => {
    const response = await fetch('/email-template.html');
    emailContent = await response.text();
    
    emailContent = emailContent
      .replace('{{PERFORMANCE_ANALYSIS}}', performanceAnalysis)
      .replace('{{GOAL_BASED_INSIGHT}}', goalBasedInsight)
      .replace('{{OPTION_1_TITLE}}', option1.title)
      .replace('{{OPTION_1_CONTENT}}', option1.content)
      .replace('{{OPTION_2_TITLE}}', option2.title)
      .replace('{{OPTION_2_CONTENT}}', option2.content)
      .replace('{{OPTION_3_TITLE}}', option3.title)
      .replace('{{OPTION_3_CONTENT}}', option3.content)
      .replace('{{ADVANCED_SUGGESTIONS}}', advancedSuggestions);
  });
</script>

{#if emailContent}
  {@html emailContent}
{:else}
  <div class="loading">Loading template...</div>
{/if}

<style>
  .loading {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-size: 1.2rem;
    color: #666;
  }

  :global(.metrics-grid) {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 15px;
  }

  :global(.metrics) {
    display: inline-block;
    background-color: #f7f7fa;
    padding: 4px 8px;
    border-radius: 4px;
    font-weight: 500;
    font-size: 0.9rem;
  }

  :global(.compact-list) {
    margin: 0;
    padding-left: 20px;
  }

  :global(.compact-list li) {
    margin-bottom: 5px;
  }

  :global(.workout-details) {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  :global(.workout-details span) {
    background: #f7f7fa;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 0.9rem;
  }

  :global(.tips-grid) {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 10px;
    font-size: 0.9rem;
  }

  :global(.tips-grid span) {
    background: #f7f7fa;
    padding: 8px;
    border-radius: 4px;
    text-align: center;
  }
</style>