---
title: Custom Reporter
description: Learn how to create and use a custom reporter in Nightwatch.
---

<div class="page-header"><h2>Create a custom reporter</h2></div>

### Overview
You can generate your own reports by using the provided the results object. This can be done is at least two main ways:

### As a separate file

#### Step 1. create the file

Define your custom reporter in a separate file (e.g. `custom_reporter.js`). Choose either a callback or a Promise to signal that reporting is complete.

<div class="sample-test"><i>custom_reporter.js</i>
<pre class="line-numbers"><code class="language-javascript">module.exports = {
  write : function(results, options, done) {
    console.log('custom reporting...');

    done();
  }
};</code></pre></div>

<div class="sample-test"><i>custom_reporter.js</i>
<pre class="line-numbers"><code class="language-javascript">module.exports = {
  write: async function(results, options) {

    console.log('custom reporting...');    

  }
};</code></pre></div>

#### Step 2. run the reporter

Run the following command with the correct path to the custom reporter:

<pre class="language-bash"><code class="language-bash">nightwatch --reporter=junit --reporter=/path/to/custom_reporter.js</code></pre>

Run the following command to generate multiple reports (the built-in HTML report and the custom_reporter) – since v2.2+:

<pre class="language-bash"><code class="language-bash">nightwatch --reporter=/path/to/custom_reporter.js --reporter=html</code></pre>

### As an NPM package

A custom reporter can also be published to NPM. 

#### Example
<div class="sample-test"><pre class="hide-indicator language-bash"><code>  ├── / 
  |   ├── src/
  |   |    ├── my_custom_reporter_lib.js
  |   |    └── my_other_custom_reporter_lib.js
  |   └── test/
  |        ├── test_for_my_custom_reporter_lib.js
  |        └── test_for_my_other_custom_reporter_lib.js
  ├── index.js
  ├── LICENSE.md
  ├── package.json
  └── README.md
</code></pre></div>

If you're new to publishing NPM packages, read the [Creating and publishing unscoped public packages](https://docs.npmjs.com/creating-and-publishing-unscoped-public-packages) guide first.

The `index.js` file needs to implement the same interface as the file-based custom reporter:

<div class="sample-test"><i>index.js</i>
<pre class="line-numbers"><code class="language-javascript">module.exports = {
  write: async function(results, options) {

    console.log('custom reporting...');

  }
};</code></pre></div>

#### Usage


1) Install the NPM package for the custom reporter you wish to use:

<pre class="language-bash"><code class="language-bash">npm i &lt;nightwatch-custom-reporter&gt;</code></pre>

2) Use the custom reporter:

<pre class="language-bash"><code class="language-bash">nightwatch --reporter=&lt;nightwatch-custom-reporter&gt;</code></pre>

### Recommended content
- [How-to guides > Use reporters > HTML reporter](/guide/reporters/use-html-reporter.html)
- [How-to guides > Use reporters > JUnit-XML reporter](/guide/reporters/use-junit-reporter.html)
- [Reference > Nightwatch CLI](/guide/nightwatch-cli/command-line-options.html)