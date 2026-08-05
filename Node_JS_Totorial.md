<h1>How to Fetch a Full Kundali Report & Dynamic 5-Level Dasha Tree (Prana Dasha) with Node JS</h1>

<p>This complete step-by-step tutorial demonstrates how to set up, integrate, and build a full Vedic Astrology system using the <strong>Jyothisya API</strong> via RapidAPI. You will learn how to generate a complete Kundali report and dynamically calculate a <strong>5-Level Vimshottari Dasha Tree (down to Prana Dasha)</strong> in Node.js / JavaScript.</p>

<hr />

<h2>🎯 What You Will Learn</h2>
<ul>
  <li><strong>Step 1:</strong> Understanding the API architecture & dynamic 2-step dasha strategy.</li>
  <li><strong>Step 2:</strong> Configuring input birth parameters & headers.</li>
  <li><strong>Step 3:</strong> Fetching the core report & Level 1–3 Dashas (<code>/full-report</code>).</li>
  <li><strong>Step 4:</strong> Fetching Level 4 (Sookshma) & Level 5 (Prana) Dashas on-demand (<code>/dasha/sub-tree</code>).</li>
  <li><strong>Step 5:</strong> Complete production-ready Node.js code implementation.</li>
  <li><strong>Step 6:</strong> Practical Frontend/UI tree view rendering algorithm.</li>
</ul>

<hr />

<h2>🏗️ Step 1: Architectural Strategy (Two-Step On-Demand Fetching)</h2>

<p>Calculating 5 deep levels of Vimshottari Dashas upfront generates over <strong>10,000 sub-periods (~3MB+ JSON output)</strong>. Requesting all 5 levels in one single call causes unnecessarily slow HTTP responses and high mobile data usage.</p>

<p>To solve this, <strong>Jyothisya API</strong> employs an optimized <strong>Two-Step On-Demand Strategy</strong>:</p>

<ol>
  <li><strong>Primary Request (<code>/full-report</code>):</strong> Loads the birth chart, planetary positions, house cusps, yogas, panchang, and the top <strong>Level 1–3 Dasha tree</strong> (Maha &rarr; Antar &rarr; Pratyantar).</li>
  <li><strong>On-Demand Sub-Request (<code>/dasha/sub-tree</code>):</strong> When the user clicks to expand a specific Pratyantar node in the UI, an on-demand background call fetches <strong>Level 4 (Sookshma)</strong> and <strong>Level 5 (Prana)</strong> sub-periods for that specific branch.</li>
</ol>

<hr />

<h2>🔑 Step 2: API Input Parameters Reference</h2>

<p>Both API endpoints share the exact same standardized birth input parameter format:</p>

<table border="1" cellpadding="8" cellspacing="0" style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr style="background-color: #f2f2f2;">
      <th>Parameter</th>
      <th>Type</th>
      <th>Required</th>
      <th>Description & Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong><code>year</code>, <code>month</code>, <code>day</code></strong></td>
      <td>Integer</td>
      <td><strong>Yes</strong></td>
      <td>Date of birth (e.g. <code>1995</code>, <code>6</code>, <code>15</code>)</td>
    </tr>
    <tr>
      <td><strong><code>hour</code>, <code>minute</code>, <code>second</code></strong></td>
      <td>Integer</td>
      <td><strong>Yes</strong></td>
      <td>Time of birth in 24-hour format (e.g. <code>10</code>, <code>30</code>, <code>0</code>)</td>
    </tr>
    <tr>
      <td><strong><code>latitude</code>, <code>longitude</code></strong></td>
      <td>Float</td>
      <td><strong>Yes</strong></td>
      <td>Geographic coordinates (e.g. <code>6.9271</code>, <code>79.8612</code> for Colombo)</td>
    </tr>
    <tr>
      <td><strong><code>timezoneName</code></strong></td>
      <td>String</td>
      <td><strong>Yes</strong></td>
      <td>IANA Timezone string (e.g. <code>"Asia/Colombo"</code>, <code>"Asia/Kolkata"</code>, <code>"UTC"</code>)</td>
    </tr>
    <tr>
      <td><strong><code>lang</code></strong></td>
      <td>String</td>
      <td><strong>No</strong></td>
      <td>Output language: <code>"en"</code>, <code>"si"</code>, <code>"ta"</code>, <code>"hi"</code> (Default: <code>"en"</code>)</td>
    </tr>
    <tr>
      <td><strong><code>ayanamsa</code></strong></td>
      <td>String</td>
      <td><strong>No</strong></td>
      <td><code>"lahiri"</code>, <code>"kp"</code>, <code>"raman"</code>, <code>"tropical"</code> (Default: <code>"lahiri"</code>)</td>
    </tr>
    <tr>
      <td><strong><code>house_system</code></strong></td>
      <td>String</td>
      <td><strong>No</strong></td>
      <td><code>"sripati"</code>, <code>"whole_sign"</code>, <code>"placidus"</code> (Default: <code>"sripati"</code>)</td>
    </tr>
  </tbody>
