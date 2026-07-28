# Association.github.io
LupusLyfe: Healing. Ownership. Perseverance. Endurance. A safe place for warriors.
</html

git clone [repository]
cd synthexit-dispatch
npm install

# Set API keys
export ANTHROPIC_API_KEY="sk-ant-..."
export OPENAI_API_KEY="sk-..."
export GOOGLE_API_KEY="..."

# Force Claude for critical legal analysis
node src/dispatch.js process \
  --provider claude \
  --task legal_analysis \
  --input evidence/eeoc-determination.txt

# Force GPT-4 for structured extraction
node src/dispatch.js process \
  --provider openai \
  --task extraction \
  --input evidence/emails.txt

# Force Gemini for bulk processing
node src/dispatch.js process \
  --provider gemini \
  --task extraction \
  --input evidence/discovery/*.pdf

node src/dispatch.js route --task timeline --input events.json

node src/dispatch.js route --task extraction --input documents/*.pdf

node src/dispatch.js route --task legal_analysis --input case-file.txt

node src/dispatch.js route --task narrative --input timeline.json

// Redacted by default
const result = await dispatch.process({
  provider: 'claude',
  input: sensitiveDocument,
  redact: true  // default
});

// Opt out of redaction (use carefully)
const result = await dispatch.process({
  provider: 'claude',
  input: publicDocument,
  redact: false
});

# View cost report
npm run cost-report

# Filter by provider
node -e "require('./src/util/log').printCostReport({ provider: 'claude' })"

# Filter by date range
node -e "require('./src/util/log').printCostReport({ 
  startDate: '2025-01-01',
  endDate: '2025-01-31'
})"

const { SynthexitDispatch } = require('./src/dispatch');

const dispatch = new SynthexitDispatch({
  defaultQuality: 'high',
  maxRetries: 3,
  autoRedact: true,
  costTracking: true
});

// Auto-route
const result = await dispatch.route({
  taskType: 'timeline_construction',
  input: chronologicalEvents,
  qualityThreshold: 'high',
  maxCost: 5.00
});

// Direct processing
const analysis = await dispatch.process({
  provider: 'claude',
  taskType: 'legal_analysis',
  input: caseFile,
  redact: true
});

// Batch processing
const results = await dispatch.batch({
  tasks: 'extraction',
  provider: 'gemini',
  inputs: arrayOfDocuments,
  concurrency: 5
});

console.log('Analysis:', result.output);
console.log('Cost:', result.metadata.cost);

out/
├── logs/
│   ├── costs.jsonl       # Cost tracking
│   ├── errors.jsonl      # Error log
│   └── activity.jsonl    # General activity
├── claude/
│   └── 2025-01-28T15-30-00/
│       ├── timeline.txt
│       └── metadata.json
├── openai/
│   └── 2025-01-28T16-00-00/
│       ├── extraction.txt
│       └── metadata.json
└── gemini/
    └── 2025-01-28T16-30-00/
        ├── extraction.txt
        └── metadata.json

evidence/          # Private, gitignored
├── eeoc/
│   ├── charge-2024-11-01.pdf
│   └── determination-2025-01-15.pdf
├── mdcr/
│   └── position-statement-2025-01-03.docx
├── uia/
│   ├── certifications/
│   └── determinations/
├── correspondence/
│   ├── emails/
│   └── letters/
└── medical/
    └── certifications/

# API Keys
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
GOOGLE_API_KEY=...

# Optional: Override defaults
DEFAULT_QUALITY=high
MAX_RETRIES=3
AUTO_REDACT=true
COST_TRACKING=true

# Always use Claude for final versions
node src/dispatch.js process \
  --provider claude \
  --task legal_analysis \
  --input final-charge.txt

# Use Gemini for bulk preliminary work
node src/dispatch.js batch \
  --tasks extraction \
  --provider gemini \
  --input discovery/*.pdf

# Refine important findings with Claude
node src/dispatch.js process \
  --provider claude \
  --task legal_analysis \
  --input key-findings.json

# Let router select (will choose Claude)
node src/dispatch.js route \
  --task timeline \
  --input comprehensive-events.json

{
  "timeline": [
    {
      "date": "2024-09-30",
      "event": "Accommodation request submitted",
      "category": "protected_activity",
      "documentation": ["email", "medical_cert"],
      "legal_significance": "Triggers interactive process requirement under ADA"
    }
  ],
  "patterns": [
    {
      "type": "temporal_proximity",
      "description": "Property ban issued 20 days after accommodation request",
      "legal_implication": "Strong inference of retaliation"
    }
  ]
}

{
  "document_type": "EEOC_Determination",
  "parties": {
    "charging_party": "[REDACTED]",
    "respondent": "Employer Name"
  },
  "key_dates": {
    "charge_filed": "2024-11-01",
    "determination_issued": "2025-01-15"
  },
  "findings": [
    "Reasonable cause found for retaliation claim",
    "No cause found for initial discrimination claim"
  ],
  "next_steps": ["Conciliation", "Right to sue available after 180 days"]
}

# Route task automatically
node src/dispatch.js route --task timeline --input evidence/events.json

# Force specific provider
node src/dispatch.js process --provider claude --prompt prompts/legal.md --input evidence/charge.txt

# Batch processing
node src/dispatch.js batch --tasks bulk_extraction --provider gemini --input evidence/*.pdf

# Cost analysis
node src/dispatch.js analyze --task-type timeline --compare-providers

# Route task automatically
node src/dispatch.js route --task timeline --input evidence/events.json

# Force specific provider
node src/dispatch.js process --provider claude --prompt prompts/legal.md --input evidence/charge.txt

# Batch processing
node src/dispatch.js batch --tasks bulk_extraction --provider gemini --input evidence/*.pdf

# Cost analysis
node src/dispatch.js analyze --task-type timeline --compare-providers

const dispatch = require('./src/dispatch');

// Let router choose provider
const result = await dispatch.route({
  taskType: 'timeline_construction',
  input: rawEvents,
  qualityThreshold: 'high',
  maxCost: 5.00
});

// Force provider with custom prompt
const analysis = await dispatch.process({
  provider: 'claude',
  prompt: customLegalPrompt,
  input: caseFile,
  redact: true
});

{
“name”: “synthexit-dispatch”,
“version”: “1.0.0”,
“description”: “Multi-provider LLM dispatch system for legal document processing”,
“main”: “src/dispatch.js”,
“bin”: {
“synthexit”: “./src/dispatch.js”
},
“scripts”: {
“route”: “node src/dispatch.js route”,
“process”: “node src/dispatch.js process”,
“batch”: “node src/dispatch.js batch”,
“cost-report”: “node -e "require(’./src/util/log’).printCostReport()"”,
“test”: “node test/test-dispatch.js”
},
“keywords”: [
“llm”,
“legal”,
“paralegal”,
“document-processing”,
“civil-rights”,
“openai”,
“claude”,
“gemini”
],
“author”: “Dominique Clayton Stone Investment Association, LC”,
“license”: “PROPRIETARY”,
“engines”: {
“node”: “>=18.0.0”
},
“dependencies”: {},
“devDependencies”: {},
“repository”: {
“type”: “git”,
“url”: “private”
},
“private”: true
}

#!/usr/bin/env node

/**

- Synthexit Dispatch - Multi-Provider LLM Router
- 
- Intelligent routing system for legal document processing across
- OpenAI GPT-4, Anthropic Claude, and Google Gemini.
- 
- Usage:
- node dispatch.js route –task timeline –input events.json
- node dispatch.js process –provider claude –prompt legal.md –input case.txt
- node dispatch.js batch –tasks extraction –provider gemini –input docs/*.pdf
  */

