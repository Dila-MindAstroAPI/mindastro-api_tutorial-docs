<h1>How to Fetch a Full Kundali Report & Dynamic 5-Level Dasha Tree (Prana Dasha) in Dart / Flutter</h1>

<p>This complete step-by-step integration guide demonstrates how to seamlessly build a production-grade Vedic Astrology system using the <strong>Jyothisya API</strong> via RapidAPI inside a <strong>Dart or Flutter</strong> application. You will learn how to generate a complete Kundali report and dynamically fetch a <strong>5-Level Vimshottari Dasha Tree (down to Prana Dasha)</strong> using pure Dart code.</p>

<hr />

<h2>🎯 What You Will Learn</h2>
<ul>
  <li><strong>Step 1: Create a New GitHub Repository for Your Documentation</strong></li>
  <li><strong>Step 2: Set Up HTTP Dependencies in Your Flutter / Dart Project</strong></li>
  <li><strong>Step 3: Understand the Two-Step On-Demand Architectural Strategy</strong></li>
  <li><strong>Step 4: Configure Birth Input Parameters & Request Headers</strong></li>
  <li><strong>Step 5: Fetch Core Kundali Report & Level 1–3 Dashas (<code>/full-report</code>)</strong></li>
  <li><strong>Step 6: Fetch Level 4 (Sookshma) & Level 5 (Prana) Dashas On-Demand (<code>/dasha/sub-tree</code>)</strong></li>
  <li><strong>Step 7: Implement the Complete Production-Ready Dart API Service</strong></li>
  <li><strong>Step 8: Parse Expected JSON Response Payloads into Dart Models</strong></li>
  <li><strong>Step 9: Build the Flutter UI (Nested ExpansionTile Integration Workflow)</strong></li>
  <li><strong>Step 10: Link Your GitHub Documentation to RapidAPI Studio</strong></li>
</ul>

<hr />

<h2>📌 Step 1: Create a New GitHub Repository for Your Documentation</h2>

<p>To keep your documentation organized, clean, and easily maintainable across updates, host the full tutorial source on GitHub:</p>

<ol>
  <li>Go to <a href="https://github.com" target="_blank" rel="noopener noreferrer">GitHub.com</a> and log into your developer account.</li>
  <li>Click the <strong><code>+</code></strong> icon at the top-right corner and select <strong>New repository</strong>.</li>
  <li>Set the repository name (e.g., <code>jyothisya-flutter-integration-guide</code>).</li>
  <li>Select <strong>Public</strong> so developers and API consumers can access it without authentication barriers.</li>
  <li>Check the box next to <strong>Add a README file</strong>.</li>
  <li>Click <strong>Create repository</strong>.</li>
  <li>Open the newly created <code>README.md</code> file, click the pencil icon (<strong>Edit this file</strong>), and paste this HTML/Markdown documentation. Click <strong>Commit changes</strong> when done.</li>
</ol>

<hr />

<h2>📦 Step 2: Set Up HTTP Dependencies in Your Flutter / Dart Project</h2>

<p>Before writing the integration logic, add the standard HTTP networking package to your Dart runtime or Flutter app.</p>

<p>Open your project's <code>pubspec.yaml</code> file and add <code>http</code> under the <code>dependencies</code> block:</p>

<pre><code class="language-yaml">dependencies:
  flutter:
    sdk: flutter
  http: ^1.1.0 # Standard HTTP client package for Dart
</code></pre>

<p>Then, execute the package fetch command in your terminal:</p>

<pre><code class="language-bash">flutter pub get
# Or for pure Dart projects:
dart pub get
</code></pre>

<hr />

<h2>🏗️ Step 3: Understand the Two-Step On-Demand Architectural Strategy</h2>

<p>Calculating 5 deep levels of Vimshottari Dashas upfront generates over <strong>10,000 sub-periods (~3MB+ raw JSON payload)</strong>. Requesting all 5 levels in a single HTTP call causes unnecessarily slow network responses, high memory overhead, and excessive mobile data consumption on mobile devices.</p>

<p>To optimize mobile app performance, <strong>Jyothisya API</strong> employs a <strong>Two-Step On-Demand Strategy</strong>:</p>