</table>

<hr />

<h2>🚀 Step 3: Fetching Full Kundali & Level 1–3 Dashas</h2>

<p>Call the <strong><code>/full-report</code></strong> endpoint to retrieve the primary chart details alongside <strong>Level 1 to 3 Vimshottari Dashas</strong>.</p>

<p><strong>API Request Specification:</strong></p>
<ul>
  <li><strong>HTTP Method:</strong> <code>GET</code></li>
  <li><strong>Endpoint:</strong> <code>https://mindastro-api.p.rapidapi.com/api/v1/full-report</code></li>
  <li><strong>Headers:</strong>
    <ul>
      <li><code>x-rapidapi-key</code>: <strong>YOUR_RAPIDAPI_KEY</strong></li>
      <li><code>x-rapidapi-host</code>: <strong>mindastro-api.p.rapidapi.com</strong></li>
    </ul>
  </li>
</ul>

<hr />

<h2>🔍 Step 4: Fetching Level 4 (Sookshma) & Level 5 (Prana) Dashas On-Demand</h2>

<p>When a user interacts with your application UI to expand a Pratyantar Dasha node, send a <code>GET</code> request to <strong><code>/dasha/sub-tree</code></strong> passing the parent node's names:</p>

<p><strong>Sub-Tree Required Query Parameters:</strong></p>
<ul>
  <li>All standard birth parameters (<code>year</code>, <code>month</code>, <code>day</code>, <code>hour</code>, <code>minute</code>, <code>second</code>, <code>latitude</code>, <code>longitude</code>, <code>timezoneName</code>)</li>
  <li><strong><code>parent_maha</code>:</strong> Name of the parent Maha Dasha planet (e.g., <code>"Sun"</code>)</li>
  <li><strong><code>parent_antar</code>:</strong> Name of the parent Antar Dasha planet (e.g., <code>"Sun"</code>)</li>
  <li><strong><code>parent_pratyantar</code>:</strong> Name of the parent Pratyantar Dasha planet (e.g., <code>"Rahu"</code>)</li>
</ul>

<hr />

<h2>💻 Step 5: Complete Node.js / JavaScript Implementation</h2>

<p>Below is a complete, ready-to-run Node.js script utilizing <code>axios</code> to execute both Step 3 and Step 4 seamlessly.</p>

<pre><code class="language-javascript">const axios = require('axios');

// Configure your RapidAPI credentials
const RAPIDAPI_KEY = 'YOUR_RAPIDAPI_KEY_HERE';
const RAPIDAPI_HOST = 'mindastro-api.p.rapidapi.com';

// Standard birth parameters
const birthDetails = {
    year: 1995,
    month: 6,
    day: 15,
    hour: 10,
    minute: 30,
    second: 0,
    latitude: 6.9271,
    longitude: 79.8612,
    timezoneName: 'Asia/Colombo',
    lang: 'si',          // Language set to Sinhala
    ayanamsa: 'lahiri',
    house_system: 'sripati'
};

// Common HTTP headers for RapidAPI
const headers = {
    'x-rapidapi-key': RAPIDAPI_KEY,
    'x-rapidapi-host': RAPIDAPI_HOST
};

/**
 * Step 3 Execution: Fetch Full Astrology Report (Level 1–3 Dashas)
 */
async function getFullAstrologyReport() {
    try {
        console.log("Fetching Full Report & Level 1-3 Dashas...");
        const response = await axios.get(`https://${RAPIDAPI_HOST}/api/v1/full-report`, {
            params: birthDetails,
            headers: headers
        });

        const report = response.data.data;
        
        console.log("=== Primary Chart Info ===");
        console.log("Lagna Sign:", report.lagna.sign_translated);
        console.log("Active Yogas Count:", report.yogas.summary.total_count);
        console.log("Maha Dashas Loaded:", report.dasha.length);

        return report;
    } catch (error) {
        console.error("Error fetching full report:", error.response?.data || error.message);
    }
}

/**
 * Step 4 Execution: Fetch Level 4 (Sookshma) & Level 5 (Prana) Dashas On-Demand
 */
