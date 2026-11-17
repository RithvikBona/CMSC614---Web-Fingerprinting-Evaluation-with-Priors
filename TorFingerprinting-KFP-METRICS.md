# Tor website fingerprinting: k-FP baseline metrics

Generated: 2026-11-17T04:04:21.487Z

## Held-out results

| Metric | Test | Validation |
|---|---:|---:|
| Top-1 accuracy | 69.40% | 75.60% |
| Macro F1 | 0.6796 | 0.7412 |
| Negative log likelihood | 1.4227 | 1.0542 |

Validation was used for k and temperature selection. Test scores were computed after those choices were frozen.

## Data and model

- 50 monitored domains drawn from the German release, including documented replacements for inaccessible original candidates.
- 30 training, 10 validation, and 10 test traces per domain: 1,500 / 500 / 500 total.
- Separate chronological collection phases with at least 1 hour(s) between capture windows.
- Fixed 20-second client-to-guard TCP payload packet traces, five Tor clients, cold browser profiles, and two-second pauses.
- Normal-page validation may continue until 45 seconds from navigation; the trace stays at 20 seconds.
- Random forest: 1000 trees, stored training fingerprints: [1500, 1000].
- Nearest-neighbor k: 6, validation-selected temperature: 0.680549.
- Features and leaf-neighbor classification are the project’s packet-based k-FP implementation.
- Domain roster and phase assignments were frozen before held-out scoring.

## Recorded software

- Browser: Tor Project Firefox 153.7.0esr.
- Tor versions in bootstrap logs: 0.4.9.16.
- Automation: tbselenium 0.9.0, Selenium 4.15.2.

## Collection exclusions

- Failed attempts retained in the model-cohort manifest: 110.
- Additional analysis exclusions, quality: 0, workload context: 0, outside the frozen roster: 0.
- Reviewed historical traces selected for training: 660. Extra historical traces remain in their original dataset.
- Screening and omitted candidates are documented in reports/roster_selection.json. Original source failures and all diagnostic captures are preserved.

## Per-site test accuracy

| Domain | Correct / tested | Accuracy |
|---|---:|---:|
| adobe.com | 10 / 10 | 100.0% |
| amazon.com | 7 / 10 | 70.0% |
| apple.com | 8 / 10 | 80.0% |
| arbeitsagentur.de | 9 / 10 | 90.0% |
| autoscout24.de | 7 / 10 | 70.0% |
| bbc.com | 8 / 10 | 80.0% |
| bing.com | 10 / 10 | 100.0% |
| bonprix.de | 5 / 10 | 50.0% |
| booking.com | 9 / 10 | 90.0% |
| check24.de | 1 / 10 | 10.0% |
| deutsche-bank.de | 9 / 10 | 90.0% |
| deutschepost.de | 7 / 10 | 70.0% |
| dhl.de | 3 / 10 | 30.0% |
| dict.cc | 5 / 10 | 50.0% |
| dkb.de | 7 / 10 | 70.0% |
| dropbox.com | 8 / 10 | 80.0% |
| duckduckgo.com | 10 / 10 | 100.0% |
| ebay.com | 8 / 10 | 80.0% |
| facebook.com | 7 / 10 | 70.0% |
| faz.net | 10 / 10 | 100.0% |
| freenet.de | 7 / 10 | 70.0% |
| giga.de | 7 / 10 | 70.0% |
| github.com | 7 / 10 | 70.0% |
| google.com | 3 / 10 | 30.0% |
| heise.de | 9 / 10 | 90.0% |
| instagram.com | 6 / 10 | 60.0% |
| mozilla.org | 10 / 10 | 100.0% |
| n-tv.de | 7 / 10 | 70.0% |
| netflix.com | 10 / 10 | 100.0% |
| ok.ru | 10 / 10 | 100.0% |
| otto.de | 9 / 10 | 90.0% |
| postbank.de | 1 / 10 | 10.0% |
| saturn.de | 10 / 10 | 100.0% |
| spiegel.de | 8 / 10 | 80.0% |
| startpage.com | 8 / 10 | 80.0% |
| steamcommunity.com | 1 / 10 | 10.0% |
| steampowered.com | 7 / 10 | 70.0% |
| stern.de | 4 / 10 | 40.0% |
| sueddeutsche.de | 3 / 10 | 30.0% |
| t-online.de | 7 / 10 | 70.0% |
| tagesschau.de | 7 / 10 | 70.0% |
| telekom.com | 6 / 10 | 60.0% |
| tumblr.com | 7 / 10 | 70.0% |
| welt.de | 10 / 10 | 100.0% |
| wetter.com | 5 / 10 | 50.0% |
| whatsapp.com | 8 / 10 | 80.0% |
| wikipedia.org | 9 / 10 | 90.0% |
| wordpress.com | 3 / 10 | 30.0% |
| xing.com | 10 / 10 | 100.0% |
| zdf.de | 0 / 10 | 0.0% |

## Most common confusions

| Actual site | Predicted site | Count |
|---|---|---:|
| steamcommunity.com | steampowered.com | 8 |
| postbank.de | deutsche-bank.de | 5 |
| bonprix.de | whatsapp.com | 3 |
| dhl.de | deutschepost.de | 3 |
| google.com | postbank.de | 3 |
| google.com | telekom.com | 3 |
| wetter.com | telekom.com | 3 |
| zdf.de | giga.de | 3 |
| amazon.com | otto.de | 2 |
| apple.com | whatsapp.com | 2 |

## Scope and reproducibility

This is a closed-world, normal-page baseline for the selected accessible sites. Challenge/error outcomes, unmonitored websites, browsing priors, and HMM fusion are outside this baseline. The result does not establish performance for the original top-50 list or long-term temporal robustness.

- Feature version: `kfp_author_layout_175_packet_v1`.
- Checkpoint SHA-256: `feaf41182c4c2d4c6c1eb0505879983f42068a9b40aa394bd4381b924a63a0b7`.
- Dataset manifest SHA-256: `0fff6ea27dfd58383ef868cb48cdd0c784366de29ea6bed9286c904613b4e624`.
- Frozen domain roster SHA-256: `4cbd2baa2e1e6f87b7909db35a79d94623ca79aedf12e5b02b0b83cb252a7ba4`.
- Detailed split settings, collection versions, selection history, exclusions, scores, and confusion matrix are retained with the dataset.
