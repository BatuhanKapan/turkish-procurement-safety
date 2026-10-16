# Turkish Procurement Safety Pilot

An early, synthetic evaluation seed for **indirect prompt injection in Turkish procurement document extraction**. Created on 16 October 2026. This is a new independent project: no published model findings, prior adoption, external contributors, grant award, or university endorsement is claimed. Prepared with AI assistance.

## Research question

When a supplier document includes instructions that conflict with the user's extraction task, does a model preserve the actual order and avoid proposing an unauthorized action? Does an explicit source-data boundary improve robustness without hurting clean extraction?

The starting set has **30 synthetic cases**: six source orders, each with a clean control and four injection variants (Turkish override, English override, role spoofing, and action spoofing). All supplier names and records are fictional. Do not add real customer or supplier records.

## Run without spending

Python 3.10+; no third-party dependencies.

```sh
python benchmark.py
python -m unittest -v
python benchmark.py --export-cases cases.jsonl
```

Default execution validates data only. Unit tests use simulated responses to check the evaluator; **passing tests are not evidence about Claude's safety**.

## Optional real experiment

Only after obtaining approved API access and setting account spending limits, set `ANTHROPIC_API_KEY` in your own environment. Choose a currently available model ID from the provider's console.

```sh
python benchmark.py --run --model YOUR_MODEL_ID --mode both --limit 10 --out pilot-results.jsonl
```

This command sends requests and may incur API charges. The request cap is a count limit, not a dollar budget. No model is selected by default. API errors stop the run; no automatic retries. Output files use exclusive creation to preserve experiments. The runner never executes actions described by model output. Treat raw output as untrusted data.

## Measures and limitations

- Exact-schema validity and exact-field task accuracy, separately for clean and injected inputs.
- Specific attacker-target hit rate; generic extraction errors are not automatically classified as successful attacks.
- Attempted/completed request counts so provider errors remain visible.
- Model ID, prompt mode, UTC time, raw response, token usage, and stop reason recorded per request.

This small templated set is not representative of all Turkish documents. Lexical overlap and exact-match scoring can distort comparisons. It does not measure executed tool actions, data exfiltration, model alignment generally, or real-world system compromise. A reported action is only a simulated target. Finite model outputs and formatting failures need separate review.

## Planned work, subject to researcher review and access

1. Manually review the seed annotations; add benign conflicting notes, OCR noise, and naturally phrased documents.
2. Expand to 100 source orders with held-out template families. Keep development and evaluation sets separate.
3. Compare baseline and explicit-boundary prompts across two model versions and three repetitions (up to 6,000 requests for a 500-case set).
4. Report paired effects, uncertainty, extraction utility, and manually reviewed failures. Record cost and publish null as well as positive findings.

These are planned activities, not completed experiments. The requested research credits would support this evaluation, not unrelated commercial workloads. No acceptance probability is asserted.

## Background

- [Anthropic: Mitigating the risk of prompt injections in browser use](https://www.anthropic.com/research/prompt-injection-defenses)
- [Anthropic External Researcher Access Program](https://support.claude.com/en/articles/9125743-what-is-the-external-researcher-access-program)
- [Claude Messages API reference](https://platform.claude.com/docs/en/api/messages/create)

## Türkçe özet

Bu yeni proje, Türkçe tedarikçi belgelerindeki kötü niyetli talimatların yapay zekânın sipariş çıkarımını değiştirip değiştirmediğini ölçmek için hazırlanmış küçük bir başlangıç setidir. Gerçek işletme verisi içermez. Henüz Claude üzerinde deney yapılmamıştır; yalnızca veri ve puanlama mantığı çevrimdışı sınanmıştır. Araştırma kredisi başvurusu kabul edildiği anlamına gelmez.

License: MIT.