<ol>
  <li><strong>Primary Request (<code>/full-report</code>):</strong> Loads the primary birth chart, planetary positions, house cusps, yogas, panchang, and the top <strong>Level 1–3 Dasha tree</strong> (Maha &rarr; Antar &rarr; Pratyantar).</li>
  <li><strong>On-Demand Sub-Request (<code>/dasha/sub-tree</code>):</strong> When a Flutter app user taps to expand a specific Pratyantar node in the UI, a background HTTP GET call fetches <strong>Level 4 (Sookshma)</strong> and <strong>Level 5 (Prana)</strong> sub-periods strictly for that selected branch.</li>
</ol>

<hr />

<h2>🔑 Step 4: Configure Birth Input Parameters & Request Headers</h2>

<p>Both endpoints accept input parameters passed as a key-value structure in the HTTP query string:</p>

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
      <td>String / Integer</td>
      <td><strong>Yes</strong></td>
      <td>Date of birth (e.g., <code>"1995"</code>, <code>"6"</code>, <code>"15"</code>)</td>
    </tr>
    <tr>
      <td><strong><code>hour</code>, <code>minute</code>, <code>second</code></strong></td>
      <td>String / Integer</td>
      <td><strong>Yes</strong></td>
      <td>Time of birth in 24-hour format (e.g., <code>"10"</code>, <code>"30"</code>, <code>"0"</code>)</td>
    </tr>
    <tr>
      <td><strong><code>latitude</code>, <code>longitude</code></strong></td>
      <td>String / Float</td>
      <td><strong>Yes</strong></td>
      <td>Geographic coordinates (e.g., <code>"6.9271"</code>, <code>"79.8612"</code> for Colombo)</td>
    </tr>
    <tr>
      <td><strong><code>timezoneName</code></strong></td>
      <td>String</td>
      <td><strong>Yes</strong></td>
      <td>IANA Timezone identifier (e.g., <code>"Asia/Colombo"</code>, <code>"Asia/Kolkata"</code>, <code>"UTC"</code>)</td>
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

<h2>🚀 Step 5: Fetch Core Kundali Report & Level 1–3 Dashas (<code>/full-report</code>)</h2>

<p>Make a GET request to <strong><code>/full-report</code></strong> using Dart's <code>http.get()</code> to retrieve the primary birth chart details alongside <strong>Level 1 to 3 Vimshottari Dashas</strong>.</p>

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

<h2>🔍 Step 6: Fetch Level 4 (Sookshma) & Level 5 (Prana) Dashas On-Demand (<code>/dasha/sub-tree</code>)</h2>

<p>When an end-user expands a Pratyantar Dasha node in your Flutter UI, execute an HTTP GET request to <strong><code>/dasha/sub-tree</code></strong> passing the parent node identifiers:</p>

<p><strong>Sub-Tree Required Query Parameters:</strong></p>
<ul>
  <li>All standard birth parameters (<code>year</code>, <code>month</code>, <code>day</code>, <code>hour</code>, <code>minute</code>, <code>second</code>, <code>latitude</code>, <code>longitude</code>, <code>timezoneName</code>)</li>
  <li><strong><code>parent_maha</code>:</strong> Name of the parent Maha Dasha planet (e.g., <code>"Sun"</code>)</li>
  <li><strong><code>parent_antar</code>:</strong> Name of the parent Antar Dasha planet (e.g., <code>"Sun"</code>)</li>
  <li><strong><code>parent_pratyantar</code>:</strong> Name of the parent Pratyantar Dasha planet (e.g., <code>"Rahu"</code>)</li>
</ul>

<hr />

<h2>💻 Step 7: Implement the Complete Production-Ready Dart API Service</h2>

<p>Below is a clean, fully commented, self-contained Dart service class utilizing <code>package:http/http.dart</code> and <code>dart:convert</code>:</p>

<pre><code class="language-dart">import 'dart:convert';
import 'package:http/http.dart' as http;

class JyothisyaApiService {
  // RapidAPI Access Credentials
  static const String _rapidApiKey = 'YOUR_RAPIDAPI_KEY_HERE';
  static const String _rapidApiHost = 'mindastro-api.p.rapidapi.com';

