---
slug: contributing-to-semgrep-rules-repository
description: "This article outlines how to contribute to Semgrep Registry."
hide_title: true
title: Contribute rules to the Semgrep Registry
toc_max_heading_level: 4
---

import LinkToRegistryRule from "/src/components/LinkToRegistryRule"
import RequiredRuleFields from "/src/components/reference/_required-rule-fields.mdx"

# Contribute rules to the Semgrep Registry

Publish rules to the Semgrep Registry to share them with the Semgrep community and contribute to the field of software security. There are two ways in which you can contribute rules to the Semgrep Registry:

<dl>
    <dt>For users of Semgrep AppSec Platform</dt>
    <dd>Contribute new rules to the Semgrep Registry through Semgrep AppSec Platform. This workflow is recommended. See <a href="#contribute-through-semgrep-appsec-platform-recommended"> Contribute through Semgrep AppSec Platform (recommended)</a>. This workflow creates the necessary pull request for you and streamlines the whole process.</dd>
    <dt>For contributors to the repository through GitHub</dt>
    <dd>Contribute rules to the Semgrep Registry, or suggest changes to existing rules, through a pull request to `semgrep-rules`. See the <a href="#contribute-through-github"> Contribute through GitHub</a> section for detailed information.</dd>
</dl>

## Contribute through Semgrep AppSec Platform (recommended)