async function fetchPranaDashaTree(parentMaha, parentAntar, parentPratyantar) {
    try {
        console.log(`\nFetching Level 4 & 5 sub-tree for: ${parentMaha} -> ${parentAntar} -> ${parentPratyantar}...`);
        
        const subTreeParams = {
            ...birthDetails,
            parent_maha: parentMaha,
            parent_antar: parentAntar,
            parent_pratyantar: parentPratyantar
        };

        const response = await axios.get(`https://${RAPIDAPI_HOST}/api/v1/dasha/sub-tree`, {
            params: subTreeParams,
            headers: headers
        });

        const subTree = response.data.data;
        
        console.log("=== Sookshma & Prana Dasha Results ===");
        subTree.sookshma_dashas.forEach((sookshma, idx) => {
            console.log(`[Level 4 Sookshma ${idx + 1}] Lord: ${sookshma.planet_translated} (${sookshma.start_date} to ${sookshma.end_date})`);
            
            // Level 5 Prana Dashas
            sookshma.prana_dashas.forEach((prana, pIdx) => {
                console.log(`   └─ [Level 5 Prana ${pIdx + 1}] Lord: ${prana.planet_translated} (${prana.start_date} to ${prana.end_date})`);
            });
        });

        return subTree;
    } catch (error) {
        console.error("Error fetching Dasha sub-tree:", error.response?.data || error.message);
    }
}

/**
 * Master Execution Flow
 */
async function runAstrologyWorkflow() {
    // 1. Load initial Kundali report and Level 1-3 Dasha Tree
    const fullReport = await getFullAstrologyReport();

    // 2. Simulate user expanding a node in UI: e.g., Sun -> Sun -> Rahu
    if (fullReport) {
        await fetchPranaDashaTree('Sun', 'Sun', 'Rahu');
    }
}

runAstrologyWorkflow();
</code></pre>

<hr />

<h2>📄 Step 6: Expected JSON Response Structures</h2>

<h3>1. <code>/full-report</code> Payload Structure (Truncated Preview)</h3>

<pre><code class="language-json">{
  "status": "success",
  "lang": "si",
  "data": {
    "lagna": { 
      "sign": "Simha", 
      "sign_translated": "සිංහ", 
      "degree": 14.32 
    },
    "planets": [
      { 
        "name": "Sun", 
        "name_translated": "සූර්ය", 
        "sign": "Mithuna", 
        "sign_translated": "මිථුන", 
        "house": 11 
      }
    ],
    "dasha": [
      {
        "planet": "Sun",
        "planet_translated": "සූර්ය",
        "start_date": "1990-06-15",
        "end_date": "1996-06-15",
        "antar_dashas": [
          {
            "planet": "Sun",
            "planet_translated": "සූර්ය",
            "start_date": "1990-06-15",
            "end_date": "1990-10-03",
            "pratyantar_dashas": [
              {
                "planet": "Rahu",
                "planet_translated": "රාහු",
                "start_date": "1990-10-03",
                "end_date": "1990-11-20"
              }
            ]
          }
        ]
      }
    ]
  }
}
</code></pre>

<h3>2. <code>/dasha/sub-tree</code> Payload Structure (Level 4 Sookshma & Level 5 Prana)</h3>

<pre><code class="language-json">{
  "status": "success",
  "data": {
    "parent_maha": "Sun",
    "parent_antar": "Sun",
    "parent_pratyantar": "Rahu",
    "sookshma_dashas": [
      {
        "planet": "Jupiter",
        "planet_translated": "ගුරු",
        "start_date": "1990-10-03 12:00:00",
        "end_date": "1990-10-11 04:30:00",
        "prana_dashas": [
          {
            "planet": "Saturn",
            "planet_translated": "ශනි",
            "start_date": "1990-10-03 12:00:00",
            "end_date": "1990-10-05 08:15:00"
          }
        ]
      }
    ]
  }
}
</code></pre>

<hr />

<h2>🎨 Step 7: Frontend UI Implementation Workflow</h2>

<p>To construct an interactive 5-level expandable tree structure in React, Vue, or Web components:</p>

<ol>
  <li><strong>Render Top Levels (1–3):</strong> Map over <code>report.dasha</code> array retrieved from <code>/full-report</code> to display Maha, Antar, and Pratyantar Dasha list items.</li>
  <li><strong>Attach Click Handlers:</strong> Add an <code>onClick</code> or expand listener to every Pratyantar level list element.</li>
  <li><strong>Trigger Dynamic Fetching:</strong> When clicked, check if <code>sookshma_dashas</code> exist in local UI state. If not, trigger <code>fetchPranaDashaTree(parentMaha, parentAntar, parentPratyantar)</code> with a loading spinner.</li>
  <li><strong>Append to Tree:</strong> Inject the returned <code>sookshma_dashas</code> and nested <code>prana_dashas</code> dynamically under that clicked node.</li>
</ol>

<hr />

<h2>💡 Summary</h2>

<p>By adopting this <strong>2-step strategy</strong>:</p>
<ul>
  <li>Initial chart loading speed remains under <strong>10ms</strong>.</li>
  <li>Mobile payload size decreases from <strong>3MB+ down to ~15KB</strong>.</li>
  <li>End-users can access complete <strong>Prana Dasha precision</strong> instantly on-demand.</li>
</ul># mindastro-api_tutorial-docs
