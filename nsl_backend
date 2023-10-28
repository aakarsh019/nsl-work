<script>
	let userInput = '';
	let results = [];
  
	const performDNSLookup = () => {
	  // Perform the DNS lookup here for various record types
	  const recordTypes = ['A', 'AAAA', 'MX', 'CNAME', 'TXT', 'NS', 'SOA', 'SRV'];
	  
	  // Create an array of promises to fetch DNS records for each type
	  const promises = recordTypes.map(recordType => {
		return fetch(`https://dns.google/resolve?name=${userInput}&type=${recordType}`)
		  .then(response => response.json())
		  .then(data => ({ recordType, data }))
		  .catch(error => ({ recordType, error: error.message }));
	  });
	  
	  // Execute all promises concurrently and store the results
	  Promise.all(promises)
		.then(records => {
		  results = records;
		});
	}
  </script>
  
  <main>
	<h1>DNS Lookup Tool</h1>
	<input bind:value={userInput} placeholder="Enter IP address or domain name" />
	<button on:click={performDNSLookup}>Lookup DNS</button>
	
	{#if results.length > 0}
	  <div>
		{#each results as { recordType, data, error }}
		  <h2>{recordType} Records</h2>
		  <pre>
			{#if error}
			  Error: {error}
			{:else}
			  {JSON.stringify(data, null, 2)}
			{/if}
		  </pre>
		{/each}
	  </div>
	{/if}
  </main>
  