This is the recommended path for adding a new rule. To suggest a change to an existing rule, see [Update existing rules in Semgrep Registry](#update-existing-rules-in-semgrep-registry).

1. Sign in to [<i class="fas fa-external-link fa-xs"></i> Semgrep AppSec Platform](https://semgrep.dev/login).
1. Go to the [<i class="fas fa-external-link fa-xs"></i> Semgrep Playground](https://semgrep.dev/playground/new).
1. Click <i className="fa-solid fa-file-plus-minus inline_svg"></i> **Create New Rule**.
1. Choose one of the following:
    - Create a new rule and test code by clicking <i class="fa-solid fa-circle-plus"></i> **plus** icon, select **New rule** and then click <i className="fa-solid fa-floppy-disk inline_svg"></i> **Save**. Note: The test file must contain at least one true positive and one true negative test case to be approved. See the [Tests](#tests) section of this document for more information.
    - In the <i class="fa-solid fa-server"></i> **Library** panel, select a rule from a category in **Semgrep Registry**. Click <i className="fa-solid fa-code-branch inline_svg"></i> **Fork**, modify the rule or test code, and then click <i className="fa-solid fa-floppy-disk inline_svg"></i> **Save**.
1. Click <i className="fa-solid fa-earth-americas inline_svg"></i> **Share**.
1. Click <i className="fa-solid fa-cloud-arrow-up inline_svg"></i> **Publish to Registry**.
1. Fill in the required and optional fields.
1. Click <i className="fa-solid fa-circle-check inline_svg"></i> **Continue**, and then click <i className="fa-solid fa-code-pull-request inline_svg"></i> **Create PR**.

This workflow automatically creates a pull request in the GitHub [Semgrep Registry](https://github.com/semgrep/semgrep-rules). Find more about the Semgrep Registry by reading the [Rule writing](#write-a-rule-for-semgrep-registry) and [Tests](#tests) sections.

You can also publish rules as private rules outside of Semgrep Registry. These rules are not included in the Semgrep Registry, but they are accessible to your Semgrep organisation. See the [Private rules](/writing-rules/private-rules) documentation for more information.

## Contribute through GitHub

1. Create a pull request in the [<i class="fas fa-external-link fa-xs"></i> semgrep/semgrep-rules](https://github.com/semgrep/semgrep-rules) repository. The pull request requires two files:
    - The Semgrep rule saved as a YAML file.
    - The test file with the file extension of the language or framework. The test file must contain at least one true positive and one true negative test case to be approved. See the [Tests](#tests) section of this document for more information.
1. Sign the Contributor License Agreement (CLA) on GitHub; this is required before Semgrep can accept your contributions.

Pull requests require the approval of at least one maintainer and successfully passed [CI jobs](https://github.com/semgrep/semgrep-rules/actions).

Find more about the Semgrep Registry by reading the [Rule writing](#write-a-rule-for-semgrep-registry) and [Tests](#tests) sections.

## Licensing

The Semgrep Registry can import rules from different repositories. These repositories can enforce their own licensing for rules. If you'd like to enforce a specific license, such as the MIT license or GNU Lesser GPL:

1. Create a GitHub repository and store your rules there.
1. Reach out to the Semgrep team through the [<i class="fas fa-external-link fa-xs"></i> Community Slack](https://go.semgrep.dev/slack)  or [Support](/support)


## Write a rule for Semgrep Registry

The following sections document necessary fields in rule files of Semgrep Registry, provide information about rule messages, inform about test files, mention rule quality checkers, and describe additional fields required by rules in the security category.

### General rule requirements

All rules in general, regardless of whether they are intended only as local rules or for Semgrep Registry, have the same initial requirements. The following table is also included in the [Rule Syntax](/writing-rules/rule-syntax) article.

<RequiredRuleFields />

Every rule also requires a test file in the language that the rule is targeting. See [Tests](#tests) for more details.

### Semgrep registry rule requirements

In addition to the fields mentioned above, rules submitted to Semgrep Registry have additional required fields:

<table>
  <thead><tr>
   <th>Field</th>
   <th>Description</th>
   <th>Possible values</th>
   <th>Example</th>
  </tr></thead>
  <tbody>
        <tr>
            <td rowspan="2">
                <code>metadata</code>
            </td>
            <td rowspan="2">
                All rules require <code>technology</code>, <code>category</code>, and <code>references</code>. The <code>category: security</code> has more requirements. See <a href="#fields-required-by-the-security-category"> Including fields required by security category.</a>
            </td>
            <td>
               Required by all Semgrep Registry rules:
                <ul>
                  <li><code>references</code></li>
                  <li><code>category</code></li>
                  <li><code>technology</code></li>
                </ul>
            </td>
            <td rowspan="2">
              <pre>
              <code>metadata:<br /></code>
              <code>  cwe:<br /></code>
              <code>    - "CWE-94: (...)"<br /></code>
              <code>  category: security<br /></code>
              <code>  technology:<br /></code>
              <code>    - unicode<br /></code>
              <code>  references:<br /></code>
              <code>    - https://trojansource.codes/<br /></code>
              </pre>
            </td>
        </tr>
        <tr>
            <td>
              Additional keys required when <code>category</code> is <code>security</code>:
              <ul>
                  <li><code>cwe</code></li>
                  <li><code>owasp</code></li>
                  <li><code>confidence</code></li>
                  <li><code>subcategory</code></li>
                  <li><code>likelihood</code></li>
                  <li><code>impact</code></li>
                  <li><code>vulnerability_class</code></li>
              </ul>
            </td>
        </tr>
  <tr>
   <td><code>technology</code></td>
   <td>Nested under the <code>metadata</code> field. Additional information about the technology. This helps to specify rulesets in Semgrep Registry.</td>
   <td>
    <ul>
        <li><code>django</code></li>
        <li><code>docker</code></li>
        <li><code>express</code></li>
        <li><code>kubernetes</code></li>
        <li><code>nginx</code></li>
        <li><code>react</code></li>
        <li><code>terraform</code></li>
        <li><code>--no-technology--</code></li>
    </ul>
   </td>
   <td>
    <pre>
        <code>metadata:<br /></code>
        <code>  technology:<br /></code>
        <code>    - react</code>
    </pre>
   </td>
  </tr>
  <tr>
   <td><code>category</code></td>
   <td>Nested under the <code>metadata</code> field. If you use catagory <code>security</code>, include additional metadata. See <a href="#fields-required-by-the-security-category"> Including fields required by security category</a>.</td>
   <td>
    <ul>
      <li><code>best-practice</code></li>
      <li><code>correctness</code></li>
      <li><code>maintainability</code></li>
      <li><code>performance</code></li>
      <li><code>portability</code></li>
      <li><code>security</code></li>
    </ul>
   </td>
    <td>
    <pre>
    category: security
    </pre>
    </td>
  </tr>
  <tr>
   <td><code>references</code></td>
   <td>Additional information that gives more context to the user of the rule. This helps developers understand the issue and how to fix it.</td>
   <td>No finite value. Any additional information that gives more context.</td>
   <td>
    <pre style={{"white-space": "pre-wrap", "word-break": "keep-all"}}>
    <code>references:<br /></code>
    <code>  - [OWASP DOM based XSS Prevention Cheat Sheet][OWASP-DOM-based-XSS-prevention]</code>
    </pre>
   </td>
  </tr>
  </tbody>
</table>

:::info
- If you use category <code>security</code>, include additional metadata. See <a href="#fields-required-by-the-security-category"> Including fields required by security category</a>.
- Cross-file (interfile) analysis requires `interfile: true` under the `options` key in YAML rules. For more information, see [Creating rules that analyze across files](/semgrep-code/semgrep-pro-engine-intro/#write-rules-that-analyze-across-files-and-functions).
:::

### Rule namespace

The namespacing format for contributing rules in the [Semgrep Registry](https://github.com/semgrep/semgrep-rules) is `<language>/<framework>/<category>/$MORE`. If the rule does not belong to a particular framework, add it to the language directory, which uses the word `lang` in place of the `<framework>` - `<language>/<lang>`.

### Tests

Include a test file in the language that your rule is targeting. A test file includes the following:

- At least one test where the rule detects a finding. This is called a true positive finding.
- At least one test where the rule does **not** detect a finding. This is called a true negative finding.

Test file names must match the rule filename, except for the file extension. For example, if the rule is in `my-rule.yaml`, the test filename must be `my-rule.js`. Use any valid extension for the target language.

:::info Requirements of test files
- In the test file, include examples that mark:
    - What is expected to be a finding.
    - What is not a finding.
- The test filename must match the rule filename, except for the file extension.
:::

See the examples of the rule and test file below:

Rule file:
```yaml
rules:
- id: my-rule
  pattern: var $X = "...";
  …
```

In the test file, mark an expected finding with a comment tag and the `ruleid` of your rule in the comment before the expected finding. Also, mark the code that is expected not to be a finding with a comment stating `ok` and add the `ruleid` also. See the example below:
```js
// ruleid: my-rule
var strdata = "hello";
// ok: my-rule
var numdata = 1;
```

For more information, visit [Testing rules](/writing-rules/testing-rules).

### Rule messages

Include a rule message that provides details about the matched pattern and informs about how to mitigate any related issues. Provide the following information in a rule message:

1. Description of the pattern. For example: missing parameter, dangerous flag, out-of-order function calls.
2. Description of why this pattern was detected. For example: logic bug, introduces a security vulnerability, bad practice.
3. An alternative that resolves the issue. For example: Use another function, validate data first, and discard the dangerous flag.

Use the YAML multiline string operator `>-` when rule messages span multiple lines. This presents the best-looking rule message on the command line without having to worry about line wrapping or escaping the quote or using the backslash.

For an example of a good rule message, see: [this rule for Django's `mark_safe`](https://semgrep.dev/r?q=python.django.security.audit.avoid-mark-safe.avoid-mark-safe).

:::note Rule message example
`mark_safe()` is used to mark a string as safe for HTML output. This disables escaping and may expose the content to XSS attacks. Instead, use `django.utils.html.format_html()` to build HTML for rendering.
:::

### Rule quality checker

When you contribute rules to the Semgrep Registry, our quality checkers (linters) evaluate if the rule conforms to Semgrep, Inc. standards. The `semgrep-rule-lints` job runs linters on a new rule to check for mistakes, performance problems, and best practices for submitting to the Semgrep Registry. To improve your rule writing, use Semgrep itself to [scan semgrep-rules](https://semgrep.dev/blog/2021/how-we-made-semgrep-rules-run-on-semgrep-rules/).

### Fields required by the `security` category

Rules in category `security` in the Semgrep Registry require specific metadata fields that ensure consistency across the ecosystem in both Semgrep AppSec Platform and Semgrep CLI. Nest these metadata under the `metadata` field.

If your rule has a `category: security`, the following metadata are required:

<table>
  <thead><tr>
   <th>Required metadata field</th>
   <th>Values</th>
   <th>Example use</th>
  </tr></thead>
  <tbody>
  <tr>
   <td><code>cwe</code></td>
   <td>A <a href="https://cwe.mitre.org/index.html">Comment Weakness Enumeration (CWE)</a></td>
   <td><pre>cwe: "CWE-502: Deserialization of Untrusted Data"</pre></td>
  </tr>
  <tr>
   <td><code>owasp</code></td>
   <td>An <a href="https://owasp.org/Top10/">OWASP Top 10 category</a></td>
   <td>
    <pre>owasp:<br />  - A05:2021 - Security Misconfiguration</pre>
   </td>
  </tr>
  <tr>
   <td><code>confidence</code></td>
   <td><code>HIGH</code>, <code>MEDIUM</code>, <code>LOW</code></td>
   <td><pre>confidence: MEDIUM</pre></td>
  </tr>
  <tr>
   <td><code>likelihood</code></td>
   <td><code>HIGH</code>, <code>MEDIUM</code>, <code>LOW</code></td>
   <td><pre>likelihood: MEDIUM</pre></td>
  </tr>
  <tr>
   <td><code>impact</code></td>
   <td><code>HIGH</code>, <code>MEDIUM</code>, <code>LOW</code></td>
   <td><pre>impact: HIGH</pre></td>
  </tr>
  <tr>
   <td><code>subcategory</code></td>
   <td><code>vuln</code>, <code>audit</code>, <code>secure default</code></td>
   <td>
    <pre>subcategory:<br />  - vuln</pre>
  </td>
  </tr>
    <tr>
   <td><code>vulnerability_class</code></td>
   <td>See [Vulnerability class](#vulnerability-class) for a list of sample values. Accepts custom values.</td>
   <td>
    <pre>vulnerability_class:<br />  - Hard-coded Secrets</pre>
  </td>
  </tr>
  </tbody>
</table>

These fields help you to find rules in different categories such as:
- High confidence security rules for CI pipelines.
- OWASP Top 10 or CWE Top 25 rulesets.
- Technology. For example, `react` so it is easy to find React rulesets.
- Audit rules with lower confidence are intended for code auditors.

Examples of rules with a full list of required metadata:
- High confidence JavaScript and TypeScript rule: <LinkToRegistryRule ruleId="javascript.express.security.audit.express-open-redirect.express-open-redirect" />
- Medium confidence Python rule: <LinkToRegistryRule ruleId="python.lang.security.dangerous-system-call.dangerous-system-call" />
- Low confidence C# rule: <LinkToRegistryRule ruleId="csharp.lang.security.ssrf.rest-client.ssrf" />

:::note
Details of each field mentioned above are provided in the subsections below with examples.
:::

#### CWE

Include the appropriate <a href="https://cwe.mitre.org/index.html">Comment Weakness Enumeration (CWE)</a>. CWE can explain what vulnerability your rule is trying to find. Examples:

If you write an SQL Injection rule, use the following:
```yaml
cwe:
  - "CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')"
```

If you write an XSS rule, use the following:
```yaml
cwe:
  - "CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')"
```

#### Confidence

Indicate confidence of the rule to detect true positives. See the possible options below:

- **HIGH** - Security concern, with high true positives. Useful in CI/CD pipelines.
- **MEDIUM** - Security concern, but some false positives. Useful in CI/CD pipelines.
- **LOW** - Expect a fair amount of false positives, similar to audit style rules. These rules can detect many false positives.

##### HIGH

HIGH confidence rules can use Semgrep advanced features such as `metavariable-comparison` or `taint mode`, to detect true positives. See examples below:

- <LinkToRegistryRule ruleId="go.lang.security.audit.crypto.use_of_weak_rsa_key.use-of-weak-rsa-key" />
- <LinkToRegistryRule ruleId="javascript.express.security.audit.express-open-redirect.express-open-redirect" />
- <LinkToRegistryRule ruleId="javascript.jose.security.jwt-hardcode.hardcoded-jwt-secret" />

```yaml
confidence: HIGH
```

##### MEDIUM

MEDIUM confidence rules can use Semgrep advanced features such as `metavariable-comparison` or `taint mode`, but with some false positives. See examples below:

- <LinkToRegistryRule ruleId="javascript.express.security.audit.express-ssrf.express-ssrf" />
- <LinkToRegistryRule ruleId="javascript.express.security.express-xml2json-xxe.express-xml2json-xxe" />

```yaml
confidence: MEDIUM
```

##### LOW

Low confidence rules generally find something which appears to be dangerous while reporting a lot of false positives. See examples below:

- <LinkToRegistryRule ruleId="php.lang.security.eval-use.eval-use" />
- <LinkToRegistryRule ruleId="javascript.browser.security.dom-based-xss.dom-based-xss" />

```yaml
confidence: LOW
```

#### Likelihood

Specify how likely it is that an attacker can exploit the issue that has been found. The possible values are `LOW`, `MEDIUM`, `HIGH`.

##### HIGH

HIGH likelihood rules specify a very high concern that the vulnerability can be exploited. Examples:

- The use of weak encryption: <LinkToRegistryRule ruleId="go.lang.security.audit.crypto.use_of_weak_rsa_key.use-of-weak-rsa-key" />
- Disabled security feature in a configuration: <LinkToRegistryRule ruleId="javascript.angular.security.detect-angular-sce-disabled.detect-angular-sce-disabled" />
- Hardcoded secrets that use a constant value `"..."`: <LinkToRegistryRule ruleId="javascript.jose.security.jwt-hardcode.hardcoded-jwt-secret" />
- Rules that leverage `taint mode sources` which indicate sources that can come from an attacker. Such as HTTP `POST`, `GET`, `PUT`, and `DELETE` request values. For example: <LinkToRegistryRule ruleId="javascript.express.security.audit.express-open-redirect.express-open-redirect" />

```yaml
likelihood: HIGH
```

##### MEDIUM

MEDIUM likelihood rules detect a vulnerability in most circumstances. Although it can be hard for an attacker to exploit them. Also, these rules can detect part of a problem, but not the whole issue. Examples:

- `taint mode sources` that reach a `taint mode sink`  but the source is only vulnerable in certain conditions for example OS Environment Variables, or loading from disk: <LinkToRegistryRule ruleId="python.aws-lambda.security.dangerous-spawn-process.dangerous-spawn-process" />
- `taint mode sources` with a `taint mode sink` but is missing a `taint mode sanitizer` which can introduce more false positives: <LinkToRegistryRule ruleId="javascript.express.security.express-puppeteer-injection.express-puppeteer-injection" />

```yaml
likelihood: MEDIUM
```

##### LOW

LOW likelihood rules tend to find something dangerous, but are not evaluating whether something is truly vulnerable, for example:

- `taint mode sources` such as function arguments which may or may not be tainted which reach a `taint mode sink`: <LinkToRegistryRule ruleId="typescript.react.security.audit.react-href-var.react-href-var" />
- A rule which uses `search mode` to find the use of a dangerous function for example: `trustAsHTML`, `bypassSecurityTrust()`, `eval()`, or `innerHTML`: <LinkToRegistryRule ruleId="javascript.browser.security.dom-based-xss.dom-based-xss" />

```yaml
likelihood: LOW
```

#### Impact

Indicate how much damage can a vulnerability cause. Use LOW, MEDIUM, and HIGH.


##### HIGH

HIGH impact rules can detect extremely damaging vulnerabilities, such as injection vulnerabilities. Examples:

- <LinkToRegistryRule ruleId="javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection" />
- <LinkToRegistryRule ruleId="ruby.rails.security.audit.xxe.xml-external-entities-enabled.xml-external-entities-enabled" />

```yaml
impact: HIGH
```

##### MEDIUM

MEDIUM impact rules are issues that are less likely to lead to full system compromise but still are fairly damaging. Examples:

- <LinkToRegistryRule ruleId="python.flask.security.injection.raw-html-concat.raw-html-format" />
- <LinkToRegistryRule ruleId="python.flask.security.injection.ssrf-requests.ssrf-requests" />

```yaml
impact: MEDIUM
```

##### LOW

LOW impact rules are rules that leverage a security issue, but the impact is not too damaging to the application if discovered.

- <LinkToRegistryRule ruleId="go.gorilla.security.audit.session-cookie-missing-secure.session-cookie-missing-secure" />
- <LinkToRegistryRule ruleId="javascript.browser.security.raw-html-join.raw-html-join" />

```yaml
impact: LOW
```

#### References

References help provide more context to a developer on what the issue is, and how to remediate the vulnerability, see examples below:

- A rule that is finding an issue in React: <LinkToRegistryRule ruleId="typescript.react.security.audit.react-href-var.react-href-var" />
    ```yaml
    references:
      - https://reactjs.org/blog/2019/08/08/react-v16.9.0.html#deprecating-javascript-urls
    ```
- A rule that is detecting an issue in Express: <LinkToRegistryRule ruleId="javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection" />
    ```yaml
    references:
      - https://sequelize.org/docs/v6/core-concepts/raw-queries/#replacements
    ```

#### Subcategory

Include a subcategory to explain what is the type of the rule. See the subsections below for more details.

<!-- vale off -->
##### vuln
<!-- vale on -->

A vulnerability rule is something that developers certainly want to resolve. For example, an SQL Injection rule that uses taint mode. Example:

- <LinkToRegistryRule ruleId="javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection" />

```yaml
subcategory:
  - vuln
```

##### audit

An audit rule is useful for code auditors. For example, an SQL rule which finds all uses of the `database.exec(...)` that can be problematic. Example:

- <LinkToRegistryRule ruleId="generic.html-templates.security.unquoted-attribute-var.unquoted-attribute-var" />

```yaml
subcategory:
  - audit
```

##### secure default

A secure default rule makes use of inherently secure libraries, frameworks, configurations, or settings. These rules enforce the mitigation of common security concerns, such as preventing cross-site request forgery (CSRF) by properly verifying inbound requests in Django or Flask applications.

A secure default rule must contain remediation that suggests applying a one-time setting that ensures security throughout the codebase without the need for repeated application by developers. For example, configuring a global security setting in a web application framework that applies to all routes and inputs.

```yaml
subcategory:
  - secure default
```

#### Technology

Technology helps to define specific rulesets for languages, libraries, and frameworks that are available in [Semgrep Registry](https://semgrep.dev/explore), for example `express` will be included in the `p/express` ruleset.

- <LinkToRegistryRule ruleId="javascript.express.security.audit.express-open-redirect.express-open-redirect" />

```yaml
technology:
  - express
```

#### Vulnerability class

The vulnerability class defines the category to which a rule and its resulting findings belong. The categories are used to group rules in Semgrep AppSec Platform's **Policies** page to help find similar rules. The category is also displayed on the **Finding Details** pages.

You can provide custom values. Sample values include:

- Active Debug Code
- Code Injection
- Command Injection
- Cookie Security
- Cross-Site Request Forgery (CSRF)
- Cross-Site-Scripting (XSS)
- Cryptographic Issues
- Dangerous Method or Function
- Denial-of-Service (DoS)
- Hard-coded Secrets
- Improper Authentication
- Improper Authorization 
- Improper Encoding
- Improper Validation
- Insecure Deserialization
- Insecure Hashing Algorithm
- Insufficient Logging 
- LDAP Injection
- Mass Assignment
- Memory Issues
- Mishandled Sensitive information
- Open Redirect
- Other Security
- Path Traversal
- SQL Injection
- Server-Side Request Forgery (SSRF)
- XML Injection
- XPath Injection

## Update existing rules in Semgrep Registry

1. Find a rule you want to update in the [semgrep-rules](https://github.com/semgrep/semgrep-rules/) repository.
2. Submit a PR to the repository with your new update.
3. Follow the same instructions and recommendations as you can find in the rest of this document. For example the security category has specific metadata requirements.
4. Leave a message in the PR. Explain why are you making changes. What is the motivation for this update?

See a [PR example](https://github.com/semgrep/semgrep-rules/pull/2730).

There can be specific messages in the repository’s pipeline informing you about specific details of your rule. Ensure that your rule fulfills all of the necessities and requirements. However, sometimes the pipeline running in the [semgrep-rules](https://github.com/semgrep/semgrep-rules/) repository can have specific issues. In such a case, wait for a Semgrep reviewer's help.


[OWASP-DOM-based-XSS-prevention]: https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html