  // Standard Base Birth Details Map
  static final Map&lt;String, String&gt; _baseBirthParams = {
    'year': '1995',
    'month': '6',
    'day': '15',
    'hour': '10',
    'minute': '30',
    'second': '0',
    'latitude': '6.9271',
    'longitude': '79.8612',
    'timezoneName': 'Asia/Colombo',
    'lang': 'si', // Set language to Sinhala
    'ayanamsa': 'lahiri',
    'house_system': 'sripati',
  };

  // HTTP Header Map
  static final Map&lt;String, String&gt; _headers = {
    'x-rapidapi-key': _rapidApiKey,
    'x-rapidapi-host': _rapidApiHost,
  };

  /// Step 5 Method: Fetch Full Astrology Report (Level 1–3 Dashas)
  static Future&lt;Map&lt;String, dynamic&gt;?&gt; getFullAstrologyReport() async {
    try {
      final uri = Uri.https(_rapidApiHost, '/api/v1/full-report', _baseBirthParams);
      print('Fetching Full Kundali Report...');

      final response = await http.get(uri, headers: _headers);

      if (response.statusCode == 200) {
        final Map&lt;String, dynamic&gt; decoded = jsonDecode(response.body);
        final report = decoded['data'];

        print('=== Primary Chart Loaded Successfully ===');
        print('Lagna Sign: ${report['lagna']['sign_translated']}');
        print('Total Yogas: ${report['yogas']['summary']['total_count']}');
        print('Maha Dashas Loaded: ${report['dasha'].length}');

        return report;
      } else {
        print('HTTP Error ${response.statusCode}: ${response.body}');
      }
    } catch (e) {
      print('Exception occurred while fetching full report: $e');
    }
    return null;
  }

  /// Step 6 Method: Fetch Level 4 (Sookshma) & Level 5 (Prana) Dashas On-Demand
  static Future&lt;Map&lt;String, dynamic&gt;?&gt; fetchPranaDashaTree({
    required String parentMaha,
    required String parentAntar,
    required String parentPratyantar,
  }) async {
    try {
      // Merge base parameters with parent dasha node identifiers
      final subTreeParams = Map&lt;String, String&gt;.from(_baseBirthParams)..addAll({
        'parent_maha': parentMaha,
        'parent_antar': parentAntar,
        'parent_pratyantar': parentPratyantar,
      });

      final uri = Uri.https(_rapidApiHost, '/api/v1/dasha/sub-tree', subTreeParams);
      print('Fetching Sub-tree for $parentMaha -&gt; $parentAntar -&gt; $parentPratyantar...');

      final response = await http.get(uri, headers: _headers);

      if (response.statusCode == 200) {
        final Map&lt;String, dynamic&gt; decoded = jsonDecode(response.body);
        final subTree = decoded['data'];

        print('=== Sookshma & Prana Dasha Sub-Tree Loaded ===');
        final List sookshmaList = subTree['sookshma_dashas'] ?? [];
        
        for (var i = 0; i &lt; sookshmaList.length; i++) {
          final sookshma = sookshmaList[i];
          print('[Level 4 Sookshma ${i + 1}] Lord: ${sookshma['planet_translated']} (${sookshma['start_date']} to ${sookshma['end_date']})');

          final List pranaList = sookshma['prana_dashas'] ?? [];
          for (var j = 0; j &lt; pranaList.length; j++) {
            final prana = pranaList[j];
            print('   └─ [Level 5 Prana ${j + 1}] Lord: ${prana['planet_translated']} (${prana['start_date']} to ${prana['end_date']})');
          }
        }

        return subTree;
      } else {
        print('HTTP Error ${response.statusCode}: ${response.body}');
      }
    } catch (e) {
      print('Exception occurred while fetching sub-tree: $e');
    }
    return null;
  }
}

// Main Execution Flow
void main() async {
  // 1. Initial Call: Load main report and Level 1-3 Dashas
  final report = await JyothisyaApiService.getFullAstrologyReport();

  // 2. Dynamic Call: User expands Sun -> Sun -> Rahu node in Flutter UI
  if (report != null) {
    await JyothisyaApiService.fetchPranaDashaTree(
      parentMaha: 'Sun',
      parentAntar: 'Sun',
      parentPratyantar: 'Rahu',
    );
  }
}
</code></pre>