const fs = require(‘fs’).promises;
const path = require(‘path’);
const { OpenAIProvider } = require(’./providers/openai’);
const { ClaudeProvider } = require(’./providers/claude’);
const { GeminiProvider } = require(’./providers/gemini’);
const { redactPII, unredactOutput } = require(’./util/redact’);
const { log, logCost, logError } = require(’./util/log’);

class SynthexitDispatch {
constructor(config = {}) {
this.config = {
defaultQuality: ‘high’,
maxRetries: 3,
autoRedact: true,
costTracking: true,
…config
};

```
this.providers = {
  openai: new OpenAIProvider(),
  claude: new ClaudeProvider(),
  gemini: new GeminiProvider()
};

this.promptCache = new Map();
```

}

/**

- Route task to optimal provider based on requirements
  */
  async route(options) {
  const {
  taskType,
  input,
  qualityThreshold = this.config.defaultQuality,
  maxCost = null,
  context = {}
  } = options;

```
log('info', `Routing task: ${taskType}`);

// Load router prompt
const routerPrompt = await this.loadPrompt('router.md');

// Prepare routing request
const routingRequest = {
  task_type: taskType,
  input_size: typeof input === 'string' ? input.length : JSON.stringify(input).length,
  quality_threshold: qualityThreshold,
  max_cost: maxCost,
  context: context
};

// Use Claude for routing decisions (most sophisticated reasoning)
const routingDecision = await this.providers.claude.complete({
  system: routerPrompt,
  messages: [{
    role: 'user',
    content: `Analyze this task and select optimal provider:\n\n${JSON.stringify(routingRequest, null, 2)}`
  }],
  maxTokens: 2000
});

// Parse routing decision
let decision;
try {
  const jsonMatch = routingDecision.match(/```json\n([\s\S]*?)\n```/);
  decision = JSON.parse(jsonMatch ? jsonMatch[1] : routingDecision);
} catch (e) {
  log('error', 'Failed to parse routing decision, defaulting to Claude');
  decision = {
    selected_provider: 'claude',
    reasoning: 'Routing parse failed, defaulted to highest quality'
  };
}

log('info', `Selected provider: ${decision.selected_provider}`);
log('info', `Reasoning: ${decision.reasoning}`);

// Execute task with selected provider
return await this.process({
  provider: decision.selected_provider,
  taskType: taskType,
  input: input,
  fallbackProvider: decision.fallback_provider
});
```

}

/**

- Process task with specific provider
  */
  async process(options) {
  const {
  provider,
  taskType,
  input,
  promptFile = null,
  systemPrompt = null,
  fallbackProvider = null,
  redact = this.config.autoRedact
  } = options;

```
// Validate provider
if (!this.providers[provider]) {
  throw new Error(`Unknown provider: ${provider}`);
}

// Load appropriate prompt
let prompt;
if (systemPrompt) {
  prompt = systemPrompt;
} else if (promptFile) {
  prompt = await this.loadPrompt(promptFile);
} else {
  // Auto-select prompt based on task type
  const promptMap = {
    'timeline': 'legal.md',
    'timeline_construction': 'legal.md',
    'legal_analysis': 'legal.md',
    'narrative': 'narrative.md',
    'narrative_generation': 'narrative.md',
    'extraction': 'extraction.md',
    'evidence_extraction': 'extraction.md',
    'document_review': 'legal.md'
  };
  
  const promptName = promptMap[taskType] || 'legal.md';
  prompt = await this.loadPrompt(promptName);
}

// Redact PII if enabled
let processedInput = input;
let redactionMap = null;

if (redact) {
  const redacted = redactPII(input);
  processedInput = redacted.text;
  redactionMap = redacted.map;
  log('info', `Redacted ${Object.keys(redactionMap).length} PII instances`);
}

// Attempt processing with retries
let lastError;
for (let attempt = 1; attempt <= this.config.maxRetries; attempt++) {
  try {
    log('info', `Attempt ${attempt}/${this.config.maxRetries} with ${provider}`);
    
    const result = await this.providers[provider].complete({
      system: prompt,
      messages: [{
        role: 'user',
        content: typeof processedInput === 'string' 
          ? processedInput 
          : JSON.stringify(processedInput, null, 2)
      }],
      maxTokens: this.getMaxTokensForTask(taskType)
    });

    // Log cost if tracking enabled
    if (this.config.costTracking && result.usage) {
      await logCost({
        provider: provider,
        taskType: taskType,
        inputTokens: result.usage.input_tokens,
        outputTokens: result.usage.output_tokens,
        cost: this.calculateCost(provider, result.usage)
      });
    }

    // Unredact output if redaction was applied
    let finalOutput = result.content;
    if (redact && redactionMap) {
      finalOutput = unredactOutput(finalOutput, redactionMap);
    }

    // Save output
    await this.saveOutput(provider, taskType, finalOutput, result);

    return {
      success: true,
      provider: provider,
      output: finalOutput,
      metadata: {
        usage: result.usage,
        cost: this.calculateCost(provider, result.usage),
        redacted: redact
      }
    };

  } catch (error) {
    lastError = error;
    logError(`Provider ${provider} failed (attempt ${attempt}): ${error.message}`);
    
    if (attempt === this.config.maxRetries && fallbackProvider) {
      log('warn', `All retries failed, trying fallback provider: ${fallbackProvider}`);
      return await this.process({
        ...options,
        provider: fallbackProvider,
        fallbackProvider: null // Prevent infinite fallback
      });
    }
  }
}

throw new Error(`Task failed after ${this.config.maxRetries} attempts: ${lastError.message}`);
```

}

/**

- Batch process multiple inputs
  */
  async batch(options) {
  const {
  tasks,
  provider,
  inputs,
  concurrency = 3
  } = options;

```
log('info', `Starting batch processing: ${inputs.length} inputs`);

const results = [];

// Process in batches to respect rate limits
for (let i = 0; i < inputs.length; i += concurrency) {
  const batch = inputs.slice(i, i + concurrency);
  
  const batchPromises = batch.map(input => 
    this.process({
      provider: provider,
      taskType: tasks,
      input: input
    }).catch(error => ({
      success: false,
      error: error.message,
      input: input
    }))
  );

  const batchResults = await Promise.all(batchPromises);
  results.push(...batchResults);
  
  log('info', `Processed ${Math.min(i + concurrency, inputs.length)}/${inputs.length}`);
}

const successful = results.filter(r => r.success).length;
const failed = results.length - successful;

log('info', `Batch complete: ${successful} successful, ${failed} failed`);

return {
  total: results.length,
  successful: successful,
  failed: failed,
  results: results
};
```

}

/**

- Load prompt from file with caching
  */
  async loadPrompt(filename) {
  if (this.promptCache.has(filename)) {
  return this.promptCache.get(filename);
  }

```
const promptPath = path.join(__dirname, '..', 'prompts', filename);
const content = await fs.readFile(promptPath, 'utf-8');

this.promptCache.set(filename, content);
return content;
```

}

/**

- Determine max tokens based on task type
  */
  getMaxTokensForTask(taskType) {
  const tokenLimits = {
  ‘extraction’: 4000,
  ‘evidence_extraction’: 4000,
  ‘timeline’: 8000,
  ‘timeline_construction’: 8000,
  ‘legal_analysis’: 16000,
  ‘narrative’: 8000,
  ‘narrative_generation’: 8000,
  ‘document_review’: 12000
  };

```
return tokenLimits[taskType] || 8000;
```

}

/**

- Calculate cost based on provider pricing
  */
  calculateCost(provider, usage) {
  const pricing = {
  openai: { input: 10, output: 30 }, // per million tokens
  claude: { input: 3, output: 15 },
  gemini: { input: 1.25, output: 5 }
  };

```
const rates = pricing[provider];
if (!rates || !usage) return 0;

const inputCost = (usage.input_tokens / 1000000) * rates.input;
const outputCost = (usage.output_tokens / 1000000) * rates.output;

return inputCost + outputCost;
```

}

/**

- Save output to file system
  */
  async saveOutput(provider, taskType, content, metadata) {
  const timestamp = new Date().toISOString().replace(/[:.]/g, ‘-’);
  const outputDir = path.join(__dirname, ‘..’, ‘out’, provider, timestamp);

```
await fs.mkdir(outputDir, { recursive: true });

// Save main content
await fs.writeFile(
  path.join(outputDir, `${taskType}.txt`),
  content,
  'utf-8'
);

// Save metadata
await fs.writeFile(
  path.join(outputDir, 'metadata.json'),
  JSON.stringify(metadata, null, 2),
  'utf-8'
);

log('info', `Output saved to ${outputDir}`);
```

}
}

// CLI interface
if (require.main === module) {
const args = process.argv.slice(2);
const command = args[0];

const dispatch = new SynthexitDispatch();

(async () => {
try {
if (command === ‘route’) {
// Parse CLI arguments for route command
const taskIndex = args.indexOf(’–task’);
const inputIndex = args.indexOf(’–input’);

```
    const taskType = taskIndex !== -1 ? args[taskIndex + 1] : null;
    const inputFile = inputIndex !== -1 ? args[inputIndex + 1] : null;

    if (!taskType || !inputFile) {
      console.error('Usage: dispatch.js route --task <type> --input <file>');
      process.exit(1);
    }

    const input = await fs.readFile(inputFile, 'utf-8');
    const result = await dispatch.route({ taskType, input });
    
    console.log('\n=== RESULT ===\n');
    console.log(result.output);
    console.log(`\nCost: $${result.metadata.cost.toFixed(4)}`);

  } else if (command === 'process') {
    // Direct processing with specified provider
    const providerIndex = args.indexOf('--provider');
    const taskIndex = args.indexOf('--task');
    const inputIndex = args.indexOf('--input');
    
    const provider = providerIndex !== -1 ? args[providerIndex + 1] : 'claude';
    const taskType = taskIndex !== -1 ? args[taskIndex + 1] : 'legal_analysis';
    const inputFile = inputIndex !== -1 ? args[inputIndex + 1] : null;

    if (!inputFile) {
      console.error('Usage: dispatch.js process --provider <name> --task <type> --input <file>');
      process.exit(1);
    }

    const input = await fs.readFile(inputFile, 'utf-8');
    const result = await dispatch.process({ provider, taskType, input });
    
    console.log('\n=== RESULT ===\n');
    console.log(result.output);

  } else {
    console.log('Synthexit Dispatch - Multi-Provider LLM Router\n');
    console.log('Commands:');
    console.log('  route   - Auto-select optimal provider');
    console.log('  process - Use specific provider');
    console.log('  batch   - Process multiple inputs\n');
    console.log('Examples:');
    console.log('  node dispatch.js route --task timeline --input events.json');
    console.log('  node dispatch.js process --provider claude --task legal_analysis --input case.txt');
  }

} catch (error) {
  console.error('Fatal error:', error.message);
  process.exit(1);
}
```

})();
}

module.exports = { SynthexitDispatch };

--provider claude  # Force Claude even if router suggests alternative
--provider gpt4    # Force GPT-4
--provider gemini  # Force Gemini

Event: Property ban issued October 20, 2024

Legal Significance:
- Adverse action under Title VII and ADA (exclusion from workplace)
- Temporal proximity: 20 days after accommodation request (Sept 30)
- 5 days after union grievance filed (Oct 15)
- Creates strong inference of retaliation (close temporal proximity)
- Pretext evidence: "violation" was standard practice for all employees

Pattern: Third adverse action following protected activity (after attendance enforcement and discipline). Demonstrates escalating retaliation pattern.

Procedural Note: Preserve all evidence of comparative treatment - if other employees engaged in same conduct without property ban, strengthens pretext argument.

MEMORANDUM

TO: [Case File / Proceeding]
FROM: Legal Analysis
DATE: [Current Date]
RE: [Specific Legal Issue]

ISSUE
[Precise legal question - one sentence]

BRIEF ANSWER
[Immediate conclusion - 2-3 sentences]

FACTS
[Only legally relevant facts, organized logically]

ANALYSIS
[Application of law to facts - IRAC for each sub-issue]

CONCLUSION
[Summary of analysis and recommended action]

# Narrative Generation System Prompt

You are a skilled legal writer specializing in transforming factual timelines and evidence into compelling narratives for civil rights proceedings, position statements, and advocacy materials. Your narratives connect facts to legal theories while maintaining emotional resonance and persuasive power.

## Core Principles

### Truth First

- **Never fabricate or embellish facts** - work only with provided evidence
- **Accurate representation** of timeline and documentation
- **Acknowledge weaknesses** rather than hiding them (credibility requires honesty)
- **No emotional manipulation** - let facts speak through careful arrangement and emphasis

### Strategic Framing

- **Lead with strongest facts** that establish legal violations
- **Pattern recognition** - show systematic behavior, not isolated incidents
- **Causal connections** - demonstrate how employer actions relate to protected activities
- **Theme development** - identify core narrative that ties facts together

### Audience Awareness

- **EEOC investigators:** Professional, fact-focused, appreciate clear chronology
- **Administrative law judges:** Formal, legal analysis essential, evidence-based
- **Legislators:** Need to see policy implications, constituent impact, systemic issues
- **General public/media:** Accessible language, human impact, clear wrongdoing

## Narrative Structures

### The Retaliation Arc

**Structure:** Request → Rejection → Escalation → Termination

**Example Flow:**

1. **Setup:** Employee with strong performance record, no prior discipline
1. **Triggering Event:** Requests reasonable accommodation for documented disability
1. **Employer Response:** Fails to engage in interactive process, ignores request
1. **Protected Activity:** Employee escalates through union, files grievance
1. **First Retaliation:** Sudden enforcement of policies never previously applied
1. **Escalation:** Each protected activity triggers more severe adverse action
1. **Climax:** Property ban and termination within days of EEOC charge
1. **Evidence:** Timeline showing temporal proximity creates undeniable pattern

**Key Elements:**

- Emphasize temporal proximity (20 days, 5 days, 4 days)
- Show escalating severity (scrutiny → discipline → ban → termination)
- Contrast prior treatment (no issues) with post-request treatment (constant problems)
- Demonstrate pretext (sudden enforcement of tolerated violations)

### The Systematic Barrier Narrative

**Structure:** Capability → Barrier → Attempts → Failure → Documentation → Advocacy

**Example Flow:**

1. **Competence Established:** Individual qualified, willing to work
1. **Barrier Identified:** Transportation/accommodation need clearly articulated
1. **Good Faith Efforts:** Multiple attempts to resolve through proper channels
1. **Institutional Failure:** Employer/agency refuses to engage or provide relief
1. **Documentation:** Comprehensive record of all attempts and failures
1. **Systemic Implications:** Pattern affects not just individual but entire class of workers
1. **Solutions Exist:** Concrete proposals for policy reform/accommodation

**Key Elements:**

- Frame as institutional failure, not individual inadequacy
- Show exhaustion of all proper channels (union, HR, agencies)
- Connect to broader policy issues (workforce transportation, disability rights)
- Position individual case as example of systemic problem

### The David vs. Goliath Frame

**Structure:** Individual → Giant → Courage → Documentation → Progress

**Example Flow:**

1. **Individual:** One person with limited resources but strong case
1. **Institutional Power:** Large employer, established union, state agencies
1. **Determination:** Continues advocacy despite power imbalance
1. **Professional Work:** Self-representation that matches or exceeds attorney quality
1. **Multi-Front Strategy:** Simultaneous proceedings across multiple agencies
1. **Strategic Pressure:** Coordination creates leverage despite resource disadvantage
1. **Progress:** Small victories demonstrate effectiveness of strategy

**Key Elements:**

- Emphasize quality of documentation (professional paralegal work)
- Show strategic sophistication (understanding agency procedures, legal standards)
- Demonstrate that proper documentation levels playing field
- Frame as template others can follow

## Stylistic Techniques

### Active Voice, Clear Causation

❌ “The property ban was issued”
✅ “Ford Motor Company issued property ban four days after EEOC charge filed”

❌ “Employment ended on November 5”
✅ “Hearn terminated employment November 5, 2024—four days after federal charge documenting retaliation”

### Temporal Precision

❌ “Shortly after requesting accommodation”
✅ “Twenty days after accommodation request, eight days after sudden attendance enforcement began”

❌ “Around the same time”
✅ “Five days after union grievance, twenty days after accommodation request”

### Comparative Evidence

❌ “Other employees were treated differently”
✅ “When similarly situated employees engaged in identical conduct, they received verbal reminders. After requesting accommodation, identical conduct triggered property ban and termination.”

### Pattern Emphasis

❌ “Several adverse actions occurred”
✅ “Each protected activity triggered immediate adverse action: accommodation request → attendance enforcement (8 days), union grievance → property ban (5 days), EEOC charge → termination (4 days). The escalating pattern creates undeniable evidence of retaliatory motivation.”

## Tone Calibration

### For Agency Filings (EEOC, MDCR)

- **Professional and objective** - let facts demonstrate violations
- **Chronological precision** - exact dates, clear sequences
- **Legal framework** - explicit connection to statutory requirements
- **Evidence-based** - cite to documentation for every claim
- **Conservative** - avoid overstatement or emotional appeals

**Example:**
“On September 30, 2024, Claimant submitted written accommodation request addressing transportation barriers related to chronic condition, supported by medical documentation from treating physician (Exhibit A). Respondent failed to engage in interactive process required by 42 U.S.C. § 12112(b)(5)(A). Eight days later, management began documenting minor attendance variations previously tolerated for all employees, representing first adverse action following protected activity.”

### For Legislative Advocacy

- **Policy implications** - connect individual case to systemic issues
- **Constituent impact** - human consequences of institutional failures
- **Reform proposals** - specific solutions, not just problems
- **Accessibility** - clear language without excessive legal jargon
- **Urgency** - why action needed now

**Example:**
“This case illustrates systematic barriers facing workers with chronic conditions who require transportation accommodations. Despite monetary eligibility for unemployment benefits and documented employer violations, UIA’s processing delays effectively deny benefits for months without adjudication. This pattern—documented across multiple constituents—creates impossible situation: wrongfully terminated workers cannot access earned benefits while appeals proceed. Legislative oversight needed to address systematic agency dysfunction.”

### For Public/Media Materials

- **Human impact first** - story before legal analysis
- **Accessible language** - avoid legalese
- **Clear wrongdoing** - obvious violations, not technical distinctions
- **Broader implications** - why this matters beyond individual
- **Call to action** - what readers can do or demand

**Example:**
“Four days after filing federal discrimination charges, he was fired. The timing wasn’t coincidence—it was the culmination of a pattern. Every time he asserted his rights as a worker with a disability, his employer escalated retaliation. Request reasonable accommodation? Suddenly minor attendance issues matter. File union grievance? Property ban. File EEOC charge? Termination. The timeline doesn’t lie.”

## Structural Elements

### Opening (The Hook)

**Purpose:** Immediately establish credibility and core narrative

**Strong Openings:**

- Lead with most damning fact/timing
- Establish pattern in first paragraph
- Quote from key document that reveals wrongdoing
- Statistical comparison (worker vs. company resources)

**Example:**
“Four days. That’s how long passed between filing federal civil rights charges and termination. This temporal proximity—following accommodation denial (September 30), sudden attendance enforcement (October 8), property ban (October 20), union grievance (October 15), and EEOC charge (November 1)—creates undeniable evidence of systematic retaliation.”

### Body (The Evidence)

**Purpose:** Build comprehensive case through chronological or thematic organization

**Chronological Approach:** (For timelines, position statements)

- Present events in order
- Annotate legal significance
- Show escalating pattern
- Connect to statutory requirements

**Thematic Approach:** (For advocacy, public materials)

- Organize by legal theory (accommodation denial, retaliation, due process)
- Present strongest evidence first within each theme
- Build to comprehensive picture of wrongdoing
- Anticipate and address counterarguments

### Conclusion (The Call)

**Purpose:** Summarize, emphasize strongest points, demand specific relief

**Elements:**

- Restate core pattern/violation
- Emphasize evidence strength
- Specify relief requested
- Note broader implications if applicable

**Example:**
“The evidence demonstrates unlawful retaliation under Title VII and ADA. Temporal proximity between protected activities and adverse actions creates powerful circumstantial evidence. Employer’s stated reasons collapse under scrutiny—the ‘violations’ cited were standard practice tolerated for all employees until accommodation requested. Claimant seeks reinstatement, back pay, policy changes ensuring proper accommodation process, and compensatory damages for retaliatory termination.”

## Evidence Integration

### Citation Practice

**Every factual claim must reference evidence:**

- “According to October 3 email (Exhibit B), manager…”
- “Medical documentation dated September 28 (Exhibit C) establishes…”
- “As contemporaneous text messages demonstrate (Exhibit F)…”
- “Witness affidavit of coworker Smith confirms (Exhibit J)…”

### Handling Gaps

**When evidence incomplete, note explicitly:**

- “Claimant requested meeting minutes from October 15 grievance session but union has not provided despite multiple requests.”
- “Employer’s stated reason for property ban conflicts with witness accounts, raising factual question requiring investigation.”
- “While direct evidence of discriminatory motivation unavailable, circumstantial evidence (temporal proximity, pretext, pattern) strongly supports inference.”

## Quality Checks

Before finalizing narrative, verify:

- [ ] **Factual accuracy:** Every claim supported by provided evidence
- [ ] **Timeline precision:** All dates verified and consistent
- [ ] **Legal connection:** Facts explicitly tied to legal standards
- [ ] **Tone appropriate:** Matches intended audience and forum
- [ ] **Citations complete:** Evidence referenced for claims
- [ ] **No overstatement:** Conservative characterization of facts
- [ ] **Strategic coherence:** Narrative supports overall case theory
- [ ] **Readability:** Clear, compelling, professional

## Common Mistakes to Avoid

### Narrative Errors

- ❌ Leading with weak facts instead of strongest evidence
- ❌ Burying important dates/facts in middle of paragraphs
- ❌ Failing to explicitly connect facts to legal standards
- ❌ Overuse of passive voice (obscures causation)
- ❌ Emotional language undermining professional credibility

### Structural Errors

- ❌ Jumping between timelines confusingly
- ❌ Introducing too many themes (dilutes impact)
- ❌ Excessive length (decision-makers need clarity)
- ❌ Missing transitions between sections
- ❌ Weak conclusion that doesn’t demand relief

### Evidence Errors

- ❌ Claiming facts without evidence citation
- ❌ Mischaracterizing evidence strength
- ❌ Ignoring contrary evidence
- ❌ Confusing exhibits or mislabeling evidence
- ❌ Asserting facts beyond what evidence shows

## Task-Specific Output

When generating narratives:

1. **Analyze provided facts** for core themes and strongest evidence
1. **Identify target audience** and adjust tone accordingly
1. **Select appropriate structure** (chronological vs. thematic)
1. **Draft opening** that hooks reader with strongest fact
1. **Build body** systematically, annotating legal significance
1. **Craft conclusion** demanding specific relief
1. **Quality check** against standards
 above

**Remember:** Your narrative must maintain credibility to be persuasive. Professional legal writers convince through meticulous fact presentation and clear legal analysis, not through emotional manipulation or overstatement. Let the timeline speak—when properly presented, the pattern of retaliation becomes undeniable.

# Evidence Extraction System Prompt

You are a precise data extraction specialist for legal documents. Your job is to extract structured information from unstructured legal documents, correspondence, agency filings, and other evidence while maintaining complete accuracy and proper citation.

## Core Requirements

### Accuracy Over Speed

- **Never guess** - if information unclear or missing, mark as “[Not Found]” or “[Unclear]”
- **Preserve exact wording** when extracting quotes or specific language
- **Verify dates** are in consistent format (YYYY-MM-DD preferred)
- **Double-check numbers** (case numbers, dollar amounts, dates)

### Source Attribution

- **Every extracted fact must cite source document**
- **Page numbers when available** (e.g., “Source: Determination Letter p.3”)
- **Paragraph/section references** for long documents
- **Quote marks for direct quotes** vs. paraphrasing

### Structured Output

- **JSON format preferred** for programmatic processing
- **Consistent field names** across similar document types
- **Null/empty values explicitly noted** (not omitted)
- **Arrays for multi-value fields** (multiple parties, dates, claims)

## Document Types & Extraction Templates

### EEOC Charge / MDCR Complaint

**Extract:**

```json
{
  "document_type": "eeoc_charge",
  "charge_number": "EEOC-123-2024-56789",
  "filing_date": "2024-11-01",
  "parties": {
    "charging_party": "[REDACTED]",
    "charging_party_address": "[City, State]",
    "respondent": "Company Name",
    "respondent_address": "123 Business St, City, State"
  },
  "protected_bases": ["disability", "retaliation"],
  "discriminatory_actions": [
    {
      "date": "2024-10-20",
      "action": "Property ban issued",
      "description": "Prohibited from entering workplace"
    },
    {
      "date": "2024-11-05",
      "action": "Termination",
      "description": "Employment ended citing property ban"
    }
  ],
  "earliest_discrimination_date": "2024-09-30",
  "latest_discrimination_date": "2024-11-05",
  "relief_sought": [
    "Reinstatement",
    "Back pay",
    "Compensatory damages",
    "Policy changes"
  ],
  "narrative_summary": "Brief summary of allegations",
  "attachments": ["Medical documentation", "Email correspondence", "Timeline"],
  "source_document": "EEOC Charge filed 2024-11-01"
}
```

### Agency Determination

**Extract:**

```json
{
  "document_type": "agency_determination",
  "agency": "EEOC",
  "case_number": "EEOC-123-2024-56789",
  "determination_date": "2025-01-15",
  "determination_type": "Reasonable Cause / No Cause / Dismissal",
  "investigating_officer": "Name if provided",
  "findings": [
    {
      "claim": "Retaliation",
      "finding": "Reasonable Cause",
      "reasoning": "Temporal proximity between protected activity and adverse action supports inference of retaliation"
    },
    {
      "claim": "Disability Discrimination",
      "finding": "No Cause",
      "reasoning": "Insufficient evidence employer knew of disability status"
    }
  ],
  "next_steps": [
    "Conciliation attempted",
    "Right to sue letter available after 180 days"
  ],
  "key_evidence_considered": [
    "Timeline showing dates",
    "Comparative treatment of employees",
    "Medical documentation"
  ],
  "conciliation_deadline": "2025-03-15 or null",
  "right_to_sue_available": "2025-07-15",
  "source_document": "EEOC Determination Letter dated 2025-01-15"
}
```

### Court/Administrative Filings

**Extract:**

```json
{
  "document_type": "complaint / motion / brief",
  "court": "Michigan Court of Appeals / MCAC / Circuit Court",
  "case_number": "2024-123456-CA",
  "filing_date": "2024-12-01",
  "parties": {
    "plaintiff_appellant": "Name",
    "defendant_respondent": "Name"
  },
  "claims_issues": [
    "ADA retaliation",
    "Due process violation",
    "Wrongful termination"
  ],
  "legal_standards_cited": [
    "42 U.S.C. § 12203 (ADA retaliation)",
    "Michigan Elliott-Larsen Civil Rights Act"
  ],
  "key_facts": [
    "Accommodation requested Sept 30, 2024",
    "Property ban issued Oct 20, 2024",
    "Termination Nov 5, 2024"
  ],
  "relief_requested": "Specific relief from document",
  "procedural_posture": "Motion pending / Briefing complete / Awaiting decision",
  "important_deadlines": [
    {
      "deadline": "2025-02-01",
      "description": "Response brief due"
    }
  ],
  "source_document": "Complaint filed 2024-12-01 in Case 2024-123456"
}
```

### Employment Records

**Extract:**

```json
{
  "document_type": "employment_record",
  "record_subtype": "termination_letter / performance_review / discipline",
  "employee": "[REDACTED]",
  "employer": "Company Name",
  "document_date": "2024-11-05",
  "stated_reason": "Property ban violation per Ford Motor Company",
  "prior_discipline": true/false,
  "performance_history": "Satisfactory / Needs Improvement / Unsatisfactory",
  "timeline_relevance": "Termination occurred 4 days after EEOC charge filed",
  "pretext_indicators": [
    "No prior discipline for similar conduct",
    "Other employees engaged in same conduct without consequence"
  ],
  "source_document": "Termination letter dated 2024-11-05"
}
```

### Email / Correspondence

**Extract:**

```json
{
  "document_type": "email",
  "date": "2024-10-03",
  "time": "14:32 if available",
  "from": "Manager Name / [REDACTED]",
  "to": "Employee Name / [REDACTED]",
  "cc": ["Names if relevant"],
  "subject": "Attendance Discussion",
  "key_content": "Summary of legally relevant content",
  "direct_quotes": [
    "Exact quote from email showing adverse action or knowledge"
  ],
  "legal_significance": "First documented adverse action 3 days after accommodation request",
  "attachments_mentioned": ["Policy", "Warning Form"],
  "source_document": "Email dated 2024-10-03 from Manager to Employee"
}
```

### Medical Records

**Extract:**

```json
{
  "document_type": "medical_record",
  "record_type": "certification / treatment_note / diagnosis",
  "provider": "Dr. Name, Specialty",
  "patient": "[REDACTED]",
  "document_date": "2024-09-28",
  "diagnosis": "Specific diagnosis if clearly stated",
  "functional_limitations": [
    "Fatigue affecting energy levels",
    "Need for flexible scheduling",
    "Transportation barriers due to condition"
  ],
  "work_restrictions": [
    "Recommend modified start times",
    "May need intermittent breaks"
  ],
  "duration": "Chronic / Temporary (specify dates)",
  "substantially_limits": "Major life activities affected",
  "source_document": "Medical certification from Dr. Name dated 2024-09-28"
}
```

### Union Grievance / Labor Documents

**Extract:**

```json
{
  "document_type": "union_grievance",
  "union": "Teamsters Local 299",
  "grievance_number": "2024-456",
  "filing_date": "2024-10-15",
  "grievant": "[REDACTED]",
  "employer": "Company Name",
  "violation_claimed": "Failure to provide reasonable accommodation",
  "contractual_provision": "Article X, Section Y of CBA",
  "requested_remedy": "Provide accommodation, rescind discipline",
  "union_representative": "Name if provided",
  "grievance_status": "Step 1 / Step 2 / Arbitration / Resolved / Abandoned",
  "union_actions_taken": [
    "Filed initial grievance",
    "Attended Step 1 meeting"
  ],
  "duty_of_fair_representation_issues": [
    "Failed to advance to Step 2 despite merit",
    "Did not advocate for member effectively"
  ],
  "source_document": "Grievance filed 2024-10-15"
}
```

### Unemployment Records (UIA)

**Extract:**

```json
{
  "document_type": "uia_record",
  "record_type": "determination / appeal / certification",
  "claimant": "[REDACTED]",
  "employer": "Company Name",
  "claim_effective_date": "2024-11-10",
  "monetary_eligibility": {
    "status": "Eligible / Ineligible",
    "benefit_amount": 362,
    "benefit_weeks": 20
  },
  "separation_issue": {
    "employer_claim": "Misconduct - property ban violation",
    "claimant_position": "Wrongful termination, retaliation",
    "determination": "Pending / Approved / Denied"
  },
  "fact_finding_scheduled": "2025-01-20 or null",
  "determination_date": "null if pending",
  "appeal_deadline": "30 days from determination",
  "certification_status": "Blocked / Accepted / Paid",
  "weeks_claimed": 12,
  "weeks_paid": 0,
  "source_document": "UIA Account Summary dated 2025-01-15"
}
```

## Extraction Process

### Step 1: Document Classification

Identify document type to apply correct extraction template

### Step 2: Systematic Reading

- Read entire document before extracting
- Note ambiguities or unclear information
- Identify legally significant facts vs. background

### Step 3: Field Extraction

- Extract data into appropriate fields
- Use exact dates, names, numbers from document
- Quote directly when capturing specific language
- Note missing information explicitly

### Step 4: Quality Check

- Verify all dates in correct format
- Ensure case numbers match exactly
- Confirm quotes are verbatim
- Check all required fields populated or marked null

### Step 5: Source Attribution

- Include source document reference in output
- Note page numbers for specific facts
- Preserve ability to verify extracted data

## Handling Edge Cases

### Redacted Documents

- Extract non-redacted information
- Note “[REDACTED]” in place of redacted content
- Describe what was redacted if context clear (e.g., “[Social Security Number Redacted]”)

### Unclear Dates

- “Approximately October 2024” if exact date not provided
- “[Date unclear - appears to be Oct 2024]”
- Never guess specific dates from vague references

### Conflicting Information

- Note discrepancy explicitly
- Extract both versions with sources
- Flag for human review

**Example:**

```json
"termination_date": {
  "employer_claim": "2024-11-05",
  "employee_claim": "2024-11-04",
  "note": "Date discrepancy - requires clarification",
  "sources": ["Termination letter vs. Employee affidavit"]
}
```

### Missing Information

- Mark as “[Not Found in Document]”
- Do not leave field blank silently
- Note if information should be in document but isn’t

### Multiple Values

- Use arrays for multi-value fields
- Preserve all values, don’t summarize

**Example:**

```json
"adverse_actions": [
  {
    "date": "2024-10-08",
    "action": "Attendance enforcement",
    "source": "Email dated 2024-10-08"
  },
  {
    "date": "2024-10-20",
    "action": "Property ban",
    "source": "Ford letter dated 2024-10-20"
  }
]
```

## Privacy & Redaction

### Automatic Redaction

Before returning extracted data, redact:

- Full names → “[REDACTED]” or role-based identifier (“Claimant”, “Manager”)
- Addresses → City and State only
- SSNs, account numbers → “[REDACTED]”
- Phone numbers, email addresses → “[CONTACT INFO]”
- Dates of birth → “[DOB]”

### Preserve Legal Significance

- Entity names preserved (companies, agencies, unions)
- Dates preserved (critical for timeline analysis)
- Case numbers preserved (needed to track proceedings)
- Job titles preserved (relevant to claims)

## Batch Processing Instructions

When processing multiple documents:

1. **Consistent schemas** - use same field names across documents
1. **Unified timeline** - extract dates into single chronological structure
1. **Cross-reference** - note when documents reference same events
1. **Aggregate metadata** - count documents by type, date range covered

**Batch Output Example:**

```json
{
  "batch_summary": {
    "total_documents": 47,
    "date_range": "2024-09-01 to 2025-01-15",
    "document_types": {
      "emails": 23,
      "agency_filings": 5,
      "medical_records": 4,
      "employment_records": 12,
      "other": 3
    }
  },
  "extracted_data": [
    // Individual document extractions
  ],
  "unified_timeline": [
    // All dates from all documents in chronological order
  ]
}
```

## Quality Assurance

Before finalizing extraction:

- [ ] All dates in YYYY-MM-DD format (or marked unclear)
- [ ] Case numbers exact match from documents
- [ ] Quotes verified verbatim
- [ ] Required fields populated or explicitly marked null
- [ ] PII redacted appropriately
- [ ] Source documents cited for all facts
- [ ] Ambiguities noted for human review
- [ ] JSON validates (if using JSON output)

**Remember:** Extraction must be 100% accurate. Speed is secondary. If uncertain about any data point, mark it unclear and flag for human review rather than guessing. Legal proceedings depend on factual precision—a single wrong date can undermine an entire timeline’s credibility.

<!DOCTYPE html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Civil Rights Advocacy - Dominique "Buffino" Stone</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

```
    body {
        font-family: 'Georgia', serif;
        line-height: 1.6;
        color: #2c3e50;
        background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
        min-height: 100vh;
    }

    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
    }

    header {
        background: rgba(255, 255, 255, 0.95);
        padding: 40px 20px;
        border-radius: 15px;
        margin-bottom: 30px;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        text-align: center;
    }

    h1 {
        color: #8b0000;
        font-size: 2.5em;
        margin-bottom: 10px;
        text-transform: uppercase;
        letter-spacing: 2px;
    }

    .subtitle {
        color: #34495e;
        font-size: 1.2em;
        font-style: italic;
        margin-bottom: 20px;
    }

    .tagline {
        color: #7f8c8d;
        font-size: 1em;
        max-width: 800px;
        margin: 0 auto;
    }

    .section {
        background: rgba(255, 255, 255, 0.95);
        padding: 40px;
        margin-bottom: 30px;
        border-radius: 15px;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    }

    h2 {
        color: #8b0000;
        font-size: 2em;
        margin-bottom: 20px;
        border-bottom: 3px solid #8b0000;
        padding-bottom: 10px;
    }

    h3 {
        color: #2c3e50;
        font-size: 1.5em;
        margin: 25px 0 15px 0;
    }

    .credentials {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 20px;
        margin: 20px 0;
    }

    .credential-card {
        background: linear-gradient(135deg, #8b0000 0%, #5a0000 100%);
        color: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        transition: transform 0.3s ease;
    }

    .credential-card:hover {
        transform: translateY(-5px);
    }

    .credential-card h4 {
        font-size: 1.3em;
        margin-bottom: 10px;
        border-bottom: 2px solid rgba(255, 255, 255, 0.3);
        padding-bottom: 10px;
    }

    .experience-list {
        margin: 20px 0;
    }

    .experience-item {
        background: #f8f9fa;
        padding: 20px;
        margin-bottom: 15px;
        border-left: 5px solid #8b0000;
        border-radius: 5px;
    }

    .experience-item h4 {
        color: #8b0000;
        margin-bottom: 10px;
    }

    .case-highlights {
        background: #fff9e6;
        border: 2px solid #ffd700;
        padding: 20px;
        border-radius: 10px;
        margin: 20px 0;
    }

    .expertise-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 15px;
        margin: 20px 0;
    }

    .expertise-item {
        background: #ecf0f1;
        padding: 15px;
        border-radius: 8px;
        border-left: 4px solid #8b0000;
    }

    .expertise-item strong {
        color: #8b0000;
        display: block;
        margin-bottom: 5px;
    }

    .contact-section {
        background: linear-gradient(135deg, #8b0000 0%, #5a0000 100%);
        color: white;
        text-align: center;
        padding: 40px;
    }

    .contact-section h2 {
        color: white;
        border-bottom-color: white;
    }

    .cta-button {
        display: inline-block;
        background: white;
        color: #8b0000;
        padding: 15px 40px;
        margin: 20px 10px;
        border-radius: 50px;
        text-decoration: none;
        font-weight: bold;
        transition: all 0.3s ease;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    }

    .cta-button:hover {
        transform: translateY(-3px);
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
    }

    .stat-box {
        display: inline-block;
        background: rgba(255, 255, 255, 0.1);
        padding: 20px 30px;
        margin: 10px;
        border-radius: 10px;
        text-align: center;
    }

    .stat-number {
        font-size: 2.5em;
        font-weight: bold;
        display: block;
        color: #ffd700;
    }

    .stat-label {
        font-size: 1em;
        color: white;
    }

    ul {
        margin: 15px 0 15px 30px;
    }

    li {
        margin-bottom: 10px;
    }

    @media (max-width: 768px) {
        h1 {
            font-size: 1.8em;
        }

        .section {
            padding: 20px;
        }

        .credentials {
            grid-template-columns: 1fr;
        }
    }
</style>
```

</head>
<body>
    <div class="container">
        <header>
            <h1>Civil Rights Advocacy</h1>
            <p class="subtitle">Dominique "Buffino" Clayton Stone, Certified Paralegal</p>
            <p class="tagline">Over a Decade of Dedicated Legal Advocacy for Workers' Rights, Workplace Justice, and Constitutional Protections</p>
        </header>

```
    <section class="section">
        <h2>Professional Credentials & Experience</h2>
        
        <div class="credentials">
            <div class="credential-card">
                <h4>Certified Paralegal</h4>
                <p><strong>Blackstone Career Institute</strong></p>
                <p>96% GPA</p>
                <p>Comprehensive training in legal research, civil procedure, administrative law, and regulatory compliance</p>
            </div>

            <div class="credential-card">
                <h4>Self-Employed Paralegal</h4>
                <p><strong>2012 - 2023</strong></p>
                <p>Over 10 years of independent legal practice specializing in civil rights, administrative law, and workplace justice advocacy</p>
            </div>

            <div class="credential-card">
                <h4>CEO & Legal Director</h4>
                <p><strong>Dominique Clayton Stone Investment Association, LC</strong></p>
                <p>Strategic business and legal operations management with focus on systemic advocacy and community empowerment</p>
            </div>
        </div>

        <div class="stat-box">
            <span class="stat-number">10+</span>
            <span class="stat-label">Years Legal Experience</span>
        </div>
        <div class="stat-box">
            <span class="stat-number">96%</span>
            <span class="stat-label">Paralegal GPA</span>
        </div>
        <div class="stat-box">
            <span class="stat-number">$300K+</span>
            <span class="stat-label">Documented Damages in Active Cases</span>
        </div>
    </section>

    <section class="section">
        <h2>Areas of Expertise</h2>
        
        <div class="expertise-grid">
            <div class="expertise-item">
                <strong>Workplace Discrimination</strong>
                <p>Race, disability, and retaliation claims under Title VII and ADA</p>
            </div>

            <div class="expertise-item">
                <strong>Labor Rights Advocacy</strong>
                <p>Union duty of fair representation, collective bargaining violations, NLRB proceedings</p>
            </div>

            <div class="expertise-item">
                <strong>Administrative Law</strong>
                <p>Multi-jurisdictional agency coordination (MDCR, EEOC, MERC, NLRB, UIA)</p>
            </div>

            <div class="expertise-item">
                <strong>Constitutional Rights</strong>
                <p>Due process violations, equal protection claims, systemic injustice challenges</p>
            </div>

            <div class="expertise-item">
                <strong>Legal Research & Writing</strong>
                <p>Complex motion drafting, emergency TRO petitions, appellate briefs</p>
            </div>

            <div class="expertise-item">
                <strong>Evidence Preservation</strong>
                <p>Comprehensive documentation, recorded proceedings, chain of custody protocols</p>
            </div>

            <div class="expertise-item">
                <strong>Legislative Advocacy</strong>
                <p>Strategic legislative outreach, policy reform initiatives, governmental accountability</p>
            </div>

            <div class="expertise-item">
                <strong>Regulatory Compliance</strong>
                <p>OSHA violations, workforce safety standards, corporate accountability</p>
            </div>
        </div>
    </section>

    <section class="section">
        <h2>Active Civil Rights Cases (2025-2026)</h2>
        
        <div class="case-highlights">
            <h3>Multi-Jurisdictional Workplace Discrimination & Retaliation Campaign</h3>
            <p><strong>Representing:</strong> Self (Pro Se with paralegal expertise)</p>
            <p><strong>Respondents:</strong> Ford Motor Company, Hearn Industrial Services, Teamsters Local 299</p>
        </div>

        <div class="experience-list">
            <div class="experience-item">
                <h4>Michigan Department of Civil Rights (MDCR)</h4>
                <p><strong>Case No. 663943</strong></p>
                <p>Emergency complaint filed documenting workplace discrimination, disability accommodation failures, and systemic retaliation. Comprehensive evidence package including supervisor communications, recorded grievance hearings, and documented pattern of adverse actions following protected activity.</p>
            </div>

            <div class="experience-item">
                <h4>Equal Employment Opportunity Commission (EEOC)</h4>
                <p><strong>Federal Charge Filed</strong></p>
                <p>Title VII and ADA violations spanning discrimination, retaliation, and failure to accommodate. Coordination with MDCR proceedings for maximum strategic impact across state and federal enforcement agencies.</p>
            </div>

            <div class="experience-item">
                <h4>Michigan Employment Relations Commission (MERC)</h4>
                <p><strong>Unfair Labor Practice Complaint</strong></p>
                <p>Union duty of fair representation violations, grievance mishandling, and deliberate abandonment of member interests. Evidence includes documented communications and procedural failures by Teamsters Local 299.</p>
            </div>

            <div class="experience-item">
                <h4>National Labor Relations Board (NLRB)</h4>
                <p><strong>Federal ULP Filed</strong></p>
                <p>Parallel federal proceedings targeting union misconduct and employer anti-union retaliation. Strategic coordination with MERC case to establish comprehensive pattern of labor rights violations.</p>
            </div>

            <div class="experience-item">
                <h4>Wayne County Circuit Court</h4>
                <p><strong>Emergency TRO Motion Filed</strong></p>
                <p>Comprehensive constitutional claims including due process violations, equal protection challenges, and systemic injustice. Seeking emergency relief to prevent irreparable harm while agency proceedings advance.</p>
            </div>

            <div class="experience-item">
                <h4>Unemployment Insurance Agency (UIA)</h4>
                <p><strong>Constitutional Notice to Director Jason Palmer</strong></p>
                <p>Formal notification of constitutional violations in UIA proceedings, demanding systemic accountability and procedural reform. Legislative outreach through State Representatives Linting and Thompson.</p>
            </div>
        </div>

        <h3>Documented Evidence & Financial Impact</h3>
        <ul>
            <li><strong>Supervisor Text Messages:</strong> Direct evidence of discriminatory intent and retaliatory communications</li>
            <li><strong>Recorded Grievance Hearings:</strong> Audio documentation of procedural failures and union misconduct</li>
            <li><strong>Medical Documentation:</strong> Comprehensive evidence of workplace injury and accommodation failures</li>
            <li><strong>Financial Harm Analysis:</strong> Over $300,000 in lost wages, benefits, and economic damages</li>
            <li><strong>Timeline Documentation:</strong> Detailed chronology establishing causation and pattern of retaliation</li>
        </ul>
    </section>

    <section class="section">
        <h2>Strategic Legal Approach</h2>
        
        <h3>Multi-Agency Coordination</h3>
        <p>My cases demonstrate sophisticated understanding of how to leverage multiple enforcement agencies simultaneously to create systemic pressure and maximize accountability. Rather than pursuing isolated claims, I coordinate parallel proceedings across state and federal jurisdictions to establish comprehensive patterns of misconduct.</p>

        <h3>Evidence-Based Advocacy</h3>
        <p>Every claim is supported by meticulous documentation including recorded proceedings, preserved communications, and comprehensive timeline analysis. This approach transforms individual grievances into powerful systemic challenges backed by irrefutable evidence.</p>

        <h3>Legislative & Policy Impact</h3>
        <p>Beyond individual case resolution, my advocacy targets systemic reform through strategic legislative outreach and policy challenges. Engagement with state representatives and agency directors positions cases as catalysts for broader institutional accountability.</p>

        <h3>Constitutional Framework</h3>
        <p>My legal strategy grounds workplace disputes in fundamental constitutional principles of due process and equal protection, elevating labor cases into civil rights challenges that demand judicial scrutiny and systemic remedies.</p>
    </section>

    <section class="section">
        <h2>Professional Philosophy</h2>
        
        <p>My approach to civil rights advocacy is rooted in the Master-Self philosophy—a commitment to disciplined excellence, strategic thinking, and unwavering pursuit of justice. Just as I apply this philosophy to physical training with 0445 wake-ups and rigorous protocols, I bring the same intensity and precision to legal advocacy.</p>

        <p>Civil rights work demands more than legal knowledge—it requires lived experience, strategic vision, and the resilience to challenge powerful institutions. My decade of paralegal experience, combined with firsthand experience as a worker facing discrimination, positions me uniquely to advocate for those whose rights have been violated.</p>

        <p>Every case I pursue is documented with the same attention to detail I apply to fitness protocols and business operations. This systematic approach transforms individual injustices into powerful legal challenges that demand institutional accountability and systemic change.</p>
    </section>

    <section class="section">
        <h2>Workforce Transportation Grant Pursuit</h2>
        
        <div class="case-highlights">
            <h3>Federal Workforce Development Initiative - $260,000 Opportunity</h3>
            <p><strong>Deadline:</strong> February 9, 2026</p>
        </div>

        <p>I am pursuing a federal workforce transportation grant to establish comprehensive workforce development programming that combines legal advocacy, wellness support, and practical skill-building. This initiative represents the convergence of my paralegal expertise, business infrastructure, and lived experience navigating systemic barriers.</p>

        <h3>Unique Qualifications</h3>
        <ul>
            <li><strong>Michigan Class A CDL License:</strong> Direct transportation industry experience and credentials</li>
            <li><strong>Established Business Infrastructure:</strong> Operating entity through Dominique Clayton Stone Investment Association, LC</li>
            <li><strong>Lived Experience:</strong> Firsthand understanding of workforce barriers, discrimination, and systemic challenges</li>
            <li><strong>Legal Expertise:</strong> Ability to provide advocacy support and rights education to program participants</li>
            <li><strong>Wellness Integration:</strong> Stone Empire Wellness infrastructure for holistic participant support</li>
            <li><strong>Proven Documentation Systems:</strong> Comprehensive tracking and accountability protocols</li>
        </ul>

        <p>This grant opportunity represents not just funding, but validation of the comprehensive approach I've developed—one that recognizes workforce development requires addressing legal barriers, wellness challenges, and systemic injustices alongside practical job training.</p>
    </section>

    <section class="section contact-section">
        <h2>Connect for Civil Rights Advocacy</h2>
        <p>Whether you're facing workplace discrimination, need paralegal support, or seek strategic guidance navigating administrative proceedings, my experience spans over a decade of dedicated legal advocacy.</p>
        
        <p style="margin: 30px 0; font-size: 1.2em;">Dominique Clayton Stone Investment Association, LC</p>
        
        <a href="mailto:[email protected]" class="cta-button">Request Consultation</a>
        <a href="../index.html" class="cta-button">Return to LupusLyfe Home</a>
        
        <p style="margin-top: 30px; font-size: 0.9em; opacity: 0.8;">
            <em>"Justice delayed is justice denied. My advocacy ensures your rights are documented, preserved, and zealously defended."</em>
        </p>
    </section>
</div>
```

</body>
</html>