<hr />

<h2>📄 Step 8: Parse Expected JSON Response Payloads into Dart Models</h2>

<h3>1. <code>/full-report</code> Response Sample (Level 1–3 Tree Preview)</h3>

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

<h3>2. <code>/dasha/sub-tree</code> Response Sample (Level 4 Sookshma & Level 5 Prana)</h3>

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

<h2>🎨 Step 9: Build the Flutter UI (Nested ExpansionTile Integration Workflow)</h2>

<p>To present this deep hierarchical tree inside a smooth Flutter user interface:</p>

<ol>
  <li><strong>Render Levels 1–3:</strong> Bind the initial <code>dasha</code> array returned from <code>/full-report</code> to nested Flutter <code>ExpansionTile</code> widgets (Maha &rarr; Antar &rarr; Pratyantar).</li>
  <li><strong>Attach Expansion Listener:</strong> Use the <code>onExpansionChanged</code> callback on the 3rd-level (Pratyantar) <code>ExpansionTile</code>.</li>
  <li><strong>Dynamic Sub-Tree Fetching:</strong> When expanded by the user, if the local state for Level 4/5 is unpopulated, trigger a loading indicator (<code>CircularProgressIndicator</code>) and invoke <code>JyothisyaApiService.fetchPranaDashaTree()</code>.</li>
  <li><strong>Update Reactive State:</strong> Call <code>setState()</code> or emit a new state in your state management framework (Provider, Bloc, Riverpod) to instantly draw the nested Level 4 (Sookshma) and Level 5 (Prana) tiles.</li>
</ol>

<hr />

<h2>🔗 Step 10: Link Your GitHub Documentation to RapidAPI Studio</h2>

<p>Once your repository is updated on GitHub, publish a concise Markdown entry on your <strong>RapidAPI Studio Tutorials Tab</strong> that links directly to your public GitHub guide:</p>

<p><strong>Copy and paste this markdown block into RapidAPI Studio Tutorials Editor:</strong></p>

<pre><code class="language-markdown"># How to Fetch a Full Kundali Report & Dynamic 5-Level Dasha Tree in Dart / Flutter

This guide covers the complete Dart/Flutter integration pattern for building a high-performance Vedic Astrology mobile app, featuring a dynamic **5-Level Vimshottari Dasha Tree (Prana Dasha)** fetching system.

### 📚 Complete Guide & Production Dart Code

To view the full architectural design, Flutter UI integration guidelines, and complete copy-pasteable Dart code, visit our official documentation repository on GitHub:

👉 **[View Full Dart / Flutter Integration Tutorial on GitHub](YOUR_GITHUB_README_LINK_HERE)** *(Right-click or Ctrl+Click to open in new tab)*

---

### 🔑 Quick Summary
* **Step 1:** Create GitHub Documentation Repository
* **Step 2:** Add HTTP Package Dependencies
* **Step 3:** Dynamic 2-Step Fetching Architecture
* **Step 4:** API Input Parameters Reference
* **Step 5:** Fetching Core Kundali & Level 1-3 Dashas
* **Step 6:** Fetching Level 4 & 5 Dashas On-Demand
* **Step 7:** Full Production-Ready Dart Service Implementation
* **Step 8:** Expected JSON Payloads
* **Step 9:** Flutter UI ExpansionTile Tree View Integration
</code></pre>

<hr />

<h2>💡 Summary & Performance Gains</h2>

<p>By implementing this <strong>2-step strategy in your Dart / Flutter app</strong>:</p>
<ul>
  <li>Initial app load times for chart generation stay under <strong>10ms</strong>.</li>
  <li>Mobile network bandwidth consumption drops dramatically from <strong>~3MB+ to ~15KB</strong> per initial Kundali lookup.</li>
  <li>Your users enjoy instant access to precise <strong>5-level Vimshottari Dasha calculations</strong> without experiencing UI jank or memory freeze.</li>
</ul>
